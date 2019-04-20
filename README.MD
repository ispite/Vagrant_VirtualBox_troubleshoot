# DESCRIPTION
These are just notes for me, with a solution that worked for me.

my Specs:
* Win 10 x64
* proccessor: amd

I had this error:
```
Timed out while waiting for the machine to boot. This means that
Vagrant was unable to communicate with the guest machine within
the configured ("config.vm.boot_timeout" value) time period.

If you look above, you should be able to see the error(s) that
Vagrant had when attempting to connect to the machine. These errors
are usually good hints as to what may be wrong.

If you're using a custom box, make sure that networking is properly
working and you're able to connect to the machine. It is a common
problem that networking isn't setup properly in these boxes.
Verify that authentication configurations are also setup properly,
as well.

If the box appears to be booting properly, you may want to increase
the timeout ("config.vm.boot_timeout") value.
```

First of all, you need to check whether the SSH client is installed?
If is, then:
Verify that VirtualBox is working properly, for example the following code in a Vagrantfile:
```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
config.vm.provider :virtualbox do |vb|
	vb.gui = true
end
end
```
In my case, VirtualBox hangs on (freeze) for no reason.
### Solution is:
turn off Hyper-V in windows components
and
check in cmd.exe as administrator

```
bcdedit
```
[image](../resources/hypervisorlaunchtype auto.png)

if set to "auto", disable it:
```
bcdedit /set hypervisorlaunchtype off
```