PostgreSQL role for Ansible
===========================

A role for deploying and configuring [PostgreSQL](http://www.postgresql.org/) and extensions on unix hosts using [Ansible](http://www.ansibleworks.com/).

It can additionally be used as a playbook for quickly provisioning hosts.

Vagrant machines are provided to produce a boxed install of PostgreSQL or a VM for integration testing.


Supports
--------

Supported PostgreSQL versions:

- PostgreSQL 9.3

Supported targets:

- Ubuntu 12.04 "Precise Pangolin"
- Other LTS ubuntu versions (untested)
- Debian (untested)

Installation methods:

- Binary packages from the official repositories at [postgresql.org](http://www.postgresql.org/download/)

Available extensions (under a switch):

- Development headers - `postgresql_dev_headers`
- The [psycopg2](http://initd.org/psycopg/) driver for Python - `postgresql_psycopg2`
- [PostGIS](http://postgis.net/) - `postgresql_postgis`


Usage
-----

Clone this repo into your roles directory:

    $ git clone https://github.com/zenoamaro/ansible-postgresql.git roles/postgresql

And add it to your play's roles:

    - hosts: ...
      roles:
        - postgresql
        - ...

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in `defaults/main.yml` for help in configuration. All provided variables start with `postgresql_`.

You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

    $ ansible-playbook -i inventory --extra-vars='{...}' main.yml

To provision a standalone PostgreSQL box, start the `boxed` VM, which is a Ubuntu 12.04 box:

    $ vagrant up boxed

You will find PostgreSQL listening on the VM's `5432` port on address `192.168.33.20` in the private network. You can then connect to it as any user. Please note that this is highly insecure, so if you're going to publish this VM you'll want to provide actual authentication.

Run the tests by provisioning the appropriate VM:

    $ vagrant up test-ubuntu-precise

At the moment, `ubuntu-precise` is the only test VM available.


Still to do
-----------

- Add repositories, tasks and test VMs for other distros
- Allow installation from sources if requested
- Add support for different PostgreSQL versions (9.x and possibly 8.x)
- Add support for PostgreSQL clusters
- Add support for [PgBouncer](http://wiki.postgresql.org/wiki/PgBouncer)
- Try to make the boxed VM more secure by default
- Add links to the relevant documentation in configuration files
- Provide a library of custom modules


Changelog
---------

### 0.1

Initial version.
