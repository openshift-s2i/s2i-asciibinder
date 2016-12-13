AsciiBinder - CentOS Docker image
=================================

This repository contains the source building a Source-to-Image builder
for [AsciiBinder](http://asciibinder.org) repositories. 

Versions
--------

* AsciiBinder v0.1.8

CentOS versions currently provided are:

* CentOS7

Installation
------------

This image is available oon DockerHub. To download it, run:

```
docker pull openshift/asciibinder-018-centos7
```

To build the AsciiBinder image from scratch, run:

```
git clone https://github.com/openshift-s2i/s2i-asciibinder.git
cd s2i-asciibinder
make build VERSION=0.1.8
```

Usage
-----

To create an image that renders an existing AsciiBinder repository, use 
[s2i](https://github.com/openshift/source-to-image) to create the image and 
then run it:

```
s2i build https://github.com/openshift/openshift-docs.git openshift/asciibinder-018-centos7 openshift-docs
docker run -p 8080:8080 openshift-docs
```

**Accessing the application:**
Point your browser to [http://localhost:8080](http://localhost:8080)

Test
----

This repository also provides a [S2I](https://github.com/openshift/source-to-image) test framework,
which launches tests to check functionality of a simple AsciiBinder repository built on top of the AsciiBinder image.

*  **CentOS based image**

   ```
   $ cd s2i-asciibinder
   $ make test VERSION=0.1.8
   ```

Repository Organization:
-----------------------
* **`<AsciiBinder-version>`**

    * **Dockerfile**

        CentOS based Dockerfile

    * **`s2i/bin/`**

        This folder contains scripts that are run by [S2I](https://github.com/openshift/source-to-image):

        *   **assemble**

            Runs an AsciiBinder build on the provided repository.
            The result is a set of static files ready for rendering.

        *   **run**

          This script will launch an *asdf* server to serve static files 
          generated by the asciibinder build process.


    * **`test/`**

        This folder contains the [S2I](https://github.com/openshift/source-to-image)
        test framework with a simple AsciiBinder repository.

        * **`test-repo/`**

            A simple AsciiBindeer repository used for testing purposes by the [S2I](https://github.com/openshift/source-to-image) test framework.

        * **run**

            This script runs the [S2I](https://github.com/openshift/source-to-image) test framework.

* **`hack/`**

    Folder containing scripts which are responsible for the build and test actions performed by the `Makefile`.


Image name structure
------------------------
##### Structure: openshift/1-2-3

1. Platform name (lowercase) - asciibinder
2. AsciiBinder version(without dots) - 018
3. Base builder image - centos7

Example: `openshift/asciibinder-018-centos7`

Copyright
---------

Released under the Apache License 2.0. See the [LICENSE](LICENSE) file.
