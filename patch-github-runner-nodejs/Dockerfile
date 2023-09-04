FROM ubuntu
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y patchelf
COPY patch_externals /patch_externals
CMD cd /mnt/home/runner/runners/*/externals && /patch_externals && touch /done && sleep 1d
HEALTHCHECK CMD cat /done || exit 1
