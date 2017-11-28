---
title: "Özel IP adreslerini VM'ler için (Klasik) - Azure portalında yapılandırın | Microsoft Docs"
description: "Azure Portalı'nı kullanarak sanal makineleri (Klasik) için özel IP adresleri yapılandırmayı öğrenin."
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
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="25ca0-103">Azure Portalı'nı kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="25ca0-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="25ca0-104">Bu makale, klasik dağıtım modelini kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="25ca0-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="25ca0-105">Ayrıca [Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="25ca0-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="25ca0-106">Aşağıdaki örnek adımları zaten oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="25ca0-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="25ca0-107">Bu belgede gösterildiği adımları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="25ca0-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="25ca0-108">Bir VM oluşturulurken özel bir statik IP adresi belirtme</span><span class="sxs-lookup"><span data-stu-id="25ca0-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="25ca0-109">Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="25ca0-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="25ca0-110">Tarayıcıdan http://portal.azure.com adresine gidin ve gerekiyorsa Azure hesabınıza giriş yapın.</span><span class="sxs-lookup"><span data-stu-id="25ca0-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="25ca0-111">Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, dikkat **dağıtımmodeliseçin** listesinde zaten gösterir **Klasik**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="25ca0-113">İçinde **VM Oluştur** dikey penceresinde oluşturulacak VM adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası.</span><span class="sxs-lookup"><span data-stu-id="25ca0-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="25ca0-115">Tıklatın **isteğe bağlı yapılandırma** > **ağ** > **sanal ağ**ve ardından **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="25ca0-116">Varsa **TestVNet** kullanılamıyor kullandığınızdan emin olun *Orta ABD* konumu ve bu makalenin başında açıklanan test ortamında oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="25ca0-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="25ca0-118">İçinde **ağ** dikey penceresinde seçili alt ağı olduğundan emin olun *ön uç*, ardından **IP adreslerini**altında **IP adresi ataması**tıklatın **statik**ve ardından girin *192.168.1.101* için **IP adresi** aşağıda görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="25ca0-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="25ca0-120">' I tıklatın **Tamam** içinde **IP adreslerini** dikey penceresinde, ardından **Tamam** içinde **ağ** dikey penceresinde'ye tıklayın **Tamam** içinde **isteğe bağlı yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="25ca0-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="25ca0-121">İçinde **VM Oluştur** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="25ca0-122">Panonuzda görüntülenen döşemenin aşağıdaki dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="25ca0-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="25ca0-124">Bir VM için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="25ca0-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="25ca0-125">Yukarıdaki adımları ile oluşturulan sanal makine için statik özel IP adresi bilgilerini görüntülemek için aşağıdaki adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="25ca0-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="25ca0-126">Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri (Klasik)** > **DNS01** > **tüm ayarları** > **IP adreslerini** ve IP adresi ve IP adresi ataması aşağıda görüldüğü gibi dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="25ca0-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="25ca0-128">Özel bir statik IP adresi bir VM'den kaldırma</span><span class="sxs-lookup"><span data-stu-id="25ca0-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="25ca0-129">Özel statik IP adresi yukarıda oluşturduğunuz sanal makineden kaldırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="25ca0-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="25ca0-130">Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** sağındaki **IP adresi ataması**, ardından **kaydetmek**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="25ca0-132">Mevcut bir VM'yi özel bir statik IP adresi ekleme</span><span class="sxs-lookup"><span data-stu-id="25ca0-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="25ca0-133">Yukarıdaki adımları kullanılarak oluşturulan VM için özel bir statik IP adresi eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="25ca0-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="25ca0-134">Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** sağındaki **IP adresi ataması**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="25ca0-135">Tür *192.168.1.101* için **IP adresi**, ardından **kaydetmek**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="25ca0-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25ca0-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25ca0-136">Next steps</span></span>
* <span data-ttu-id="25ca0-137">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="25ca0-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="25ca0-138">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="25ca0-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="25ca0-139">Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="25ca0-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

