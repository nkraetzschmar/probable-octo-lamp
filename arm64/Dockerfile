FROM amd64/debian as native
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y patchelf
COPY setup_native /setup_native
RUN /setup_native export
FROM arm64v8/debian
COPY pkgs /pkgs
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y build-essential $(cat /pkgs)
COPY setup_native /setup_native
COPY --from=native /native /native
RUN /setup_native import
RUN rm /pkgs /setup_native
RUN gcc --print-search-dir && echo "int main() { return 0; }" > main.c && gcc -o main main.c && ./main
