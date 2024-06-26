
## Overview:
    1. This script is used to create PIM role assignment(s) with SC-ALT account for:
        a. Critical permanent role assignment(s) and 
        b. Critical PIM non SC-ALT role assignment(s) 
    2. Remove critical permanent role assignment(s) for which the PIM role assignment(s) is successfully created in the Subscription or in resource group.

## Control ID:
    1. Azure_Subscription_AuthZ_Dont_Grant_Persistent_Access 
    2. Azure_Subscription_AuthZ_Dont_Grant_Persistent_Access_RG 
    3. Azure_Subscription__Use_Only_Alt_Credentials

## Display Name:
    1. Do not grant permanent access for critical subscription level roles 
    2. Do not grant permanent access for critical resource group level roles 
    3. Use Smart-Card ALT (SC-ALT) accounts to access critical roles on subscription and resource groups

## Prerequisites: 
    Owner and higher privileged role assignment on the Subscription is required and atleast one service adminstrator role assignment must be present on the subscription level.

## Critical roles considered by control:
#### 1. Azure_Subscription_AuthZ_Dont_Grant_Persistent_Access
	     Critical roles at subscription level :
	     *   Owner
	     *   Contributor
	     *   User Access Administrator
#### 2. Azure_Subscription_AuthZ_Dont_Grant_Persistent_Access_RG
        Critical roles at resource group level :
        *   Owner
        *   User Access Administrator
#### 3. Azure_Subscription_Use_Only_Alt_Credentials
        Critical roles at subscription level :
        *   Owner
        *   Contributor
        *   User Access Administrator

        Critical roles at resource group level :
        *   Owner
        *   User Access Administrator

## Important Points:
    1. First run the script using the -DryRun switch and for migration user needs to pass two files one for all the critical role assignments
       needs to migrated(Mandatory) and other file with their SC-ALT mapping(Not Mandatory in case all the role assignments are mapped to SC-ALT) which are provided as output of dryrun.
    2. Script will only migrate the role assignment(s) if corresponding SC-ALT account mapping is provided by the user or already mapped to 
       SC-ALT account, Otherwise the role assignment(s) will be skipped from migration.
    3. The user critical role assignment(s) will not be removed.
    4. The user needs to renew the PIM role assignments because they are created for a specific time interval which is 30 days.
    5. Rollback is not supported in this script.
    6. The Azure_Subscription_Use_Only_Alt_Credentials control will be partially migrated(corresponding PIM SC-ALT role assignment(s) will be
       created but the PIM non SC-ALT role assignment(s) will not be removed).
    7. User needs to delete the PIM non SC-ALT role assignment(s) and migrate user's critical role assignment(s) to SC-ALT PIM after the script 
       execution.

## FAQs:
     Q.1. While running the remediation script I am getting error "Unable to find type [Microsoft.Azure.Commands.Common.Authentication.AzureSession]". How can I resolve this error?
     A.1 Please run these commands "Install-Module -Name Az.Accounts -Scope CurrentUser -Repository "PSGallery" -Force  -AllowClobber -ErrorAction Stop" in a new session, followed by 'Connect-AzAccount' and then load the script.



