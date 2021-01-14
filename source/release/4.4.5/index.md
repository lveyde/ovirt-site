---
title: oVirt 4.4.5 Release Notes
category: documentation
authors: lveyde sandrobonazzola
toc: true
page_classes: releases
---

# oVirt 4.4.5 Release Notes

The oVirt Project is pleased to announce the availability of the 4.4.5 First Release Candidate as of January 14, 2021.

oVirt is a free open-source distributed virtualization solution,
designed to manage your entire enterprise infrastructure.
oVirt uses the trusted KVM hypervisor and is built upon several other community
projects, including libvirt, Gluster, PatternFly, and Ansible.

This release is available now for Red Hat Enterprise Linux 8.2/8.3 (8.3 recommended) and
CentOS Linux 8.2 (or similar).

To find out how to interact with oVirt developers and users and ask questions,
visit our [community page](/community/).
All issues or bugs should be reported via
[Red Hat Bugzilla](https://bugzilla.redhat.com/enter_bug.cgi?classification=oVirt).

The oVirt Project makes no guarantees as to its suitability or usefulness.
This pre-release should not to be used in production, and it is not feature
complete.


If you'd like to try oVirt as quickly as possible, follow the instructions on
the [Download](/download/) page.

For complete installation, administration, and usage instructions, see
the [oVirt Documentation](/documentation/).

For a general overview of oVirt, read the [About oVirt](/community/about.html)
page.

To learn about features introduced before 4.4.5, see the
[release notes for previous versions](/documentation/#latest-release-notes).

## RELEASE CANDIDATE

In order to install this Release Candidate you will need to enable pre-release repository.

`# yum install `[`http://resources.ovirt.org/pub/yum-repo/ovirt-release44-pre.rpm`](http://resources.ovirt.org/pub/yum-repo/ovirt-release44-pre.rpm)


## Known issues

### How to prevent hosts entering emergency mode after upgrade from oVirt 4.4.1

Due to **[[Bug 1837864]](https://bugzilla.redhat.com/show_bug.cgi?id=1837864) - Host enter emergency mode after upgrading to latest build**,

If you have your root file system on a multipath device on your hosts you should be aware that after upgrading from 4.4.1 to 4.4.5 you may get your host entering emergency mode.

In order to prevent this be sure to upgrade oVirt Engine first, then on your hosts:
1. Remove the current lvm filter while still on 4.4.1, or in emergency mode (if rebooted).
2. Reboot.
3. Upgrade to 4.4.5 (redeploy in case of already being on 4.4.5).
4. Run vdsm-tool config-lvm-filter to confirm there is a new filter in place.
5. Only if not using oVirt Node:
   - run "dracut --force --add multipath” to rebuild initramfs with the correct filter configuration
6. Reboot.


## What's New in 4.4.5?

### Enhancements

#### oVirt Engine

 - [BZ 1853906](https://bugzilla.redhat.com/1853906) **[RFE] Add the ability to reboot after install/ reinstall**

   Feature: 'Reboot' option was added to the install and reinstall flows and is enabled by default (same as in the upgrade flow)



Reason: Rebooting the host is needed is several cases such as specifying new kernel parameters and when switching from iptables to firewalld



Result: When installing/ reinstalling host, reboot is enabled by default (can be disabled by the administrator)


### Bug Fixes

#### oVirt Engine SDK 4 Python

 - [BZ 1848586](https://bugzilla.redhat.com/1848586) **Fix upload_ova_as_template.py**


#### oVirt Engine

 - [BZ 1914648](https://bugzilla.redhat.com/1914648) **Q35: BIOS type changed to "Default" when creating new VM from template with Q35 chipset.**

 - [BZ 1890665](https://bugzilla.redhat.com/1890665) **Update numa node value is not applied after the VM restart**

 - [BZ 1905108](https://bugzilla.redhat.com/1905108) **Cannot hotplug disk reports libvirtError: Requested operation is not valid: Domain already contains a disk with that address**

 - [BZ 1910338](https://bugzilla.redhat.com/1910338) **OVA export might fail with: nlosetup: /var/tmp/ova_vm.ova.tmp: failed to set up loop device: Resource temporarily unavailable**

 - [BZ 1908757](https://bugzilla.redhat.com/1908757) **Create VM by auto_pinning_policy=adjust fails with ArrayIndexOutOfBoundsException**

 - [BZ 1906270](https://bugzilla.redhat.com/1906270) **HW clock and windows clock problem in Turkey Standard Time**


#### VDSM

 - [BZ 1773922](https://bugzilla.redhat.com/1773922) **remote-viewer prompts for password after migration of a VM with expired ticket**


### Other

#### cockpit-ovirt

 - [BZ 1908234](https://bugzilla.redhat.com/1908234) **Order of hosts not preserved for day2 operations**

   

 - [BZ 1884223](https://bugzilla.redhat.com/1884223) **[GSS][RHHI 1.7][Error message '&lt;device-path&gt;  is not a valid name for this device' showing up every two hours]**

   


#### OTOPI

 - [BZ 1908602](https://bugzilla.redhat.com/1908602) **dnf packager is broken on CentOS Stream**

   


#### imgbased

 - [BZ 1903777](https://bugzilla.redhat.com/1903777) **chronyd is disabled after upgrading RHV-H 4.4.2 -&gt; 4.4.3**

   


#### oVirt Engine

 - [BZ 1886520](https://bugzilla.redhat.com/1886520) **Cannot import OVA that was exported from oVirt on PPC**

   

 - [BZ 1897160](https://bugzilla.redhat.com/1897160) **SCSI Pass-Through is enabled by default**

   


### No Doc Update

#### OTOPI

 - [BZ 1908617](https://bugzilla.redhat.com/1908617) **otopi is using a private dnf method _read_conf_file**

   


#### oVirt Engine

 - [BZ 1581677](https://bugzilla.redhat.com/1581677) **[scale] search (VMs + storage domain) is taking too long**

   

 - [BZ 1846294](https://bugzilla.redhat.com/1846294) **Engine restart needed after ovirt-register-sso-client-tool**

   

 - [BZ 1911303](https://bugzilla.redhat.com/1911303) **host deploy fails when parameters are set with the value null**

   


#### Contributors

24 people contributed to this release:

	Ahmad Khiet (Contributed to: ovirt-engine)
	Ales Musil (Contributed to: vdsm)
	Amit Bawer (Contributed to: vdsm)
	Arik Hadas (Contributed to: ovirt-engine)
	Artur Socha (Contributed to: ovirt-engine)
	Asaf Rachmani (Contributed to: imgbased)
	Aviv Turgeman (Contributed to: cockpit-ovirt, ovirt-engine-nodejs-modules)
	Dana Elfassy (Contributed to: ovirt-engine)
	Eli Mesika (Contributed to: ovirt-engine)
	Jean-Louis Dupond (Contributed to: vdsm)
	Lev Veyde (Contributed to: ovirt-engine, ovirt-release)
	Liran Rotenberg (Contributed to: ovirt-engine)
	Martin Perina (Contributed to: ovirt-engine)
	Milan Zamazal (Contributed to: ovirt-engine, vdsm)
	Nir Soffer (Contributed to: vdsm)
	Ori Liel (Contributed to: ovirt-engine, ovirt-engine-sdk)
	Parth Dhanjal (Contributed to: cockpit-ovirt)
	Roman Bednar (Contributed to: vdsm)
	Sandro Bonazzola (Contributed to: cockpit-ovirt, ovirt-cockpit-sso, ovirt-engine, ovirt-release)
	Scott J Dickerson (Contributed to: ovirt-engine-nodejs-modules)
	Shani Leviim (Contributed to: ovirt-engine)
	Steven Rosenberg (Contributed to: ovirt-engine, ovirt-engine-sdk)
	Tomáš Golembiovský (Contributed to: vdsm)
	Yedidyah Bar David (Contributed to: otopi, ovirt-cockpit-sso, ovirt-engine)
