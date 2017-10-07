---
title: "bir abonelik taşıdıktan sonra aaaChange hello anahtar kasası Kiracı kimliği | Microsoft Docs"
description: "Bir abonelik tamamlandıktan sonra bir anahtar kasası için tooswitch hello Kiracı kimliği tooa farklı Kiracı nasıl taşınır öğrenin"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Abonelik taşıma işlemi sonrasında anahtar kasası kiracı kimliğini değiştirme
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>S: Aboneliğimi Kiracı A tootenant B. taşındı Nasıl my olan bir anahtar kasası için hello Kiracı kimliği değiştirmek ve Kiracı B Sorumlular için doğru ACL ayarlamak?
Bir abonelikte yeni bir anahtar kasası oluşturduğunuzda, bu abonelik için otomatik olarak bağlı toohello varsayılan Azure Active Directory Kiracı kimliği olur. Tüm erişim ilkesi girdileri de bağlı toothis Kiracı kimliğidir. Azure aboneliğinize taşıdığınızda kiracısı tootenant B, varolan anahtarınızı kasaları tarafından erişilemez Merhaba ilkelerini (kullanıcılar ve uygulamalar) Kiracı B. toofix içinde bu sorunu, gerekir:

* Bu abonelik tootenant B. içinde varolan tüm anahtar kasalarını ilişkili değişiklik hello Kiracı kimliği
* Mevcut tüm erişim ilkesi girdilerini kaldırın.
* B kiracısı ile ilişkili yeni erişim ilkesi girdileri ekleyin.

Örneğin, Kiracı A tootenant B, burada 's taşınan bir abonelikte 'myvault' anahtar kasası varsa, nasıl toochange hello kimliği bu anahtar kasası için Kiracı ve eski erişim ilkelerini kaldırın.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Bu kasaya Kiracı A hello taşıma önce olduğundan, özgün değeri hello **$vault. Properties.TenantId** Kiracı a while **(Get-AzureRmContext). Tenant.TenantId** olan Kiracı b

Kasanızı hello doğru Kiracı kimliği ile ilişkili olan ve eski erişim ilkesi girdileri kaldırılır artık, yeni erişim ilkesi girişlerle ayarlayın [kümesi AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Sonraki adımlar
Azure anahtar kasası hakkında sorularınız varsa hello ziyaret [Azure anahtar kasası forumları](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

