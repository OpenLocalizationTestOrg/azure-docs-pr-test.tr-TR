---
title: "aaaAdd sahipleri ve Azure DevTest Labs kullanıcılar | Microsoft Docs"
description: "Hello Azure portal veya PowerShell kullanarak Azure DevTest Labs içinde sahipleri ve kullanıcılar ekleme"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="f1adb-103">Azure DevTest Labs'de sahipleri ve kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="f1adb-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="f1adb-104">Azure DevTest Labs Access'te tarafından denetlenir [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f1adb-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="f1adb-105">RBAC kullanarak, ekibiniz içinde içinde görevlerini ayırabilirsiniz *rolleri* burada verdiğiniz yalnızca hello miktarını erişim gerekli toousers tooperform işlerini.</span><span class="sxs-lookup"><span data-stu-id="f1adb-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="f1adb-106">Üç RBAC rolde olan *sahibi*, *DevTest Labs kullanıcı*, ve *katkıda bulunan*.</span><span class="sxs-lookup"><span data-stu-id="f1adb-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="f1adb-107">Bu makalede, hangi eylemlerin her hello üç ana RBAC rolü gerçekleştirilebilir öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f1adb-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="f1adb-108">Buradan, nasıl tooadd kullanıcılar tooa Laboratuvar - aracılığıyla her ikisi de hello öğrenin portal ve farklı bir PowerShell Betiği ve nasıl tooadd kullanıcılar abonelik düzeyinde hello aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="f1adb-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="f1adb-109">Her rol gerçekleştirilen eylemler</span><span class="sxs-lookup"><span data-stu-id="f1adb-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="f1adb-110">Bir kullanıcı atayabilirsiniz üç ana rol vardır:</span><span class="sxs-lookup"><span data-stu-id="f1adb-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="f1adb-111">Sahip</span><span class="sxs-lookup"><span data-stu-id="f1adb-111">Owner</span></span>
* <span data-ttu-id="f1adb-112">DevTest Labs kullanıcı</span><span class="sxs-lookup"><span data-stu-id="f1adb-112">DevTest Labs User</span></span>
* <span data-ttu-id="f1adb-113">Katılımcı</span><span class="sxs-lookup"><span data-stu-id="f1adb-113">Contributor</span></span>

<span data-ttu-id="f1adb-114">Merhaba aşağıdaki tabloda bu rollerin her biri bulunan kullanıcılar tarafından gerçekleştirilen hello Eylemler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f1adb-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="f1adb-115">**Bu roldeki kullanıcılar eylemleri gerçekleştirebilirsiniz**</span><span class="sxs-lookup"><span data-stu-id="f1adb-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="f1adb-116">**DevTest Labs kullanıcı**</span><span class="sxs-lookup"><span data-stu-id="f1adb-116">**DevTest Labs User**</span></span> | <span data-ttu-id="f1adb-117">**Sahibi**</span><span class="sxs-lookup"><span data-stu-id="f1adb-117">**Owner**</span></span> | <span data-ttu-id="f1adb-118">**Katkıda bulunan**</span><span class="sxs-lookup"><span data-stu-id="f1adb-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f1adb-119">**Laboratuvar görevleri**</span><span class="sxs-lookup"><span data-stu-id="f1adb-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="f1adb-120">Kullanıcıların tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="f1adb-120">Add users tooa lab</span></span> |<span data-ttu-id="f1adb-121">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-121">No</span></span> |<span data-ttu-id="f1adb-122">Yes</span><span class="sxs-lookup"><span data-stu-id="f1adb-122">Yes</span></span> |<span data-ttu-id="f1adb-123">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-123">No</span></span> |
| <span data-ttu-id="f1adb-124">Maliyet ayarlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f1adb-124">Update cost settings</span></span> |<span data-ttu-id="f1adb-125">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-125">No</span></span> |<span data-ttu-id="f1adb-126">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-126">Yes</span></span> |<span data-ttu-id="f1adb-127">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-127">Yes</span></span> |
| <span data-ttu-id="f1adb-128">**VM temel görevleri**</span><span class="sxs-lookup"><span data-stu-id="f1adb-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="f1adb-129">Özel resimler ekleyip</span><span class="sxs-lookup"><span data-stu-id="f1adb-129">Add and remove custom images</span></span> |<span data-ttu-id="f1adb-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-130">No</span></span> |<span data-ttu-id="f1adb-131">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-131">Yes</span></span> |<span data-ttu-id="f1adb-132">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-132">Yes</span></span> |
| <span data-ttu-id="f1adb-133">Ekleme, güncelleştirme ve formülleri silme</span><span class="sxs-lookup"><span data-stu-id="f1adb-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="f1adb-134">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-134">Yes</span></span> |<span data-ttu-id="f1adb-135">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-135">Yes</span></span> |<span data-ttu-id="f1adb-136">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-136">Yes</span></span> |
| <span data-ttu-id="f1adb-137">Beyaz liste Azure Marketi görüntüleri</span><span class="sxs-lookup"><span data-stu-id="f1adb-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="f1adb-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-138">No</span></span> |<span data-ttu-id="f1adb-139">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-139">Yes</span></span> |<span data-ttu-id="f1adb-140">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-140">Yes</span></span> |
| <span data-ttu-id="f1adb-141">**VM görevleri**</span><span class="sxs-lookup"><span data-stu-id="f1adb-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="f1adb-142">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1adb-142">Create VMs</span></span> |<span data-ttu-id="f1adb-143">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-143">Yes</span></span> |<span data-ttu-id="f1adb-144">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-144">Yes</span></span> |<span data-ttu-id="f1adb-145">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-145">Yes</span></span> |
| <span data-ttu-id="f1adb-146">Başlatma, durdurma ve sanal makineleri silin</span><span class="sxs-lookup"><span data-stu-id="f1adb-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="f1adb-147">Yalnızca Hello kullanıcı tarafından oluşturulan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="f1adb-147">Only VMs created by hello user</span></span> |<span data-ttu-id="f1adb-148">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-148">Yes</span></span> |<span data-ttu-id="f1adb-149">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-149">Yes</span></span> |
| <span data-ttu-id="f1adb-150">VM ilkelerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f1adb-150">Update VM policies</span></span> |<span data-ttu-id="f1adb-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-151">No</span></span> |<span data-ttu-id="f1adb-152">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-152">Yes</span></span> |<span data-ttu-id="f1adb-153">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-153">Yes</span></span> |
| <span data-ttu-id="f1adb-154">Veri diskleri için/VMs Ekle/Kaldır</span><span class="sxs-lookup"><span data-stu-id="f1adb-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="f1adb-155">Yalnızca Hello kullanıcı tarafından oluşturulan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="f1adb-155">Only VMs created by hello user</span></span> |<span data-ttu-id="f1adb-156">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-156">Yes</span></span> |<span data-ttu-id="f1adb-157">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-157">Yes</span></span> |
| <span data-ttu-id="f1adb-158">**Yapı görevleri**</span><span class="sxs-lookup"><span data-stu-id="f1adb-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="f1adb-159">Ekleme ve yapı depoları kaldırma</span><span class="sxs-lookup"><span data-stu-id="f1adb-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="f1adb-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="f1adb-160">No</span></span> |<span data-ttu-id="f1adb-161">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-161">Yes</span></span> |<span data-ttu-id="f1adb-162">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-162">Yes</span></span> |
| <span data-ttu-id="f1adb-163">Yapıları Uygula</span><span class="sxs-lookup"><span data-stu-id="f1adb-163">Apply artifacts</span></span> |<span data-ttu-id="f1adb-164">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-164">Yes</span></span> |<span data-ttu-id="f1adb-165">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-165">Yes</span></span> |<span data-ttu-id="f1adb-166">Evet</span><span class="sxs-lookup"><span data-stu-id="f1adb-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="f1adb-167">Bir kullanıcı bir VM oluşturduğunda, bu kullanıcının toohello otomatik olarak atanır **sahibi** VM oluşturulan hello rolü.</span><span class="sxs-lookup"><span data-stu-id="f1adb-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="f1adb-168">Merhaba Laboratuvar düzeyinde sahibi veya kullanıcı ekleyin</span><span class="sxs-lookup"><span data-stu-id="f1adb-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="f1adb-169">Sahipleri ve kullanıcıların hello Laboratuvar düzeyinde hello Azure portal aracılığıyla eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="f1adb-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="f1adb-170">Bu geçerli bir dış kullanıcılarla içerir [Microsoft hesabı (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="f1adb-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="f1adb-171">Aşağıdaki adımları hello Azure DevTest Labs'de bir sahibi veya kullanıcı tooa Laboratuvar ekleme hello işleminde size kılavuzluk eder:</span><span class="sxs-lookup"><span data-stu-id="f1adb-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="f1adb-172">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f1adb-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f1adb-173">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="f1adb-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f1adb-174">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f1adb-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="f1adb-175">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="f1adb-176">Merhaba üzerinde **yapılandırma** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="f1adb-177">Merhaba üzerinde **kullanıcılar** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Kullanıcı ekle](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="f1adb-179">Merhaba üzerinde **bir rol seçin** dikey penceresinde, select hello istenen rol.</span><span class="sxs-lookup"><span data-stu-id="f1adb-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="f1adb-180">Merhaba bölüm [her rolünde gerçekleştirilen eylemler](#actions-that-can-be-performed-in-each-role) listeleri hello hello sahibi, DevTest kullanıcı ve katkıda bulunan rollerinin bulunan kullanıcılar tarafından gerçekleştirilen çeşitli eylemler.</span><span class="sxs-lookup"><span data-stu-id="f1adb-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="f1adb-181">Merhaba üzerinde **kullanıcıları eklemek** dikey penceresinde hello e-posta adresi veya belirttiğiniz hello rolündeki tooadd istediğiniz hello kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="f1adb-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="f1adb-182">Merhaba kullanıcı bulunamazsa, bir hata iletisi hello sorun açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f1adb-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="f1adb-183">Merhaba kullanıcı bulunursa, o kullanıcı listelenen ve seçili.</span><span class="sxs-lookup"><span data-stu-id="f1adb-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="f1adb-184">Seçin **seçin**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-184">Select **Select**.</span></span>
10. <span data-ttu-id="f1adb-185">Seçin **Tamam** tooclose hello **erişim Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="f1adb-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="f1adb-186">Toohello döndüğünüzde **kullanıcılar** dikey penceresinde hello kullanıcı eklendi.</span><span class="sxs-lookup"><span data-stu-id="f1adb-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="f1adb-187">PowerShell kullanarak bir dış kullanıcı tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="f1adb-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="f1adb-188">Ayrıca tooadding kullanıcılar'hello Azure portal'ın bir PowerShell komut dosyası kullanarak bir dış kullanıcı tooyour laboratuvarı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1adb-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="f1adb-189">Hello hello altında hello parametre değerleri yalnızca değiştirme örneği, aşağıdaki **değerleri toochange** açıklama.</span><span class="sxs-lookup"><span data-stu-id="f1adb-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="f1adb-190">Merhaba alabilir `subscriptionId`, `labResourceGroup`, ve `labName` hello Laboratuvar dikey penceresinde hello Azure portal değerleri.</span><span class="sxs-lookup"><span data-stu-id="f1adb-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f1adb-191">Kullanıcı Konuk toohello Active Directory eklendi ve hello durumda değilse, başarısız olur, hello belirtilen Hello örnek betik varsayar.</span><span class="sxs-lookup"><span data-stu-id="f1adb-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="f1adb-192">tooadd hello Active Directory tooa Laboratuvar olmayan bir kullanıcı hello bölümünde gösterildiği gibi hello Azure portal tooassign hello kullanıcı tooa rolü kullanmak [sahibi veya kullanıcı hello Laboratuvar düzeyinde ekleme](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="f1adb-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="f1adb-193">Merhaba abonelik düzeyinde sahibi veya kullanıcı ekleyin</span><span class="sxs-lookup"><span data-stu-id="f1adb-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="f1adb-194">Azure izinleri üst kapsam toochild kapsamdan Azure yayılır.</span><span class="sxs-lookup"><span data-stu-id="f1adb-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="f1adb-195">Dolayısıyla, labs içeren Azure aboneliği sahipleri, otomatik olarak bu labs sahipleri altındadır.</span><span class="sxs-lookup"><span data-stu-id="f1adb-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="f1adb-196">Ayrıca hello VM'ler ve hello Laboratuvar'ın kullanıcılar hello Azure DevTest Labs hizmeti tarafından oluşturulan ve diğer kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="f1adb-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="f1adb-197">Hello hello Laboratuvar'ın dikey penceresi aracılığıyla ek sahipleri tooa Laboratuvar ekleyebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f1adb-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="f1adb-198">Ancak, hello sahibinin yönetim kapsamını hello abonelik sahibinin kapsamı daha dar eklenir.</span><span class="sxs-lookup"><span data-stu-id="f1adb-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="f1adb-199">Örneğin, hello sahipleri hello abonelikte hello DevTest Labs hizmeti tarafından oluşturulan hello kaynakların tam erişim toosome yok eklendi.</span><span class="sxs-lookup"><span data-stu-id="f1adb-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="f1adb-200">tooadd sahibi tooan Azure aboneliği, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f1adb-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="f1adb-201">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f1adb-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f1adb-202">Seçin **daha Hizmetleri**ve ardından **abonelikleri** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="f1adb-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="f1adb-203">İstenen hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="f1adb-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="f1adb-204">Seçin **erişim** simgesi.</span><span class="sxs-lookup"><span data-stu-id="f1adb-204">Select **Access** icon.</span></span> 
   
    ![Erişim kullanıcıları](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="f1adb-206">Merhaba üzerinde **kullanıcılar** dikey penceresinde, select **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Kullanıcı ekle](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="f1adb-208">Merhaba üzerinde **bir rol seçin** dikey penceresinde, seçin **sahibi**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="f1adb-209">Merhaba üzerinde **kullanıcıları eklemek** dikey penceresinde hello e-posta adresi veya adı girin hello kullanıcısı sahibi olarak tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="f1adb-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="f1adb-210">Merhaba kullanıcı bulunamazsa, hello sorunu açıklayan bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f1adb-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="f1adb-211">Merhaba kullanıcı bulunursa, o kullanıcı hello altında listelenen **kullanıcı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f1adb-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="f1adb-212">Merhaba bulunduğu kullanıcı adını seçin.</span><span class="sxs-lookup"><span data-stu-id="f1adb-212">Select hello located user name.</span></span>
9. <span data-ttu-id="f1adb-213">Seçin **seçin**.</span><span class="sxs-lookup"><span data-stu-id="f1adb-213">Select **Select**.</span></span>
10. <span data-ttu-id="f1adb-214">Seçin **Tamam** tooclose hello **erişim Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="f1adb-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="f1adb-215">Toohello döndüğünüzde **kullanıcılar** dikey penceresinde hello kullanıcı sahibi olarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="f1adb-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="f1adb-216">Bu kullanıcı artık bu abonelik altında oluşturulan labs sahibi ve böylece mümkün tooperform sahibi görevler.</span><span class="sxs-lookup"><span data-stu-id="f1adb-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

