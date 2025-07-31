## 1. Install KVM & Related Packages

Update package lists:

```bash
sudo apt update
```

Install KVM and necessary virtualization packages:

```bash
sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst
```

Enable and start the libvirt service:

```bash
sudo systemctl enable --now libvirtd
```



## 2. Download Kali Linux ISO to VPS

Download the Kali Linux ISO directly to the libvirt directory:

```bash
wget https://cdimage.kali.org/kali-rolling/amd64/iso/kali-linux-2025.1-installer-amd64.iso -O /var/lib/libvirt/kali.iso
```




## 3. Create the Kali VM with VNC Graphics

Create a VM named `kali-vm` with 2GB RAM, 2 CPUs, 20GB disk, using the Kali ISO and VNC for GUI access:

```bash
sudo virt-install \
--name kali-vm \
--ram 2048 \
--vcpus 2 \
--disk path=/var/lib/libvirt/images/kali-vm.img,size=20 \
--os-variant=debian10 \
--cdrom=/var/lib/libvirt/kali.iso \
--network network=default \
--graphics vnc,listen=0.0.0.0 \
--noautoconsole
```




## 4. Manage VM Lifecycle

* **Start VM:**

  ```bash
  sudo virsh start kali-vm
  ```

* **Shutdown VM:**

  ```bash
  sudo virsh shutdown kali-vm
  ```

* **Delete VM and remove storage:**

  ```bash
  sudo virsh undefine kali-vm --remove-all-storage
  ```


