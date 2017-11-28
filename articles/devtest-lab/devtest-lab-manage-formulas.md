---
title: "Sanal makineleri oluşturmak için Azure DevTest Labs formüller yönetme | Microsoft Docs"
description: "Güncelleştirme ve Azure DevTest Labs formüller kaldırma hakkında bilgi edinin"
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
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="49e43-103">Azure DevTest Labs formüller yönetme</span><span class="sxs-lookup"><span data-stu-id="49e43-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="49e43-104">Bu makalede temel (özel görüntü, Market görüntüsü veya başka bir formül) veya mevcut bir VM'yi bir formül oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="49e43-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="49e43-105">Bu makalede ayrıca, varolan formüller yönetme aracılığıyla size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="49e43-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="49e43-106">Formül oluşturma</span><span class="sxs-lookup"><span data-stu-id="49e43-106">Create a formula</span></span>
<span data-ttu-id="49e43-107">DevTest Labs kimseyle *kullanıcılar* izinleridir formül temel olarak kullanarak sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49e43-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="49e43-108">Formülleri oluşturmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="49e43-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="49e43-109">Formül tüm özelliklerini tanımlamak bir taban - kullanın.</span><span class="sxs-lookup"><span data-stu-id="49e43-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="49e43-110">Bir var olan Laboratuvar VM - mevcut bir VM'yi ayarlarınızı temel alan bir formül oluşturmak istediğinizde kullanın.</span><span class="sxs-lookup"><span data-stu-id="49e43-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="49e43-111">Kullanıcılar ve izinler ekleme hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sahipleri ve kullanıcılar ekleme](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="49e43-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="49e43-112">Formül bir taban oluşturma</span><span class="sxs-lookup"><span data-stu-id="49e43-112">Create a formula from a base</span></span>
<span data-ttu-id="49e43-113">Aşağıdaki adımlar bir formül özel bir görüntü, Market görüntüsü ya da başka bir formül oluşturma işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="49e43-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="49e43-114">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="49e43-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="49e43-115">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="49e43-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="49e43-116">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="49e43-117">Laboratuvar 's dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.</span><span class="sxs-lookup"><span data-stu-id="49e43-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="49e43-119">Üzerinde **formüller** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="49e43-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Formül ekleme](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="49e43-121">Üzerinde **bir temel seçin** dikey penceresinde, seçin istediğiniz için temel (özel görüntü, Market görüntüsünü veya formül) formülü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49e43-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Temel listesi](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="49e43-123">Üzerinde **formül oluşturma** dikey penceresinde, aşağıdaki değerleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="49e43-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="49e43-124">**Formül adı** -formül için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="49e43-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="49e43-125">Bir VM oluştururken bu değeri temel görüntü listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="49e43-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="49e43-126">Ad, yazdığınız ve geçerli değil, bir ileti geçerli bir ad gereksinimlerini gösterir doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="49e43-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="49e43-127">**Açıklama** -formül için anlamlı bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="49e43-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="49e43-128">Bir VM oluştururken bu değeri formülün bağlam menüsünden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="49e43-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="49e43-129">**Kullanıcı adı** -yönetici ayrıcalıkları verilmiş bir kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="49e43-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="49e43-130">**Parola** - girin - veya aşağı açılır listeden seçin - belirtilen kullanıcı için kullanmak istediğiniz gizliliği (parola) ile ilişkili olan bir değer.</span><span class="sxs-lookup"><span data-stu-id="49e43-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="49e43-131">Gizli anahtarları hakkında daha fazla bilgi için bkz: [Azure DevTest Labs: Kişisel gizli depolama](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="49e43-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="49e43-132">**Sanal makine disk türü** - iki HDD (sabit disk sürücüsü) belirtin veya bu temel görüntü kullanılarak sağlanan sanal makineler için hangi depolama disk türünü belirtmek için (katı hal sürücüsü) SSD izin verilir.</span><span class="sxs-lookup"><span data-stu-id="49e43-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="49e43-133">** Sanal makine boyutu ** - işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu oluşturmak için VM belirtin önceden tanımlanmış öğeleri birini seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="49e43-134">**Yapıları** - açmak için Select **yapıları eklemek** dikey penceresinde, seçin ve temel görüntü eklemek istediğiniz yapıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="49e43-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="49e43-135">Yapılar hakkında daha fazla bilgi için bkz: [Azure DevTest Labs yönetmek VM yapıları](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="49e43-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="49e43-136">**Gelişmiş ayarlar** - açmak için Select **Gelişmiş** aşağıdaki ayarları yapılandırdığınız dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="49e43-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="49e43-137">**Sanal ağ** -istenen sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="49e43-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="49e43-138">**Alt ağ** -istenen alt ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="49e43-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="49e43-139">**IP adresi yapılandırması** -genel, özel veya paylaşılan IP adreslerini isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="49e43-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="49e43-140">Paylaşılan IP adresleri hakkında daha fazla bilgi için bkz: [anlayın paylaşılan Azure DevTest Labs IP adresleri](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="49e43-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="49e43-141">**Bu makineyi claimable hale** -bir makine "claimable" yapmadan anlamına gelir, sahipliği oluşturma sırasında atanması değil.</span><span class="sxs-lookup"><span data-stu-id="49e43-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="49e43-142">Bunun yerine Laboratuvar kullanıcılara ("talep") Laboratuvar 's dikey penceresinde makine sahipliğini mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="49e43-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="49e43-143">**Görüntü** -Bu alan, seçili temel görüntü adı önceki dikey penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="49e43-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="49e43-145">Seçin **oluşturma** formül oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="49e43-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="49e43-146">Formül oluşturduğunuzda listede görüntüler **formüller** dikey.</span><span class="sxs-lookup"><span data-stu-id="49e43-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="49e43-147">Bir sanal makineden bir formül oluşturma</span><span class="sxs-lookup"><span data-stu-id="49e43-147">Create a formula from a VM</span></span>
<span data-ttu-id="49e43-148">Aşağıdaki adımları var olan bir VM temelinde bir formül oluşturma işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="49e43-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="49e43-149">Bir sanal makineden bir formül oluşturmak için VM 30 Mart 2016'dan sonra oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="49e43-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="49e43-150">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="49e43-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="49e43-151">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="49e43-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="49e43-152">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="49e43-153">Laboratuvar 's üzerinde **genel bakış** dikey penceresinde, istediğiniz formül oluşturmak VM seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Labs VM'ler](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="49e43-155">VM'ın dikey penceresinde, seçin **formül (yeniden kullanılabilir temel) oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="49e43-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Formül oluşturma](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="49e43-157">Üzerinde **formül oluşturma** dikey penceresinde girin bir **adı** ve **açıklama** için yeni formül.</span><span class="sxs-lookup"><span data-stu-id="49e43-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Formül dikey penceresi oluşturma](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="49e43-159">Seçin **Tamam** formül oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="49e43-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="49e43-160">Bir formülü değiştirme</span><span class="sxs-lookup"><span data-stu-id="49e43-160">Modify a formula</span></span>
<span data-ttu-id="49e43-161">Bir formülü değiştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49e43-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="49e43-162">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="49e43-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="49e43-163">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="49e43-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="49e43-164">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="49e43-165">Laboratuvar 's dikey penceresinde, seçin **formüller (yeniden kullanılabilir tabanları)**.</span><span class="sxs-lookup"><span data-stu-id="49e43-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="49e43-167">Üzerinde **Laboratuvar formüller** dikey penceresinde değiştirmek istediğiniz formülü seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="49e43-168">Üzerinde **güncelleştirme formülü** dikey penceresinde, istenen düzenlemeleri yapın ve seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="49e43-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="49e43-169">Formül silme</span><span class="sxs-lookup"><span data-stu-id="49e43-169">Delete a formula</span></span>
<span data-ttu-id="49e43-170">Formül silmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="49e43-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="49e43-171">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="49e43-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="49e43-172">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="49e43-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="49e43-173">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="49e43-174">Laboratuvar üzerinde **ayarları** dikey penceresinde, select **formüller**.</span><span class="sxs-lookup"><span data-stu-id="49e43-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="49e43-176">Üzerinde **Laboratuvar formüller** dikey penceresinde, silmek istediğiniz formülü sağındaki üç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="49e43-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Formül menüsü](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="49e43-178">Formülün bağlam menüsünde seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="49e43-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Formül bağlam menüsü](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="49e43-180">Seçin **Evet** silme onayı iletişim.</span><span class="sxs-lookup"><span data-stu-id="49e43-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="49e43-181">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="49e43-181">Related blog posts</span></span>
* [<span data-ttu-id="49e43-182">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="49e43-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="49e43-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49e43-183">Next steps</span></span>
<span data-ttu-id="49e43-184">Bir VM oluştururken kullanmak için bir formül oluşturduktan sonra sıradaki adım olacak [Laboratuvarınızı için bir VM eklemek](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="49e43-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

