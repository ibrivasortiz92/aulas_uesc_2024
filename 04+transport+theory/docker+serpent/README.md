### 1 Preparation

- Copy source files into `Serpent/src`

- Copy XS files into `Serpent/xs`

### 2 Compile Source Code

```console
docker-compose run --rm -it serpent cd src && make clean && make
```

### 3 Link Libraries

```console
docker-compose run -rm -it serpemd cd xs && perl xsdirconvert_j311.pl sss_jeff311u.xsdir > sss_jeff311u.xsdata
docker-compose run -rm -it serpemd cd xs && perl xsdirconvert_j31.pl sss_jeff31u.xsdir > sss_jeff31u.xsdata
docker-compose run -rm -it serpemd cd xs && perl xsdirconvert_j22.pl sss_jef22u.xsdir > sss_jef22u.xsdata
docker-compose run -rm -it serpemd cd xs && perl xsdirconvert_end.pl sss_endfb7u.xsdir > sss_endfb7u.xsdata
docker-compose run -rm -it serpemd cd xs && perl xsdirconvert_end.pl sss_endfb68u.xsdir > sss_endfb68u.xsdata
```

### 4 Run

```console
docker-compose run --rm -it serpent ./src/sss2 -version
```
