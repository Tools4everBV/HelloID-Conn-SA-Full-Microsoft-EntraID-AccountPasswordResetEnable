# Change Log

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [2.0.0] - 2026-03-02

This is the first official release of HelloID-Conn-SA-Full-EntraID-AccountPasswordResetEnable. This release includes functionality to reset passwords and/or enable Entra ID user accounts through HelloID Service Automation delegated forms.

### Added

• Added GitHub Actions workflow for automated release creation (`Create Release` workflow)
• Added GitHub Actions workflow to verify CHANGELOG.md updates on pull requests (`Verify CHANGELOG Updated` workflow)
• Added password generation data source (`Generate-Random-Password`) that creates random passwords meeting security requirements
  - Minimum 12 characters
  - At least one uppercase letter from: ABCDEFGHJKMNPQRSTUVWXYZ (excludes I, L, O)
  - At least one lowercase letter from: abcdefghjkmnpqrstuvwxyz (excludes i, l, o)
  - At least one digit from: 2 3 4 5 6 7 8 9 (excludes 0 and 1)
  - At least one special character from: ! # $ @ * ?
• Added data source to retrieve user account enabled status (`Entra-ID-Get-User-Attribute-AccountEnabled`)

### Changed

• BREAKING: Migrated from Azure AD terminology to Microsoft Entra ID terminology throughout all scripts, documentation, and configuration files
• BREAKING: Updated global variable names to use Entra ID naming convention:
  - Old: `AADTenantId` → New: `EntraIdTenantId`
  - Old: `AADAppId` → New: `EntraIdAppId`  
  - Old: `AADAppSecret` → New: `EntraIdCertificateBase64String` and `EntraIdCertificatePassword`
• BREAKING: Replaced client secret authentication with certificate-based authentication for Microsoft Graph API access
  - Now uses JWT (JSON Web Tokens) generated from X.509 certificates
  - Requires certificate to be uploaded to Entra ID App Registration
• BREAKING: Refactored data source names from Azure AD to Entra ID naming:
  - Old: `Azure-AD-User-Reset-Password-generate-table-wildcard` → New: `EntraID-Get-Users-Wildcard-DisplayName-UPN-Mail`
• Updated task name from "Azure AD Account - Reset password & Unlock" to "Entra ID Account - Reset password & Unlock"
• Enhanced delegated form with improved user experience, grid columns, and field layout
• Improved password validation with detailed RegEx pattern and user-friendly error messages
• Updated form schema with better visibility settings and field dependencies
• Enhanced error handling with improved error messages and line number information
• Improved audit logging for all password reset and account enable operations
• Updated README.md with comprehensive documentation including requirements, API permissions, connection settings, and remarks
• Improved code formatting and consistency across all PowerShell scripts

### Deprecated

• Deprecated support for Azure AD naming convention in global variables (use Entra ID naming convention instead)
• Deprecated client secret authentication method (use certificate-based authentication instead)

### Removed

• Removed support for client secret-based authentication in favor of certificate-based authentication
• Removed Azure AD terminology from all scripts and documentation

### Fixed

## [1.0.2] - 2022-10-11

### Added

• Added id-based user lookup instead of userPrincipalName for more accurate user identification

### Changed

• Updated user lookup to use object ID (`id`) instead of `userPrincipalName` to ensure correct user is targeted

### Deprecated

### Removed

### Fixed

## [1.0.2] - 2022-08-16

### Added

• Added version numbering to scripts
• Added support for HelloID Service Automation agent
• Added enhanced audit logging functionality

### Changed

• Updated code to support SA-agent execution
• Improved audit logging output

### Deprecated

### Removed

### Fixed

## [1.0.1] - 2021-11-08

### Added

• Added version number to scripts

### Changed

• Updated all-in-one setup script

### Deprecated

### Removed

### Fixed

## [1.0.0] - 2021-09-02

### Added

• Initial release of HelloID-Conn-SA-Full-AzureAD-AccountPasswordResetEnable
• Basic Azure AD account password reset functionality
• Azure AD account enable functionality
• Form-based user selection with wildcard search across displayName, userPrincipalName
• Optional password reset with manual password entry (toggleable switch)
• Optional account enable (toggleable switch, independent from password reset)
• Configurable "change password at next sign-in" option
• Client secret-based authentication for Microsoft Graph API
• Data source for searching Azure AD users (`Azure-AD-User-Reset-Password-generate-table-wildcard`)
• Data source for displaying user attributes (`Azure-AD-User-Reset-Password-generate-table-attributes-basic`)
• Task for password reset and account enable operations
• All-in-one setup script for HelloID form deployment
• Basic error handling and audit logging

### Changed

### Deprecated

### Removed

### Fixed
