# modify vnet ddos protection settings

Adds non-compliant Vnets to an Azure [DDoS Network Protection Plan](https://learn.microsoft.com/en-us/azure/ddos-protection/ddos-protection-overview#tiers). 

[Only one DDoS protection Plan is needed per tenant](https://learn.microsoft.com/en-us/azure/ddos-protection/ddos-faq#how-does-pricing-work-):

> Under a tenant, a single DDoS protection plan can be used across multiple subscriptions, so there's no need to create more than one DDoS protection plan.

```pwsh
Get-AzPolicyAlias | Select-Object -ExpandProperty 'Aliases' | Where-Object { $_.DefaultMetadata.Attributes -eq 'Modifiable' -and $_.Name -like "*ddos*"}
```

Policy will apply the Vnet DDoS protection settings everytime a Vnet setting is updated (e.g. change DNS servers or add Service Endpoints)

[Policy functions](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/definition-structure#policy-functions)