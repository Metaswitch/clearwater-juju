Project Clearwater is backed by Metaswitch Networks.  We have discontinued active support for this project as of 1st December 2019.  The mailing list archive is available in GitHub.  All of the documentation and source code remains available for the community in GitHub.  Metaswitch’s Clearwater Core product, built on Project Clearwater, remains an active and successful commercial offering.  Please contact clearwater@metaswitch.com for more information.

# Overview

This repository contains a collection of [Juju charms and deployment bundles](https://jujucharms.com/about), which support deployment and scaling of a [Project Clearwater](http://www.projectclearwater.org) IMS core.

This repository also contains a proxy charm for managing an all-in-one node spun up from an OVA or QCOW2 image - for more information on that, see [its README.md](charms/trusty/clearwater-aio-proxy/README.md).

# Usage

Before deploying this charm, you should have bootstrapped a Juju environment, as documented at https://jujucharms.com/docs/stable/getting-started. This charm has been tested on Amazon EC2, with plans to test on OpenStack in the near future - if you get it working on a different cloud service, please let us know!

Clearwater is a reasonably complex system (especially compared to typical beginner Juju examples like Wordpress + MySQL) - deploying a Clearwater IMS core involves deploying and configuring six or seven charms and adding relations between them.

Fortunately, we've set up a Juju bundle that ties all these charms and their relations together, allowing a full system to be deployed in a single step. The bundle contains some default configuration, but additional configuration files can be used to customise the deployment - see [bundle-config.yaml.example](bundle-config.yaml.example) for an example.

A Clearwater system can be deployed in a Juju environment by creating a bundle-config.yaml file then running the following commands.

    git clone https://github.com/Metaswitch/clearwater-juju.git
    cd clearwater-juju
    JUJU_REPOSITORY=charms juju-deployer -c charms/bundles/clearwater/bundle/bundles.yaml -c bundle-config.yaml

# Configuration

See [bundle-config.yaml.example](bundle-config.yaml.example), which lists the main configuration fields with comments about their meanings.

# Testing

This repository contains Amulet tests for automated testing. To run them, use:

    git clone https://github.com/Metaswitch/clearwater-juju.git
    cd clearwater-juju
    JUJU_REPOSITORY=charms juju test -o logs -v -p JUJU_REPOSITORY,HOME --timeout=1200s
