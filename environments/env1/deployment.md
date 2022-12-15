
## Lab user name and password
login - csLabsUser
password - de22c4!DE22C4@de22c4

## Deploy template

```

az deployment group create --resource-group az-cslabs-phase2-1 --template-file linux-windows.bicep --parameters linuxVmAdminUsername=csLabsUser windowsVmAdminUsername=csLabsUser

```
