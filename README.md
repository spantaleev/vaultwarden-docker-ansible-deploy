# Vaultwarden server setup using Ansible and Docker

------

**WARNING**: this playbook has been **made obsolete** by the [MASH playbook](https://github.com/mother-of-all-self-hosting/mash-playbook), which also supports installing the [Vaultwarden service](https://github.com/mother-of-all-self-hosting/mash-playbook/blob/main/docs/services/vaultwarden.md). There's a [migration guide](CHANGELOG.md#this-playbook-has-been-absorbed-into-the-mash-playbook) in the changelog.

------

This [Ansible](https://www.ansible.com/) playbook can help you set up your own [Vaultwarden](https://github.com/dani-garcia/vaultwarden) server (unofficial [Bitwarden](https://bitwarden.com/) compatible server) instance:

- on your own Debian/CentOS/RedHat server

- with all services ([Vaultwarden](https://github.com/dani-garcia/vaultwarden), [PostgreSQL](https://www.postgresql.org/), [Traefik](https://traefik.io), etc.) running in [Docker](https://www.docker.com/) containers

- powered by the official [vaultwarden/server](https://hub.docker.com/r/vaultwarden/server) container image

- [interoperates nicely](docs/configuring-playbook-interoperability.md) with [related](#related) Ansible playbooks or other services using Traefik for reverse-proxying

SSL certificates are automatically managed by a [Traefik](https://traefik.io) reverse-proxy.

Various components (Postgres, Traefik, etc.) can be disabled and replaced with your own other implementations (see [configuring the playbook](docs/configuring-playbook.md)).


## Features

Using this playbook, you can get the following services configured on your server:

- a [Vaultwarden](https://github.com/dani-garcia/vaultwarden) server - a [Bitwarden](https://bitwarden.com/)-API-compatible server storing your passwords and providing a web interface

- (optional) a [PostgreSQL](https://www.postgresql.org/) database for Vaultwarden

- (optional) free [Let's Encrypt](https://letsencrypt.org/) SSL certificate, which secures the connection to the Vaultwarden server

- (optional) [backups](docs/configuring-playbook-backups.md)

Basically, this playbook aims to get you up-and-running with all the basic necessities around Vaultwarden.


## Installation

To configure and install Vaultwarden on your own server, follow the [README in the docs/ directory](docs/README.md).


## Changes

This playbook evolves over time, sometimes with backward-incompatible changes.

When updating the playbook, refer to [the changelog](CHANGELOG.md) to catch up with what's new.


## Support

- Matrix room: [#vaultwarden-docker-ansible-deploy:devture.com](https://matrix.to/#/#vaultwarden-docker-ansible-deploy:devture.com)

- GitHub issues: [spantaleev/vaultwarden-docker-ansible-deploy/issues](https://github.com/spantaleev/vaultwarden-docker-ansible-deploy/issues)


## Related

You may also be interested in these other playbooks:

- [gitea-docker-ansible-deploy](https://github.com/spantaleev/gitea-docker-ansible-deploy) - for deploying a [Gitea](https://gitea.io/) git version-control server

- [matrix-docker-ansible-deploy](https://github.com/spantaleev/matrix-docker-ansible-deploy) - for deploying a fully-featured [Matrix](https://matrix.org) homeserver

- [nextcloud-docker-ansible-deploy](https://github.com/spantaleev/nextcloud-docker-ansible-deploy) - for deploying a [Nextcloud](https://nextcloud.com/) server

- [peertube-docker-ansible-deploy](https://github.com/spantaleev/peertube-docker-ansible-deploy) - for deploying a [PeerTube](https://joinpeertube.org/) video-platform server
