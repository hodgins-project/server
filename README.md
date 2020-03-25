<!--
Shields
Headers
-->

# Hodgins: Server

A repository, providing the Hodgins Server.

## Motivation

A Home Server / Small Office Server / Lab Server should provide different
applications and technologies to do it's job. Most available solutions are built
around a NAS (network attached storage) server and add features to it. This
apporach comes with some pain, if you need to add applications in different
versions, wants to add more services or play with the server, without messing it
up.

## Description

Hodgins is a small Home Server / Office Server / Lab Server platform. Hodgins
will provide a way to deploy, develop and manage different applications in
containers and facilitate upstream software like the below:

- [Fedora](https://getfedora.org/)
  Fedora will be used as the base OS and the base image for containers. It
  provides a strong foundation with tools like [firewalld]() or [SELinux]() and
  is available for x86_64 and aarch64.
- [Ansible](https://www.ansible.com/)
- [Podman](https://podman.io/)
- [Buildah](https://buildah.io/)
- [Cockpit Project](https://cockpit-project.org/)
- [Performance Co-Pilot](https://pcp.io/)
- [tuned](https://tuned-project.org/)

## Requirements

You will need a Virtual Machine, a Bare Metal Machine or an SoC, which is
compatible to Fedora. The minimum requirements are:

- CPU: 2 cores
- RAM: 2 GiB
- HDD: 20 GiB
- NET: connection to the internet needed for installations

## Install

This section describes the deployment process:

### Install the base OS

You need to install the base OS by Hand for now. You can download the ISO
[here](https://getfedora.org/en/server/download/). During the installation, you
should follow these steps:

- Software Selection
  - choose "Minimal" (when using the Netinstall ISO)
  - choose "Fedora Custom Operating System" (when using Stadard ISO)
- User Creation
  - provide "Full name"
  - provide "User name"
  - check "Make this user administrator"
  - provide "Password"
- Begin Installation

After a reboot at the end, you should be able to login to the server.

### Hodgins customizations

The customizations for the freh Fedora Minimal installations will be done via
Ansible. You can do this in 2 ways:

#### Self-hosted deployment

The self-hosted deployment does not need any additional host. The hodgins server
will get all the tools, bells and whistles to manage itself. This may be a good
idea for getting started and if you do not have access to another Linux machine.

1. Login to your Hodgins Server via SSH as <your-hodgins-user>.
2. Update the server
    ```
    $ sudo dnf update -y
    ```
2. Install ansible and git
    ```
    $ sudo dnf install -y ansible git
    ```
3. Clone the repository
    ```
    git clone https://github.com/hodgins-project/server.git
    ```
4. Edit the inventory
    ```
    cp -r <path-to-repository>/inventories/example/ <path-to-inventory>/inventories/<name>/
    vi <path-to-inventory>/inventories/<name>/inventory
    ```
    Configure the proper host
    ```
    [server]
    localhost
    ```
5. 3. Run the ansible playbook
    ```
    ansible-playbook -i <path-to-inventory>/inventories/<name>/inventory -K playbooks/server.yml
    ```
6. Reboot the machine
    ```
    $ sudo systemctl reboot
    ```
7. Login to the web interface on [https://<your-hodgins-ip>:9090](https://<your-hodgins-ip>:9090)

#### Ansible host

If you have access to a dedicated management machine / control host, you can
manage your Hodgins server from it. The control host needs to have git and
Ansible installed (Version 2.7+) and should be able to connect to the hodgins
server.

1. Clone the repository
    ```
    git clone https://github.com/hodgins-project/server.git
    ```
2. Edit the inventory
    ```
    cp -r <path-to-repository>/inventories/example/ <path-to-inventory>/inventories/<name>/
    vi <path-to-inventory>/inventories/<name>/inventory
    ```
    Configure the proper host
    ```
    [server]
    <your-hodgins-ip> or <your.hodgins.domain.tld>
    ```
3. Run the ansible playbook
    ```
    ansible-playbook -i <path-to-inventory>/inventories/<name>/inventory -k -K -u hodgins playbooks/server.yml
    ```

## Usage

After the base installation, you can start to deploy and use applications. An
example service can be found [here](https://github.com/hodgins-project/service-example).

## Changelog

The repository contains a curated, chronological [changelog](CHANGELOG.md),
maintained by the owner for each release/tag.

## Contribute

Thank you so much for considering to contribute! We are happy, when someone is
joining the hard work. Please feel free to contribute, after having a look at
the [Conventions](https://github.com/while-true-do/doc-library/).

- [Bugs and Feature Requests](https://github.com/hodgins-project/server/issues)
- [Pull Requests](https://github.com/hodgins-project/server/pulls)

See who has contributed already in the [KUDOS.txt](KUDOS.txt).

## Test

tbd

## License

This work is [licensed](LICENSE) under a
[BSD-3-Clause License](https://opensource.org/licenses/BSD-3-Clause).

## Contact

-   Site <https://while-true-do.io>
-   Code <https://github.com/while-true-do>
-   Mail [hello@while-true-do.io](mailto:hello@while-true-do.io)
-   Chat [@freenode #while-true-do](https://webchat.freenode.net/#while-true-do)
