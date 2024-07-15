### Preparation

- Copy source files into `Serpent/src`

- Copy XS files into `Serpent/xs`

### Compile Source Code

```console
docker-compose run --rm -it serpent cd src && make clean && make
```

### Run

```console
docker-compose run --rm -it serpent ./src/sss2 -version
```
