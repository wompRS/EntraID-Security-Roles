#### [Back to main page](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/tree/main#entraid-role-best-practices)

# Security Engineer - Tier 1
Purpose: This role is the general analyst for the organization. They are in the trenches every day and frequently need to see deep into the logs to triage events. This role is going to be the least permissive Security Engineer position, but that role also comes with greater permissions overall than similar engineer positions.

## Defender XDR Role-Based Access Control (RBAC)
Defender XDR now has its own set of permissions which can be created and assigned to the Defender XDR suite of tools, with more on the way. It is best-practice to utilize Defender XDR RBAC for controlling Microsoft Defender XDR permissions to things like Defender ATP, Defender for Endpoint, Defender Cloud App Security, Defender for Identity, and more. This gives you the most granular control over these modules, and is far superior to the default Azure Entra ID Roles.

### [ Defender XDR RBAC - Tier 1](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/blob/450ce6398ac84948c0db2e6ab5ede2129627c64c/Defender%20XDR%20RBAC%20-%20Tier%201.md)

This is a custom role that will need to be created. See the documentation [here](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/blob/450ce6398ac84948c0db2e6ab5ede2129627c64c/Defender%20XDR%20RBAC%20-%20Tier%201.md) for a full guide, or click the header. 

## Microsoft Entra ID Role Assignments
* Attack Payload Author
* Authentication Administrator 
* Cloud Device Administrator
* Message Center Reader
* Security Reader
* Service Support Administrator

## Permission Details

### Attack Payload author
Users in this role can create attack payloads but not actually launch or schedule them. Attack payloads are then available to all administrators in the tenant who can use them to create a simulation.

| Permission | Description |
| --- | --- |
| `microsoft.office365.protectionCenter/attackSimulator/payload/allProperties/allTasks` | Create and manage attack payloads in Attack Simulator |
| `microsoft.office365.protectionCenter/attackSimulator/reports/allProperties/read` | Create and manage attack payloads in Attack Simulator |


### Authentication Administrator - Privileged
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

### Cloud Device Administrator
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


### Message Center Reader
Users in this role can monitor notifications and advisory health updates in Message center for their organization on configured services such as Exchange, Intune, and Microsoft Teams. Message Center Readers receive weekly email digests of posts, updates, and can share 		message center posts in Microsoft 365. In Microsoft Entra ID, users assigned to this role will only have read-only access on Microsoft Entra services such as users and groups. This role has no access to view, create, or manage support tickets.

| Permission | Description |
| --- | --- |
| `microsoft.office365.messageCenter/messages/read` | Read messages in Message Center in the Microsoft 365 admin center, excluding security messages |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |


### Security Reader - Privileged
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


### Service Support Administrator
Users with this role can create and manage support requests with Microsoft for Azure and Microsoft 365 services, and view the service dashboard and message center in the Azure portal and Microsoft 365 admin center.

| Permission | Description |
| --- | --- |
| `microsoft.azure.serviceHealth/allEntities/allTasks` | Read and configure Azure Service Health |
| `microsoft.azure.supportTickets/allEntities/allTasks` | Create and manage Azure support tickets |
| `microsoft.office365.network/performance/allProperties/read` | Read all network performance properties in the Microsoft 365 admin center |
| `microsoft.office365.serviceHealth/allEntities/allTasks` | Read and configure Service Health in the Microsoft 365 admin center |
| `microsoft.office365.supportTickets/allEntities/allTasks` | Create and manage Microsoft 365 service requests |
| `microsoft.office365.webPortal/allEntities/standard/read` | Read basic properties on all resources in the Microsoft 365 admin center |




			
