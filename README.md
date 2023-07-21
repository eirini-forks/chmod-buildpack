# Chmod buildpack
This fork of https://github.com/anthonydahanne/chmod-buildpack is tailored to address the following issue with certain Rails
apps running on Jammy stacks:
https://github.com/paketo-buildpacks/ruby/issues/889

It is intended to be a short-term fix and not meant to be used generically.

## Build the buildpack

```bash
pack buildpack package us-west1-docker.pkg.dev/cf-on-k8s-wg/buildpacks/chmod:latest
docker push us-west1-docker.pkg.dev/cf-on-k8s-wg/buildpacks/chmod:latest
```
