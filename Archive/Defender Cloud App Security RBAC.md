### [Back to main page](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/blob/c0a59e10c90151a82f4d2847ea2dcaef311184b1/README.md)

# Overview
Defender Cloud App Security (Defender for Cloud, CASB, Defender Cloud App Security, etc) is a module that Microsoft offers which tracks which applications that people are using. This primarily tracks cloud applications, however, it will also give you the ability to uninstall applications on desktops if the cloud app is related to a desktop application. 

# Cloud App Security Best Practices

## Tier 1
* Security Operator
This role will be able to view enough information in CASB to do analyst work but does not have the permissions necessary to impact users by sanctioning/unsanctioning applications. If your organization sees fit to allow Tier 1 to do so, then you could add them to Cloud App Security Administrator, but it is not recommended or a best practice.

## Tier 2
* Cloud App Security Administrator
This level of access is granted because there is nothing available that is more granular which also allows the user to sanction/unsanction applications. As such, this is the least privilege we can grant the user at this time for this role.

## Tier 3
* Security Administrator
This user will already have Security Administrator per the Tier 3 role document. This has full access to CASB. 


# Entra ID Default Role Access
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
