---
title: "aaaConfigure özel IP adresleri VM'ler (Klasik) - Azure portalı | Microsoft Docs"
description: "Tooconfigure özel IP adresleri kullanarak sanal makineleri (Klasik) için Azure portalını nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="d1fca-103">Hello Azure portal kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d1fca-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d1fca-104">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d1fca-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="d1fca-105">Ayrıca [hello Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="d1fca-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="d1fca-106">Merhaba örnek adımları zaten oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="d1fca-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="d1fca-107">Bu belgede gösterildiği toorun hello adımları istiyorsanız, ilk derleme açıklandığı hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="d1fca-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="d1fca-108">Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken</span><span class="sxs-lookup"><span data-stu-id="d1fca-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="d1fca-109">toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d1fca-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d1fca-110">Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="d1fca-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="d1fca-111">Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, o hello fark **dağıtımmodeliseçin** listesinde zaten gösterir **Klasik**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="d1fca-113">Merhaba, **VM Oluştur** dikey penceresinde hello VM toobe oluşturulan hello adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası hello.</span><span class="sxs-lookup"><span data-stu-id="d1fca-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="d1fca-115">Tıklatın **isteğe bağlı yapılandırma** > **ağ** > **sanal ağ**ve ardından **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="d1fca-116">Varsa **TestVNet** kullanılamıyor hello kullandığınızdan emin olun *Orta ABD* konumu ve bu makalenin hello başında açıklanan hello test ortamı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d1fca-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="d1fca-118">Merhaba, **ağ** dikey penceresinde seçili yapma emin hello alt ağıdır *ön uç*, ardından **IP adreslerini**altında **IP adresi ataması** tıklatın **statik**ve ardından girin *192.168.1.101* için **IP adresi** aşağıda görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="d1fca-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="d1fca-120">' I tıklatın **Tamam** hello içinde **IP adresleri** dikey penceresinde'ye tıklayın **Tamam** hello içinde **ağ** dikey penceresinde ve tıklatın **Tamam**hello içinde **isteğe bağlı yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="d1fca-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="d1fca-121">Merhaba, **VM Oluştur** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="d1fca-122">Panonuzda görüntülenen bildirim hello döşeme aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="d1fca-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="d1fca-124">Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi</span><span class="sxs-lookup"><span data-stu-id="d1fca-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="d1fca-125">VM yukarıdaki hello adımları ile oluşturulan tooview hello statik özel IP adresi bilgileri hello hello adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="d1fca-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="d1fca-126">Hello Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri (Klasik)** > **DNS01**  >   **Tüm ayarları** > **IP adreslerini** ve IP adresi ve IP adresi ataması aşağıda görüldüğü gibi hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d1fca-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="d1fca-128">Nasıl tooremove bir statik özel IP adresi bir sanal makineden</span><span class="sxs-lookup"><span data-stu-id="d1fca-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="d1fca-129">tooremove hello statik özel IP adresinden yukarıda, VM oluşturduğunuz hello hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d1fca-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="d1fca-130">Hello gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** toohello sağ **IP adresi ataması**, ardından **kaydetmek**ve ardından tıklatın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="d1fca-132">Nasıl tooadd statik özel IP adresi VM varolan tooan</span><span class="sxs-lookup"><span data-stu-id="d1fca-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="d1fca-133">tooadd bir statik özel IP adresi toohello hello yukarıdaki adımları kullanarak oluşturulan VM hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d1fca-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="d1fca-134">Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** sağında toohello **IP adresi ataması**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="d1fca-135">Tür *192.168.1.101* için **IP adresi**, ardından **kaydetmek**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d1fca-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1fca-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1fca-136">Next steps</span></span>
* <span data-ttu-id="d1fca-137">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="d1fca-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d1fca-138">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="d1fca-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d1fca-139">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1fca-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

