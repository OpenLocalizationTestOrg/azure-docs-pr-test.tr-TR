---
title: aaaCreate ilk VM'nizi Azure DevTest Labs laboratuvarda | Microsoft Docs
description: "Bilgi nasıl toocreate ilk sanal makinenizde bir laboratuar ortamında Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="54637-103">Azure DevTest Labs laboratuvarda ilk VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="54637-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="54637-104">Başlangıçta DevTest Labs erişmek ve ilk VM toocreate istediğiniz zaman, büyük olasılıkla bunu önceden yüklenmiş kullanarak yapacağınız [temel Market görüntüsü](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="54637-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="54637-105">Daha sonra gelen mümkün toochoose de bir [özel görüntü ve bir formül](devtest-lab-add-vm.md) daha fazla sanal makineleri oluştururken.</span><span class="sxs-lookup"><span data-stu-id="54637-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="54637-106">Bu öğreticide, Azure portal tooadd hello kullanılarak üzerinden ilk VM tooa laboratuvarınızda DevTest Labs açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54637-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="54637-107">İlk VM tooa laboratuvarınızda Azure DevTest Labs tooadd adımları</span><span class="sxs-lookup"><span data-stu-id="54637-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="54637-108">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="54637-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="54637-109">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="54637-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="54637-110">Labs Hello listeden toocreate hello VM istediğiniz hello Laboratuvar seçin.</span><span class="sxs-lookup"><span data-stu-id="54637-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="54637-111">Merhaba Laboratuvar'ın üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="54637-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="54637-113">Merhaba üzerinde **bir temel seçin** bir Market görüntü dikey penceresinde, select hello VM.</span><span class="sxs-lookup"><span data-stu-id="54637-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="54637-114">Merhaba üzerinde **sanal makine** dikey penceresinde hello hello yeni bir sanal makine için bir ad girin **sanal makine adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="54637-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="54637-116">Girin bir **kullanıcı adı** hello sanal makinede yönetici ayrıcalıkları verilmiş.</span><span class="sxs-lookup"><span data-stu-id="54637-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="54637-117">Etiketli hello metin alanına bir parola girin **bir değer yazın**.</span><span class="sxs-lookup"><span data-stu-id="54637-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="54637-118">Merhaba **sanal makine disk türü** hello laboratuarda hello sanal makineler için hangi depolama disk türüne izin belirler.</span><span class="sxs-lookup"><span data-stu-id="54637-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="54637-119">Seçin **sanal makine boyutu** ve hello birini seçin hello işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu hello VM toocreate hello belirtin öğeleri önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="54637-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="54637-120">Seçin **yapıları** - - yapılarının hello listesinden seçin ve tooadd toohello temel görüntü istediğiniz hello yapıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="54637-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="54637-121">**Not:** yeni tooDevTest Labs olduğunuz ya da yapılar yapılandırma toohello başvurmak [var artifact tooa VM eklemek](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.</span><span class="sxs-lookup"><span data-stu-id="54637-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="54637-122">Seçin **oluşturma** tooadd hello belirtilen VM toohello Laboratuvar.</span><span class="sxs-lookup"><span data-stu-id="54637-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="54637-123">Merhaba Laboratuvar dikey görüntüler hello VM'in oluşturma - hello durumunu ilk olarak **oluşturma**, ardından olarak **çalıştıran** VM başlatıldığında hello sonra.</span><span class="sxs-lookup"><span data-stu-id="54637-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54637-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54637-124">Next steps</span></span>
* <span data-ttu-id="54637-125">Bir kez VM oluşturulan hello toohello VM seçerek bağlayabilirsiniz **Bağlan** hello VM'in dikey.</span><span class="sxs-lookup"><span data-stu-id="54637-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="54637-126">Kullanıma [VM tooa Laboratuvar ekleme](devtest-lab-add-vm.md) sonraki VM'ler laboratuvarınızda ekleme hakkında daha ayrıntılı bilgi.</span><span class="sxs-lookup"><span data-stu-id="54637-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="54637-127">Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="54637-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
