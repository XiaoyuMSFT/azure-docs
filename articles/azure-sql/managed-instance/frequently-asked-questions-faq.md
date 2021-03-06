---
title: Frequently asked questions (FAQ)
titleSuffix: Azure SQL Managed Instance 
description: Azure SQL Managed Instance frequently asked questions (FAQ)
services: sql-database
ms.service: sql-managed-instance
ms.subservice: operations
ms.custom: sqldbrb=1
ms.devlang: 
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: sstein, carlrab
ms.date: 03/17/2020
---
# Azure SQL Managed Instance frequently asked questions (FAQ)
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

This article contains the most common questions about [Azure SQL Managed Instance](sql-managed-instance-paas-overview.md).

## Supported features

**Where can I find a list of features supported on SQL Managed Instance?**

For a list of supported features in SQL Managed Instance, see [Azure SQL Managed Instance features](../database/features-comparison.md).

For differences in syntax and behavior between Azure SQL Managed Instance and SQL Server, see [T-SQL differences from SQL Server](transact-sql-tsql-differences-sql-server.md).


## Technical specification, resource limits and other limitations
 
**Where can I find technical characteristics and resource limits for SQL Managed Instance?**

For available hardware generation characteristics, see [Technical differences in hardware generations](resource-limits.md#hardware-generation-characteristics).
For available service tiers and their characteristics, see [Technical differences between service tiers](resource-limits.md#service-tier-characteristics).

**What service tier am I eligible for?**

Any customer is eligible for any service tier. However, if you want to exchange your existing licenses for discounted rates on Azure SQL Managed Instance by using [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit/), bear in mind that SQL Server Enterprise Edition customers with Software Assurance are eligible for the [General Purpose](../database/service-tier-general-purpose.md) or [Business Critical](../database/service-tier-business-critical.md) performance tiers and SQL Server Standard Edition customers with Software Assurance are eligible for the General Purpose performance tier only. For more details, see [Specific rights of the AHB](../azure-hybrid-benefit.md?tabs=azure-powershell#what-are-the-specific-rights-of-the-azure-hybrid-benefit-for-sql-server).

**What subscription types are supported for SQL Managed Instance?**

For the list of supported subscription types, see [Supported subscription types](resource-limits.md#supported-subscription-types). 

**Which Azure regions are supported?**

Managed instances can be created in most of the Azure regions; see [Supported regions for SQL Managed Instance](https://azure.microsoft.com/global-infrastructure/services/?products=sql-database&regions=all). If you need managed instance in a region that is currently not supported, [send a support request via the Azure portal](../database/quota-increase-request.md).

**Are there any quota limitations for SQL Managed Instance deployments?**

Managed instance has two default limits: limit on the number of subnets you can use and a limit on the number of vCores you can provision. Limits vary across the subscription types and regions. For the list of regional resource limitations by subscription type, see table from [Regional resource limitation](resource-limits.md#regional-resource-limitations). These are soft limits that can be increased on demand. If you need to provision more managed instances in your current regions, send a support request to increase the quota using the Azure portal. For more information, see [Request quota increases for Azure SQL Database](../database/quota-increase-request.md).

**Can I increase the number of databases limit (100) on my managed instance on demand?**

No, and currently there are no committed plans to increase the number of databases on SQL Managed Instance. 

**Where can I migrate if I have more than 8TB of data?**
You can consider migrating to other Azure flavors that suit your workload: [Azure SQL Database Hyperscale](../database/service-tier-hyperscale.md) or [SQL Server on Azure Virtual Machines](../virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview.md).

**Where can I migrate if I have specific hardware requirements such as larger RAM to vCore ratio or more CPUs?**
You can consider migrating to [SQL Server on Azure Virtual Machines](../virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview.md) or [Azure SQL Database](../database/sql-database-paas-overview.md) memory/cpu optimized.

## Known issues & bugs

**Where can I find known issues and bugs?**

For bugs and known issues, see [Known issues](../database/doc-changes-updates-release-notes.md#known-issues).

## New features

**Where can I find latest features and the features in public preview?**

For new and preview features, see [Release notes](../database/doc-changes-updates-release-notes.md?tabs=managed-instance).

## Create, update, delete or move SQL Managed Instance

**How can I provision SQL Managed Instance?**

You can provision an instance from [Azure Portal](instance-create-quickstart.md), [PowerShell](scripts/create-configure-managed-instance-powershell.md), [Azure CLI](https://techcommunity.microsoft.com/t5/azure-sql-database/create-azure-sql-managed-instance-using-azure-cli/ba-p/386281) and [ARM templates](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/creating-azure-sql-managed-instance-using-arm-templates).

**Can I provision Managed Instances in an existing subscription?**

Yes, you can provision a Managed Instance in an existing subscription if that subscription belongs to the [Supported subscription types](resource-limits.md#supported-subscription-types).

**Why couldn’t I provision a Managed Instance in the subnet which name starts with a digit?**

This is a current limitation on underlying component that verifies subnet name against the regex ^[a-zA-Z_][^\\\/\:\*\?\"\<\>\|\`\'\^]*(?<![\.\s])$. All names that pass the regex and are valid subnet names are currently supported.

**How can I scale my managed instance?**

You can scale your managed instance from [Azure Portal](../database/service-tiers-vcore.md?tabs=azure-portal#selecting-a-hardware-generation), [PowerShell](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/change-size-azure-sql-managed-instance-using-powershell), [Azure CLI](https://docs.microsoft.com/cli/azure/sql/mi?view=azure-cli-latest#az-sql-mi-update) or [ARM templates](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/updating-azure-sql-managed-instance-properties-using-arm-templates).

**Can I move my Managed Instance from one region to another?**

Yes, you can. For instructions, see [Move resources across regions](../database/move-resources-across-regions.md).

**How can I delete my Managed Instance?**

You can delete Managed Instances via Azure Portal, [PowerShell](https://docs.microsoft.com/powershell/module/az.sql/remove-azsqlinstance?view=azps-4.3.0), [Azure CLI](https://docs.microsoft.com/cli/azure/sql/mi?view=azure-cli-latest#az-sql-mi-delete) or [Resource Manager REST APIs](https://docs.microsoft.com/rest/api/sql/managedinstances/delete).

**How much time does it take to create or update an instance, or to restore a database?**

Expected time to create a new managed instance or to change service tiers (vCores, storage), depends on several factors. See [Management operations](sql-managed-instance-paas-overview.md#management-operations).
 
## Naming conventions

**Can a managed instance have the same name as a SQL Server on-premises instance?**

Changing a managed instance name is not supported.

**Can I change DNS zone prefix?**

Yes, Managed Instance default DNS zone *.database.windows.net* can be changed. 

To use another DNS zone instead of the default, for example, *.contoso.com*: 
- Use CliConfig to define an alias. The tool is just a registry settings wrapper, so it can be done using group policy or a script as well.
- Use *CNAME* with the *TrustServerCertificate=true* option.

## Move a database from SQL Managed Instance 

**How can I move a database from SQL Managed Instance back to SQL Server or Azure SQL Database?**

You can [export a database to BACPAC](../database/database-export.md) and then [import the BACPAC file](../database/database-import.md). This is the recommended approach if your database is smaller than 100 GB.

Transactional replication can be used if all tables in the database have primary keys.

Native `COPY_ONLY` backups taken from SQL Managed Instance cannot be restored to SQL Server because SQL Managed Instance has a higher database version compared to SQL Server.

## Migrate an instance database

**How can I migrate my instance database to Azure SQL Database?**

One option is to [export the database to a BACPAC](../database/database-export.md) and then [import the BACPAC file](../database/database-import.md). 

This is the recommended approach if your database is smaller than 100 GB. Transactional replication can be used if all tables in the database have primary keys.

## Switch hardware generation 

**Can I switch my SQL Managed Instance hardware generation between Gen 4 and Gen 5 online?**

Automated online switching between hardware generations is possible if both hardware generations are available in the region where SQL Managed Instance is provisioned. In this case, you can check the [vCore model overview page](../database/service-tiers-vcore.md), which explains how to switch between hardware generations.

This is a long-running operation, as a new managed instance will be provisioned in the background and databases automatically transferred between the old and new instances, with a quick failover at the end of the process. 

**What if both hardware generations are not supported in the same region?**

If both hardware generations are not supported in the same region, changing the hardware generation is possible but must be done manually. This requires you to provision a new instance in the region where the wanted hardware generation is available, and manually back up and restore data between the old and new instances.

**What if there are not enough IP addresses for performing update operation?**

In case there are not enough IP addresses in the subnet where your managed instance is provisioned, you will have to create a new subnet and a new managed instance inside it. We also suggest that the new subnet is created with more IP addresses allocated so future update operations will avoid similar situations. (For proper subnet size, check [how to determine the size of a VNet subnet](vnet-subnet-determine-size.md).) After the new instance is provisioned, you can manually back up and restore data between the old and new instances or perform cross-instance [point-in-time restore](point-in-time-restore.md?tabs=azure-powershell). 


## Tune performance

**How do I tune performance of SQL Managed Instance?**

SQL Managed Instance in the General Purpose tier uses remote storage, so the size of data and log files matters to performance. For more information, see [Impact of log file size on General Purpose SQL Managed Instance performance](https://medium.com/azure-sqldb-managed-instance/impact-of-log-file-size-on-general-purpose-managed-instance-performance-21ad170c823e).

If your workload consists of lots of small transactions, consider switching the connection type from proxy to redirect mode.

## Maximum storage size

**What is the maximum storage size for SQL Managed Instance?**

Storage size for SQL Managed Instance depends on the selected service tier (General Purpose or Business Critical). For storage limitations of these service tiers, see [Service tier characteristics](../database/service-tiers-general-purpose-business-critical.md).

  
## Networking requirements 

**What are the current inbound/outbound NSG constraints on the Managed Instance subnet?**

The required NSG and UDR rules are documented [here](connectivity-architecture-overview.md#mandatory-inbound-security-rules-with-service-aided-subnet-configuration), and automatically set by the service.
Please keep in mind that these rules are just the ones we need for maintaining the service. To connect to managed instance and use different features you will need to set additional, feature specific rules, that you need to maintain.

**How can I set inbound NSG rules on management ports?**

SQL Managed Instance is responsible for setting rules on management ports. This is achieved through functionality named [service-aided subnet configuration](connectivity-architecture-overview.md#service-aided-subnet-configuration).
This is to ensure uninterrupted flow of management traffic in order to fulfill an SLA.

**Can I get the source IP ranges that are used for the inbound management traffic?**

Yes. You could analyze traffic coming through your networks security group by [configuring Network Watcher flow logs](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#analyze-traffic-to-or-from-a-network-security-group).

**Can I set NSG to control access to the data endpoint (port 1433)?**

Yes. After a Managed Instance is provisioned you can set NSG that controls inbound access to the port 1433. It is advised to narrow its IP range as much as possible.

**Can I set the NVA or on-premises firewall to filter the outbound management traffic based on FQDNs?**

No. This is not supported for several reasons:
-	Routing traffic that represent response to inbound management request would be asymmetric and could not work.
-	Routing traffic that goes to storage would be affected by throughput constraints and latency so this way we won’t be able to provide expected service quality and availability.
-	Based on experience, these configurations are error prone and not supportable.

**Can I set the NVA or firewall for the outbound non-management traffic?**

Yes. The simplest way to achieve this is to add 0/0 rule to a UDR associated with managed instance subnet to route traffic through NVA.
 
**How many IP addresses do I need for a Managed Instance?**

Subnet must have sufficient number of available [IP addresses](connectivity-architecture-overview.md#network-requirements). To determine VNet subnet size for SQL Managed Instance, see [Determine required subnet size and range for Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-determine-size-vnet-subnet). 

**What if there are not enough IP addresses for performing instance update operation?**

In case there are not enough [IP addresses](connectivity-architecture-overview.md#network-requirements) in the subnet where your managed instance is provisioned, you will have to create a new subnet and a new managed instance inside it. We also suggest that the new subnet is created with more IP addresses allocated so future update operations will avoid similar situations. After the new instance is provisioned, you can manually back up and restore data between the old and new instances or perform cross-instance [point-in-time restore](point-in-time-restore.md?tabs=azure-powershell).

**Do I need an empty subnet to create a Managed Instance?**

No. You can use either an empty subnet or a subnet that already contains Managed Instance(s). 

**Can I change the subnet address range?**

Not if there are Managed Instances inside. This is an Azure networking infrastructure limitation. You are only allowed to [add additional address space to an empty subnet](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-subnet#change-subnet-settings). 

**Can I move my managed instance to another subnet?**

No. This is a current Managed Instance design limitation. However, you can provision a new instance in another subnet and manually back up and restore data between the old and the new instance or perform cross-instance [point-in-time restore](point-in-time-restore.md?tabs=azure-powershell).

**Do I need an empty virtual network to create a Managed Instance?**

This is not required. You can either [Create a virtual network for Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-vnet-subnet) or [Configure an existing virtual network for Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).

**Can I place a Managed Instance with other services in a subnet?**

No. Currently we do not support placing Managed Instance in a subnet that already contains other resource types.


## Mitigate data exfiltration risks  

**How can I mitigate data exfiltration risks?**

To mitigate any data exfiltration risks, customers are recommended to apply a set of security settings and controls:

- Turn on [Transparent Data Encryption (TDE)](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql) on all databases.
- Turn off Common Language Runtime (CLR). This is recommended on-premises as well.
- Use Azure Active Directory (Azure AD) authentication only.
- Access the instance with a low-privileged DBA account.
- Configure JIT jumpbox access for the sysadmin account.
- Turn on [SQL auditing](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine), and integrate it with alerting mechanisms.
- Turn on [Threat Detection](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) from the [advanced data security (ADS)](https://docs.microsoft.com/azure/sql-database/sql-database-advanced-data-security) suite.


## Cost-saving use cases

**Where can I find use cases and resulting cost savings with SQL Managed Instance?**

SQL Managed Instance case studies:

- [Komatsu](https://customers.microsoft.com/story/komatsu-australia-manufacturing-azure)
- [KMD](https://customers.microsoft.com/en-ca/story/kmd-professional-services-azure-sql-database)
- [PowerDETAILS](https://customers.microsoft.com/story/powerdetails-partner-professional-services-azure-sql-database-managed-instance)
- [Allscripts](https://customers.microsoft.com/story/allscripts-partner-professional-services-azure)

To get a better understanding of the benefits, costs, and risks associated with deploying Azure SQL Managed Instance, there's also a Forrester study: [The Total Economic Impact of Microsoft Azure SQL Database Managed Instance](https://azure.microsoft.com/resources/forrester-tei-sql-database-managed-instance).


## DNS

**Can I configure a custom DNS for SQL Managed Instance?**

Yes. See [How to configure a Custom DNS for Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

**Can I do DNS refresh?**

Currently, we don't provide a feature to refresh DNS server configuration for SQL Managed Instance.

DNS configuration is eventually refreshed:

- When DHCP lease expires.
- On platform upgrade.

As a workaround, downgrade SQL Managed Instance to 4 vCores and upgrade it again afterward. This has a side effect of refreshing the DNS configuration.


## IP address

**Can I connect to SQL Managed Instance using an IP address?**

Connecting to SQL Managed Instance using an IP address is not supported. The SQL Managed Instance host name maps to a load balancer in front of the SQL Managed Instance virtual cluster. As one virtual cluster could host multiple managed instances, connections cannot be routed to the proper managed instance without specifying the name explicitly.

For more information on SQL Managed Instance virtual cluster architecture, see [Virtual cluster connectivity architecture](connectivity-architecture-overview.md#virtual-cluster-connectivity-architecture).

**Can SQL Managed Instance have a static IP address?**

In rare but necessary situations, we might need to do an online migration of SQL Managed Instance to a new virtual cluster. If needed, this migration is because of changes in our technology stack aimed to improve security and reliability of the service. Migrating to a new virtual cluster results in changing the IP address that is mapped to the SQL Managed Instance host name. The SQL Managed Instance service doesn't claim static IP address support and reserves the right to change it without notice as a part of regular maintenance cycles.

For this reason, we strongly discourage relying on immutability of the IP address as it could cause unnecessary downtime.

## Change time zone

**Can I change the time zone for an existing managed instance?**

Time zone configuration can be set when a managed instance is provisioned for the first time. Changing the time zone of an existing managed instance isn't supported. For details, see [Time zone limitations](timezones-overview.md#limitations).

Workarounds include creating a new managed instance with the proper time zone and then either performing a manual backup and restore, or what we recommend, performing a [cross-instance point-in-time restore](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2018/06/07/cross-instance-point-in-time-restore-in-azure-sql-database-managed-instance/).


## Security and database encryption

**Is the sysadmin server role available for SQL Managed Instance?**

Yes, customers can create logins that are members of the sysadmin role.  Customers who assume the sysadmin privilege are also assuming responsibility for operating the instance, which can negatively impact the SLA commitment. To add login to sysadmin server role, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-aad-security-tutorial#azure-ad-authentication).

**Is Transparent Data Encryption supported for SQL Managed Instance?**

Yes, Transparent Data Encryption is supported for SQL Managed Instance. For details, see [Transparent Data Encryption for SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql?tabs=azure-portal).

**Can I leverage the “bring your own key” model for TDE?**

Yes, Azure Key Vault for BYOK scenario is available for Azure SQL Managed Instance. For details, see [Transparent Data Encryption with customer-managed key](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-ver15&tabs=azure-portal#customer-managed-transparent-data-encryption---bring-your-own-key).

**Can I migrate an encrypted SQL Server database?**

Yes, you can. To migrate an encrypted SQL Server database, you need to export and import your existing certificates into Managed Instance, then take a full database backup and restore it in Managed Instance. 

You can also use [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) to migrate the TDE encrypted databases.

**How can I configure TDE protector rotation for SQL Managed Instance?**

You can rotate TDE protector for Managed Instance using Azure Cloud Shell. For instructions, see [Transparent Data Encryption in SQL Managed Instance using your own key from Azure Key Vault](scripts/transparent-data-encryption-byok-powershell.md).

**Can I restore my encrypted database to SQL Managed Instance?**

Yes, you don't need to decrypt your database to restore it to SQL Managed Instance. You do need to provide a certificate/key used as the encryption key protector on the source system to SQL Managed Instance to be able to read data from the encrypted backup file. There are two possible ways to do it:

- *Upload certificate-protector to SQL Managed Instance*. It can be done using PowerShell only. The [sample script](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-migrate-tde-certificate) describes the whole process.
- *Upload asymmetric key-protector to Azure Key Vault and point SQL Managed Instance to it*. This approach resembles bring-your-own-key (BYOK) TDE use case that also uses Key Vault integration to store the encryption key. If you don't want to use the key as an encryption key protector, and just want to make the key available for SQL Managed Instance to restore encrypted database(s), follow instructions for [setting up BYOK TDE](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql#manage-transparent-data-encryption), and don’t check the checkbox **Make the selected key the default TDE protector**.

Once you make the encryption protector available to SQL Managed Instance, you can proceed with the standard database restore procedure.

## Purchasing models and benefits

**What purchasing models are available for SQL Managed Instance?**

SQL Managed Instance offers [vCore-based purchasing model](sql-managed-instance-paas-overview.md#vcore-based-purchasing-model).

**What cost benefits are available for SQL Managed Instance?**

You can save costs with the Azure SQL benefits in the following ways:
-	Maximize existing investments in on-premises licenses and save up to 55 percent with [Azure Hybrid Benefit](https://docs.microsoft.com/azure/azure-sql/azure-hybrid-benefit?tabs=azure-powershell). 
-	Commit to a reservation for compute resources and save up to 33 percent with [Reserved Instance Benefit](https://docs.microsoft.com/azure/sql-database/sql-database-reserved-capacity). Combine this with Azure Hybrid benefit for savings up to 82 percent. 
-	Save up to 55 percent versus list prices with [Azure Dev/Test Pricing Benefit](https://azure.microsoft.com/pricing/dev-test/) that offers discounted rates for your ongoing development and testing workloads.

**Who is eligible for Reserved Instance benefit?**

To be eligible for reserved Instance benefit, your subscription type must be an enterprise agreement (offer numbers: MS-AZR-0017P or MS-AZR-0148P) or an individual agreement with pay-as-you-go pricing (offer numbers: MS-AZR-0003P or MS-AZR-0023P). For more information about reservations, see [Reserved Instance Benefit](https://docs.microsoft.com/azure/sql-database/sql-database-reserved-capacity). 

**Is it possible to cancel, exchange or refund reservations?**

You can cancel, exchange or refund reservations with certain limitations. For more information, see [Self-service exchanges and refunds for Azure Reservations](https://docs.microsoft.com/azure/cost-management-billing/reservations/exchange-and-refund-azure-reservations).

## Billing for Managed Instance and backup storage

**What are the SQL Managed Instance pricing options?**

To explore Managed Instance pricing options, see [Pricing page](https://azure.microsoft.com/pricing/details/azure-sql/sql-managed-instance/single/).

**How can I track billing cost for my managed instance?**

You can do so using the [Azure Cost Management solution](https://docs.microsoft.com/azure/cost-management-billing/). Navigate to **Subscriptions** in the [Azure portal](https://portal.azure.com) and select **Cost Analysis**. 

Use the **Accumulated costs** option and then filter by the **Resource type** as `microsoft.sql/managedinstances`.

**How much automated backups cost?**

You get the equal amount of free backup storage space as the reserved data storage space purchased, regardless of the backup retention period set. If your backup storage consumption is within the allocated free backup storage space, automated backups on managed instance will have no additional cost for you, therefore will be free of charge. Exceeding the use of backup storage above the free space will result in costs of about $0.20 - $0.24 per GB/month in US regions, or see the pricing page for details for your region. For more details, see [Backup storage consumption explained](https://techcommunity.microsoft.com/t5/azure-sql-database/backup-storage-consumption-on-managed-instance-explained/ba-p/1390923).

**How can I monitor billing cost for my backup storage consumption?**

You can monitor cost for backup storage via Azure Portal. For instructions, see [Monitor costs for automated backups](https://docs.microsoft.com/azure/azure-sql/database/automated-backups-overview?tabs=managed-instance#monitor-costs). 

**How can I optimize my backup storage costs on the managed instance?**

To optimize your backup storage costs, see [Fine backup tuning on SQL Managed Instance](https://techcommunity.microsoft.com/t5/azure-sql-database/fine-tuning-backup-storage-costs-on-managed-instance/ba-p/1390935).

## Password policy 

**What password policies are applied for SQL Managed Instance SQL logins?**

SQL Managed Instance password policy for SQL logins inherits Azure platform policies that are applied to the VMs forming virtual cluster holding the managed instance. At the moment it is not possible to change any of these settings as these settings are defined by Azure and inherited by managed instance.

 > [!IMPORTANT]
 > Azure platform can change policy requirements without notifying services relying on that policies.

**What are current Azure platform policies?**

Each login must set its password upon login and change its password after it reaches maximum age.

| **Policy** | **Security Setting** |
| --- | --- |
| Maximum password age | 42 days |
| Minimum password age | 1 day |
| Minimum password length | 10 characters |
| Password must meet complexity requirements | Enabled |

**Is it possible to disable password complexity and expiration in SQL Managed Instance on login level?**

Yes, it is possible to control CHECK_POLICY and CHECK_EXPIRATION fields on login level. You can check current settings by executing following T-SQL command:

```sql
SELECT *
FROM sys.sql_logins
```

After that, you can modify specified login settings by executing :

```sql
ALTER LOGIN <login_name> WITH CHECK_POLICY = OFF;
ALTER LOGIN <login_name> WITH CHECK_EXPIRATION = OFF;
```

(replace 'test' with desired login name and adjust policy and expiration values)

## Azure feedback and support

**Where can I leave my ideas for SQL Managed Instance improvements?**

You can vote for a new Managed Instance feature or put a new improvement idea on voting on [SQL Managed Instance Feedback Forum](https://feedback.azure.com/forums/915676-sql-managed-instance). This way you can contribute to the product development and help us prioritize our potential improvements.

**How can I create Azure support request?**

To learn how to create Azure support request, see [How to create Azure support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).

