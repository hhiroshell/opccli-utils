Utilities for PaaS Service Manager Command Line Interface (PSMcli)
===================================================================
PSMcli is a command line interface for Oracle PaaS.
For detail, see [PaaS Service Manager Command Line Interface Reference](https://docs.oracle.com/en/cloud/paas/java-cloud/pscli/toc.htm)

Usage
-----
To use PSMcli through this utilities, first you have to build a docker container of PSMcli envilonment.

### 1. Clone or download this repository.

### 2. Move the dockerfile(/psmcli/dockerfile) to the place you can use "docker" commands.

### 3. Build the docker image.
Run the "docker build" command below.

    docker build -t psmcli:sample_id_domain --force-rm=true --rm=true ./ \
                 --build-arg user=sample_admin \
                 --build-arg password=sample_password \
                 --build-arg identitydomain=sample_id_domain \
                 --build-arg region=us \
                 --build-arg datacenter=psm.us.oraclecloud.com

### 4. Run the container.
Run the "docker run" command below

    docker run --rm=true -it psmcli:sample_id_domain /bin/bash

### 5. Now, you can use PSMcli commands.

    psm -v
    psm help

