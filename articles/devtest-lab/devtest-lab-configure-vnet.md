---
title: "Azure DevTest Labs sanal bir ağa aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl tooconfigure bir varolan sanal ağ ve alt ağ ve bunları Azure DevTest Labs bir VM'de kullanın"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="db60f-103">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="db60f-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="db60f-104">Merhaba makalesinde açıklandığı gibi [yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md), bir laboratuar ortamında bir VM oluştururken yapılandırılmış bir sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="db60f-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="db60f-105">Bunu yapmak için bir tooaccess gerekiyorsa corpnet kaynaklarınızdan kullanarak, Vm'lerde ExpressRoute veya siteden siteye VPN ile yapılandırılmış sanal ağ hello senaryodur.</span><span class="sxs-lookup"><span data-stu-id="db60f-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="db60f-106">Merhaba aşağıdaki bölümlerde göstermeye nasıl tooadd varolan sanal ağınıza onun kullanılabilir toochoose Vm'leri oluştururken, böylece bir laboratuvar ait sanal ağ ayarları.</span><span class="sxs-lookup"><span data-stu-id="db60f-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="db60f-107">Hello Azure portal kullanarak bir laboratuvar için bir sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="db60f-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="db60f-108">Merhaba aşağıdaki adımlar, böylece bir VM hello oluşturulurken kullanılabilir var olan sanal ağ (ve alt ağ) tooa Laboratuvar eklerken size yol aynı Laboratuvar.</span><span class="sxs-lookup"><span data-stu-id="db60f-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="db60f-109">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="db60f-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="db60f-110">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="db60f-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="db60f-111">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="db60f-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="db60f-112">Merhaba Laboratuvar'ın dikey penceresinde, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="db60f-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="db60f-113">Merhaba Laboratuvar'ın üzerinde **yapılandırma** dikey penceresinde, select **sanal ağlar**.</span><span class="sxs-lookup"><span data-stu-id="db60f-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="db60f-114">Merhaba üzerinde **sanal ağlar** dikey penceresinde hello geçerli Laboratuvar ve bunun yanı sıra, laboratuvarınız için oluşturulan hello varsayılan sanal ağ için yapılandırılan sanal ağların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="db60f-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="db60f-115">Seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="db60f-115">Select **+ Add**.</span></span>
   
    ![Varolan bir sanal ağ tooyour Laboratuvar ekleme](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="db60f-117">Merhaba üzerinde **sanal ağ** dikey penceresinde, select **[Select sanal ağ]**.</span><span class="sxs-lookup"><span data-stu-id="db60f-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Varolan bir sanal ağı seçin](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="db60f-119">Merhaba üzerinde **Seç sanal ağ** dikey penceresinde, select hello istenen sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="db60f-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="db60f-120">Merhaba dikey gösterir altında aynı hello olan tüm hello sanal ağları hello Laboratuvar olarak hello Abonelikteki bölge.</span><span class="sxs-lookup"><span data-stu-id="db60f-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="db60f-121">Bir sanal ağı seçtikten sonra toohello döndürülür **sanal ağ** hello dikey penceresinde hello sonundaki hello listesinde hello alt ağ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="db60f-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Alt ağ listesi](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="db60f-123">Merhaba Laboratuvar alt dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="db60f-123">hello Lab Subnet blade is displayed.</span></span>

    ![Laboratuvar alt dikey penceresi](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="db60f-125">Belirtin bir **Laboratuvar alt ağ adı**.</span><span class="sxs-lookup"><span data-stu-id="db60f-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="db60f-126">VM oluşturma, Laboratuvar içinde kullanılan bir alt ağ toobe tooallow seçin **sanal makine oluşturma kullanımda**.</span><span class="sxs-lookup"><span data-stu-id="db60f-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="db60f-127">tooenable bir [genel IP adresi paylaşılan](devtest-lab-shared-ip.md)seçin **etkinleştir paylaşılan ortak IP**.</span><span class="sxs-lookup"><span data-stu-id="db60f-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="db60f-128">tooallow genel IP adresleri bir alt ağ seçin **ortak IP oluşturmaya izin**.</span><span class="sxs-lookup"><span data-stu-id="db60f-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="db60f-129">Merhaba, **kullanıcı başına en fazla sanal makine** alanında, belirtin her alt ağ için kullanıcı başına en fazla VMs hello.</span><span class="sxs-lookup"><span data-stu-id="db60f-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="db60f-130">Sanal makineleri sınırsız sayıda istiyorsanız bu alanı boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="db60f-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="db60f-131">Seçin **Tamam** tooclose hello Laboratuvar alt dikey.</span><span class="sxs-lookup"><span data-stu-id="db60f-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="db60f-132">Seçin **kaydetmek** tooclose hello sanal ağ dikey.</span><span class="sxs-lookup"><span data-stu-id="db60f-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="db60f-133">Merhaba sanal ağı yapılandırılır, bir VM oluşturulurken seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="db60f-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="db60f-134">toosee nasıl toocreate VM ve bir sanal ağ belirtin, toohello makalesine başvurun [yapıları tooa Laboratuvar'yle bir VM'yi eklemek](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="db60f-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="db60f-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db60f-135">Next steps</span></span>
<span data-ttu-id="db60f-136">Merhaba istenen sanal ağ tooyour Laboratuvar ekledikten sonra hello sonraki çok adımdır[VM tooyour Laboratuvar ekleme](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="db60f-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

