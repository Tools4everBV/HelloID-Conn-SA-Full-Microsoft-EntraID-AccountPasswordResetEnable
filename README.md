# HelloID-Conn-SA-Full-EntraID-AccountPasswordResetEnable

| :information_source: Information |
| :------------------------------- |
| This repository contains the connector and configuration code only. The implementer is responsible for acquiring the connection details such as tenant ID, client ID/secret, certificate, etc. You might need to complete prerequisite setup in Microsoft Entra ID before implementing this connector. Please coordinate requirements with the application owner. |

## Description
HelloID-Conn-SA-Full-EntraID-AccountPasswordResetEnable is a template for a HelloID Service Automation (SA) Delegated Form that can reset the password of and/or enable Microsoft Entra ID users.

Using this delegated form, you can:
 1. Search and select the target user
 2. Optionally toggle Reset Password
    1. Enter the new password
    2. Optionally toggle Change password at next sign-in
 3. Optionally toggle Enable account
 4. After confirmation, the password is reset and, optionally, the user account is enabled

## Getting started
### Requirements

#### App Registration & Certificate Setup

Before implementing this connector, make sure to configure a Microsoft Entra ID, an App Registration. During the setup process, you’ll create a new App Registration in the Entra portal, assign the necessary API permissions (such as user and group read/write), and generate and assign a certificate.

Follow the official Microsoft documentation for creating an App Registration and setting up certificate-based authentication:
- [App-only authentication with certificate (Exchange Online)](https://learn.microsoft.com/en-us/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps#set-up-app-only-authentication)

#### HelloID-specific configuration

Once you have completed the Microsoft setup and followed their best practices, configure the following HelloID-specific requirements.

- **API Permissions** (Application permissions):
  - `User.ReadWrite.All`
  - `Group.ReadWrite.All`
  - `GroupMember.ReadWrite.All`
  - `UserAuthenticationMethod.ReadWrite.All`
  - `User.EnableDisableAccount.All`
  - `User-PasswordProfile.ReadWrite.All`
  - `User-Phone.ReadWrite.All`
- **Certificate:**
  - Upload the public key file (.cer) in Entra ID
  - Provide the certificate as a Base64 string in HelloID. For instructions on creating the certificate and obtaining the base64 string, refer to our forum post: [Setting up a certificate for Microsoft Graph API in HelloID connectors](https://forum.helloid.com/forum/helloid-provisioning/5338-instruction-setting-up-a-certificate-for-microsoft-graph-api-in-helloid-connectors#post5338)

### Connection settings

The following user-defined variables are used by the connector.

| Setting     | Description                              | Mandatory |
| ----------- | ---------------------------------------- | --------- |
| EntraTenantId | Entra tenant ID                       | Yes       |
| EntraAppId    | Entra application (client) ID         | Yes       |
| EntraCertificateBase64String | Entra Certificate string      | Yes       |
| EntraCertificatePassword | Entra Certificate password      | Yes       |

## Remarks

### Uses Object ID for Correlation
- The connector uses the Entra ID `id` (object ID) to identify users rather than `userPrincipalName`, ensuring the correct user is targeted across rename/UPN change scenarios.

### Password Reset Behavior
- Password reset is performed via Microsoft Graph by updating the user's `passwordProfile`. Optionally sets `forceChangePasswordNextSignIn` when requested.

### Enabling Accounts
- Enabling an account sets `accountEnabled` to `true` via Microsoft Graph.

### Throttling and Propagation
- Microsoft Graph may throttle requests; implementers should be aware of HTTP 429 responses. Directory changes can exhibit short propagation delays.

## Development resources

### API endpoints

The following Microsoft Graph endpoints are used by the connector (v1.0):

| Endpoint | Description |
| -------- | ----------- |
| GET /users?$select=id,displayName,userPrincipalName,accountEnabled&$filter=startsWith(displayName,'{search}') | Search and list users for selection |
| GET /users/{id} | Retrieve user details |
| PATCH /users/{id} | Update `passwordProfile`, `accountEnabled`, and related properties |

### API documentation

- Users overview: https://learn.microsoft.com/graph/api/resources/user
- List users: https://learn.microsoft.com/graph/api/user-list
- Update user (password/profile): https://learn.microsoft.com/graph/api/user-update
- Graph authentication and app permissions: https://learn.microsoft.com/graph/auth/auth-concepts

## Getting help
> :bulb: Tip:  
> For more information on Delegated Forms, please refer to our documentation pages: https://docs.helloid.com/en/service-automation/delegated-forms.html

## HelloID docs
The official HelloID documentation can be found at: https://docs.helloid.com/