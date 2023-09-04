FROM amd64/debian as native
COPY pkgs /pkgs
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y bbe patchelf $(awk '{ print $NF }' /pkgs)
COPY setup_native /setup_native
RUN /setup_native export $(awk '{ print $NF }' pkgs)
FROM arm64v8/debian
COPY pkgs /pkgs
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y build-essential $(awk '{ print $1 }' /pkgs)
COPY setup_native /setup_native
COPY --from=native /native /native
RUN /setup_native import $(awk '{ print $1 }' pkgs)
RUN rm /pkgs /setup_native
RUN gcc --print-search-dir && echo "int main() { return 0; }" > main.c && gcc -o main main.c && ./main
