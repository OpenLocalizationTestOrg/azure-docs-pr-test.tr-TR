---
title: "Abonelik taşıma işlemi sonrasında anahtar kasası kiracı kimliğini değiştirme | Microsoft Belgeleri"
description: "Abonelik farklı bir kiracıya taşındıktan sonra anahtar kasasına ilişkin kiracı kimliğini nasıl değiştireceğinizi öğrenin"
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="15a16-103">Abonelik taşıma işlemi sonrasında anahtar kasası kiracı kimliğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="15a16-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="15a16-104">S: Aboneliğim A kiracısından B kiracısına taşındı. Mevcut anahtar kasama ilişkin kiracı kimliğini nasıl değiştirebilir ve B kiracısındaki sorumlular için doğru ACL'leri nasıl belirleyebilirim?</span><span class="sxs-lookup"><span data-stu-id="15a16-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="15a16-105">Abonelikte yeni bir anahtar kasası oluşturduğunuzda, kasa bu abonelik için varsayılan Azure Active Directory kiracı kimliğine otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="15a16-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="15a16-106">Tüm erişim ilkesi girdileri de bu kiracı kimliğine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="15a16-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="15a16-107">Azure aboneliğinizi A kiracısından B kiracısına taşıdığınızda mevcut anahtar kasalarınız, B kiracısındaki sorumlular (kullanıcılar ve uygulamalar) tarafından erişilemez hale gelir. Bu sorunu düzeltmek için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="15a16-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="15a16-108">Bu abonelikte var olan tüm anahtar kasalarıyla ilişkili kiracı kimliklerini B kiracısı olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="15a16-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="15a16-109">Mevcut tüm erişim ilkesi girdilerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="15a16-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="15a16-110">B kiracısı ile ilişkili yeni erişim ilkesi girdileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="15a16-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="15a16-111">Örneğin, bir abonelikte A kiracısından B kiracısına taşınan 'myvault' adlı bir anahtar kasanız varsa bu anahtar kasası için kiracı kimliğini nasıl değiştireceğiniz ve eski erişim ilkelerini nasıl kaldıracağınız aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="15a16-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="15a16-112">Taşıma işlemi öncesinde bu kasa A kiracısında olduğundan, ilk **$vault.Properties.TenantId** değeri A kiracısıyken **(Get-AzureRmContext).Tenant.TenantId** değeri B kiracısıdır.</span><span class="sxs-lookup"><span data-stu-id="15a16-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="15a16-113">Artık kasanız doğru kiracı kimliğiyle ilişkilendirildiğine ve eski erişim ilkesi girdileri kaldırıldığına göre, [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx) ile yeni erişim ilkesi girdileri belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a16-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a16-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15a16-114">Next steps</span></span>
<span data-ttu-id="15a16-115">Azure Anahtar Kasası ile ilgili sorularınız varsa bkz. [Azure Anahtar Kasası Forumları](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="15a16-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

