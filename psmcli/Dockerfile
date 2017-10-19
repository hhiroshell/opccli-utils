FROM python:3.6

ARG user
ARG password
ARG identitydomain
ARG region="us"
ARG datacenter="psm.us.oraclecloud.com"

WORKDIR /root

# Install PSMcli.
RUN curl -X GET \
         -u ${user}:${password} \
         -H X-ID-TENANT-NAME:${identitydomain} \
         https://${datacenter}/paas/core/api/v1.1/cli/${identitydomain}/client \
         -o psmcli.zip
RUN pip3 install -U psmcli.zip && \
    rm psmcli.zip

# Setup PSMcli.
RUN echo "${user}\n${password}\n${password}\n${identitydomain}\n${region}\nshort" | psm setup

# Add payload files.
RUN mkdir ./payloads
ADD samples ./payloads/

CMD ["/bin/bash"]
