---
title: "Azure DevTest Labs toocreate VM'ler aaaManage formüller | Microsoft Docs"
description: "Bilgi nasıl tooupdate ekleme ve kaldırma Azure DevTest Labs formüller"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="d0360-103">Azure DevTest Labs formüller yönetme</span><span class="sxs-lookup"><span data-stu-id="d0360-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="d0360-104">Bu makalede gösterilmektedir nasıl toocreate temel (özel görüntü, Market görüntüsü veya başka bir formül) veya mevcut bir VM'yi bir formül.</span><span class="sxs-lookup"><span data-stu-id="d0360-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="d0360-105">Bu makalede ayrıca, varolan formüller yönetme aracılığıyla size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0360-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="d0360-106">Formül oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0360-106">Create a formula</span></span>
<span data-ttu-id="d0360-107">DevTest Labs kimseyle *kullanıcıların* izinleri olan bir formül temel olarak kullanarak mümkün toocreate VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d0360-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="d0360-108">Toocreate formüller iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="d0360-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="d0360-109">Merhaba formülü tüm hello özelliklerini toodefine istediğinizde bir taban - kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0360-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="d0360-110">Var olan Laboratuvar VM - formül mevcut bir VM'yi hello ayarlarınızı temel alan toocreate istediğinizde kullanın</span><span class="sxs-lookup"><span data-stu-id="d0360-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="d0360-111">Kullanıcılar ve izinler ekleme hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sahipleri ve kullanıcılar ekleme](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="d0360-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="d0360-112">Formül bir taban oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0360-112">Create a formula from a base</span></span>
<span data-ttu-id="d0360-113">Aşağıdaki adımları hello formül özel bir görüntü, Market görüntüsü ya da başka bir formül oluşturma hello işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="d0360-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="d0360-114">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0360-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="d0360-115">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="d0360-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="d0360-116">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0360-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="d0360-117">Merhaba Laboratuvar'ın dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.</span><span class="sxs-lookup"><span data-stu-id="d0360-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="d0360-119">Merhaba üzerinde **formüller** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d0360-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Formül ekleme](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="d0360-121">Merhaba üzerinde **bir temel seçin** dikey penceresinde, toocreate hello formülü istediğiniz select hello temel (özel görüntü, Market görüntüsünü veya formülü).</span><span class="sxs-lookup"><span data-stu-id="d0360-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Temel listesi](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="d0360-123">Merhaba üzerinde **formül oluşturma** dikey penceresinde hello aşağıdaki değerleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="d0360-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="d0360-124">**Formül adı** -formül için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d0360-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="d0360-125">Bu değer bir VM oluşturma hello temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d0360-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="d0360-126">Merhaba adı yazdığınız ve geçerli değil, bir ileti için geçerli bir ad hello gereksinimleri gösterir doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="d0360-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="d0360-127">**Açıklama** -formül için anlamlı bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="d0360-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="d0360-128">Bir VM oluştururken bu değeri hello formülün bağlam menüsünden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0360-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="d0360-129">**Kullanıcı adı** -yönetici ayrıcalıkları verilmiş bir kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="d0360-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="d0360-130">**Parola** - girin - veya hello aşağı açılır listeden seçin - toouse hello belirtilen kullanıcı için istediğiniz hello gizliliği (parola) ile ilişkili olan bir değer.</span><span class="sxs-lookup"><span data-stu-id="d0360-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="d0360-131">Merhaba gizli anahtarları hakkında daha fazla bilgi için bkz: [Azure DevTest Labs: Kişisel gizli depolama](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="d0360-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="d0360-132">**Sanal makine disk türü** - iki HDD (sabit disk sürücüsü) belirtin veya bu temel görüntü kullanılarak sağlanan hello sanal makineler için hangi depolama disk türü SSD (katı hal sürücüsü) tooindicate izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d0360-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="d0360-133">** Sanal makine boyutu ** - hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin önceden tanımlanmış hello öğeleri birini seçin.</span><span class="sxs-lookup"><span data-stu-id="d0360-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="d0360-134">**Yapıları** -Select tooopen hello **yapıları eklemek** dikey penceresinde, seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d0360-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="d0360-135">Yapılar hakkında daha fazla bilgi için bkz: [Azure DevTest Labs yönetmek VM yapıları](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0360-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="d0360-136">**Gelişmiş ayarlar** -Select tooopen hello **Gelişmiş** hello ayarları aşağıdaki yapılandırdığınız dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="d0360-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="d0360-137">**Sanal ağ** -hello istenen sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0360-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="d0360-138">**Alt ağ** -hello istenen alt ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0360-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="d0360-139">**IP adresi yapılandırması** -hello genel, özel veya paylaşılan IP adreslerini isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0360-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="d0360-140">Paylaşılan IP adresleri hakkında daha fazla bilgi için bkz: [anlayın paylaşılan Azure DevTest Labs IP adresleri](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="d0360-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="d0360-141">**Bu makineyi claimable hale** -bir makine "claimable" yapmadan anlamına gelir, sahipliği hello oluşturma sırasında atanması değil.</span><span class="sxs-lookup"><span data-stu-id="d0360-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="d0360-142">Bunun yerine Laboratuvar kullanıcılar mümkün tootake sahipliği ("talep") hello makine hello Laboratuvar'ın dikey penceresinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0360-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="d0360-143">**Görüntü** -Bu alan hello önceki dikey penceresinde hello temel görüntü seçtiğiniz adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0360-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="d0360-145">Seçin **oluşturma** toocreate hello formül.</span><span class="sxs-lookup"><span data-stu-id="d0360-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="d0360-146">Merhaba formülü oluşturduğunuzda hello hello listesinde görüntüler **formüller** dikey.</span><span class="sxs-lookup"><span data-stu-id="d0360-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="d0360-147">Bir sanal makineden bir formül oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0360-147">Create a formula from a VM</span></span>
<span data-ttu-id="d0360-148">Merhaba aşağıdaki adımları var olan bir VM temelinde bir formül oluşturma hello işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="d0360-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0360-149">bir VM formülünden toocreate hello VM 30 Mart 2016'dan sonra oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0360-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="d0360-150">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0360-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0360-151">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="d0360-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="d0360-152">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0360-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="d0360-153">Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select hello VM içinden istediğiniz toocreate hello formül.</span><span class="sxs-lookup"><span data-stu-id="d0360-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Labs VM'ler](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="d0360-155">Merhaba VM'in dikey penceresinde, seçin **formül (yeniden kullanılabilir temel) oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d0360-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="d0360-157">Merhaba üzerinde **formül oluşturma** dikey penceresinde girin bir **adı** ve **açıklama** için yeni formül.</span><span class="sxs-lookup"><span data-stu-id="d0360-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Formül dikey penceresi oluşturma](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="d0360-159">Seçin **Tamam** toocreate hello formül.</span><span class="sxs-lookup"><span data-stu-id="d0360-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="d0360-160">Bir formülü değiştirme</span><span class="sxs-lookup"><span data-stu-id="d0360-160">Modify a formula</span></span>
<span data-ttu-id="d0360-161">toomodify bir formül şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0360-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="d0360-162">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0360-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0360-163">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="d0360-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="d0360-164">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0360-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="d0360-165">Merhaba Laboratuvar'ın dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.</span><span class="sxs-lookup"><span data-stu-id="d0360-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="d0360-167">Merhaba üzerinde **Laboratuvar formüller** dikey penceresinde, select hello formül toomodify istiyor.</span><span class="sxs-lookup"><span data-stu-id="d0360-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="d0360-168">Merhaba üzerinde **güncelleştirme formülü** dikey penceresinde, istenen hello düzenlemeleri yapın ve seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="d0360-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="d0360-169">Formül silme</span><span class="sxs-lookup"><span data-stu-id="d0360-169">Delete a formula</span></span>
<span data-ttu-id="d0360-170">toodelete bir formül şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0360-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="d0360-171">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d0360-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="d0360-172">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="d0360-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="d0360-173">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0360-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="d0360-174">Merhaba Laboratuvar üzerinde **ayarları** dikey penceresinde, select **formüller**.</span><span class="sxs-lookup"><span data-stu-id="d0360-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="d0360-176">Merhaba üzerinde **Laboratuvar formüller** , dikey penceresinde, select hello üç nokta toohello hello formülü sağında toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="d0360-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="d0360-178">Merhaba formülün bağlam menüsünde seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d0360-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Formül bağlam menüsü](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="d0360-180">Seçin **Evet** toohello silme onayı iletişim.</span><span class="sxs-lookup"><span data-stu-id="d0360-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="d0360-181">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="d0360-181">Related blog posts</span></span>
* [<span data-ttu-id="d0360-182">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="d0360-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="d0360-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0360-183">Next steps</span></span>
<span data-ttu-id="d0360-184">Bir VM oluştururken kullanmak için bir formül oluşturduktan sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="d0360-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

