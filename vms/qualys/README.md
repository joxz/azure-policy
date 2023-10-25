# qualys agent deploy policy

Deploy Qualys Cloud Agent as a VM extension with Azure Policy. When assigned the policy will add the VM extension around 10mins[^1] after deployment on Windows and Linux VMs

VMs can be excluded from this policy by setting a tag of `noqualysagent : true`. This tag has to be set when deploying a new VM, or before running the remediation task for existing resources.
Tag name and value to exclude can be defined in assignment parameters

A valid Qualys license code is required to install the VM extension (has to be set in the assignment parameters)

[^1]: [DeployIfNotExists properties](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effects#deployifnotexists-properties)


## AzCLI 

List VM extensions available:

```bash
> az vm extension image list --publisher Qualys -o table

Name                              Publisher                      Version
--------------------------------  -----------------------------  ---------
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.13
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.14
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.15
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.16
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.17
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.2
LinuxAgent.AzureSecurityCenter    Qualys                         1.0.0.3
QualysAgent                       Qualys                         0.0.0.9
QualysAgent                       Qualys                         1.6.4.10
QualysAgent                       Qualys                         1.6.4.11
QualysAgent                       Qualys                         1.6.4.13
QualysAgent                       Qualys                         1.6.4.14
QualysAgent                       Qualys                         1.6.4.9
QualysAgent                       Qualys                         3.1.3.34
QualysAgentLinux                  Qualys                         1.5.0.72
QualysAgentLinux                  Qualys                         1.5.0.73
QualysAgentLinux                  Qualys                         1.5.0.82
QualysAgentLinux                  Qualys                         1.6.0.1
QualysAgentLinux                  Qualys                         1.6.0.100
QualysAgentLinux                  Qualys                         1.6.0.101
QualysAgentLinux                  Qualys                         1.6.0.105
QualysAgentLinux                  Qualys                         1.6.0.3
QualysAgentLinux                  Qualys                         1.6.0.90
QualysAgentLinux                  Qualys                         1.6.0.91
QualysAgentLinux                  Qualys                         1.6.0.93
QualysAgentLinux                  Qualys                         1.6.0.96
QualysAgentLinux                  Qualys                         1.6.1.4
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.10
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.15
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.16
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.18
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.20
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.21
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.5
WindowsAgent.AzureSecurityCenter  Qualys                         1.0.0.9
QualysAgentGL                     Qualys.LinuxAgent.GrayLabel    1.0.0.2
QualysAgentGL                     Qualys.WindowsAgent.GrayLabel  1.0.0.2
```

```bash
> az vm extension set --publisher Qualys --name QualysAgentLinux --settings '{"LicenseCode": "LICENSECODE"}' --ids "/subscriptions/SUBSCRIPTIONID/resourceGroups/RGNAME/providers/Microsoft.Compute/virtualMachines/VMNAME"

{
  "autoUpgradeMinorVersion": true,
  "enableAutomaticUpgrade": null,
  "forceUpdateTag": null,
  "id": "/subscriptions/SUBSCRIPTIONID/resourceGroups/RGNAME/providers/Microsoft.Compute/virtualMachines/VMNAME/extensions/QualysAgentLinux",
  "instanceView": null,
  "location": "westeurope",
  "name": "QualysAgentLinux",
  "protectedSettings": null,
  "protectedSettingsFromKeyVault": null,
  "provisioningState": "Succeeded",
  "publisher": "Qualys",
  "resourceGroup": "RGNAME",
  "settings": {
    "LicenseCode": "LICENSECODE"
  },
  "suppressFailures": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.6",
  "typePropertiesType": "QualysAgentLinux"
}
```