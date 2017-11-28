---
title: "aaaGrant kullanıcı izinleri toospecific Laboratuvar ilkeleri | Microsoft Docs"
description: "Nasıl toogrant kullanıcı izinleri toospecific Laboratuvar ilkeleri DevTest Labs her kullanıcının ihtiyaçlarına göre bilgi edinin"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="51331-103">Kullanıcı izinleri toospecific Laboratuvar ilkeleri</span><span class="sxs-lookup"><span data-stu-id="51331-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="51331-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="51331-104">Overview</span></span>
<span data-ttu-id="51331-105">Bu makalede gösterilmektedir nasıl toouse PowerShell toogrant kullanıcıların izinleri tooa belirli Laboratuvar ilkesi.</span><span class="sxs-lookup"><span data-stu-id="51331-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="51331-106">Bu şekilde izinleri her kullanıcının gereksinimlerinize göre uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="51331-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="51331-107">Örneğin, bir belirli kullanıcı hello özelliği toochange hello VM ilke ayarları toogrant isteyebilirsiniz, ancak değil hello ilkeleri maliyeti.</span><span class="sxs-lookup"><span data-stu-id="51331-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="51331-108">İlke kaynakları olarak</span><span class="sxs-lookup"><span data-stu-id="51331-108">Policies as resources</span></span>
<span data-ttu-id="51331-109">Hello anlatıldığı gibi [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md) makale, RBAC Azure kaynaklarının ayrıntılı erişim yönetimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="51331-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="51331-110">RBAC kullanarak, DevOps ekibiniz içinde görevleri kurabilmeleri ve tooperform işlerini gereken erişim toousers yalnızca hello miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51331-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="51331-111">DevTest Labs'de hello RBAC eylem sağlayan bir kaynak türü ilkedir **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="51331-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="51331-112">Her Laboratuvar ilke hello İlkesi kaynak türü, bir kaynak değildir ve bir kapsam tooan RBAC rolü olarak atanabilir.</span><span class="sxs-lookup"><span data-stu-id="51331-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="51331-113">Örneğin, sipariş toogrant kullanıcıların okuma/yazma izni toohello içinde **izin VM boyutları** İlkesi, hello ile çalışır, özel bir rol oluşturmak **Microsoft.DevTestLab/labs/policySets/policies/** * Eylem ve ata hello uygun kullanıcıları toothis özel rol hello kapsamındaki **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="51331-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="51331-114">toolearn RBAC, özel rolleri hakkında daha fazla bilgi görmek hello [özel roller erişim denetimi](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="51331-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="51331-115">PowerShell kullanarak bir lab özel rol oluşturma</span><span class="sxs-lookup"><span data-stu-id="51331-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="51331-116">Başlatılan sipariş tooget içinde anlatılmıştır makale aşağıdaki tooread hello gerekir nasıl tooinstall ve hello Azure PowerShell cmdlet'leri yapılandırma: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="51331-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="51331-117">Azure PowerShell cmdlet'lerini hello ayarladıktan sonra hello aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51331-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="51331-118">Bir kaynak sağlayıcısı için tüm hello operations/eylemler listesi</span><span class="sxs-lookup"><span data-stu-id="51331-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="51331-119">Belirli bir rol eylemler listesi:</span><span class="sxs-lookup"><span data-stu-id="51331-119">List actions in a particular role:</span></span>
* <span data-ttu-id="51331-120">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="51331-120">Create a custom role</span></span>

<span data-ttu-id="51331-121">PowerShell Betiği aşağıdaki hello örnekleri gösterilmektedir tooperform bu görevler:</span><span class="sxs-lookup"><span data-stu-id="51331-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="51331-122">İzinleri tooa kullanıcı için özel roller kullanarak belirli bir ilke atama</span><span class="sxs-lookup"><span data-stu-id="51331-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="51331-123">Özel rollerinizi tanımladığınız sonra bunları toousers atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51331-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="51331-124">Sipariş tooassign özel rol tooa kullanıcı, ilk hello edinmelidir **objectID** bu kullanıcıyı temsil eden.</span><span class="sxs-lookup"><span data-stu-id="51331-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="51331-125">Merhaba kullanın, toodo **Get-AzureRmADUser** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="51331-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="51331-126">Aşağıdaki örneğine hello hello **objectID** Merhaba, *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="51331-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="51331-127">Merhaba olduktan sonra **objectID** hello kullanıcı ve özel rol adı için bu rolü toohello kullanıcı hello ile atayabilirsiniz **New-AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="51331-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="51331-128">Merhaba önceki örnekte hello **AllowedVmSizesInLab** İlkesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51331-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="51331-129">Aşağıdaki ilkeler hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51331-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="51331-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="51331-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="51331-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="51331-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="51331-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="51331-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="51331-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="51331-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="51331-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51331-134">Next steps</span></span>
<span data-ttu-id="51331-135">Bir kez bazı sonraki adımları tooconsider İşte kullanıcı izinleri toospecific Laboratuvar ilkeleri, verilen:</span><span class="sxs-lookup"><span data-stu-id="51331-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="51331-136">[Güvenli erişim tooa Laboratuvar](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="51331-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="51331-137">[Laboratuvar ilkeleri belirleme](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="51331-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="51331-138">[Laboratuvar şablonu oluşturma](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="51331-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="51331-139">[VM'leriniz için özel yapılar oluşturma](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="51331-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="51331-140">[Yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="51331-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

