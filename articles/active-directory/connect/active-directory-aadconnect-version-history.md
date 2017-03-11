---
title: 'Azure AD Connect: Version release history | Microsoft Docs'
description: This article lists all releases of Azure AD Connect and Azure AD Sync
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''

ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: billmath

---
# Azure AD Connect: Version release history
The Azure Active Directory (Azure AD) team regularly updates Azure AD Connect with new features and functionality. Not all additions are applicable to all audiences.

This article is designed to help you keep track of the versions that have been released, and to understand whether you need to update to the newest version or not.

This is a list of related topics:


Topic |  Details
--------- | --------- |
Steps to upgrade from Azure AD Connect | Different methods to [upgrade from a previous version to the latest](active-directory-aadconnect-upgrade-previous-version.md) Azure AD Connect release.
Required permissions | For permissions required to apply an update, see [accounts and permissions](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Download| [Download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## 1.1.443.0
Released: March 2017

**Fixed issues:**

Azure AD Connect sync
* Fixed an issue which causes Azure AD Connect wizard to fail if the display name of the Azure AD Connector does not contain the initial onmicrosoft.com domain assigned to the Azure AD tenant.
* Fixed an issue which causes Azure AD Connect wizard to fail while making connection to SQL database when the password of the Sync Service Account contains special characters such as apostrophe, colon and space.
* Fixed an issue which causes the error “The dimage has an anchor that is different than the image” to occur on an Azure AD Connect server in staging mode, after you have temporarily excluded an on-premises AD object from syncing and then included it again for syncing.
* Fixed an issue which causes the error “The object located by DN is a phantom” to occur on an Azure AD Connect server in staging mode, after you have temporarily excluded an on-premises AD object from syncing and then included it again for syncing.

AD FS management
* Fixed an issue where Azure AD Connect wizard does not update AD FS configuration and set the right claims on the relying party trust after Alternate Login ID is configured.
* Fixed an issue where Azure AD Connect wizard is unable to correctly handle AD FS servers whose service accounts are configured using userPrincipalName format instead of sAMAccountName format.

Pass-through Authentication
* Fixed an issue which causes Azure AD Connect wizard to fail if Pass Through Authentication is selected but registration of its connector fails.
* Fixed an issue which causes Azure AD Connect wizard to bypass validation checks on sign-in method selected when Desktop SSO feature is enabled.

**New features/improvements:**

Azure AD Connect sync
* Get-ADSyncScheduler cmdlet now returns a new Boolean property named SyncCycleInProgress. If the returned value is true, it means that there is a scheduled synchronization cycle in progress.
* Destination folder for storing Azure AD Connect installation and setup logs has been moved from %localappdata%\AADConnect to %programdata%\AADConnect to improve accessibility to the log files.

AD FS management
* Added support for updating AD FS Farm SSL Certificate.
* Added support for managing AD FS 2016.
* You can now specify existing gMSA (Group Managed Service Account) during AD FS installation.
* You can now configure SHA-256 as the signature hash algorithm for Azure AD relying party trust.

Password Management
* Improved support for persisting idle connections (Password Writeback service)
* Simplified firewall configuration
* [More info here](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#step-3-configure-your-firewall)

## 1.1.380.0
Released: December 2016

**Fixed issue:**

* Fixed the issue where the issuerid claim rule for Active Directory Federation Services (AD FS) is missing in this build.

>[!NOTE]
>This build is not available to customers through the Azure AD Connect Auto Upgrade feature.

## 1.1.371.0
Released: December 2016

**Known issue:**

* The issuerid claim rule for AD FS is missing in this build. The issuerid claim rule is required if you are federating multiple domains with Azure Active Directory (Azure AD). If you are using Azure AD Connect to manage your on-premises AD FS deployment, upgrading to this build removes the existing issuerid claim rule from your AD FS configuration. You can work around the issue by adding the issuerid claim rule after the installation/upgrade. For details on adding the issuerid claim rule, refer to this article on [Multiple domain support for federating with Azure AD](active-directory-aadconnect-multiple-domains.md).

**Fixed issue:**

* If Port 9090 is not opened for the outbound connection, the Azure AD Connect installation or upgrade fails.

>[!NOTE]
>This build is not available to customers through the Azure AD Connect Auto Upgrade feature.

## 1.1.370.0
Released: December 2016

**Known issues:**

* The issuerid claim rule for AD FS is missing in this build. The issuerid claim rule is required if you are federating multiple domains with Azure AD. If you are using Azure AD Connect to manage your on-premises AD FS deployment, upgrading to this build removes the existing issuerid claim rule from your AD FS configuration. You can work around the issue by adding the issuerid claim rule after installation/upgrade. For details on adding issuerid claim rule, refer to this article on [Multiple domain support for federating with Azure AD](active-directory-aadconnect-multiple-domains.md).
* Port 9090 must be open outbound to complete installation.

**New features:**

* Pass-through Authentication (Preview).

>[!NOTE]
>This build is not available to customers through the Azure AD Connect Auto Upgrade feature.

## 1.1.343.0
Released: November 2016

**Known issue:**

* The issuerid claim rule for AD FS is missing in this build. The issuerid claim rule is required if you are federating multiple domains with Azure AD. If you are using Azure AD Connect to manage your on-premises AD FS deployment, upgrading to this build removes the existing issuerid claim rule from your AD FS configuration. You can work around the issue by adding the issuerid claim rule after installation/upgrade. For details on adding issuerid claim rule, refer to this article on [Multiple domain support for federating with Azure AD](active-directory-aadconnect-multiple-domains.md).

**Fixed issues:**

* Sometimes, installing Azure AD Connect fails because it is unable to create a local service account whose password meets the level of complexity specified by the organization's password policy.
* Fixed an issue where join rules are not reevaluated when an object in the connector space simultaneously becomes out-of-scope for one join rule and become in-scope for another. This can happen if you have two or more join rules whose join conditions are mutually exclusive.
* Fixed an issue where inbound synchronization rules (from Azure AD), which do not contain join rules, are not processed if they have lower precedence values than those containing join rules.

**Improvements:**

* Added support for installing Azure AD Connect on Windows Server 2016 Standard or higher.
* Added support for using SQL Server 2016 as the remote database for Azure AD Connect.

## 1.1.281.0
Released: August 2016

**Fixed issues:**

* Changes to sync interval do not take place until after the next sync cycle is complete.
* Azure AD Connect wizard does not accept an Azure AD account whose username starts with an underscore (\_).
* Azure AD Connect wizard fails to authenticate the Azure AD account if the account password contains too many special characters. Error message "Unable to validate credentials. An unexpected error has occurred." is returned.
* Uninstalling staging server disables password synchronization in Azure AD tenant and causes password synchronization to fail with active server.
* Password synchronization fails in uncommon cases when there is no password hash stored on the user.
* When Azure AD Connect server is enabled for staging mode, password writeback is not temporarily disabled.
* Azure AD Connect wizard does not show the actual password synchronization and password writeback configuration when server is in staging mode. It always shows them as disabled.
* Configuration changes to password synchronization and password writeback are not persisted by Azure AD Connect wizard when server is in staging mode.

**Improvements:**

* Updated the Start-ADSyncSyncCycle cmdlet to indicate whether it is able to successfully start a new sync cycle or not.
* Added the Stop-ADSyncSyncCycle cmdlet to terminate sync cycle and operation, which are currently in progress.
* Updated the Stop-ADSyncScheduler cmdlet to terminate sync cycle and operation, which are currently in progress.
* When configuring [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md) in Azure AD Connect wizard, the Azure AD attribute of type "Teletex string" can now be selected.

## 1.1.189.0
Released: June 2016

**Fixed issues and improvements:**

* Azure AD Connect can now be installed on a FIPS-compliant server.
  * For password synchronization, see [Password sync and FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Fixed an issue where a NetBIOS name could not be resolved to the FQDN in the Active Directory Connector.

## 1.1.180.0
Released: May 2016

**New features:**

* Warns and helps you verify domains if you didn’t do it before running Azure AD Connect.
* Added support for [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Added support for the latest [Microsoft Azure Government cloud](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infrastructure with new URL requirements.

**Fixed issues and improvements:**

* Added filtering to the Sync Rule Editor to make it easy to find sync rules.
* Improved performance when deleting a connector space.
* Fixed an issue when the same object was both deleted and added in the same run (called delete/add).
* A disabled sync rule no longer re-enables included objects and attributes on upgrade or directory schema refresh.

## 1.1.130.0
Released: April 2016

**New features:**

* Added support for multi-valued attributes to [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md).
* Added support for more configuration variations for [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) to be considered eligible for upgrade.
* Added some cmdlets for [custom scheduler](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## 1.1.119.0
Released: March 2016

**Fixed issues:**

* Made sure Express installation cannot be used on Windows Server 2008 (pre-R2) because password sync is not supported on this operating system.
* Upgrade from DirSync with a custom filter configuration did not work as expected.
* When upgrading to a newer release and there are no changes to the configuration, a full import/synchronization should not be scheduled.

## 1.1.110.0
Released: February 2016

**Fixed issues:**

* Upgrade from earlier releases does not work if the installation is not in the default C:\Program Files folder.
* If you install and clear **Start the synchronization process** at the end of the installation wizard, running the installation wizard a second time will not enable the scheduler.
* The scheduler doesn't work as expected on servers where the US-en date/time format is not used. It will also block `Get-ADSyncScheduler` to return correct times.
* If you installed an earlier release of Azure AD Connect with AD FS as the sign-in option and upgrade, you cannot run the installation wizard again.

## 1.1.105.0
Released: February 2016

**New features:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature for Express settings customers.
* Support for the global admin by using Azure Multi-Factor Authentication and Privileged Identity Management in the installation wizard.
  * You need to allow your proxy to also allow traffic to https://secure.aadcdn.microsoftonline-p.com if you use Multi-Factor Authentication.
  * You need to add https://secure.aadcdn.microsoftonline-p.com to your trusted sites list for Multi-Factor Authentication to properly work.
* Allow changing the user's sign-in method after initial installation.
* Allow [Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in the installation wizard. This also allows connecting to forests where not all domains are available.
* [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) is built in to the sync engine.

**Features promoted from preview to GA:**

* [Device writeback](active-directory-aadconnect-feature-device-writeback.md).
* [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md).

**New preview features:**

* The new default sync cycle interval is 30 minutes. Used to be three hours for all earlier releases. Adds support to change the [scheduler](active-directory-aadconnectsync-feature-scheduler.md) behavior.

**Fixed issues:**

* The verify DNS domains page didn't always recognize the domains.
* Prompts for domain admin credentials when configuring AD FS.
* The on-premises AD accounts are not recognized by the installation wizard if located in a domain with a different DNS tree than the root domain.

## 1.0.9131.0
Released: December 2015

**Fixed issues:**

* Password sync might not work when you change passwords in Active Directory Domain Services (AD DS), but works when you do set a password.
* When you have a proxy server, authentication to Azure AD might fail during installation, or if an upgrade is canceled on the configuration page.
* Updating from a previous release of Azure AD Connect with a full SQL Server instance fails if you are not a SQL Server system administrator (SA).
* Updating from a previous release of Azure AD Connect with a remote SQL Server shows the “Unable to access the ADSync SQL database” error.

## 1.0.9125.0
Released: November 2015

**New features:**

* Can reconfigure AD FS to Azure AD trust.
* Can refresh the Active Directory schema and regenerate sync rules.
* Can disable a sync rule.
* Can define "AuthoritativeNull" as a new literal in a sync rule.

**New preview features:**

* [Azure AD Connect Health for sync](../connect-health/active-directory-aadconnect-health-sync.md).
* Support for [Azure AD Domain Services](../active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords) password synchronization.

**New supported scenario:**

* Supports multiple on-premises Exchange organizations. For more information, see [Hybrid deployments with multiple Active Directory forests](https://technet.microsoft.com/library/jj873754.aspx).

**Fixed issues:**

* Password synchronization issues:
  * An object moved from out-of-scope to in-scope will not have its password synchronized. This includes both OU and attribute filtering.
  * Selecting a new OU to include in sync does not require a full password sync.
  * When a disabled user is enabled the password does not sync.
  * The password retry queue is infinite and the previous limit of 5,000 objects to be retired has been removed.
  * [Improved troubleshooting](active-directory-aadconnectsync-implement-password-synchronization.md#troubleshooting-password-synchronization).
* Not able to connect to Active Directory with Windows Server 2016 forest-functional level.
* Not able to change the group that is used for group filtering after the initial installation.
* No longer creates a new user profile on the Azure AD Connect server for every user doing a password change with password writeback enabled.
* Not able to use Long Integer values in sync rules scopes.
* The check box "device writeback" remains disabled if there are unreachable domain controllers.

## 1.0.8667.0
Released: August 2015

**New features:**

* The Azure AD Connect installation wizard is now localized to all Windows Server languages.
* Added support for account unlock when using Azure AD password management.

**Fixed issues:**

* Azure AD Connect installation wizard crashes if another user continues installation rather than the person who first started the installation.
* If a previous uninstallation of Azure AD Connect fails to uninstall Azure AD Connect sync cleanly, it is not possible to reinstall.
* Cannot install Azure AD Connect using Express installation if the user is not in the root domain of the forest or if a non-English version of Active Directory is used.
* If the FQDN of the Active Directory user account cannot be resolved, a misleading error message “Failed to commit the schema” is shown.
* If the account used on the Active Directory Connector is changed outside the wizard, the wizard fails on subsequent runs.
* Azure AD Connect sometimes fails to install on a domain controller.
* Cannot enable and disable “Staging mode” if extension attributes have been added.
* Password writeback fails in some configurations because of a bad password on the Active Directory Connector.
* DirSync cannot be upgraded if a distinguished name (DN) is used in attribute filtering.
* Excessive CPU usage when using password reset.

**Removed preview features:**

* The preview feature [User writeback](active-directory-aadconnect-feature-preview.md#user-writeback) was temporarily removed based on feedback from our preview customers. It will be added again later after we have addressed the provided feedback.

## 1.0.8641.0
Released: June 2015

**Initial release of Azure AD Connect.**

Changed name from Azure AD Sync to Azure AD Connect.

**New features:**

* [Express settings](active-directory-aadconnect-get-started-express.md) installation
* Can [configure AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* Can [upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Introduced [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)

**New preview features:**

* [User writeback](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Group writeback](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Device writeback](active-directory-aadconnect-feature-device-writeback.md)
* [Directory extensions](active-directory-aadconnect-feature-preview.md)

## 1.0.494.0501
Released: May 2015

**New Requirement:**

* Azure AD Sync now requires the .NET Framework version 4.5.1 to be installed.

**Fixed issues:**

* Password writeback from Azure AD is failing with an Azure Service Bus connectivity error.

## 1.0.491.0413
Released: April 2015

**Fixed issues and improvements:**

* The Active Directory Connector does not process deletes correctly if the recycle bin is enabled and there are multiple domains in the forest.
* The performance of import operations has been improved for the Azure Active Directory Connector.
* When a group has exceeded the membership limit (by default, the limit is set to 50,000 objects), the group was deleted in Azure Active Directory. With the new behavior, the group is not deleted, an error is thrown, and new membership changes are not exported.
* A new object cannot be provisioned if a staged delete with the same DN is already present in the connector space.
* Some objects are marked for synchronization during a delta sync even though there's no change staged on the object.
* Forcing a password sync also removes the preferred DC list.
* CSExportAnalyzer has problems with some objects states.

**New features:**

* A join can now connect to “ANY” object type in the MV.

## 1.0.485.0222
Released: February 2015

**Improvements:**

* Improved import performance.

**Fixed issues:**

* Password Sync honors the cloudFiltered attribute that is used by attribute filtering. Filtered objects are no longer in scope for password synchronization.
* In rare situations where the topology had many domain controllers, password sync doesn’t work.
* “Stopped-server” when importing from the Azure AD Connector after device management has been enabled in Azure AD/Intune.
* Joining Foreign Security Principals (FSPs) from multiple domains in same forest causes an ambiguous-join error.

## 1.0.475.1202
Released: December 2014

**New features:**

* Password synchronization with attribute-based filtering is now supported. For more information, see [Password synchronization with filtering](active-directory-aadconnectsync-configure-filtering.md).
* The msDS-ExternalDirectoryObjectID attribute is written back to Active Directory. This feature adds support for Office 365 applications. It uses OAuth2 to access Online and On-Premises mailboxes in a Hybrid Exchange Deployment.

**Fixed upgrade issues:**

* A newer version of the sign-in assistant is available on the server.
* A custom installation path was used to install Azure AD Sync.
* An invalid custom join criterion blocks the upgrade.

**Other fixes:**

* Fixed the templates for Office Pro Plus.
* Fixed installation issues caused by user names that start with a dash.
* Fixed losing the sourceAnchor setting when running the installation wizard a second time.
* Fixed ETW tracing for password synchronization.

## 1.0.470.1023
Released: October 2014

**New features:**

* Password synchronization from multiple on-premises Active Directory to Azure AD.
* Localized installation UI to all Windows Server languages.

**Upgrading from AADSync 1.0 GA**

If you already have Azure AD Sync installed, there is one additional step you have to take in case you have changed any of the out-of-box synchronization rules. After you have upgraded to the 1.0.470.1023 release, the synchronization rules you have modified are duplicated. For each modified sync rule, do the following:

1.  Locate the sync rule you have modified and take a note of the changes.
* Delete the sync rule.
* Locate the new sync rule that is created by Azure AD Sync and then reapply the changes.

**Permissions for the Active Directory account**

The Active Directory account must be granted additional permissions to be able to read the password hashes from Active Directory. The permissions to grant are named “Replicating Directory Changes” and “Replicating Directory Changes All.” Both permissions are required to be able to read the password hashes.

## 1.0.419.0911
Released: September 2014

**Initial release of Azure AD Sync.**

## Next steps
Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).
