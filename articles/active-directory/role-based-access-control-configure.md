---
title: "hello Azure portalı içinde aaaRole tabanlı erişim denetimi | Microsoft Docs"
description: "Erişim Yönetimi'nde hello Azure Portal'ın rol tabanlı erişim denetimi ile çalışmaya başlayın. Rol atamaları tooassign izinleri tooyour kaynağı kullanın."
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
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="a4331-104">Rol tabanlı erişim denetimi toomanage erişim tooyour Azure aboneliği kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="a4331-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4331-105">Kullanıcı veya gruba göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="a4331-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="a4331-106">Kaynağa göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="a4331-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="a4331-107">Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4331-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="a4331-108">RBAC kullanarak, kullanıcıların işlerini tooperform gerektiğini yalnızca hello erişim miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4331-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="a4331-109">Bu makalede, hello Azure portalında RBAC ile başlamak ve çalıştırmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a4331-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="a4331-110">RBAC'nin erişimi yönetmenize nasıl yardımcı olduğu konusunda daha fazla bilgi isterseniz bkz. [Rol Tabanlı Erişim Denetimi Nedir?](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="a4331-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="a4331-111">Her abonelik içinde too2000 rol atamalarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4331-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="a4331-112">Erişimi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a4331-112">View access</span></span>
<span data-ttu-id="a4331-113">Hello erişim tooa kaynak, kaynak grubuna veya aboneliğe da ana dikey olanların görebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4331-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a4331-114">Örneğin, erişim tooone bizim kaynak grubuna sahip toosee isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4331-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="a4331-115">Seçin **kaynak grupları** hello sol gezinti çubuğunda hello.</span><span class="sxs-lookup"><span data-stu-id="a4331-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="a4331-116">![Kaynak grupları - simge](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="a4331-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="a4331-117">Merhaba hello kaynak grubundan SELECT hello adını **kaynak grupları** dikey.</span><span class="sxs-lookup"><span data-stu-id="a4331-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="a4331-118">Seçin **erişim denetimi (IAM)** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="a4331-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="a4331-119">Merhaba erişim denetimi dikey tüm kullanıcılar, gruplar ve erişim toohello kaynak grubuna verilen uygulamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="a4331-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Kullanıcılar dikey penceresi - devralınmış veya atanmış erişim ekran görüntüsü](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="a4331-121">Bazı roller çok kapsamlı fark**bu kaynak** diğerleri çalışırken **devralınan** başka bir kapsamda ondan.</span><span class="sxs-lookup"><span data-stu-id="a4331-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="a4331-122">Erişim özellikle toohello kaynak grubuna atanmış veya bir atama toohello üst abonelikten devralındı.</span><span class="sxs-lookup"><span data-stu-id="a4331-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a4331-123">Klasik abonelik yöneticileri ve ortak Yöneticiler hello abonelik sahipleri hello yeni RBAC modelinde olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a4331-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="a4331-124">Erişim Ekleme</span><span class="sxs-lookup"><span data-stu-id="a4331-124">Add Access</span></span>
<span data-ttu-id="a4331-125">Merhaba kaynak, kaynak grubu veya hello rol ataması hello kapsamı abonelik içinden erişim verin.</span><span class="sxs-lookup"><span data-stu-id="a4331-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="a4331-126">Seçin **Ekle** hello erişim denetimi dikey.</span><span class="sxs-lookup"><span data-stu-id="a4331-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="a4331-127">Select hello rol hello gelen tooassign istediğiniz **bir rol seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="a4331-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="a4331-128">Dizininizde toogrant erişmesini istediğiniz Hello kullanıcı, Grup veya uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="a4331-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="a4331-129">Merhaba directory görünen adları, e-posta adresleri ve nesne tanımlayıcıları ile arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4331-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Kullanıcı ekle dikey penceresi - arama ekran görüntüsü](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="a4331-131">Seçin **Tamam** toocreate hello atama.</span><span class="sxs-lookup"><span data-stu-id="a4331-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="a4331-132">Merhaba **kullanıcı ekleme** açılan hello ilerleme durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="a4331-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="a4331-133">![Kullanıcı ekleniyor ilerleme çubuğu - ekran görüntüsü](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="a4331-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="a4331-134">Bir rol ataması başarıyla eklendikten sonra üzerinde hello görüneceği **kullanıcılar** dikey.</span><span class="sxs-lookup"><span data-stu-id="a4331-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="a4331-135">Erişimi Kaldırma</span><span class="sxs-lookup"><span data-stu-id="a4331-135">Remove Access</span></span>
1. <span data-ttu-id="a4331-136">İmlecinizi tooremove istediğiniz hello atama hello adın üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="a4331-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="a4331-137">Bir onay kutusu sonraki toohello adı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a4331-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="a4331-138">Merhaba onay kutularını tooselect kullanan bir veya daha fazla rol atamaları.</span><span class="sxs-lookup"><span data-stu-id="a4331-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="a4331-139">**Kaldır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a4331-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="a4331-140">Seçin **Evet** tooconfirm hello kaldırma.</span><span class="sxs-lookup"><span data-stu-id="a4331-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="a4331-141">Devralınmış atamalar kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="a4331-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="a4331-142">Tooremove devralınan atama gerekiyorsa, hello adresinden kapsam hello rol ataması oluşturulduğu toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4331-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="a4331-143">Merhaba, **kapsam** sütun, sonraki çok**devralınan** burada bu rolü atandı toohello kaynakları götüren bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="a4331-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="a4331-144">Bu listede toohello kaynak Git tooremove hello rol ataması.</span><span class="sxs-lookup"><span data-stu-id="a4331-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Kullanıcılar dikey penceresi - devralınmış erişim kaldır düğmesini devre dışı bırakır ekran görüntüsü](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="a4331-146">Diğer araçlar toomanage erişim</span><span class="sxs-lookup"><span data-stu-id="a4331-146">Other tools toomanage access</span></span>
<span data-ttu-id="a4331-147">Roller atayabilir ve hello Azure portal dışındaki araçlarda Azure RBAC komutları ile erişimi yönetin.</span><span class="sxs-lookup"><span data-stu-id="a4331-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="a4331-148">Merhaba bağlantılar toolearn hello önkoşulları hakkında daha fazla izleyin ve hello Azure RBAC komutlarını kullanmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="a4331-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="a4331-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4331-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="a4331-150">Azure Komut Satırı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="a4331-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="a4331-151">REST API</span><span class="sxs-lookup"><span data-stu-id="a4331-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="a4331-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a4331-152">Next Steps</span></span>
* [<span data-ttu-id="a4331-153">Erişim değişiklik geçmişi raporu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4331-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="a4331-154">Merhaba bkz [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="a4331-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="a4331-155">Kendiniz için [Azure RBAC'de özel roller](role-based-access-control-custom-roles.md) tanımlama</span><span class="sxs-lookup"><span data-stu-id="a4331-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

