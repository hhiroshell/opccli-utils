FROM python:3.5

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

# Install the expect package to automate PSMcli setup interaction.
RUN apt-get update && \
    apt-get -y install expect

# Setup PSMcli.
RUN expect -c "\
    set timeout 1;\
    spawn psm setup;\
    expect \"Username: \";                                  send \""${user}"\r\";\
    expect \"Password: \";                                  send \""${password}"\r\";\
    expect \"Retype Password: \";                           send \""${password}"\r\";\
    expect \"Identity domain: \";                           send \""${identitydomain}"\r\";\
    expect \"Region \\\\\\\\\[us\\\\\\\\\]: \";             send \""${region}"\r\";\
    expect \"Output format \\\\\\\\\[short\\\\\\\\\]: \";   send \"short\r\";\
    expect eof;\
    "

CMD ["/bin/bash"]
