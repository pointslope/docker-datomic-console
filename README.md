# Datomic Console

This Dockerfile defines a base image for the version of Datomic Console that ships with Datomic Pro Starter Edition. It defines the necessary automation steps for running Datomic Console, while deferring all privileged, user-specific configuration to a derived image via **ONBUILD** instructions.

This approach makes it trivial to customize your own Dockerfile to run any supported Datomic configuration. To do so, you need only to follow these steps:

1. Create a `Dockerfile` that is based **FROM** this image
2. Create a `.credentials` file containing your http user and password for downloading from **my.datomic.com** in the form `user:pass`
3. Add a **CMD** instruction in your `Dockerfile` with an alias for the Datomic database you wish to connect to and the Datomic uri e.g. **datomic:dev://db:4334/**

No other configuration is necessary. Simply **docker build** and **docker run** your image.

## Example Folder Structure

    .
    ├── .credentials
    └── Dockerfile

## Example Dockerfile

    FROM pointslope/datomic-console:0.9.5359
    MAINTAINER John Doe "jdoe@example.org"
    CMD ["dev", "datomic:dev://db:4334/"]

## Miscellany

The Dockerfile **EXPOSES** port 9000. Once the container is running, open the following url to view Datomic Console:

    http://{host}:9000/browse

where {host} represents the IP address or hostname of the host running the Docker container. If you are using **boot2docker**, you can obtain the ip address by executing `boot2docker ip` at the shell.

## License

The MIT License (MIT)

Copyright (c) 2015-2016 Point Slope, LLC.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
