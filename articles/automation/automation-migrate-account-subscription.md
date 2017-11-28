---
title: "aaaMigrate Automation hesaplarına ve kaynaklarına | Microsoft Docs"
description: "Bu makalede nasıl toomove bir Automation hesabı Azure Automation ve ilişkili kaynakları bir abonelik tooanother açıklanmaktadır."
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="5fa06-103">Otomasyon hesabı ve kaynakları geçirme</span><span class="sxs-lookup"><span data-stu-id="5fa06-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="5fa06-104">Automation hesapları ve hello Azure portal oluşturulup istediğiniz ilişkili kaynaklarını (yani varlıklar, runbook'ları, modüller, vb.) için bir kaynaktan toomigrate Grup tooanother veya bir abonelik tooanother bunu kolayca gerçekleştirebilirsiniz Merhaba [kaynakları taşımak](../azure-resource-manager/resource-group-move-resources.md) özelliği hello Azure portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="5fa06-105">Ancak, bu eylemle devam etmeden önce ilk hello aşağıdakileri gözden geçirmeniz gereken [kaynakları geçmeden önce denetim listesi](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) ve ayrıca, belirli tooAutomation aşağıdaki hello liste.</span><span class="sxs-lookup"><span data-stu-id="5fa06-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="5fa06-106">Merhaba hedef abonelik/kaynak grubu hello kaynağı olarak aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="5fa06-107">Yani, Automation hesapları bölgeler arasında taşınamaz.</span><span class="sxs-lookup"><span data-stu-id="5fa06-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="5fa06-108">Kaynakları (örneğin runbook'ları, işleri, vb.) taşırken hello kaynak grubu ve hello hedef grubu hello hello işlemi süresince kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="5fa06-109">Yazma ve silme işlemleri hello taşıma işlemi tamamlanana kadar hello gruplarında engellenir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="5fa06-110">Herhangi bir runbook'ları veya bir kaynak veya abonelik kimliği hello varolan abonelikten başvuran değişkenler geçiş tamamlandıktan sonra güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="5fa06-111">Bu özellik, taşıma Klasik automation kaynaklarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5fa06-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="5fa06-112">toomove hello hello portal kullanarak Automation hesabını</span><span class="sxs-lookup"><span data-stu-id="5fa06-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="5fa06-113">Otomasyon hesabınızdan tıklatın **taşıma** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="5fa06-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="5fa06-114">![Seçeneği taşıyın](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="5fa06-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="5fa06-115">Merhaba üzerinde **taşıma kaynakları** dikey penceresinde, Automation hesabınızı ve kaynak gruplarını, kaynakları ilgili tooboth yansıtacak şekilde Not.</span><span class="sxs-lookup"><span data-stu-id="5fa06-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="5fa06-116">Select hello **abonelik** ve **kaynak grubu** hello açılan listeleri ya da select hello seçeneği **yeni bir kaynak grubu oluşturma** ve yeni bir kaynak grubu adı girin sağlanan hello alanı.</span><span class="sxs-lookup"><span data-stu-id="5fa06-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="5fa06-117">Gözden geçirme ve seçme hello onay kutusunu tooacknowledge, *araçları ve komut dosyaları anlamanıza gerek güncelleştirilmiş toobe toouse yeni kaynak kaynakları taşındıktan sonra kimlikleri* ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5fa06-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="5fa06-118">![Kaynaklar dikey taşıma](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="5fa06-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="5fa06-119">Bu işlem birkaç dakika toocomplete sürer.</span><span class="sxs-lookup"><span data-stu-id="5fa06-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="5fa06-120">İçinde **bildirimleri**, - doğrulama, geçiş, gerçekleşir her eylem durumuyla sunulur ve ardından son olarak, bu tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5fa06-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="5fa06-121">toomove hello PowerShell kullanarak Automation hesabını</span><span class="sxs-lookup"><span data-stu-id="5fa06-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="5fa06-122">toomove var olan Otomasyon kaynakları tooanother kaynak grubu veya abonelik hello kullanın, **Get-AzureRmResource** cmdlet tooget hello belirli Otomasyon hesabı ve ardından **taşıma AzureRmResource** cmdlet tooperform hello taşıyın.</span><span class="sxs-lookup"><span data-stu-id="5fa06-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="5fa06-123">Merhaba ilk örneği, nasıl toomove bir Otomasyon hesabı tooa yeni kaynak grubu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fa06-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="5fa06-124">Yukarıdaki kod örneğinde hello yürüttükten sonra bu eylem tooperform istediğiniz istendiğinde tooverify olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fa06-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="5fa06-125">Tıkladığınızda **Evet** ve izin betik tooproceed Merhaba, hello geçiş yaparken, herhangi bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5fa06-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="5fa06-126">toomove tooa yeni abonelik, hello için bir değer dahil *DestinationSubscriptionId* parametresi.</span><span class="sxs-lookup"><span data-stu-id="5fa06-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="5fa06-127">Merhaba önceki örnek olarak, istendiğinde tooconfirm hello taşıma olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fa06-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5fa06-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5fa06-128">Next steps</span></span>
* <span data-ttu-id="5fa06-129">Taşıma kaynakları toonew kaynak grubuna veya aboneliğe hakkında daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="5fa06-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="5fa06-130">Azure automation'da rol tabanlı erişim denetimi hakkında daha fazla bilgi için çok başvuran[Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="5fa06-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="5fa06-131">Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında toolearn bakın [Azure PowerShell'i Resource Manager ile kullanma](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5fa06-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="5fa06-132">Aboneliğinizi yönetmek için portal özellikleri hakkında toolearn bkz [hello Azure Portal toomanage kaynakları kullanarak](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5fa06-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
