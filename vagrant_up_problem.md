# vagrant up启动失败解决办法
## 现象
```
$vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'pristine/ubuntu-budgie-18-x64' version '10.2.0' is up to date...
==> default: Vagrant has detected a configuration issue which exposes a
==> default: vulnerability with the installed version of VirtualBox. The
==> default: current guest is configured to use an E1000 NIC type for a
==> default: network adapter which is vulnerable in this version of VirtualBox.
==> default: Ensure the guest is trusted to use this configuration or update
==> default: the NIC type using one of the methods below:
==> default: 
==> default:   https://www.vagrantup.com/docs/virtualbox/configuration.html#default-nic-type
==> default:   https://www.vagrantup.com/docs/virtualbox/networking.html#virtualbox-nic-type
==> default: Clearing any previously set network interfaces...
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["hostonlyif", "create"]

Stderr: 0%...
Progress state: NS_ERROR_FAILURE
VBoxManage: error: Failed to create the host-only adapter
VBoxManage: error: VBoxNetAdpCtl: Error while adding new interface: failed to open /dev/vboxnetctl: No such file or directory
VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component HostNetworkInterfaceWrap, interface IHostNetworkInterface
VBoxManage: error: Context: "RTEXITCODE handleCreate(HandlerArg *)" at line 94 of file VBoxManageHostonly.cpp
```

## 解决办法
先执行如下命令：
```
$sudo "/Library/Application Support/VirtualBox/LaunchDaemons/VirtualBoxStartup.sh" restart
Loading VBoxDrv.kext
Loading VBoxUSB.kext
Loading VBoxNetFlt.kext
Loading VBoxNetAdp.kext
```
再执行：
```
$vagrant up
```
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'pristine/ubuntu-budgie-18-x64' version '10.2.0' is up to date...
==> default: Vagrant has detected a configuration issue which exposes a
==> default: vulnerability with the installed version of VirtualBox. The
==> default: current guest is configured to use an E1000 NIC type for a
==> default: network adapter which is vulnerable in this version of VirtualBox.
==> default: Ensure the guest is trusted to use this configuration or update
==> default: the NIC type using one of the methods below:
==> default: 
==> default:   https://www.vagrantup.com/docs/virtualbox/configuration.html#default-nic-type
==> default:   https://www.vagrantup.com/docs/virtualbox/networking.html#virtualbox-nic-type
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default: 
    default: Guest Additions Version: 6.0.4
    default: VirtualBox Version: 5.2
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => /Users/rongqing/Vagrant_VM/ubuntu1810
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
(base) rongqings-MacBook-Pro:ubuntu1810 rongqing$ vagrant ssh
Welcome to Ubuntu 18.10 (GNU/Linux 4.18.0-25-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 * Super-optimized for small spaces - read how we shrank the memory
   footprint of MicroK8s to make it the smallest full K8s around.

   https://ubuntu.com/blog/microk8s-memory-optimisation

15 packages can be updated.
0 updates are security updates.

Your Ubuntu release is not supported anymore.
For upgrade information, please visit:
http://www.ubuntu.com/releaseendoflife

New release '20.04.4 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Fri Aug  5 14:43:27 2022 from 10.0.2.2

##ference
[1](https://stackoverflow.com/questions/21069908/vboxmanage-error-failed-to-create-the-host-only-adapter)
