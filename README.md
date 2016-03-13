# oh hai


- a buildroot external.

git clone git://git.buildroot.net/buildroot

make distclean;

# Sucks in the brdnc specific external configuration
make BR2_EXTERNAL=../BRDNC brdnc_defconfig;

# Builds the whole rootfs and shits out to `buildroot/output/images/`
make

# We only asked buildroot to emit a rootfs archive (no EXT4 filesystem image) so we can use that as an import for initializing a docker image; this command assumes you're within the buildroot directory!
cat ./output/images/rootfs.tar | docker import - or13/brdnc:latest

# To test and play
docker run --rm -i -t or13/brdnc:latest bash

# You can also use it as a base image in a dockerfile
```
FROM or13/brdnc:latest

WORKDIR blah

RUN npm install -g

CMD npm serve
```

docker push or13/brdnc:latest
???

