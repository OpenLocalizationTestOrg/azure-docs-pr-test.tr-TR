---
title: "Azure DevTest Labs aaaConfigure Azure Market görüntü ayarlarında | Microsoft Docs"
description: "Hangi Azure Marketi görüntüleri bir VM Azure DevTest Labs'de oluşturulurken kullanılan yapılandırma"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="ccae3-103">Azure DevTest Labs'de Azure Market görüntü ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ccae3-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="ccae3-104">DevTest Labs Laboratuvar içinde kullanılan Azure Market görüntülerini toobe nasıl yapılandırdığınıza bağlı olarak Azure Market görüntüsünü temel oluşturma Vm'leri destekler.</span><span class="sxs-lookup"><span data-stu-id="ccae3-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="ccae3-105">Bu makale size nasıl gösterir, varsa, Azure Market görüntülerini olabilecek toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ccae3-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="ccae3-106">Bu, ekibinizin yalnızca ihtiyaç duydukları erişim toohello Market görüntülerini sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ccae3-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="ccae3-107">Bir VM oluşturulurken hangi Azure Market görüntülerini verileceğini seçin</span><span class="sxs-lookup"><span data-stu-id="ccae3-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="ccae3-108">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ccae3-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="ccae3-109">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="ccae3-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="ccae3-110">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ccae3-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="ccae3-111">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma ve ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="ccae3-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="ccae3-112">Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** altında dikey **sanal makine tabanları**seçin **Market görüntülerini**.</span><span class="sxs-lookup"><span data-stu-id="ccae3-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="ccae3-113">Tam Azure Market görüntülerini toobe yeni bir VM temeli olarak kullanmak için kullanılabilir tüm hello isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="ccae3-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="ccae3-114">Seçerseniz **Evet**, ardından tüm hello Azure Market görüntülerini tüm hello ölçütleri karşılayan verilir hello laboratuar ortamında:</span><span class="sxs-lookup"><span data-stu-id="ccae3-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="ccae3-115">Merhaba görüntüsünü oluşturur tek bir VM'ye **ve**</span><span class="sxs-lookup"><span data-stu-id="ccae3-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="ccae3-116">Merhaba görüntüsünü kullanan Azure Resource Manager tooprovision VM'ler **ve**</span><span class="sxs-lookup"><span data-stu-id="ccae3-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="ccae3-117">Hello görüntü ek lisans planı satın almayı gerektirmez</span><span class="sxs-lookup"><span data-stu-id="ccae3-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="ccae3-118">İzin verilen hiçbir görüntüleri toobe istediğiniz veya hangi görüntüleri seçin, kullanılabilir toospecify isterseniz **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="ccae3-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Seçenek tooallow tüm Market görüntülerini toobe temel görüntü olarak VM'ler için kullanılır](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="ccae3-120">Seçerseniz **Hayır** toohello önceki adım, hello **izin verilen görüntüleri/seçmek tüm** onay kutusunu etkindir.</span><span class="sxs-lookup"><span data-stu-id="ccae3-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="ccae3-121">Merhaba arama kutusu tooquickly seçin birlikte bu seçeneği kullanın veya hello listesinde görüntülenen tüm hello öğelerin seçimini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ccae3-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="ccae3-122">Tooallow VM oluşturmak için ayrı ayrı her görüntünün karşılık gelen onay kutusunu işaretleyerek istediğiniz hello Azure Market görüntülerini seçin.</span><span class="sxs-lookup"><span data-stu-id="ccae3-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="ccae3-123">Merhaba laboratuar ortamında kullanılan tüm Azure Marketi görüntüleri toobe tooallow istemiyorsanız, hiçbir şey hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ccae3-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Hangi Azure Market görüntülerini VM'ler için temel görüntü olarak kullanılabilir belirtebilirsiniz](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="ccae3-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ccae3-125">Next steps</span></span>
<span data-ttu-id="ccae3-126">Bir VM oluşturulurken Azure Market görüntülerini nasıl verildiğini yapılandırdıktan sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="ccae3-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

