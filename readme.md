# vagrant_create_subscribed_box

Creates a RHEL Vagrant Box for development purposes which has been registered using **subscription-manager**.
The Vagrant Box is for use by a single developer on a Linux machine.

**If you are a developer on a Windows based machine, please use [this readme](https://github.com/prometeo-cloud/vagrant_create_subscribed_box/blob/master/readme-win.md) instead**

## Requirements for building the Box

A developer needs the following before they can execute this role:

- To download a RHEL 7.4 Base Vagrant Box for Virtual Box from the Red Hat repository.
- An **organization id** against which the subscription has been purchased.
- A **registration key** for the subscription.
- Virtual Box installed on the development machine.
- Vagrant installed on the development machine.
- Ansible installed on the development machine.
- Internet connectivity.

**NOTE**: Organization Id and Registration Key can be requested from the subscription owner.

## How to build the subscribed Vagrant Box

Just run the following command for the terminal:

```bash
$ sh go
```

You can then check if the Vagrant Box has been imported in your machine:

```bash
$ vagrant box list
```
You should see **rhel74_sub** in the list.

**NOTE** the above has been tested on CentOS 7 and MacOS High Sierra.

## How to use the subscribed Vagrant Box for testing Ansible using Molecule

To use the Vagrant machine with Molecule do the following:

#### Create a Molecule scenario for Vagrant

 ```bash
 # from within the Ansible role folder execute the command below
 $ molecule init scenario -r <role-name> -s vagrant -d vagrant
 ```

#### Edit the molecule.yml file specifying the new Vagrant Box to use

In the **molecule/vagrant/molecule.yml** file:

 ```yaml
platforms:
  - name: role-name
     box: rhel74_sub
 ```
