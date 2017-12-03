# vagrant_create_subscribed_box

Creates a RHEL Vagrant Box for development purposes which has been registered using **subscription-manager**.
The Vagrant Box is for use by a single developer on a Windows based machine.

## Requirements for building the Box

A developer needs the following before they can execute this role:

- To download a RHEL 7.4 Base Vagrant Box for Virtual Box from the Red Hat repository.
- An **organization id** against which the subscription has been purchased.
- A **registration key** for the subscription.
- Virtual Box installed on the Windows development machine.
- Vagrant installed on the Windows development machine.
- Ansible installed on a Linux development virtual machine (Ansible controllers cannot run directly on Windows hosts)
- Internet connectivity.

**NOTE**: Organization Id and Registration Key can be requested from the subscription owner.

## How to build the subscribed Vagrant Box

1.  Download a standard Vagrantfile from the Linux based role in to a clean directory
(https://raw.githubusercontent.com/prometeo-cloud/vagrant_create_subscribed_box/master/Vagrantfile)
2.	Amend the line below to include a personal reference (to help with management of subscriptions)
    ```
    config.vm.hostname = “box”
    ```
    For example:
    ```
    config.vm.hostname = “box-MYNAME”
    ```
3.	Deploy out the VM with:
    ```
    vagrant up
    ```
4.	When the VM is up and running, SSH into the VM using:
    ```
    vagrant ssh
    ```
5.	From the VM command prompt, subscribe the box using the activation key and org ID supplied to you in the following manner:
    ```
    subscription-manager register --activationkey=xxxxxxx --org=xxxxx
    ```
6.	The box should now be subscribed correctly
7.	Update the box prior to exporting by running the following:
    ```
    sudo yum makecache fast
    sudo yum update -y
    ```
8.	Exit the VM command prompt
9.	Shutdown the VM cleanly
10.	From the Windows command prompt in the same directory, run the following command to export the VM to a Vagrant box:
    ```
    vagrant package box --output rhel74_sub.box
    ```
11.	So that the box can be used correctly, import the box you have just created back in to Vagrant using the following command:
    ```
    vagrant box add --name rhel74_sub rhel74_sub.box
    ```
12.	Copy/Store the rhel74_sub.box file securely as it now has your own unique subscription details embedded in it
13.	Once the box file is safe, destroy the temporary VM using:
    ```
    vagrant destroy -f
    ```
14.	You can now remote the directory you created including any files

*Notes: If you need to provide an administrator with your unique ID for a VM (I.E. the ID embedded in your Vagrant box), use the following command:*

    ```
    sudo subscription-manager identity
    ```

You can then check if the Vagrant Box has been imported in your machine:

```bash
$ vagrant box list
```
You should see **rhel74_sub** in the list.

**NOTE** the above has been tested on Windows 10.
