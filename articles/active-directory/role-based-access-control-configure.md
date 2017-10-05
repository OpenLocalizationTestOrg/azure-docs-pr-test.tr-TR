---
title: "Azure portalında Rol Tabanlı Access Control | Microsoft Docs"
description: "Azure Portal'da Rol Tabanlı Erişim Denetimi ile erişim yönetimine başlayın. Kaynaklarınıza izinler atamak için rol atamalarını kullanın."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 9df7f7851ef1fc6b4ed03b981aa5062d6b0913ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-access-to-your-azure-subscription-resources"></a><span data-ttu-id="257a9-104">Azure abonelik kaynaklarınıza erişimi yönetmek için Rol Tabanlı Erişim Denetimi kullanma</span><span class="sxs-lookup"><span data-stu-id="257a9-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="257a9-105">Kullanıcı veya gruba göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="257a9-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="257a9-106">Kaynağa göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="257a9-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="257a9-107">Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="257a9-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="257a9-108">RBAC kullanarak, yalnızca kullanıcıların işlerini yapmak için gereksinim duyduğu erişim miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="257a9-109">Bu makale, Azure portalında RBAC ile çalışmaya başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="257a9-109">This article helps you get up and running with RBAC in the Azure portal.</span></span> <span data-ttu-id="257a9-110">RBAC'nin erişimi yönetmenize nasıl yardımcı olduğu konusunda daha fazla bilgi isterseniz bkz. [Rol Tabanlı Erişim Denetimi Nedir?](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="257a9-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="257a9-111">Her abonelikte en fazla 2000 rol ataması verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-111">Within each subscription, you can grant up to 2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="257a9-112">Erişimi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="257a9-112">View access</span></span>
<span data-ttu-id="257a9-113">Kimin bir kaynağa, kaynak grubuna veya aboneliğe erişimi olduğunu [Azure portal](https://portal.azure.com)'da ana dikey penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="257a9-114">Örneğin, kimin kaynak gruplarımızdan birine erişimi olduğunu görmek istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="257a9-114">For example, we want to see who has access to one of our resource groups:</span></span>

1. <span data-ttu-id="257a9-115">Soldaki gezinti çubuğunda **Kaynak grupları** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="257a9-115">Select **Resource groups** in the navigation bar on the left.</span></span>  
    <span data-ttu-id="257a9-116">![Kaynak grupları - simge](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="257a9-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="257a9-117">**Kaynak grupları** dikey penceresinde kaynak grubunun adını seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-117">Select the name of the resource group from the **Resource groups** blade.</span></span>
3. <span data-ttu-id="257a9-118">Soldaki menüden **Erişim denetimi (IAM)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-118">Select **Access control (IAM)** from the left menu.</span></span>  
4. <span data-ttu-id="257a9-119">Erişim denetimi dikey penceresi, kaynak grubuna erişim verilen tüm kullanıcıları, grupları ve uygulamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="257a9-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span></span>  
   
    ![Kullanıcılar dikey penceresi - devralınmış veya atanmış erişim ekran görüntüsü](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="257a9-121">Bazı rollerin kapsamı **Bu kaynak** olarak belirlenmişken diğerlerinin başka bir kapsamdan **Devralınmış** olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="257a9-121">Notice that some roles are scoped to **This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="257a9-122">Erişim, özellikle kaynak grubuna atanmış veya üst aboneliğe yapılan atamadan devralınmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="257a9-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="257a9-123">Yeni RBAC modelinde, klasik abonelik yöneticileri ve ortak yöneticileri aboneliğin sahipleri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="257a9-123">Classic subscription admins and co-admins are considered owners of the subscription in the new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="257a9-124">Erişim Ekleme</span><span class="sxs-lookup"><span data-stu-id="257a9-124">Add Access</span></span>
<span data-ttu-id="257a9-125">Rol atamasının kapsamı olan kaynak, kaynak grubu veya abonelik içinden erişim verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span></span>

1. <span data-ttu-id="257a9-126">Erişim denetimi dikey penceresinde **Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-126">Select **Add** on the Access control blade.</span></span>  
2. <span data-ttu-id="257a9-127">**Rol seçin** dikey penceresinde atamak istediğiniz rolü seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-127">Select the role that you wish to assign from the **Select a role** blade.</span></span>
3. <span data-ttu-id="257a9-128">Dizininizde, erişim vermek istediğiniz kullanıcı, grup veya uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-128">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="257a9-129">Görünen adlar, e-posta adresleri ve nesne tanımlayıcıları ile dizinde arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-129">You can search the directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Kullanıcı ekle dikey penceresi - arama ekran görüntüsü](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="257a9-131">Atamayı oluşturmak için **Tamam**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-131">Select **OK** to create the assignment.</span></span> <span data-ttu-id="257a9-132">**Kullanıcı ekleme** açılır penceresi ilerleme durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="257a9-132">The **Adding user** popup tracks the progress.</span></span>  
    <span data-ttu-id="257a9-133">![Kullanıcı ekleniyor ilerleme çubuğu - ekran görüntüsü](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="257a9-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="257a9-134">Bir rol ataması başarıyla eklendikten sonra **Kullanıcılar** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="257a9-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="257a9-135">Erişimi Kaldırma</span><span class="sxs-lookup"><span data-stu-id="257a9-135">Remove Access</span></span>
1. <span data-ttu-id="257a9-136">İmlecinizi kaldırmak istediğiniz atama adının üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="257a9-136">Hover your cursor over the name of the assignment that you want to remove.</span></span> <span data-ttu-id="257a9-137">Adın yanında bir onay kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="257a9-137">A check box appears next to the name.</span></span>
2. <span data-ttu-id="257a9-138">Onay kutularını kullanarak bir veya daha fazla rol ataması seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-138">Use the check boxes to select one or more role assignments.</span></span>
2. <span data-ttu-id="257a9-139">**Kaldır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="257a9-140">Kaldırma işlemini onaylamak için **Evet**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="257a9-140">Select **Yes** to confirm the removal.</span></span>

<span data-ttu-id="257a9-141">Devralınmış atamalar kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="257a9-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="257a9-142">Devralınmış bir atamayı kaldırmanız gerekiyorsa bu işlemi rol atamasının oluşturulduğu kapsamda gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="257a9-142">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span></span> <span data-ttu-id="257a9-143">**Kapsam** sütunundaki **Devralınmış** seçeneğinin yanında, sizi rolün oluşturulduğu kaynaklara götüren bir bağlantı yer alır.</span><span class="sxs-lookup"><span data-stu-id="257a9-143">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span></span> <span data-ttu-id="257a9-144">Rol atamasını kaldırmak için orada listelenen kaynağa gidin.</span><span class="sxs-lookup"><span data-stu-id="257a9-144">Go to the resource listed there to remove the role assignment.</span></span>

![Kullanıcılar dikey penceresi - devralınmış erişim kaldır düğmesini devre dışı bırakır ekran görüntüsü](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-to-manage-access"></a><span data-ttu-id="257a9-146">Erişimi yönetmeye yönelik diğer araçlar</span><span class="sxs-lookup"><span data-stu-id="257a9-146">Other tools to manage access</span></span>
<span data-ttu-id="257a9-147">Azure portal dışındaki araçlarda Azure RBAC komutları ile roller atayabilir ve erişimi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257a9-147">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span></span>  <span data-ttu-id="257a9-148">Önkoşullar hakkında daha fazla bilgi edinmek ve Azure RBAC komutlarını kullanmaya başlamak için bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="257a9-148">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span></span>

* [<span data-ttu-id="257a9-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="257a9-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="257a9-150">Azure Komut Satırı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="257a9-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="257a9-151">REST API</span><span class="sxs-lookup"><span data-stu-id="257a9-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="257a9-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="257a9-152">Next Steps</span></span>
* [<span data-ttu-id="257a9-153">Erişim değişiklik geçmişi raporu oluşturma</span><span class="sxs-lookup"><span data-stu-id="257a9-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="257a9-154">Bkz. [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="257a9-154">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="257a9-155">Kendiniz için [Azure RBAC'de özel roller](role-based-access-control-custom-roles.md) tanımlama</span><span class="sxs-lookup"><span data-stu-id="257a9-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

