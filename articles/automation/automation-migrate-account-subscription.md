---
title: "Otomasyon hesabı ve kaynakları geçirmek | Microsoft Docs"
description: "Bu makalede, Azure Automation ve ilişkili kaynakları Automation hesabında bir aboneliği taşımak açıklar."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="0dbe1-103">Otomasyon hesabı ve kaynakları geçirme</span><span class="sxs-lookup"><span data-stu-id="0dbe1-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="0dbe1-104">Automation hesapları ve Azure portalında oluşturduğunuz ve bir kaynak grubundan diğerine veya bir abonelik diğerine geçirmek istiyorsanız, ilişkili kaynakları (yani varlıklar, runbook'ları, modüller, vb.) için bunu kolayca gerçekleştirebilirsiniz [kaynakları taşımak](../azure-resource-manager/resource-group-move-resources.md) Özelliği Azure portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="0dbe1-105">Ancak, bu eylem işlemine devam etmeden önce önce aşağıdakileri gözden geçirmeniz gereken [kaynakları geçmeden önce denetim listesi](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) ve Otomasyon özgü ek olarak, aşağıdaki listeye.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="0dbe1-106">Hedef abonelik/kaynak grubu kaynağı olarak aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="0dbe1-107">Yani, Automation hesapları bölgeler arasında taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="0dbe1-108">Kaynakları (örneğin runbook'ları, işleri, vb.) taşırken, hem kaynak grubu hem de hedef grup işlemi boyunca kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="0dbe1-109">Yazma ve silme işlemleri taşıma işlemi tamamlanana kadar gruplarında engellenir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="0dbe1-110">Herhangi bir runbook'ları veya varolan abonelikten bir kaynak veya abonelik kimliği başvuran değişkenler, geçiş tamamlandıktan sonra güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="0dbe1-111">Bu özellik, taşıma Klasik automation kaynaklarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="0dbe1-112">Portal kullanarak Automation hesabını taşımak için</span><span class="sxs-lookup"><span data-stu-id="0dbe1-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="0dbe1-113">Otomasyon hesabınızdan tıklatın **taşıma** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="0dbe1-114">![Seçeneği taşıyın](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="0dbe1-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="0dbe1-115">Üzerinde **taşıma kaynakları** dikey penceresinde, Automation hesabınız ve kaynak grubu ile ilgili kaynaklara sunar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="0dbe1-116">Seçin **abonelik** ve **kaynak grubu** açılan listeleri ya da seçeneği **yeni bir kaynak grubu oluşturma** ve sağlanan alana yeni bir kaynak grubu adı girin.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="0dbe1-117">Gözden geçirin ve size kabul etmek için onay kutusunu işaretleyin *araçları anlamanız ve komut dosyaları kaynakları taşındıktan sonra yeni kaynak kimlikleri kullanacak şekilde güncelleştirilmesi gerekecek* ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="0dbe1-118">![Kaynaklar dikey taşıma](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="0dbe1-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="0dbe1-119">Bu eylemin tamamlanması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="0dbe1-120">İçinde **bildirimleri**, - doğrulama, geçiş, gerçekleşir her eylem durumuyla sunulur ve ardından son olarak, bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="0dbe1-121">PowerShell kullanarak Automation hesabını taşımak için</span><span class="sxs-lookup"><span data-stu-id="0dbe1-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="0dbe1-122">Başka bir kaynak grubuna veya aboneliğe mevcut Automation kaynaklarını taşımak için kullanın **Get-AzureRmResource** cmdlet'ini belirli Otomasyonu hesabını alın ve ardından **taşıma AzureRmResource** taşımayı gerçekleştirmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="0dbe1-123">İlk örnek bir Otomasyon hesabı yeni bir kaynak grubuna taşımak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="0dbe1-124">Yukarıdaki kod örneğinde yürüttükten sonra bu eylemi gerçekleştirmek istediğiniz doğrulamak için istenir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="0dbe1-125">Tıkladığınızda **Evet** ve devam etmek komut dosyası izin, geçiş işlemi gerçekleştirirken, herhangi bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="0dbe1-126">Yeni bir aboneliği taşımak için bir değer dahil *DestinationSubscriptionId* parametresi.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="0dbe1-127">Önceki örnekte olduğu gibi taşıma onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0dbe1-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dbe1-128">Next steps</span></span>
* <span data-ttu-id="0dbe1-129">Kaynakları yeni kaynak grubuna veya aboneliğe taşıma hakkında daha fazla bilgi için bkz: [yeni kaynak grubu veya abonelik kaynaklarını taşıma](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="0dbe1-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="0dbe1-130">Azure Automation’da Rol Tabanlı Erişim Denetimi hakkında daha fazla bilgi için bkz. [Azure Automation’da rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0dbe1-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="0dbe1-131">Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında bilgi edinmek için [Azure PowerShell'i Resource Manager ile kullanma](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0dbe1-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="0dbe1-132">Aboneliğinizi yönetmeye yönelik portal özellikleri hakkında bilgi edinmek için [kaynakları yönetmek için Azure Portalı'nı kullanarak](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0dbe1-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
