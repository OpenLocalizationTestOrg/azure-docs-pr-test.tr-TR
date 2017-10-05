---
title: "Azure anahtar kasası erişmek için birçok uygulamalara iznini | Microsoft Docs"
description: "Bir anahtar kasası erişmek için birçok uygulama izni öğrenin"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="fb735-103">Bir anahtar kasası erişmek için birçok uygulama izni verin</span><span class="sxs-lookup"><span data-stu-id="fb735-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="fb735-104">S: birkaç sahip bir anahtar kasası erişmesi gerekir (üzerinde 16) uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="fb735-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="fb735-105">Anahtar kasası yalnızca 16 erişim denetimi girdileri olanak tanıdığından nasıl t, elde edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="fb735-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="fb735-106">Anahtar kasası erişim denetimi ilkesini yalnızca 16 girişleri destekler.</span><span class="sxs-lookup"><span data-stu-id="fb735-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="fb735-107">Ancak, bir Azure Active Directory güvenlik grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb735-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="fb735-108">Tüm ilişkili hizmet asıl adı bu güvenlik grubuna ekleyin ve bu anahtar kasası güvenlik grubuna erişim hakkı.</span><span class="sxs-lookup"><span data-stu-id="fb735-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="fb735-109">Ön koşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fb735-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="fb735-110">[Azure Active Directory V2 PowerShell modülünü yüklemek](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="fb735-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="fb735-111">[Azure PowerShell'i yükleme](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb735-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fb735-112">Aşağıdaki komutları çalıştırmak için Azure Active Directory Kiracı gruplarında Oluştur/Düzenle izinlerine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb735-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="fb735-113">İzinleri yoksa, Azure Active Directory yöneticinize başvurmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fb735-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="fb735-114">Şimdi PowerShell'de aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fb735-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="fb735-115">Farklı bir uygulama grubu için izinler kümesini vermeniz gerekiyorsa, bu tür uygulamalar için ayrı bir Azure Active Directory güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb735-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb735-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb735-116">Next steps</span></span>

<span data-ttu-id="fb735-117">Nasıl yapılır hakkında daha fazla bilgi [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="fb735-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
