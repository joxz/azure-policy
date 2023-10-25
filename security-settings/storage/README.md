# storage account security settings

Apply security settings for storage accounts:

 - Limit public network access
 - Enforce HTTPS and minium TLS version
 - Set SAS expiry policy [^1]

:bangbang: About SAS expiration policies
> A SAS expiration policy does not prevent a user from creating a SAS with an expiration that exceeds the limit recommended by the policy. When a user creates a SAS that violates the policy, they'll see a warning, together with the recommended maximum interval. If you have configured a diagnostic setting for logging with Azure Monitor, then Azure Storage writes a message to the SasExpiryStatus property in the logs whenever a user creates or uses a SAS that expires after the recommended interval. The message indicates that the validity interval of the SAS exceeds the recommended interval.

 [^1]: [Configure an expiration policy for shared access signatures](https://learn.microsoft.com/en-us/azure/storage/common/sas-expiration-policy?tabs=azure-portal)
