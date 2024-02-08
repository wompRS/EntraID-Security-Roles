#### [Back to main page](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/tree/main#entraid-role-best-practices)

# Security Engineer - Tier 3
### Title: Security Engineer 3
### Tier: Three
Purpose: This is the top level engineering position per the design outlined. This grants most admin actions on security tasks in the tenant while also allowing for JIT access for critical actions. 

# Defender XDR Role-Based Access Control (RBAC)
Defender XDR now has its own set of permissions which can be created and assigned to the Defender XDR suite of tools, with more on the way. It is best-practice to utilize Defender XDR RBAC for controlling Microsoft Defender XDR permissions to things like Defender ATP, Defender for Endpoint, Defender Cloud App Security, Defender for Identity, and more. This gives you the most granular control over these modules, and is far superior to the default Azure Entra ID Roles.

## [ Defender XDR RBAC - Tier 3](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/blob/72bca25e4d728d8dba2ce5c4d7e2d44a97098b56/Defender%20XDR%20RBAC%20-%20Tier%203.md)

This is a custom role that will need to be created. See the documentation [here](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/blob/72bca25e4d728d8dba2ce5c4d7e2d44a97098b56/Defender%20XDR%20RBAC%20-%20Tier%202.md) for a full guide, or click the header. 


# Microsoft Entra ID Default Role Assignments

## Security Administrator
This is a privileged role. Users with this role have permissions to manage security-related features in the Microsoft 365 Defender portal, Microsoft Entra ID Protection, Microsoft Entra Authentication, Azure Information Protection, and Microsoft Purview compliance portal. For more information about Office 365 permissions, see Roles and role groups in Microsoft Defender for Office 365 and Microsoft Purview compliance.

| In | Can do |
| --- | --- |
| Microsoft 365 Defender portal | Monitor security-related policies across Microsoft 365 services<br>Manage security threats and alerts<br>View reports |
| Identity Protection | All permissions of the Security Reader role<br>Perform all Identity Protection operations except for resetting passwords |
| Privileged Identity Management | All permissions of the Security Reader role<br>Cannot manage Microsoft Entra role assignments or settings |
| Microsoft Purview compliance portal | Manage security policies<br>View, investigate, and respond to security threats<br>View reports |
| Azure Advanced Threat Protection | Monitor and respond to suspicious security activity |
| Microsoft Defender for Endpoint | Assign roles<br>Manage machine groups<br>Configure endpoint threat detection and automated remediation<br>View, investigate, and respond to alerts<br>View machines/device inventory |
| Intune | Views user, device, enrollment, configuration, and application information<br>Cannot make changes to Intune |
| Microsoft Defender for Cloud Apps | Add admins, add policies and settings, upload logs and perform governance actions |
| Microsoft 365 service health | View the health of Microsoft 365 services |
| Smart lockout | Define the threshold and duration for lockouts when failed sign-in events happen. |
| Password Protection | Configure custom banned password list or on-premises password protection. |
| Cross-tenant synchronization | Configure cross-tenant access settings for users in another tenant. Security Administrators can't directly create and delete users, but can indirectly create and delete synchronized users from another tenant when both tenants are configured for cross-tenant synchronization, which is a privileged permission. |

| `microsoft.directory/applications/policies/update` | Update policies of applications |
| `microsoft.directory/auditLogs/allProperties/read` | Read all properties on audit logs, excluding custom security attributes audit logs |
| `microsoft.directory/authorizationPolicy/standard/read` | Read standard properties of authorization policy |
| `microsoft.directory/bitlockerKeys/key/read` | Read bitlocker metadata and key on devices |
| `microsoft.directory/crossTenantAccessPolicy/standard/read` | Read basic properties of cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/allowedCloudEndpoints/update` | Update allowed cloud endpoints of cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/basic/update` | Update basic settings of cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/default/standard/read` | Read basic properties of the default cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/default/b2bCollaboration/update` | Update Microsoft Entra B2B collaboration settings of the default cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/default/b2bDirectConnect/update` | Update Microsoft Entra B2B direct connect settings of the default cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/default/crossCloudMeetings/update` | Update cross-cloud Teams meeting settings of the default cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/default/tenantRestrictions/update` | Update tenant restrictions of the default cross-tenant access policy |
| `microsoft.directory/crossTenantAccessPolicy/partners/create` | Create cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/delete` | Delete cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/standard/read` | Read basic properties of cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/b2bCollaboration/update` | Update Microsoft Entra B2B collaboration settings of cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/b2bDirectConnect/update` | Update Microsoft Entra B2B direct connect settings of cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/crossCloudMeetings/update` | Update cross-cloud Teams meeting settings of cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/tenantRestrictions/update` | Update tenant restrictions of cross-tenant access policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/identitySynchronization/create` | Create cross-tenant sync policy for partners |
| `microsoft.directory/crossTenantAccessPolicy/partners/identitySynchronization/basic/update` | Update basic settings of cross-tenant sync policy |
| `microsoft.directory/crossTenantAccessPolicy/partners/identitySynchronization/standard/read` | Read basic properties of cross-tenant sync policy |
| `microsoft.directory/deviceLocalCredentials/standard/read` | Read all properties of the backed up local administrator account credentials for Microsoft Entra joined devices, except the password |
| `microsoft.directory/domains/federation/update` | Update federation property of domains |
| `microsoft.directory/domains/federationConfiguration/standard/read` | Read standard properties of federation configuration for domains |
| `microsoft.directory/domains/federationConfiguration/basic/update` | Update basic federation configuration for domains |
| `microsoft.directory/domains/federationConfiguration/create` | Create federation configuration for domains |
| `microsoft.directory/domains/federationConfiguration/delete` |

| Actions | Description |
| --- | --- |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationIdentitySynchronization/basic/update` | Update cross tenant sync policy templates for multi-tenant organization |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationIdentitySynchronization/resetToDefaultSettings` | Reset cross tenant sync policy template for multi-tenant organization to default settings |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationIdentitySynchronization/standard/read` | Read basic properties of cross tenant sync policy templates for multi-tenant organization |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationPartnerConfiguration/basic/update` | Update cross tenant access policy templates for multi-tenant organization |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationPartnerConfiguration/resetToDefaultSettings` | Reset cross tenant access policy template for multi-tenant organization to default settings |
| `microsoft.directory/crossTenantAccessPolicy/partners/templates/multiTenantOrganizationPartnerConfiguration/standard/read` | Read basic properties of cross tenant access policy templates for multi-tenant organization |


			
