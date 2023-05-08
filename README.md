# Chmod buildpack

A demonstration of a buildpack that can change permissions to the folders and files of the default workspace of a Paketo build.

Inspiration came from @dmikusa and [documentation here](https://github.com/buildpacks/samples/tree/main/apps/bash-script)

## Build the buildpack

```bash
pack buildpack package anthonydahanne/chmod:0.0.1
docker push anthonydahanne/chmod:0.0.1 
```

## Use the buildpack

Using the project descriptor `project.toml` from a copy of this folder

```bash
pack build --descriptor project.toml -p apache-activemq-dist.zip my-dist \ 
  -e BP_APPLICATION_SCRIPT=apache-activemq-dist/bin/activemq \ 
  --builder paketobuildpacks/builder:base
```

You should see:
```bash
---> Chmod buildpack
Before
total 12
drwxr-xr-x  3 cnb  cnb  4096 May  8 00:50 .
drwxr-xr-x  1 root root 4096 May  8 00:50 ..
drwxr-xr-x 10 cnb  cnb  4096 May  2 03:08 apache-activemq-dist
Updating rights for activemq
+ chmod -R 775 ./
+ chmod -R 755 apache-activemq-dist/bin/activemq apache-activemq-dist/bin/activemq-diag apache-activemq-dist/bin/activemq.jar apache-activemq-dist/bin/env apache-activemq-dist/bin/linux-x86-32 apache-activemq-dist/bin/linux-x86-64 apache-activemq-dist/bin/macosx apache-activemq-dist/bin/wrapper.jar
+ set +x
After
total 12
drwxrwxr-x  3 cnb  cnb  4096 May  8 00:50 .
drwxr-xr-x  1 root root 4096 May  8 00:50 ..
drwxrwxr-x 10 cnb  cnb  4096 May  2 03:08 apache-activemq-dist
```


### Easiest alternative

Or you can just simply use this command, without needing the `project.toml` descriptor:

```bash
pack build -p apache-activemq-dist.zip my-dist \ 
  -e BP_APPLICATION_SCRIPT=apache-activemq-dist/bin/activemq \
  -b paketo-buildpacks/syft \
  -b paketo-buildpacks/bellsoft-liberica \
  -b paketo-buildpacks/dist-zip \ 
  -b anthonydahanne/chmod:0.0.1 \ 
  --builder paketobuildpacks/builder:base
```
