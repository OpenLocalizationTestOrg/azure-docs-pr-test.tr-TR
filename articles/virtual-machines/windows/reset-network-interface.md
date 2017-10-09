---
title: "aaaHow tooreset ağ arabirimi için Azure Windows VM | Microsoft Docs"
description: "Nasıl tooreset ağ arabirimi için Azure Windows VM gösterir"
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="b033d-103">Nasıl tooreset ağ arabirimi için Azure Windows VM</span><span class="sxs-lookup"><span data-stu-id="b033d-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b033d-104">Merhaba varsayılan ağ arabirim (NIC) devre dışı bıraktıktan sonra tooMicrosoft Azure Windows sanal makine (VM) bağlanılamıyor veya el ile statik bir IP hello NIC için ayarlar</span><span class="sxs-lookup"><span data-stu-id="b033d-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="b033d-105">Bu makalede nasıl tooreset hello ağ arabirimi Azure Windows hangi hello uzak bağlantı sorunu gidermek için VM, gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b033d-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="b033d-106">Ağ arabirimi Sıfırla</span><span class="sxs-lookup"><span data-stu-id="b033d-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="b033d-107">Klasik VM'ler için</span><span class="sxs-lookup"><span data-stu-id="b033d-107">For Classic VMs</span></span>

<span data-ttu-id="b033d-108">tooreset ağ arabirimi, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b033d-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="b033d-109">Toohello Git [Azure portal]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b033d-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="b033d-110">Seçin **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="b033d-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="b033d-111">Sanal makine seçin hello etkilenen.</span><span class="sxs-lookup"><span data-stu-id="b033d-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="b033d-112">Seçin **IP adreslerini**.</span><span class="sxs-lookup"><span data-stu-id="b033d-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="b033d-113">Merhaba, **özel IP atama** değil **statik**, çok değiştirme**statik**.</span><span class="sxs-lookup"><span data-stu-id="b033d-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="b033d-114">Değişiklik hello **IP adresi** hello alt kullanılabilir tooanother IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b033d-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="b033d-115">Kaydet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b033d-115">Select Save.</span></span>
8.  <span data-ttu-id="b033d-116">Merhaba sanal makine tooinitialize hello yeni NIC toohello sistem yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b033d-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="b033d-117">TooRDP tooyour makine deneyin.</span><span class="sxs-lookup"><span data-stu-id="b033d-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="b033d-118">İsterseniz başarılı olursa, hello özel IP adresi geri toohello özgün değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b033d-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="b033d-119">Aksi takdirde, tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b033d-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="b033d-120">Kaynak grubu modelde dağıtılan VM'ler için</span><span class="sxs-lookup"><span data-stu-id="b033d-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="b033d-121">Toohello Git [Azure portal]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b033d-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="b033d-122">Sanal makine seçin hello etkilenen.</span><span class="sxs-lookup"><span data-stu-id="b033d-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="b033d-123">Seçin **ağ arabirimleri**.</span><span class="sxs-lookup"><span data-stu-id="b033d-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="b033d-124">Ağ arabirimi, makineyle ilişkili hello seçin</span><span class="sxs-lookup"><span data-stu-id="b033d-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="b033d-125">Seçin **IP yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="b033d-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="b033d-126">Başlangıç IP adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="b033d-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="b033d-127">Merhaba, **özel IP atama** değil **statik**, çok değiştirme**statik**.</span><span class="sxs-lookup"><span data-stu-id="b033d-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="b033d-128">Değişiklik hello **IP adresi** hello alt kullanılabilir tooanother IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b033d-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="b033d-129">Merhaba sanal makine tooinitialize hello yeni NIC toohello sistem yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b033d-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="b033d-130">TooRDP tooyour makine deneyin.</span><span class="sxs-lookup"><span data-stu-id="b033d-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="b033d-131">İsterseniz başarılı olursa, hello özel IP adresi geri toohello özgün değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b033d-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="b033d-132">Aksi takdirde, tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b033d-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="b033d-133">Silme kullanılamayan NICs hello</span><span class="sxs-lookup"><span data-stu-id="b033d-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="b033d-134">Uzak Masaüstü toohello makine yapabilecekleriniz sonra hello eski NIC'ler tooavoid hello olası sorunu silmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b033d-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="b033d-135">Aygıt Yöneticisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="b033d-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="b033d-136">Seçin **Görünüm** > **gizli aygıtları göster**.</span><span class="sxs-lookup"><span data-stu-id="b033d-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="b033d-137">Seçin **ağ bağdaştırıcıları**.</span><span class="sxs-lookup"><span data-stu-id="b033d-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="b033d-138">"Microsoft Hyper-V ağ bağdaştırıcısı" adlı hello bağdaştırıcıları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b033d-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="b033d-139">Gri renkte bağdaştırıcıyı kullanılamaz görebilirsiniz. Merhaba bağdaştırıcısına sağ tıklayın ve ardından Kaldır'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b033d-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![Merhaba NIC Hello görüntüsü](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="b033d-141">Yalnızca hello adı "Microsoft Hyper-V ağ bağdaştırıcısı" Merhaba kullanılamaz bağdaştırıcıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b033d-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="b033d-142">Diğer gizli bağdaştırıcıları hello birini kaldırırsanız, ek sorunlar neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b033d-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="b033d-143">Şimdi tüm kullanılamaz bağdaştırıcısı sisteminizden temizlenmesini.</span><span class="sxs-lookup"><span data-stu-id="b033d-143">Now all unavailable adapter should be cleared out from your system.</span></span>