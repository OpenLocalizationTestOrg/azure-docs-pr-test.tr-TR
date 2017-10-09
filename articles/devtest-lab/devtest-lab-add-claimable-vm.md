---
title: Azure DevTest Labs claimable bir VM tooa laboratuvarda aaaAdd | Microsoft Docs
description: "Bilgi nasıl tooadd Azure DevTest Labs claimable sanal makine tooa laboratuvarda"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="03ab8-103">Azure DevTest Labs'de claimable VM tooa Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="03ab8-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="03ab8-104">Bir benzer şekilde toohow claimable VM tooa Laboratuvar ekleme, [standart VM eklemek](devtest-lab-add-vm.md) – bir *temel* ya da başka bir deyişle bir [özel görüntü](devtest-lab-create-template.md), [formülü](devtest-lab-manage-formulas.md), veya [Market görüntüsü](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="03ab8-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="03ab8-105">Bu öğretici DevTest Labs claimable bir VM tooa laboratuvarda hello Azure portal tooadd kullanılarak üzerinden anlatılmaktadır ve bir kullanıcının tooclaim hello VM izlediği hello işlemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="03ab8-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="03ab8-106">Laboratuvar VM'ler aracılığıyla dağıtırsanız [Azure Resource Manager şablonları](devtest-lab-create-environment-from-arm.md), ayarı hello tarafından claimable VM'ler oluşturabilirsiniz **allowClaim** özelliği tootrue hello özellikler bölümünde.</span><span class="sxs-lookup"><span data-stu-id="03ab8-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="03ab8-107">Adımları tooadd Azure DevTest Labs claimable bir VM tooa laboratuvarda</span><span class="sxs-lookup"><span data-stu-id="03ab8-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="03ab8-108">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="03ab8-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="03ab8-109">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="03ab8-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="03ab8-110">Merhaba Laboratuvar labs Hello listeden seçin, istediğiniz toocreate hello claimable VM.</span><span class="sxs-lookup"><span data-stu-id="03ab8-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="03ab8-111">Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="03ab8-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="03ab8-113">Merhaba üzerinde **bir temel seçin** dikey penceresinde hello VM için temel bir seçin.</span><span class="sxs-lookup"><span data-stu-id="03ab8-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="03ab8-114">Merhaba üzerinde **sanal makine** dikey penceresinde hello hello yeni bir sanal makine için bir ad girin **sanal makine adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="03ab8-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="03ab8-116">Girin bir **kullanıcı adı** hello sanal makinede yönetici ayrıcalıkları verilmiş.</span><span class="sxs-lookup"><span data-stu-id="03ab8-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="03ab8-117">Toouse istiyorsanız bir parola depolanır, [gizli deposu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)seçin **kaydedilmiş gizliliği kullanın**ve tooyour gizliliği (parola) karşılık gelen bir anahtar değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="03ab8-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="03ab8-118">Aksi halde, bir parola etiketli hello metin alanına **bir değer yazın**.</span><span class="sxs-lookup"><span data-stu-id="03ab8-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="03ab8-119">Merhaba **sanal makine disk türü** hello laboratuarda hello sanal makineler için hangi depolama disk türüne izin belirler.</span><span class="sxs-lookup"><span data-stu-id="03ab8-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="03ab8-120">Seçin **sanal makine boyutu** ve hello birini seçin hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin öğeleri önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="03ab8-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="03ab8-121">Seçin **yapıları** hello yapılarının, listeden seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="03ab8-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="03ab8-122">Yeni tooDevTest Labs olduğunuz ya da yapılar yapılandırma toohello başvurmak [var artifact tooa VM eklemek](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.</span><span class="sxs-lookup"><span data-stu-id="03ab8-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="03ab8-123">Seçin **Gelişmiş ayarları** tooconfigure hello VM'in ağ seçenekleri ve sona erme tarihi seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="03ab8-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="03ab8-124">Altında **talep seçenekleri**, seçin **Evet** toomake hello makine claimable.</span><span class="sxs-lookup"><span data-stu-id="03ab8-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Toomake hello VM claimable seçin.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="03ab8-126">Tooview istediğiniz veya kopyalarsanız hello Azure Resource Manager şablonu toohello başvuran [Kaydet Azure Resource Manager şablonu](devtest-lab-add-vm.md#save-azure-resource-manager-template) bölümünde ve bittiğinde buraya dönün.</span><span class="sxs-lookup"><span data-stu-id="03ab8-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="03ab8-127">Seçin **oluşturma** tooadd hello belirtilen VM toohello Laboratuvar.</span><span class="sxs-lookup"><span data-stu-id="03ab8-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="03ab8-128">Merhaba Laboratuvar dikey görüntüler hello VM'in oluşturma - hello durumunu ilk olarak **oluşturma**, ardından olarak **çalıştıran** VM başlatıldığında hello sonra.</span><span class="sxs-lookup"><span data-stu-id="03ab8-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="03ab8-129">Claimable VM kullanma</span><span class="sxs-lookup"><span data-stu-id="03ab8-129">Using a claimable VM</span></span>

<span data-ttu-id="03ab8-130">Bir kullanıcı, aşağıdaki adımlardan birini yaparak "Claimable sanal makineler" Merhaba listesinden herhangi bir VM talep:</span><span class="sxs-lookup"><span data-stu-id="03ab8-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="03ab8-131">Hello listesinde "Claimable sanal makinelerin" Merhaba Laboratuvar'ın genel bakış dikey penceresinde hello sonundaki hello VM'ler hello listesinde birine sağ tıklayın ve seçin **talep makine**.</span><span class="sxs-lookup"><span data-stu-id="03ab8-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Belirli bir claimable VM'yi isteyin.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="03ab8-133">Merhaba hello üstündeki **genel bakış** dikey penceresinde, seçin **herhangi bir talep**.</span><span class="sxs-lookup"><span data-stu-id="03ab8-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="03ab8-134">Rastgele bir sanal makine hello claimable VM'ler listesinden atanır.</span><span class="sxs-lookup"><span data-stu-id="03ab8-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Tüm claimable VM isteyin.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="03ab8-136">Bir kullanıcı bir VM talep sonra kendi "Benim sanal makineler" listesine taşınır ve artık herhangi bir kullanıcı tarafından claimable değil.</span><span class="sxs-lookup"><span data-stu-id="03ab8-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03ab8-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03ab8-137">Next steps</span></span>
* <span data-ttu-id="03ab8-138">Bir kez VM oluşturulan hello toohello VM seçerek bağlayabilirsiniz **Bağlan** hello VM'in dikey.</span><span class="sxs-lookup"><span data-stu-id="03ab8-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="03ab8-139">Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="03ab8-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
