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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="dcdc7-103">Abonelik taşıma işlemi sonrasında anahtar kasası kiracı kimliğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="dcdc7-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="dcdc7-104">S: Aboneliğimi Kiracı A tootenant B. taşındı Nasıl my olan bir anahtar kasası için hello Kiracı kimliği değiştirmek ve Kiracı B Sorumlular için doğru ACL ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="dcdc7-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="dcdc7-105">Bir abonelikte yeni bir anahtar kasası oluşturduğunuzda, bu abonelik için otomatik olarak bağlı toohello varsayılan Azure Active Directory Kiracı kimliği olur.</span><span class="sxs-lookup"><span data-stu-id="dcdc7-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="dcdc7-106">Tüm erişim ilkesi girdileri de bağlı toothis Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="dcdc7-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="dcdc7-107">Azure aboneliğinize taşıdığınızda kiracısı tootenant B, varolan anahtarınızı kasaları tarafından erişilemez Merhaba ilkelerini (kullanıcılar ve uygulamalar) Kiracı B. toofix içinde bu sorunu, gerekir:</span><span class="sxs-lookup"><span data-stu-id="dcdc7-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="dcdc7-108">Bu abonelik tootenant B. içinde varolan tüm anahtar kasalarını ilişkili değişiklik hello Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="dcdc7-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="dcdc7-109">Mevcut tüm erişim ilkesi girdilerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="dcdc7-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="dcdc7-110">B kiracısı ile ilişkili yeni erişim ilkesi girdileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dcdc7-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="dcdc7-111">Örneğin, Kiracı A tootenant B, burada 's taşınan bir abonelikte 'myvault' anahtar kasası varsa, nasıl toochange hello kimliği bu anahtar kasası için Kiracı ve eski erişim ilkelerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="dcdc7-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="dcdc7-112">Bu kasaya Kiracı A hello taşıma önce olduğundan, özgün değeri hello **$vault. Properties.TenantId** Kiracı a while **(Get-AzureRmContext). Tenant.TenantId** olan Kiracı b</span><span class="sxs-lookup"><span data-stu-id="dcdc7-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="dcdc7-113">Kasanızı hello doğru Kiracı kimliği ile ilişkili olan ve eski erişim ilkesi girdileri kaldırılır artık, yeni erişim ilkesi girişlerle ayarlayın [kümesi AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="dcdc7-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcdc7-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dcdc7-114">Next steps</span></span>
<span data-ttu-id="dcdc7-115">Azure anahtar kasası hakkında sorularınız varsa hello ziyaret [Azure anahtar kasası forumları](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="dcdc7-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

