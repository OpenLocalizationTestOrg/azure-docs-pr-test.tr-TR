---
title: "aaaGrant izin toomany uygulamaları tooaccess Azure anahtar kasası | Microsoft Docs"
description: "Nasıl toogrant izin toomany uygulamaları tooaccess bir anahtar kasası öğrenin"
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
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="33d90-103">Bir anahtar kasası izni toomany uygulamaları tooaccess verin</span><span class="sxs-lookup"><span data-stu-id="33d90-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="33d90-104">S: birkaç sahibim tooaccess bir anahtar kasası gerekir (üzerinde 16) uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="33d90-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="33d90-105">Anahtar kasası yalnızca 16 erişim denetimi girdileri olanak tanıdığından nasıl t, elde edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="33d90-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="33d90-106">Anahtar kasası erişim denetimi ilkesini yalnızca 16 girişleri destekler.</span><span class="sxs-lookup"><span data-stu-id="33d90-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="33d90-107">Ancak, bir Azure Active Directory güvenlik grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33d90-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="33d90-108">Tüm hello ilişkilendirilmiş hizmet sorumluları toothis güvenlik grubu ve ardından erişim toothis güvenlik grubu tooKey kasası verin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="33d90-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="33d90-109">Merhaba ön koşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="33d90-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="33d90-110">[Azure Active Directory V2 PowerShell modülünü yüklemek](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="33d90-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="33d90-111">[Azure PowerShell'i yükleme](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33d90-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="33d90-112">toorun hello aşağıdaki komutları kullanarak, hello Azure Active Directory Kiracı toocreate/Düzenle gruplarda izinler gerekir.</span><span class="sxs-lookup"><span data-stu-id="33d90-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="33d90-113">İzinleri yoksa, Azure Active Directory yöneticiniz toocontact gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="33d90-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="33d90-114">Şimdi hello aşağıdaki PowerShell komutlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="33d90-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="33d90-115">Uygulama izinleri tooa grubu farklı bir dizi toogrant gerekiyorsa, bu tür uygulamalar için ayrı bir Azure Active Directory güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="33d90-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33d90-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33d90-116">Next steps</span></span>

<span data-ttu-id="33d90-117">Hakkında daha fazla çok bilgi[anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="33d90-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
