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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Bir anahtar kasası izni toomany uygulamaları tooaccess verin

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>S: birkaç sahibim tooaccess bir anahtar kasası gerekir (üzerinde 16) uygulamaları. Anahtar kasası yalnızca 16 erişim denetimi girdileri olanak tanıdığından nasıl t, elde edebilirsiniz?

Anahtar kasası erişim denetimi ilkesini yalnızca 16 girişleri destekler. Ancak, bir Azure Active Directory güvenlik grubu oluşturabilirsiniz. Tüm hello ilişkilendirilmiş hizmet sorumluları toothis güvenlik grubu ve ardından erişim toothis güvenlik grubu tooKey kasası verin ekleyin.

Merhaba ön koşullar şunlardır:
* [Azure Active Directory V2 PowerShell modülünü yüklemek](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Azure PowerShell'i yükleme](/powershell/azure/overview).
* toorun hello aşağıdaki komutları kullanarak, hello Azure Active Directory Kiracı toocreate/Düzenle gruplarda izinler gerekir. İzinleri yoksa, Azure Active Directory yöneticiniz toocontact gerekebilir.

Şimdi hello aşağıdaki PowerShell komutlarını çalıştırın.

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

Uygulama izinleri tooa grubu farklı bir dizi toogrant gerekiyorsa, bu tür uygulamalar için ayrı bir Azure Active Directory güvenlik grubu oluşturun.

## <a name="next-steps"></a>Sonraki adımlar

Hakkında daha fazla çok bilgi[anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).
