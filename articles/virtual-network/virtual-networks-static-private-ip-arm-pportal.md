---
title: "Özel IP adresleri VM'ler - Azure portal için yapılandırma | Microsoft Docs"
description: "Azure Portalı'nı kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="bfa66-103">Azure Portalı'nı kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bfa66-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfa66-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="bfa66-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="bfa66-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfa66-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="bfa66-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bfa66-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="bfa66-107">Azure portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="bfa66-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="bfa66-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="bfa66-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="bfa66-109">Azure CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="bfa66-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bfa66-110">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bfa66-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="bfa66-111">Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bfa66-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="bfa66-112">Aşağıdaki örnek adımları zaten oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="bfa66-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="bfa66-113">Bu belgede gösterildiği adımları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bfa66-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="bfa66-114">Özel statik IP adresleri test etmek için bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bfa66-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="bfa66-115">Azure portalı kullanarak bir VM Resource Manager dağıtım modunda oluşturulması sırasında özel bir statik IP adresi ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="bfa66-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="bfa66-116">VM önce oluşturmanız gerekir, statik olarak kendi özel IP tehn ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bfa66-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="bfa66-117">Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet*, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="bfa66-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="bfa66-118">Tarayıcıdan http://portal.azure.com adresine gidin ve gerekiyorsa Azure hesabınıza giriş yapın.</span><span class="sxs-lookup"><span data-stu-id="bfa66-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="bfa66-119">Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, dikkat **dağıtımmodeliseçin** listesinde zaten gösterir **Resource Manager**ve ardından **oluşturma**, aşağıdaki şekilde görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="bfa66-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="bfa66-121">İçinde **Temelleri** dikey penceresinde oluşturulacak VM adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası, aşağıdaki şekilde görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="bfa66-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="bfa66-123">Emin olun **konumu** seçili *Orta ABD*, ardından **Varolanı seç** altında **kaynak grubu**, ardından**Kaynak grubu** yeniden, ardından *TestRG*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="bfa66-125">İçinde **bir boyutu seçin** dikey penceresinde, select **A1 standart**ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="bfa66-127">İçinde **ayarları** dikey penceresinde, aşağıdaki özellikleri ayarlanmadığından emin olun değerleriyle ayarlanır ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="bfa66-128">-**Depolama hesabı**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="bfa66-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="bfa66-129">**Ağ**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="bfa66-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="bfa66-130">**Alt ağ**: *ön uç*</span><span class="sxs-lookup"><span data-stu-id="bfa66-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="bfa66-132">İçinde **Özet** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="bfa66-133">Panonuzda görüntülenen döşemenin aşağıdaki dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bfa66-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="bfa66-135">Bir VM için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="bfa66-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="bfa66-136">Yukarıdaki adımları ile oluşturulan sanal makine için statik özel IP adresi bilgilerini görüntülemek için aşağıdaki adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="bfa66-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="bfa66-137">Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri** > **DNS01** > **tüm ayarlar**   >  **Ağ arabirimleri** ve listelenen yalnızca ağ arabirimi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bfa66-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="bfa66-139">İçinde **ağ arabirimi** dikey penceresinde tıklatın **tüm ayarları** > **IP adreslerini** ve fark **atama** ve  **IP adresi** değerleri.</span><span class="sxs-lookup"><span data-stu-id="bfa66-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="bfa66-141">Mevcut bir VM'yi özel bir statik IP adresi ekleme</span><span class="sxs-lookup"><span data-stu-id="bfa66-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="bfa66-142">Yukarıdaki adımları kullanılarak oluşturulan VM için özel bir statik IP adresi eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="bfa66-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="bfa66-143">Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** altında **atama**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="bfa66-144">Tür *192.168.1.101* için **IP adresi**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="bfa66-146">' I tıklattıktan sonra IF **kaydetmek** atama hala ayarlanır fark **dinamik**, yazdığınız IP adresi zaten kullanımda olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="bfa66-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="bfa66-147">Farklı bir IP adresi deneyin.</span><span class="sxs-lookup"><span data-stu-id="bfa66-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="bfa66-148">Özel bir statik IP adresi bir VM'den kaldırma</span><span class="sxs-lookup"><span data-stu-id="bfa66-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="bfa66-149">Özel statik IP adresi yukarıda oluşturduğunuz sanal makineden kaldırmak için aşağıdaki adımı tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="bfa66-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="bfa66-150">Gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** altında **atama**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bfa66-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa66-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bfa66-151">Next steps</span></span>
* <span data-ttu-id="bfa66-152">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="bfa66-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bfa66-153">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="bfa66-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bfa66-154">Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfa66-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

