---
title: "Belirli Laboratuvar ilkeleri için kullanıcı izinleri verin | Microsoft Docs"
description: "DevTest Labs her kullanıcının ihtiyaçlarına göre belirli Laboratuvar ilkeleri kullanıcı izinleri öğrenin"
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
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="028da-103">Belirli Laboratuvar ilkeleri kullanıcı izinleri</span><span class="sxs-lookup"><span data-stu-id="028da-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="028da-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="028da-104">Overview</span></span>
<span data-ttu-id="028da-105">Bu makalede PowerShell belirli Laboratuvar ilkesi kullanıcıların izinleri için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="028da-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="028da-106">Bu şekilde izinleri her kullanıcının gereksinimlerinize göre uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="028da-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="028da-107">Örneğin, belirli bir kullanıcı VM ilke ayarları, ancak maliyet ilkeleri değiştirme olanağı vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="028da-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="028da-108">İlke kaynakları olarak</span><span class="sxs-lookup"><span data-stu-id="028da-108">Policies as resources</span></span>
<span data-ttu-id="028da-109">' Da anlatıldığı gibi [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md) makale, RBAC Azure kaynaklarının ayrıntılı erişim yönetimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="028da-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="028da-110">RBAC kullanarak, DevOps ekibiniz içinde görevleri kurabilmeleri ve işlerini yapmak için gereksinim duydukları kullanıcılara sadece erişim miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="028da-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="028da-111">DevTest Labs'de RBAC eylem sağlayan bir kaynak türü ilkedir **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="028da-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="028da-112">Her Laboratuvar ilke ilke kaynak türü, bir kaynak değildir ve bir RBAC rolü için kapsam olarak atanabilir.</span><span class="sxs-lookup"><span data-stu-id="028da-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="028da-113">Örneğin, kullanıcıların okuma/yazma izni için **izin VM boyutları** İlkesi ile çalışır, özel bir rol oluşturmak **Microsoft.DevTestLab/labs/policySets/policies/*** Eylem ve bu özel rolü kapsamında uygun kullanıcılara atamak **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="028da-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="028da-114">RBAC özel rolleri hakkında daha fazla bilgi edinmek için [özel roller erişim denetimi](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="028da-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="028da-115">PowerShell kullanarak bir lab özel rol oluşturma</span><span class="sxs-lookup"><span data-stu-id="028da-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="028da-116">Başlamak için yükleme ve Azure PowerShell cmdlet'leri yapılandırma açıklanacaktır aşağıdaki makaleyi okuyun gerekecektir: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="028da-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="028da-117">Azure PowerShell cmdlet'lerini ayarladıktan sonra aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="028da-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="028da-118">Bir kaynak sağlayıcısı için tüm işlemleri/eylemleri listesi</span><span class="sxs-lookup"><span data-stu-id="028da-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="028da-119">Belirli bir rol eylemler listesi:</span><span class="sxs-lookup"><span data-stu-id="028da-119">List actions in a particular role:</span></span>
* <span data-ttu-id="028da-120">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="028da-120">Create a custom role</span></span>

<span data-ttu-id="028da-121">Aşağıdaki PowerShell betiğini bu görevleri gerçekleştirmek nasıl örnekleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="028da-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
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

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="028da-122">Özel roller kullanarak belirli bir ilke için bir kullanıcı için izinler atama</span><span class="sxs-lookup"><span data-stu-id="028da-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="028da-123">Özel rollerinizi tanımladığınız sonra bunları kullanıcılara atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="028da-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="028da-124">Bir kullanıcıya özel bir rol atamak için önce edinmeniz gerekir **objectID** bu kullanıcıyı temsil eden.</span><span class="sxs-lookup"><span data-stu-id="028da-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="028da-125">Bunu yapmak için kullanmak **Get-AzureRmADUser** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="028da-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="028da-126">Aşağıdaki örnekte, **objectID** , *SomeUser* 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="028da-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="028da-127">Bulduktan sonra **objectID** kullanıcı ve özel rol adı için kullanıcı bu rol atayabilirsiniz **New-AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="028da-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="028da-128">Önceki örnekte, **AllowedVmSizesInLab** İlkesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="028da-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="028da-129">Aşağıdakilerden herhangi birini kullanabilirsiniz ilkeler:</span><span class="sxs-lookup"><span data-stu-id="028da-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="028da-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="028da-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="028da-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="028da-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="028da-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="028da-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="028da-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="028da-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="028da-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="028da-134">Next steps</span></span>
<span data-ttu-id="028da-135">Bir kez dikkate alınması gereken bazı sonraki adımlar şunlardır belirli Laboratuvar ilkeleri için kullanıcı izinleri verilen:</span><span class="sxs-lookup"><span data-stu-id="028da-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="028da-136">[Laboratuvara erişimin güvenliğini sağlama](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="028da-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="028da-137">[Laboratuvar ilkeleri belirleme](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="028da-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="028da-138">[Laboratuvar şablonu oluşturma](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="028da-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="028da-139">[VM'leriniz için özel yapılar oluşturma](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="028da-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="028da-140">[Yapı içeren bir VM'yi laboratuvara ekleme](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="028da-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

