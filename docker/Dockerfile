FROM ubuntu:24.04

RUN apt-get update && apt-get install -y --no-install-recommends \
        postgresql-common \
        ca-certificates \
        curl \
        unzip \
        less \
        pv \
        vim

RUN install -d /usr/share/postgresql-common/pgdg
RUN curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN sh -c 'echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt noble-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

RUN apt-get update && apt-get install -y --no-install-recommends \
        postgresql-client-17
RUN apt-get clean all

WORKDIR /tmp/awscli/

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "aws.zip" \
    && unzip "aws.zip" \
    && /tmp/awscli/aws/install && rm -rf /tmp/awscli/*


# On Ubuntu 24.04 there already exists a user with gid/uid 1000 - ubuntu - using that
# RUN groupadd --gid 1000 user \
#   && useradd --uid 1000 --gid user --create-home user

USER ubuntu

WORKDIR /home/ubuntu

ADD backup.sh .

ENTRYPOINT ./backup.sh
