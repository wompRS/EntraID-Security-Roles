# Microsoft Defender XDR Role-Based Access Control

Title: **Security Role - Tier 3**

Tier: **Three**

# Permissions
This role is configured under Microsoft Defender XDR's RBAC permissions. This role is used by senior/tier 3 analysts and engineers and has permission to do most everything in the Defender XDR platform.

**Note: Selecting "All read and manage permissions" at the top of the page will blank out all other permissions and assign them all. Below I have listed all of the permissions granted for tracking purposes.**

![image](https://github.com/CHAS-Health/EntraID-Role-Best-Practices/assets/8816079/bac071b3-d766-42cc-b12e-452161c24229)

## Security Operations
### Security Data
* All read and manage permissions
    * ✓ Security Data Basics (Read)
    * ✓ Alerts (Manage)
    * ✓ Response (Manage)
    * ✓ Basic Live Response (Manage)
    * ✓ Advanced Live Response (Manage)
    * ✓ File Collection (Manage)
    * ✓ Email Quarantine (Manage)
    * ✓ Email Advanced Actions (Manage)

### Raw Data (Email and Collaboration)
  * ✓ Email Message Headers (Read)
  * ✓ Email Content (Read)
 
_Email message permissions are entirely dependent on your organization's philosophy, structure, and job descriptions. Some organizations may not want your junior analysts to be able to read email information._

## Security Posture
### Posture Management
* All read and manage permissions
    * ✓ Vulnerability Management (Read)
    * ✓ Exception Handling (Manage)
    * ✓ Remediation Handling (Manage)
    * ✓ Application Handling (Manage)
    * ✓ Security Baselines Assessment (Manage)
    * ✓ Secure Score (Read)
    * ✓ Secure Score (Manage)

## Authorization and Settings
### Authorization
* ✓ Read and Manage

_Some organizations may opt to restrict Authorization to read-only for Tier 1 analysts, as this could impact rule logic significantly if device groups are heavily utilized._

### Security Settings
* All read and manage permissions
  * ✓ Detection Tuning (Manage)
  * ✓ Core Security Settings (Read)
  * ✓ Core Security Settings (Manage)
 

### System Settings
* ✓ Read and Manage
