# EntraID Role Best Practices
This is for determining the best practices and assigning least-privilege for all Entra ID and Defender XDR roles. EntraID is now controlling the majority of permissions in the Microsoft ecosystem. For those items which are not included by EntraID coverage, they may contain documentation on building custom roles such as Defender XDR RBAC, Microsoft Purview, and Cloud App Security. 

All documentation here is based on an average organization structure which would have an entry-level, mid-level, and senior-level analyst/engineer. Each organization is different and this document may not reflect your exact organization structure, so it is important to verify each permission granted for proper access control. Do not blindly apply permissions. 

_Disclaimer: I do not work for microsoft and this information may be incorrect. Always do your own due-dilligence._

# Links and Resources
This document relies heavily on Microsoft's official documentation. These are the resources that were used to come to the conclusions in this document.

* Microsoft RBAC roles delegated by task
	* https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/delegate-by-task
  * This document allows you to very easily compare tasks that need to be completed and the associated least privileged role for each task. This will give you a better understanding how the minimum role assignment needed for any given task.
* Microsoft RBAC Permissions Reference
	* https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference
	* This document is used as a reference for every default role that Microsoft has created. This is the master document used for determining the full breadth and depth of each role's reach. 

# Roles
Each role is separated into its respective portal. EntraID is the main role grant, while Defender XDR RBAC and Cloud App Security are supplementary to EntraID. 

## Entra ID

### Security Engineer - Tier 1 - Custom Role
Purpose: This role is the general analyst for the organization. They are in the trenches every day and frequently need to see deep into the logs to triage events. This role is going to be the least permissive Security Engineer position, but that role also comes with greater permissions overall than similar engineer positions.

#### Role Assignments
* Attack Payload Author
* Authentication Administrator 
* Cloud Device Administrator
* Message Center Reader
* Security Reader
* Service Support Administrator

#### Permission Details

##### Attack Payload author
Users in this role can create attack payloads but not actually launch or schedule them. Attack payloads are then available to all administrators in the tenant who can use them to create a simulation.

| Permission | Description |
| --- | --- |
| `microsoft.office365.protectionCenter/attackSimulator/payload/allProperties/allTasks` | Create and manage attack payloads in Attack Simulator |
| `microsoft.office365.protectionCenter/attackSimulator/reports/allProperties/read` | Create and manage attack payloads in Attack Simulator |

##### Authentication Administrator - Privileged
This role allows users to reset authentication settings such as password, change MFA authentication type, clear saved authentication credentials, revoke sign-ins, and more. This role specifically prevents the admin from resetting admin authentication. 

| Permission | Description |
| --- | --- |
| `microsoft.directory/users/authenticationMethods/create` | Update authentication methods for users |
| `microsoft.directory/users/authenticationMethods/delete` | Delete authentication methods for users - Privileged |
| `microsoft.directory/users/authenticationMethods/standard/restrictedRead` | Read standard properties of authentication methods that do not include personally identifiable information for users |
| `microsoft.directory/users/authenticationMethods/basic/update` | Update basic properties of authentication methods for users - Privileged |
| `microsoft.directory/deletedItems.users/restore` | Restore soft deleted users to original state - Privileged |
| `microsoft.directory/users/delete` | Delete users - Privileged |
| `microsoft.directory/users/disable` | Disable Users - Privileged |
| `microsoft.directory/users/enable` | Enable Users - Privileged |
| `microsoft.directory/users/invalidateAllRefreshTokens` | Force sign-out by invalidating user refresh tokens - Privileged |
| `microsoft.directory/users/restore` | Restore deleted users |
| `microsoft.directory/users/basic/update` | Update basic properties on users |
| `microsoft.directory/users/manager/update` | Update manager for users |
| `microsoft.directory/users/password/update` | Reset passwords for all users - Privileged |
| `microsoft.directory/users/userPrincipalName/update` | Update User Principal Name of users - Privileged |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

##### Cloud Device Administrator
This is a privileged role. Users in this role can enable, disable, and delete devices in Microsoft Entra ID and read Windows 10 BitLocker keys (if present) in the Azure portal. The role does not grant permissions to manage any other properties on the device.

| Permission | Description |
| --- | --- |
| `microsoft.directory/auditLogs/allProperties/read` | Read all properties on audit logs, excluding custom security attributes audit logs |
| `microsoft.directory/authorizationPolicy/standard/read` | Read standard properties of authorization policy |
| `microsoft.directory/bitlockerKeys/key/read` | Read bitlocker metadata and key on devices |
| `microsoft.directory/deletedItems.devices/delete` | Permanently delete devices, which can no longer be restored |
| `microsoft.directory/deletedItems.devices/restore` | Restore soft deleted devices to original state |
| `microsoft.directory/devices/delete` | Delete devices from Microsoft Entra ID |
| `microsoft.directory/devices/disable` | Disable devices in Microsoft Entra ID |
| `microsoft.directory/devices/enable` | Enable devices in Microsoft Entra ID |
| `microsoft.directory/deviceLocalCredentials/password/read` | Read all properties of the backed up local administrator account credentials for Microsoft Entra joined devices, including the password |
| `microsoft.directory/deviceManagementPolicies/standard/read` | Read standard properties on device management application policies |
| `microsoft.directory/deviceManagementPolicies/basic/update` | Update basic properties on device management application policies |
| `microsoft.directory/deviceRegistrationPolicy/standard/read` | Read standard properties on device registration policies |
| `microsoft.directory/deviceRegistrationPolicy/basic/update` | Update basic properties on device registration policies |
| `microsoft.directory/signInReports/allProperties/read` | Read all properties on sign-in reports, including privileged properties |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |

##### Message Center Reader
Users in this role can monitor notifications and advisory health updates in Message center for their organization on configured services such as Exchange, Intune, and Microsoft Teams. Message Center Readers receive weekly email digests of posts, updates, and can share 		message center posts in Microsoft 365. In Microsoft Entra ID, users assigned to this role will only have read-only access on Microsoft Entra services such as users and groups. This role has no access to view, create, or manage support tickets.

| Permission | Description |
| --- | --- |
| `microsoft.office365.messageCenter/messages/read` | Read messages in Message Center in the Microsoft 365 admin center, excluding security messages |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

##### Security Reader - Privileged
This is a privileged role. Users with this role have global read-only access on security-related feature, including all information in Microsoft 365 Defender portal, Microsoft Entra ID Protection, Privileged Identity Management, as well as the ability to read Microsoft 		Entra sign-in reports and audit logs, and in Microsoft Purview compliance portal. For more information about Office 365 permissions, see Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview compliance.

| Permission | Description |
| --- | --- |
| `microsoft.directory/accessReviews/definitions/allProperties/read` | Read all properties of access reviews of all reviewable resources in Microsoft Entra ID |
| `microsoft.directory/auditLogs/allProperties/read` | Read all properties on audit logs, excluding custom security attributes audit logs |
| `microsoft.directory/authorizationPolicy/standard/read` | Read standard properties of authorization policy |
| `microsoft.directory/bitlockerKeys/key/read` | Read bitlocker metadata and key on devices - Privileged |
| `microsoft.directory/deviceLocalCredentials/standard/read` | Read all properties of the backed up local administrator account credentials for Microsoft Entra joined devices, except the password |
| `microsoft.directory/domains/federationConfiguration/standard/read` | Read standard properties of federation configuration for domains |
| `microsoft.directory/entitlementManagement/allProperties/read` | Read all properties in Microsoft Entra entitlement management |
| `microsoft.directory/identityProtection/allProperties/read` | Read all resources in Microsoft Entra ID Protection |
| `microsoft.directory/namedLocations/standard/read` | Read basic properties of custom rules that define network locations |
| `microsoft.directory/policies/standard/read` | Read basic properties on policies |
| `microsoft.directory/policies/owners/read` | Read owners of policies |
| `microsoft.directory/policies/policyAppliedTo/read` | Read policies.policyAppliedTo property |
| `microsoft.directory/conditionalAccessPolicies/standard/read` | Read Conditional Access for policies |
| `microsoft.directory/conditionalAccessPolicies/owners/read` | Read the owners of Conditional Access policies |
| `microsoft.directory/conditionalAccessPolicies/policyAppliedTo/read` | Read the "applied to" property for Conditional Access policies |
| `microsoft.directory/multiTenantOrganization/joinRequest/standard/read` | Read properties of a multi-tenant organization join request |
| `microsoft.directory/multiTenantOrganization/standard/read` | Read basic properties of a multi-tenant organization |
| `microsoft.directory/multiTenantOrganization/tenants/organizationDetails/read` | Read organization details of a tenant participating in a multi-tenant organization |
| `microsoft.directory/multiTenantOrganization/tenants/standard/read` | Read basic properties of a tenant participating in a multi-tenant organization |
| `microsoft.directory/privilegedIdentityManagement/allProperties/read` | Read all resources in Privileged Identity Management |
| `microsoft.directory/provisioningLogs/allProperties/read` | Read all properties of provisioning logs |
| `microsoft.directory/signInReports/allProperties/read` | Read all properties on sign-in reports, including privileged properties |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.networkAccess/allEntities/allProperties/read` | Read all aspects of Microsoft Entra Network Access |
| `microsoft.office365.protectionCenter/allEntities/standard/read` | Read standard properties of all resources in the Security and Compliance centers |
| `microsoft.office365.protectionCenter/attackSimulator/payload/allProperties/read` | Read all properties of attack payloads in Attack Simulator |
| `microsoft.office365.protectionCenter/attackSimulator/reports/allProperties/read` | Read reports of attack simulation, responses, and associated training |
| `microsoft.office365.protectionCenter/attackSimulator/simulation/allProperties/read` | Read all properties of attack simulation templates in Attack Simulator |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

| Permission | Description |
| --- | --- |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationIdentitySynchronization/standard/read` | Read basic properties of cross tenant sync policy templates for multi-tenant organization |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationPartnerConfiguration/standard/read` | Read basic properties of cross tenant access policy templates for multi-tenant organization |


##### Service Support Administrator
Users with this role can create and manage support requests with Microsoft for Azure and Microsoft 365 services, and view the service dashboard and message center in the Azure portal and Microsoft 365 admin center.

| Permission | Description |
| --- | --- |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.office365.network/performance/allProperties/read` | Read all network performance properties in the Microsoft 365 admin center |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

### Security Engineer - Tier 2
Title: Security Engineer 2
Tier: Two
Purpose: This role is specifically intended to be used by the level two engineer. In most mid-sized organizations, this is what is classified as your mid to senior level position and will have permissions to do most things. That being said, it is not a global admin nor does it have tenant level permissions.

#### Microsoft Entra ID Role Assignments

##### Attack Simulation Administrator
Users in this role can create and manage all aspects of attack simulation creation, launch/scheduling of a simulation, and the review of simulation results. Members of this role have this access for all simulations in the tenant.

| Permission | Description |
| --- | --- |
| `microsoft.office365.protectionCenter/attackSimulator/payload/allProperties/allTasks` | Create and manage attack payloads in Attack Simulator | 
| `microsoft.office365.protectionCenter/attackSimulator/reports/allProperties/read` | Read reports of attack simulation, responses, and associated training |
| `microsoft.office365.protectionCenter/attackSimulator/simulation/allProperties/allTasks` | Create and manage attack simulation templates in Attack Simulator |

	
##### Authentication Administrator - Privileged
This role allows users to reset authentication settings such as password, change MFA authentication type, clear saved authentication credentials, revoke sign-ins, and more. This role specifically prevents the admin from resetting admin authentication. 
| Permission | Description |
| --- | --- |
| `microsoft.directory/users/authenticationMethods/create` | Update authentication methods for users |
| `microsoft.directory/users/authenticationMethods/delete` | Delete authentication methods for users - Privileged |
| `microsoft.directory/users/authenticationMethods/standard/restrictedRead` | Read standard properties of authentication methods that do not include personally identifiable information for users` |
| `microsoft.directory/users/authenticationMethods/basic/update` | Update basic properties of authentication methods for users - Privileged |
| `microsoft.directory/deletedItems.users/restore` | Restore soft deleted users to original state - Privileged |
| `microsoft.directory/users/delete` | Delete users - Privileged |
| `microsoft.directory/users/disable` | Disable Users - Privileged |
| `microsoft.directory/users/enable` | Enable Users - Privileged |
| `microsoft.directory/users/invalidateAllRefreshTokens` | Force sign-out by invalidating user refresh tokens - Privileged |
| `microsoft.directory/users/restore` | Restore deleted users |
| `microsoft.directory/users/basic/update` | Update basic properties on users |
| `microsoft.directory/users/manager/update` | Update manager for users |
| `microsoft.directory/users/password/update` | Reset passwords for all users - Privileged |
| `microsoft.directory/users/userPrincipalName/update` | Update User Principal Name of users - Privileged |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

##### Cloud Device Administrator
This is a privileged role. Users in this role can enable, disable, and delete devices in Microsoft Entra ID and read Windows 10 BitLocker keys (if present) in the Azure portal. The role does not grant permissions to manage any other properties on the device.

##### Intune Administrator
This is a privileged role. Users with this role have global permissions within Microsoft Intune Online, when the service is present. Additionally, this role contains the ability to manage users and devices in order to associate policy, as well as create and manage groups. For more information, see Role-based administration control (RBAC) with Microsoft Intune.

This role can create and manage all security groups. However, Intune Administrator does not have admin rights over Office groups. That means the admin cannot update owners or memberships of all Office groups in the organization. However, he/she can manage the Office group that he creates which comes as a part of his/her end-user privileges. So, any Office group (not security group) that he/she creates should be counted against his/her quota of 250.


| Actions | Description |
| --- | --- |
| `microsoft.directory/bitlockerKeys/key/read` | Read bitlocker metadata and key on devices |
| `microsoft.directory/contacts/create` | Create contacts |
| `microsoft.directory/contacts/delete` | Delete contacts |
| `microsoft.directory/contacts/basic/update` | Update basic properties on contacts |
| `microsoft.directory/deletedItems.devices/delete` | Permanently delete devices, which can no longer be restored |
| `microsoft.directory/deletedItems.devices/restore` | Restore soft deleted devices to original state |
| `microsoft.directory/devices/create` | Create devices (enroll in Microsoft Entra ID) |
| `microsoft.directory/devices/delete` | Delete devices from Microsoft Entra ID |
| `microsoft.directory/devices/disable` | Disable devices in Microsoft Entra ID |
| `microsoft.directory/devices/enable` | Enable devices in Microsoft Entra ID |
| `microsoft.directory/devices/basic/update` | Update basic properties on devices |
| `microsoft.directory/devices/extensionAttributeSet1/update` | Update the extensionAttribute1 to extensionAttribute5 properties on devices |
| `microsoft.directory/devices/extensionAttributeSet2/update` | Update the extensionAttribute6 to extensionAttribute10 properties on devices |
| `microsoft.directory/devices/extensionAttributeSet3/update` | Update the extensionAttribute11 to extensionAttribute15 properties on devices |
| `microsoft.directory/devices/registeredOwners/update` | Update registered owners of devices |
| `microsoft.directory/devices/registeredUsers/update` | Update registered users of devices |
| `microsoft.directory/deviceLocalCredentials/password/read` | Read all properties of the backed up local administrator account credentials for Microsoft Entra joined devices, including the password |
| `microsoft.directory/deviceManagementPolicies/standard/read` | Read standard properties on device management application policies |
| `microsoft.directory/deviceRegistrationPolicy/standard/read` | Read standard properties on device registration policies |
| `microsoft.directory/groups/hiddenMembers/read` | Read hidden members of Security groups and Microsoft 365 groups, including role-assignable groups |
| `microsoft.directory/groups.security/create` | Create Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/delete` | Delete Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/basic/update` | Update basic properties on Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/classification/update` | Update the classification property on Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/dynamicMembershipRule/update` | Update the dynamic membership rule on Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/members/update` | Update members of Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/owners/update` | Update owners of Security groups, excluding role-assignable groups |
| `microsoft.directory/groups.security/visibility/update` | Update the visibility property on Security groups, excluding role-assignable groups |
| `microsoft.directory/users/basic/update` | Update basic properties on users |
| `microsoft.directory/users/manager/update` | Update manager for users |
| `microsoft.directory/users/photo/update` | Update photo of users |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.cloudPC/allEntities/allProperties/allTasks` | Manage all aspects of Windows 365 |
| `microsoft.intune/allEntities/allTasks` | Manage all aspects of Microsoft Intune |
| `microsoft.office365.organizationalMessages/allEntities/allProperties/read` | Read all aspects of Microsoft 365 Organizational Messages |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |

##### Message Center Privacy Reader
Users in this role can monitor all notifications in the Message Center, including data privacy messages. Message Center Privacy Readers get email notifications including those related to data privacy and they can unsubscribe using Message Center Preferences. Only the Global Administrator and the Message Center Privacy Reader can read data privacy messages. Additionally, this role contains the ability to view groups, domains, and subscriptions. This role has no permission to view, create, or manage service requests.

| Permission | Description |
| --- | --- |
| `microsoft.office365.messageCenter/messages/read` | Read messages in Message Center in the Microsoft 365 admin center, excluding security messages
| `microsoft.office365.messageCenter/securityMessages/read` | Read security messages in Message Center in the Microsoft 365 admin center
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center 

##### Security Operator - Privileged
This is a privileged role. Users with this role can manage alerts and have global read-only access on security-related features, including all information in Microsoft 365 Defender portal, Microsoft Entra ID Protection, Privileged Identity Management and Microsoft Purview compliance portal. For more information about Office 365 permissions, see Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview compliance.

| In | Can do |
| --- | --- |
| Microsoft 365 Defender portal | All permissions of the Security Reader role<br>View, investigate, and respond to security threats alerts<br>Manage security settings in Microsoft 365 Defender portal |
| Identity Protection | All permissions of the Security Reader role<br>Perform all Identity Protection operations except for configuring or changing risk-based policies, resetting passwords, and configuring alert e-mails. |
| Privileged Identity Management | All permissions of the Security Reader role |
| Microsoft Purview compliance portal | All permissions of the Security Reader role<br>View, investigate, and respond to security alerts |
| Microsoft Defender for Endpoint | All permissions of the Security Reader role<br>View, investigate, and respond to security alerts<br>When you turn on role-based access control in Microsoft Defender for Endpoint, users with read-only permissions such as the Security Reader role lose access until they are assigned a Microsoft Defender for Endpoint role. |
| Intune | All permissions of the Security Reader role |
| Microsoft Defender for Cloud Apps | All permissions of the Security Reader role<br>View, investigate, and respond to security alerts |
| Microsoft 365 service health | View the health of Microsoft 365 services |

| Actions | Description |
| --- | --- |
| `microsoft.directory/auditLogs/allProperties/read` | Read all properties on audit logs, excluding custom security attributes audit logs |
| `microsoft.directory/authorizationPolicy/standard/read` | Read standard properties of authorization policy |
| `microsoft.directory/cloudAppSecurity/allProperties/allTasks` | Create and delete all resources, and read and update standard properties in Microsoft Defender for Cloud Apps |
| `microsoft.directory/identityProtection/allProperties/allTasks` | Create and delete all resources, and read and update standard properties in Microsoft Entra ID Protection |
| `microsoft.directory/privilegedIdentityManagement/allProperties/read` | Read all resources in Privileged Identity Management |
| `microsoft.directory/provisioningLogs/allProperties/read` | Read all properties of provisioning logs |
| `microsoft.directory/signInReports/allProperties/read` | Read all properties on sign-in reports, including privileged properties |
| `microsoft.azure.advancedThreatProtection/allEntities/allTasks` | Manage all aspects of Azure Advanced Threat Protection |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.intune/allEntities/read` | Read all resources in Microsoft Intune |
| `microsoft.office365.securityComplianceCenter/allEntities/allTasks` | Create and delete all resources, and read and update standard properties in the Office 365 Security & Compliance Center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.windows.defenderAdvancedThreatProtection/allEntities/allTasks` | Manage all aspects of Microsoft Defender for Endpoint |


##### Service Support Administrator
Users with this role can create and manage support requests with Microsoft for Azure and Microsoft 365 services, and view the service dashboard and message center in the Azure portal and Microsoft 365 admin center.
| Permission | Description |
| --- | --- |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.office365.network/performance/allProperties/read` | Read all network performance properties in the Microsoft 365 admin center |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center | 


## Defender XDR Role-Based Access Control

### Microsoft Defender XDR Role-Based Access Control - Tier 1
Title: Security Role - Tier 1
Tier: One

#### Permissions
This role is configured under Microsoft Defender XDR's RBAC permissions. The role will have general analyst capabilities.

##### Security Operations
###### Security Data
* Select Custom Permissions
    * ✓ Security Data Basics (Read)
    * ✓ Alerts (Manage)
    * ✓ Response (Manage)
    * ✓ Basic Live Response (Manage)
    * ✓ File Collection (Manage)
    * ✓ Email Quarantine (Manage)

_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

##### Raw Data (Email and Collaboration)
* Select Custom Permissions
  * ✓ Email Message Headers (Read)
  * ✓ Email Content (Read)
 
_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

#### Security Posture
##### Posture Management
* Select Custom Permissions
    * ✓ Vulnerability Management (Read)
    * ✓ Exception Handling (Manage)
    * ✓ Remediation Handling (Manage)
    * ✓ Application Handling (Manage)
    * ✓ Secure Score (Read)
    * ✓ Secure Score (Manage)

_Secure Score (Manage) can be restricted depending on your organization's needs._


#### Authorization and Settings
##### Authorization
* ✓ Read and Manage

_Some organizations may opt to restrict Authorization to read-only for Tier 1 analysts, as this could impact rule logic significantly if device groups are heavily utilized._

##### Security Settings
* Select Custom Permissions
  * ✓ Detection Tuning (Manage)
  * ✓ Core Security Settings (Read)
 
_Some organizations may want to restrict detection tuning to a higher role as it can have significant impacts on false negatives._


##### System Settings
* ✓ Read-only (Defender for Office, Defender for Identity)

_Granting the ability to see settings may give the analyst a better idea of the infrastructure and how things work. They cannot change anything. Your organization may have different needs._  


### Microsoft Defender XDR Role-Based Access Control - Tier 2
Title: Security Role - Tier 2
Tier: Two

### Permissions
This role is configured under Microsoft Defender XDR's RBAC permissions. The role will have more manage permissions than tier 1 does but is not able to change many settings.

#### Security Operations
##### Security Data
* Select Custom Permissions
    * ✓ Security Data Basics (Read)
    * ✓ Alerts (Manage)
    * ✓ Response (Manage)
    * ✓ Basic Live Response (Manage)
    * ✓ Advanced Live Response (Manage)
    * ✓ File Collection (Manage)
    * ✓ Email Quarantine (Manage)
    * ✓ Email Advanced Actions (Manage)

_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

##### Raw Data (Email and Collaboration)
* Select Custom Permissions
  * ✓ Email Message Headers (Read)
  * ✓ Email Content (Read)
 
_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

#### Security Posture
##### Posture Management
* Select Custom Permissions
    * ✓ Vulnerability Management (Read)
    * ✓ Exception Handling (Manage)
    * ✓ Remediation Handling (Manage)
    * ✓ Application Handling (Manage)
    * ✓ Security Baselines Assessment (Manage)
    * ✓ Secure Score (Read)
    * ✓ Secure Score (Manage)

_Secure Score (Manage) can be restricted depending on your organization's needs._


#### Authorization and Settings
##### Authorization
* ✓ Read and Manage

_Some organizations may opt to restrict Authorization to read-only for Tier 1 analysts, as this could impact rule logic significantly if device groups are heavily utilized._

##### Security Settings
* Select Custom Permissions
  * ✓ Detection Tuning (Manage)
  * ✓ Core Security Settings (Read)
  * ✓ Core Security Settings (Manage)
 
_Some organizations may want to restrict detection tuning to a higher role as it can have significant impacts on false negatives._


##### System Settings
* ✓ Read-only (Defender for Office, Defender for Identity)

_Granting the ability to see settings may give the analyst a better idea of the infrastructure and how things work. They cannot change anything. Your organization may have different needs._  



### Microsoft Defender XDR Role-Based Access Control - Tier 3
Title: Security Role - Tier 3
Tier: Three

### Permissions
This role is configured under Microsoft Defender XDR's RBAC permissions. This role is used by senior/tier 3 analysts and engineers and has permission to do most everything in the Defender XDR platform.

**Note: Selecting "All read and manage permissions" at the top of the page will blank out all other permissions and assign them all. Below I have listed all of the permissions granted for tracking purposes.**

![image](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/assets/8816079/bac071b3-d766-42cc-b12e-452161c24229)

#### Security Operations
##### Security Data
* All read and manage permissions
    * ✓ Security Data Basics (Read)
    * ✓ Alerts (Manage)
    * ✓ Response (Manage)
    * ✓ Basic Live Response (Manage)
    * ✓ Advanced Live Response (Manage)
    * ✓ File Collection (Manage)
    * ✓ Email Quarantine (Manage)
    * ✓ Email Advanced Actions (Manage)

##### Raw Data (Email and Collaboration)
  * ✓ Email Message Headers (Read)
  * ✓ Email Content (Read)
 
_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

#### Security Posture
##### Posture Management
* All read and manage permissions
    * ✓ Vulnerability Management (Read)
    * ✓ Exception Handling (Manage)
    * ✓ Remediation Handling (Manage)
    * ✓ Application Handling (Manage)
    * ✓ Security Baselines Assessment (Manage)
    * ✓ Secure Score (Read)
    * ✓ Secure Score (Manage)

#### Authorization and Settings
##### Authorization
* ✓ Read and Manage

_Some organizations may opt to restrict Authorization to read-only for Tier 1 analysts, as this could impact rule logic significantly if device groups are heavily utilized._

##### Security Settings
* All read and manage permissions
  * ✓ Detection Tuning (Manage)
  * ✓ Core Security Settings (Read)
  * ✓ Core Security Settings (Manage)
 
##### System Settings
* ✓ Read and Manage


## Cloud App Security Best Practices

### Overview
Defender Cloud App Security (Defender for Cloud, CASB, Defender Cloud App Security, etc) is a module that Microsoft offers which tracks which applications that people are using. This primarily tracks cloud applications, however, it will also give you the ability to uninstall applications on desktops if the cloud app is related to a desktop application. 

#### Tier 1
* Security Operator
This role will be able to view enough information in CASB to do analyst work but does not have the permissions necessary to impact users by sanctioning/unsanctioning applications. If your organization sees fit to allow Tier 1 to do so, then you could add them to Cloud App Security Administrator, but it is not recommended or a best practice.

#### Tier 2
* Cloud App Security Administrator
This level of access is granted because there is nothing available that is more granular which also allows the user to sanction/unsanction applications. As such, this is the least privilege we can grant the user at this time for this role.

#### Tier 3
* Security Administrator
This user will already have Security Administrator per the Tier 3 role document. This has full access to CASB. 

# Entra ID Default Role Reference
These default Entra ID roles have access to the Defender Cloud App Security portal and its following acctions:

* **Global administrator and Security administrator:** Administrators with Full access have full permissions in Defender for Cloud Apps. They can add admins, add policies and settings, upload logs and perform governance actions, access and manage SIEM agents.
* **Cloud App Security administrator:** Allows full access and permissions in Defender for Cloud Apps. This role grants full permissions to Defender for Cloud Apps, like the Azure AD Global administrator role. However, this role is scoped to Defender for Cloud Apps and won't grant full permissions across other Microsoft security products.
* **Compliance administrator:** Has read-only permissions and can manage alerts. Can't access Security recommendations for cloud platforms. Can create and modify file policies, allow file governance actions, and view all the built-in reports under Data Management.
* **Compliance data administrator:** Has read-only permissions, can create and modify file policies, allow file governance actions, and view all discovery reports. Can't access Security recommendations for cloud platforms.
* **Security operator:** Has read-only permissions and can manage alerts. These admins are restricted from doing the following actions:
	* Create policies or edit and change existing ones
	* Performing any governance actions
	* Uploading discovery logs
	* Banning or approving third-party apps
	* Accessing and viewing the IP address range settings page
	* Accessing and viewing any system settings pages
	* Accessing and viewing the Discovery settings
	* Accessing and viewing the App connectors page
	* Accessing and viewing the Governance log
	* Accessing and viewing the Manage snapshot reports page
	* Accessing and viewing SIEM agents
* **Security reader:** Has read-only permissions. These admins are restricted from doing the following actions:
	* Create policies or edit and change existing ones
	* Performing any governance actions
	* Uploading discovery logs
	* Banning or approving third-party apps
	* Accessing and viewing the IP address range settings page
	* Accessing and viewing any system settings pages
	* Accessing and viewing the Discovery settings
	* Accessing and viewing the App connectors page
	* Accessing and viewing the Governance log
	* Accessing and viewing the Manage snapshot reports page
	* Accessing and viewing SIEM agents
* **Global reader:** Has full read-only access to all aspects of Defender for Cloud Apps. Can't change any settings or take any actions.

Below is a matrix that Microsoft graciously provides which shows the permission level access for each role.

| Permissions | Global Admin | Security Admin | Compliance Admin | Compliance Data Admin | Security Operator | Security Reader | Global Reader | PBI Admin | Cloud App Security admin |
|-------------|:------------:|:--------------:|:----------------:|:---------------------:|:-----------------:|:---------------:|:------------:|:---------:|:------------------------:|
| Read alerts |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |     ✔     |            ✔             |
| Manage alerts |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |                 |              |     ✔     |            ✔             |
| Read OAuth applications |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |     ✔     |            ✔             |
| Perform OAuth application actions |      ✔       |       ✔        |                  |                       |                   |                 |              |     ✔     |            ✔             |
| Access discovered apps, the cloud app catalog, and other cloud discovery data |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |           |            ✔             |
| Configure API connectors |      ✔       |       ✔        |                  |                       |         ✔         |                 |              |           |            ✔             |
| Perform cloud discovery actions |      ✔       |       ✔        |                  |                       |                   |                 |              |           |            ✔             |
| Access files data and file policies |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |     ✔     |            ✔             |
| Perform file actions |      ✔       |       ✔        |                  |                       |                   |                 |              |     ✔     |            ✔             |
| Access governance log |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |     ✔     |            ✔             |
| Perform governance log actions |      ✔       |       ✔        |                  |                       |                   |                 |              |     ✔     |            ✔             |
| Access scoped discovery governance log |      ✔       |       ✔        |                  |                       |                   |                 |              |           |            ✔             |
| Read policies |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |     ✔     |            ✔             |
| Perform all policy actions |      ✔       |       ✔        |                  |                       |                   |                 |              |     ✔     |            ✔             |
| Perform file policy actions |      ✔       |       ✔        |        ✔         |                       |                   |                 |              |           |            ✔             |
| Perform OAuth policy actions |      ✔       |       ✔        |                  |                       |                   |                 |              |     ✔     |            ✔             |
| View manage admin access |      ✔       |       ✔        |        ✔         |           ✔           |         ✔         |        ✔        |      ✔       |           |            ✔             |
| Manage admins and activity privacy |      ✔       |       ✔        |                  |                       |                   |                 |              |           |            ✔             |


# Cloud App Security Standalone Roles
These roles are part of Cloud App Security's built-in permission roles. This is now located in Defender XDR under the Permissions > Cloud Apps section. These roles can be assigned to individual users when needed, which will overwrite the permissions that they have set in Entra ID. `Note: Global Admin and Security Admin will not be overwritten because they already have full access.`

* **Global administrator:** Has Full access similar to the Azure AD Global administrator role but only to Defender for Cloud Apps.
* **Compliance administrator:** Grants the same permissions as the Azure AD Compliance administrator role but only to Defender for Cloud Apps.
* **Security reader:** Grants the same permissions as the Azure AD Security reader role but only to Defender for Cloud Apps.
* **Security operator:** Grants the same permissions as the Azure AD Security operator role but only to Defender for Cloud Apps.
* **App/instance admin:** Has full or read-only permissions to all of the data in Defender for Cloud Apps that deals exclusively with the specific app or instance of an app selected. For example, you give a user admin permission to your Box European instance. The admin will see only data that relates to the Box European instance, whether it's files, activities, policies, or alerts:
	* Activities page - Only activities about the specific app
	* Alerts - Only alerts relating to the specific app. In some cases, alert data related to another app if the data is correlated with the specific app. Visibility to alert data related to another app is limited, and there is no access to drill down for more details
	* Policies - Can view all policies and if assigned full permissions can edit or create only policies that deal exclusively with the app/instance
	* Accounts page - Only accounts for the specific app/instance
	* App permissions - Only permissions for the specific app/instance
	* Files page - Only files from the specific app/instance
	* Conditional Access App Control - No permissions
	* Cloud Discovery activity - No permissions
	* Security extensions - Only permissions for API token with user permissions
	* Governance actions - Only for the specific app/instance
	* Security recommendations for cloud platforms - No permissions
	* IP ranges - No permissions
* **User group admin:** Has full or read-only permissions to all of the data in Defender for Cloud Apps that deals exclusively with the specific groups assigned to them.

For example, If you assign a user admin permissions to the group "Germany - all users", the admin can view and edit information in Defender for Cloud Apps only for that user group. The User group admin has the following access: 

 	* Activities page - Only activities about the users in the group
	* Alerts - Only alerts relating to the users in the group. In some cases, alert data related to another user if the data is correlated with the users in the group. Visibility to alert data related to another users is limited, and there is no access to drill down for more details.
	* Policies - Can view all policies and if assigned full permissions can edit or create only policies that deal exclusively with users in the group
	* Accounts page - Only accounts for the specific users in the group
	* App permissions – No permissions
	* Files page – No permissions
	* Conditional Access App Control - No permissions
	* Cloud Discovery activity - No permissions
	* Security extensions - Only permissions for API token with users in the group
	* Governance actions - Only for the specific users in the group
	* Security recommendations for cloud platforms - No permissions
	* IP ranges - No permissions

* **Cloud Discovery global admin:** Has permission to view and edit all Cloud Discovery settings and data. The Global Discovery admin has the following access:
	* Settings
		* System settings - View only
		* Cloud Discovery settings - View and edit all (anonymization permissions depend on whether it was allowed during role assignment)
		* Cloud Discovery activity - full permissions
	* Alerts - view and manage only alerts related to the relevant Cloud Discovery report
	* Policies - Can view all policies and can edit or create only Cloud Discovery policies
	* Activities page - No permissions
	* Accounts page - No permissions
	* App permissions – No permissions
	* Files page – No permissions
	* Conditional Access App Control - No permissions
	* Security extensions - Creating and deleting their own API tokens
	* Governance actions - Only Cloud Discovery related actions
	* Security recommendations for cloud platforms - No permissions
	* IP ranges - No permissions
* **Cloud Discovery report admin:**
	* Settings
		* System settings - View only
		* Cloud Discovery settings - View all (anonymization permissions depend on whether it was allowed during role assignment)
		* Cloud Discovery activity - read permissions only
	* Alerts – view only alerts related to the relevant Cloud Discovery report
	* Policies - Can view all policies and can create only Cloud Discovery policies, without the possibility to govern application (tagging, sanction and unsanctioned)
	* Activities page - No permissions
	* Accounts page - No permissions
	* App permissions – No permissions
	* Files page – No permissions
	* Conditional Access App Control - No permissions
	* Security extensions - Creating and deleting their own API tokens
	* Governance actions – view only actions related to the relevant Cloud Discovery report
	* Security recommendations for cloud platforms - No permissions
	* IP ranges - No permissions
