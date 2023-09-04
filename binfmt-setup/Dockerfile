FROM debian
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y binfmt-support qemu-user-static
CMD update-binfmts --enable qemu-aarch64 && cat /proc/sys/fs/binfmt_misc/qemu-aarch64 && sleep 1d
HEALTHCHECK CMD cat /proc/sys/fs/binfmt_misc/qemu-aarch64 || exit 1
