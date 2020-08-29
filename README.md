Deploy a Production Ready Open Distro Elasticsearch Cluster and Kibana using Standalone Plugin Installation method
===================================================================================================================

This ansible playbook supports the following,

- Can be deployed on baremetal and VMs(AWS EC2)
- Supports most popular **Linux distributions**(Centos7, RHEL7)
- Install and configure the Apache2.0 opensource elasticsearch and kibana
- Install and configure opendistro security plugin using standalone install method
- Configure TLS/SSL for elasticsearch transport layer(Nodes to Nodes communication) and REST API layer
- Generate self-signed certificates to configure TLS/SSL for elasticsearch
- Configure the Internal Users Database with limited users and user-defined passwords

Requirements
------------
- **Ansible**
- **Java 8**

Configure
---------

Refer the file `inventories/opendistro/group_vars/all/all.yml` to change the default values for elasticsearch and kibana Installation.

For example we need to increase the java memory heap size for elasticsearch,

    xms_value: 8
    xmx_value: 8

By default, it will install three node elasticsearch cluster. But if you want to setup five node elasticsearch cluster then you can increase the `minimum_master_nodes`.

    minimum_master_nodes: 3

Note: You need to add additional nodes details(e.g. `es4 and es5`) in `inventories/opendistro/hosts` file for five nodes elasticsearch cluster.

You can also change the elasticsearch and kibana versions. Please refer the version compatibility with [Open Distro](https://opendistro.github.io/for-elasticsearch-docs/version-history/).

Refer the file `inventories/opendistro/group_vars/all/opendistro.yml` to change the default values for Open Distro installation.

If you want to disable the opendistro security plugin installation completely

    opendistro_security_install: false
    opendistro_security_install_kibana: false

Change the opendistro security plugin version

    opendistro_plugin_version: 1.1.0.0

You can set the reserved users(`admin` and `kibanaserver`) password using `admin_password` and `kibanaserver_password` variables.

Install
-------

### Ansible

    # Deploy with ansible playbook - run the playbook as root
    ansible-playbook -i inventories/opendistro/hosts opendistro.yml

It will install and configure the elasticsearch and kibana with opendistro.
Once the deployment completed, you can access the kibana with user `admin` and password which you provided for variable `admin_password`(Default password: Test@123).
