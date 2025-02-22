---
title: Export assessment methods and properties per device
description: Provides information about the APIs that pull "threat and vulnerability management" data. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization. Since the amount of data can be large, there are two ways it can be retrieved
keywords: api, apis, export assessment, per device assessment, per machine assessment, vulnerability assessment report, device vulnerability assessment, device vulnerability report, secure configuration assessment, secure configuration report, software vulnerabilities assessment, software vulnerability report, vulnerability report by machine,
search.product: eADQiWindows 10XVcnh
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: v-jweston
author: jweston-1
localization_priority: Normal
manager: dansimp
audience: ITPro
ms.collection: M365-security-compliance
ms.topic: article
ms.technology: mde
ms.custom: api
---
 
# Export assessment methods and properties per device

[!INCLUDE [Microsoft 365 Defender rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint](https://go.microsoft.com/fwlink/p/?linkid=2154037)
- [Microsoft 365 Defender](https://go.microsoft.com/fwlink/?linkid=2118804)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp?ocid=docs-wdatp-exposedapis-abovefoldlink)

[!include[Prerelease information](../../includes/prerelease.md)]

## API description

Provides methods and property details about the APIs that pull threat and vulnerability management data on a per-device basis. There are different API calls to get different types of data. In general, each API call contains the requisite data for devices in your organization.

> [!Note]
>
> Unless indicated otherwise, all export assessment methods listed are **_full export_** and **_by device_** (also referred to as **_per device_**).

There are three API methods that you can use to retrieve (export) different types of information:

1. Export secure configurations assessment

2. Export software inventory assessment

3. Export software vulnerabilities assessment

For each method, there are different API calls to get different types of data. Because the amount of data can be large, there are two ways it can be retrieved:

- **OData**  The API pulls all data in your organization as Json responses, following the OData protocol. This method is best for _small organizations with less than 100-K devices_. The response is paginated, so you can use the \@odata.nextLink field from the response to fetch the next results.

- **via files** This API solution enables pulling larger amounts of data faster and more reliably. Therefore, it is recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows:

  - Call the API to get a list of download URLs with all your organization data.

  - Download all the files using the download URLs and process the data as you like.

Data that is collected (using either _OData_ or _via files_) is the current snapshot of the current state, and does not contain historic data. In order to collect historic data, customers must save the data in their own data storages.

## 1. Export secure configurations assessment

Returns all of the configurations and their status, on a per-device basis.

### 1.1 Methods

Method | Data type | Description
:---|:---|:---
Export secure configuration assessment **(OData)** | Secure configuration by device collection. See: [1.2 Properties (OData)](#12-properties-odata) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId. The API pulls all data in your organization as Json responses, following the OData protocol. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
Export secure configuration assessment **(via files)** | Secure configuration by device collection. See: [1.2 Properties (OData)](#12-properties-odata) | Returns a table with an entry for every unique combination of DeviceId, ConfigurationId. This API solution enables pulling larger amounts of data faster and more reliably. Therefore, it is recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: 1.  Call the API to get a list of download URLs with all your organization data. 2.  Download all the files using the download URLs and process the data as you like.

### 1.2 Properties (OData)

Property (ID) | Data type | Description
:---|:---|:---
ConfigurationCategory | string | Category or grouping to which the configuration belongs: Application, OS, Network, Accounts, Security controls
ConfigurationId | string | Unique identifier for a specific configuration
ConfigurationImpact | string | Rated impact of the configuration to the overall configuration score (1-10)
ConfigurationName | string | Display name of the configuration
ConfigurationSubcategory | string | Subcategory or subgrouping to which the configuration belongs. In many cases, this describes specific capabilities or features.
DeviceId | string | Unique identifier for the device in the service.
DeviceName | string | Fully qualified domain name (FQDN) of the device.
IsApplicable | bool | Indicates whether the configuration or policy is applicable
IsCompliant | bool | Indicates whether the configuration or policy is properly configured
IsExpectedUserImpact | bool | Indicates whether there will be user impact if the configuration will be applied
OSPlatform | string | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 10 and Windows 7. See tvm supported operating systems and platforms for details.
RbacGroupName | string | The role-based access control (RBAC) group. If this device is not assigned to any RBAC group, the value will be “Unassigned.” If the organization doesn’t contain any RBAC groups, the value will be “None.”
RecommendationReference | string | A reference to the recommendation ID related to this software.
Timestamp | string | Last time the configuration was seen on the device

### 1.3 Properties (via files)

Property (ID) | Data type | Description
:---|:---|:---
Export files | array\[string\] | A list of download URLs for files holding the current snapshot of the organization.
GeneratedTime | string | The time that the export was generated.

## 2. Export software inventory assessment

Returns all of the installed software and their details on each device.

### 2.1 Methods

Method | Data type | Description
:---|:---|:---
Export software inventory assessment **(OData)** | Software inventory by device collection. See: [2.2 Properties (OData)](#22-properties-odata) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. The API pulls all data in your organization as Json responses, following the OData protocol. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
Export software inventory assessment **(via files)** | Software inventory by device files. See: [2.3 Properties (via files)](#23-properties-via-files) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion. This API solution enables pulling larger amounts of data faster and more reliably. Therefore, it is recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: 1.  Call the API to get a list of download URLs with all your organization data. 2.  Download all the files using the download URLs and process the data as you like.

### 2.2 Properties (OData)

Property (ID) | Data type | Description
:---|:---|:---
DeviceId | string | Unique identifier for the device in the service.
DeviceName | string | Fully qualified domain name (FQDN) of the device.
DiskPaths | Array[string]  | Disk evidence that the product is installed on the device.
EndOfSupportDate | string | The date in which support for this software has or will end.
EndOfSupportStatus | string | End of support status. Can contain these possible values: None, EOS Version, Upcoming EOS Version, EOS Software, Upcoming EOS Software.
Id | string | Unique identifier for the record.
NumberOfWeaknesses | int|Number of weaknesses on this software on this device
OSPlatform | string | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 10 and Windows 7. See tvm supported operating systems and platforms for details.
RbacGroupName | string | The role-based access control (RBAC) group. If this device is not assigned to any RBAC group, the value will be “Unassigned.” If the organization doesn’t contain any RBAC groups, the value will be “None.”
RegistryPaths | Array[string] | Registry evidence that the product is installed in the device.
SoftwareFirstSeenTimestamp | string | The first time this software was seen on the device.
SoftwareName | string | Name of the software product.
SoftwareVendor | string | Name of the software vendor.
SoftwareVersion | string | Version number of the software product.

### 2.3 Properties (via files)

Property (ID) | Data type | Description
:---|:---|:---
Export files | array\[string\] | A list of download URLs for files holding the current snapshot of the organization.
GeneratedTime | string | The time that the export was generated.

## 3. Export software vulnerabilities assessment

Returns all the known vulnerabilities on a device and their details, for all devices.

### 3.1 Methods

Method | Data type | Description
:---|:---|:---
Export software vulnerabilities assessment **(OData)** | Investigation collection See: [3.2 Properties (OData)](#32-properties-odata) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion, CveId. The API pulls all data in your organization as Json responses, following the OData protocol. This method is best for small organizations with less than 100-K devices. The response is paginated, so you can use the @odata.nextLink field from the response to fetch the next results.
Export software vulnerabilities assessment **(via files)** | Investigation entity See: [3.3 Properties (via files)](#33-properties-via-files) | Returns a table with an entry for every unique combination of DeviceId, SoftwareVendor, SoftwareName, SoftwareVersion, CveId. This API solution enables pulling larger amounts of data faster and more reliably. Therefore, it is recommended for large organizations, with more than 100-K devices. This API pulls all data in your organization as download files. The response contains URLs to download all the data from Azure Storage. This API enables you to download all your data from Azure Storage as follows: 1.  Call the API to get a list of download URLs with all your organization data. 2.  Download all the files using the download URLs and process the data as you like.

### 3.2 Properties (OData)

Property (ID) | Data type | Description
:---|:---|:---
CveId | string | Unique identifier assigned to the security vulnerability under the Common Vulnerabilities and Exposures (CVE) system.
CvssScore | string | The CVSS score of the CVE.
DeviceId | string | Unique identifier for the device in the service.
DeviceName | string | Fully qualified domain name (FQDN) of the device.
DiskPaths | Array\[string\] | Disk evidence that the product is installed on the device.
ExploitabilityLevel | string | The exploitability level of this vulnerability (NoExploit, ExploitIsPublic, ExploitIsVerified, ExploitIsInKit)
FirstSeenTimestamp | string | First time the CVE of this product was seen on the device.
Id | string | Unique identifier for the record.
LastSeenTimestamp | string | Last time the CVE was seen on the device.
OSPlatform | string | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 10 and Windows 7. See tvm supported operating systems and platforms for details.
RbacGroupName | string | The role-based access control (RBAC) group. If this device is not assigned to any RBAC group, the value will be “Unassigned.” If the organization doesn’t contain any RBAC groups, the value will be “None.”
RecommendationReference | string | A reference to the recommendation ID related to this software.
RecommendedSecurityUpdate | string | Name or description of the security update provided by the software vendor to address the vulnerability.
RecommendedSecurityUpdateId | string | Identifier of the applicable security updates or identifier for the corresponding guidance or knowledge base (KB) articles
Registry Paths Array\[string\] | Registry evidence that the product is installed in the device.
SoftwareName | string | Name of the software product.
SoftwareVendor | string | Name of the software vendor.
SoftwareVersion | string | Version number of the software product.
VulnerabilitySeverityLevel | string | Severity level assigned to the security vulnerability based on the CVSS score and dynamic factors influenced by the threat landscape.

### 3.3 Properties (via files)

Property (ID) | Data type | Description
:---|:---|:---
Export files | array\[string\]  | A list of download URLs for files holding the current snapshot of the organization.
GeneratedTime | string | The time that the export was generated.

## See also

- [Export secure configuration assessment per device](get-assessment-secure-config.md)

- [Export software inventory assessment per device](get-assessment-software-inventory.md)

- [Export software vulnerabilities assessment per device](get-assessment-software-vulnerabilities.md)

Other related

- [Risk-based threat & vulnerability management](next-gen-threat-and-vuln-mgt.md)

- [Vulnerabilities in your organization](tvm-weaknesses.md)
