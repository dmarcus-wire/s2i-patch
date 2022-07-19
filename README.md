# Introduction - Source to Image

Source-to-image (s2i) is a simple method of containerizing code on the OpenShift platform. The s2i process is lightweight, minimalistic, and barebones. 

This quick, paved path, allows you to put an application into a container with basic requirements to run your code. In short, s2i means...

*YOU DON'T HAVE TO THINK ABOUT CONTAINERS!*

 Follow the links at the bottom to learn more.

# Patch the Source to Image (s2i) build?

Patching s2i allows adding dependencies to a container that your application needs - which don't exist in the default s2i container.

## Why patch the Python s2i build?

Patch the s2i build if your app needs other dependencies. 

Examples include:
  - Gurobi client libraries
  - Database connection drivers

Available patch build config templates are stored in the [openshift](openshift) folder in this repo.

# Patch s2i via `Dockerfile`

#TheHardWay

Use a `Dockerfile` when you NEED `root` for commands.

From a high level...
1. Deploy code using the default s2i process
2. Add templates from this repo into an OpenShift project (namespace)
3. Click some buttons to layer / combine those templates into a new image
4. Change your existing build from step #1 to build from the patched s2i image that you created in step #3
5. Rejoice!!!

## Quickstart Command
The following command will create a build config to patch a base s2i image

```
# add odbc driver to python s2i image
oc process -f openshift/build-s2i-ms-odbc-17.yml | oc apply -f-
```

# Patch s2i via `assemble` script

#TheEasierWay

Use `assemble` when you DO NOT need root for commands.

You can also patch via s2i. This allows you to patch your container via whatever scripting method you prefer (by default it is bash).

Move the mess you call a `Dockerfile`, including those `RUN` lines, to `.s2i/bin/assemble`.

See [.s2i/bin/assemble](.s2i/bin/assemble)

# Links
- [OpenShift Docs - Source to Image](https://docs.openshift.com/container-platform/4.10/openshift_images/using_images/using-s21-images.html)
- [GitHub - Source to Image](https://github.com/openshift/source-to-image)
- [Python s2i Docs](https://docs.openshift.com/container-platform/3.11/using_images/s2i_images/python.html#using-images-python-configuration)