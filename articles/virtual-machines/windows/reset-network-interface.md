---
title: "Ağ arabirimi için Azure Windows VM sıfırlama | Microsoft Docs"
description: "Ağ arabirimi için Azure Windows VM sıfırlamak nasıl gösterir"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="b2a62-103">Ağ arabirimi için Azure Windows VM sıfırlama</span><span class="sxs-lookup"><span data-stu-id="b2a62-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b2a62-104">Ağ arabirimi (NIC) varsayılan devre dışı bırakmak veya el ile statik bir IP NIC için ayarlar sonra Microsoft Azure Windows sanal makine (VM) bağlanamıyor</span><span class="sxs-lookup"><span data-stu-id="b2a62-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="b2a62-105">Bu makalede, Azure Windows, uzak bağlantı sorunu gidermek için VM, ağ arabiriminin sıfırlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b2a62-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="b2a62-106">Ağ arabirimi Sıfırla</span><span class="sxs-lookup"><span data-stu-id="b2a62-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="b2a62-107">Klasik VM'ler için</span><span class="sxs-lookup"><span data-stu-id="b2a62-107">For Classic VMs</span></span>

<span data-ttu-id="b2a62-108">Ağ arabirimi sıfırlamak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b2a62-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="b2a62-109">[Azure Portal]( https://ms.portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="b2a62-110">Seçin **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="b2a62-111">Etkilenen sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="b2a62-112">Seçin **IP adreslerini**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="b2a62-113">Varsa **özel IP atama** değil **statik**, kendisine değiştirme **statik**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="b2a62-114">Değişiklik **IP adresi** alt ağda kullanılabilir başka bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2a62-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="b2a62-115">Kaydet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-115">Select Save.</span></span>
8.  <span data-ttu-id="b2a62-116">Sanal makine sisteme yeni NIC başlatmak için yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="b2a62-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="b2a62-117">İçin RDP makinenize deneyin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-117">Try to RDP to your machine.</span></span> <span data-ttu-id="b2a62-118">İsterseniz başarılı olursa, özgün durumuna geri özel IP adresi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a62-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="b2a62-119">Aksi takdirde, tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a62-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="b2a62-120">Kaynak grubu modelde dağıtılan VM'ler için</span><span class="sxs-lookup"><span data-stu-id="b2a62-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="b2a62-121">[Azure Portal]( https://ms.portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="b2a62-122">Etkilenen sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="b2a62-123">Seçin **ağ arabirimleri**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="b2a62-124">Makine ile ilişkili ağ arabirimi seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="b2a62-125">Seçin **IP yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="b2a62-126">IP adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-126">Select the IP.</span></span> 
7.  <span data-ttu-id="b2a62-127">Varsa **özel IP atama** değil **statik**, kendisine değiştirme **statik**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="b2a62-128">Değişiklik **IP adresi** alt ağda kullanılabilir başka bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b2a62-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="b2a62-129">Sanal makine sisteme yeni NIC başlatmak için yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="b2a62-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="b2a62-130">İçin RDP makinenize deneyin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-130">Try to RDP to your machine.</span></span> <span data-ttu-id="b2a62-131">İsterseniz başarılı olursa, özgün durumuna geri özel IP adresi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a62-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="b2a62-132">Aksi takdirde, tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a62-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="b2a62-133">Kullanılamayan NICs Sil</span><span class="sxs-lookup"><span data-stu-id="b2a62-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="b2a62-134">Makine için Uzak Masaüstü için sonra olası sorunu önlemek için eski NIC'ler silmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b2a62-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="b2a62-135">Aygıt Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="b2a62-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="b2a62-136">Seçin **Görünüm** > **gizli aygıtları göster**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="b2a62-137">Seçin **ağ bağdaştırıcıları**.</span><span class="sxs-lookup"><span data-stu-id="b2a62-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="b2a62-138">"Microsoft Hyper-V ağ bağdaştırıcısı" adlı bağdaştırıcıları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="b2a62-139">Gri renkte bağdaştırıcıyı kullanılamaz görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2a62-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="b2a62-140">Bağdaştırıcıyı sağ tıklatın ve ardından Kaldır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b2a62-140">Right-click the adapter and then select Uninstall.</span></span>

    ![NIC görüntüsü](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="b2a62-142">Yalnızca "Microsoft Hyper-V ağ bağdaştırıcısı" adına sahip kullanılabilir bağdaştırıcıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b2a62-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="b2a62-143">Gizli bir bağdaştırıcı kaldırırsanız, ek sorunlara neden.</span><span class="sxs-lookup"><span data-stu-id="b2a62-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="b2a62-144">Şimdi tüm kullanılamaz bağdaştırıcısı sisteminizden temizlenmesini.</span><span class="sxs-lookup"><span data-stu-id="b2a62-144">Now all unavailable adapter should be cleared out from your system.</span></span>