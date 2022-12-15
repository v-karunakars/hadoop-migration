## Generalizing linux VM

1. Deprovision user 

```sh
   sudo waagent -deprovision+user

```

2. Deallocate VM

```sh

az vm deallocate \
   --resource-group az-cslabs-phase2 \
   --name az-cslabs-linux-vm

```

3. Generalize VM

```sh

az vm generalize \
   --resource-group az-cslabs-phase2 \
   --name az-cslabs-linux-vm

```

4. Take a snapshot of the OS disk of above VM, Create a new disk form it, and generate the export link using ***Disk Export** link

5. Use `AzCopy` to explort the disk to blob storage location. 

```sh

azcopy cp "https://md-vgj1mxkdzhhz.z3.blob.storage.azure.net/rbsprxkbcr0p/abcd?sv=2018-03-28&sr=b&si=5e5c3351-ce8f-41e7-be44-838e65310fb3&sig=I1qqb6BNwyAuGeVC3zuR17W5EhwSDRqgE7RzzHNgdT0%3D" "https://csalabsshrdstrg1.blob.core.windows.net/cloudacademy/databricks/linux_vm_v1_0.vhd?sv=2021-04-10&st=2022-12-15T08%3A57%3A32Z&se=2022-12-16T08%3A57%3A32Z&sr=c&sp=racwl&sig=u7ITsjVKTcuM8zOs38xnMAEwuXMFqTIGDI%2Bv1qEsS0s%3D"


```
