---
title: "aaaConfigure özel IP adresleri VM'ler - Azure portalı | Microsoft Docs"
description: "Tooconfigure özel IP adresleri kullanarak sanal makineleri için Azure portalını nasıl hello öğrenin."
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
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="1fa88-103">Hello Azure portal kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1fa88-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fa88-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1fa88-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="1fa88-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fa88-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="1fa88-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1fa88-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="1fa88-107">Azure portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="1fa88-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="1fa88-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="1fa88-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="1fa88-109">Azure CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="1fa88-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1fa88-110">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="1fa88-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1fa88-111">Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1fa88-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="1fa88-112">Merhaba örnek adımları zaten oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="1fa88-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="1fa88-113">Bu belgede gösterildiği toorun hello adımları istiyorsanız, ilk derleme açıklandığı hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1fa88-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="1fa88-114">Nasıl toocreate statik özel IP test etmek için bir VM adresleri</span><span class="sxs-lookup"><span data-stu-id="1fa88-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="1fa88-115">Hello Azure portal kullanarak bir VM hello Resource Manager dağıtım modunda hello oluşturulması sırasında özel bir statik IP adresi ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="1fa88-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="1fa88-116">Merhaba VM önce oluşturmanız gerekir, kendi özel IP toobe tehn statik olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1fa88-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="1fa88-117">toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet*, hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1fa88-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="1fa88-118">Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="1fa88-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="1fa88-119">Tıklatın **yeni** > **işlem** > **Windows Server 2012 R2 Datacenter**, o hello fark **dağıtımmodeliseçin** listesinde zaten gösterir **Resource Manager**ve ardından **oluşturma**hello aşağıdaki çizimde görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="1fa88-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="1fa88-121">Merhaba, **Temelleri** dikey penceresinde hello VM toobe oluşturulan hello adını girin (*DNS01* bizim senaryoda), yerel yönetici hesabı ve parolası, hello aşağıdaki çizimde görüldüğü gibi hello.</span><span class="sxs-lookup"><span data-stu-id="1fa88-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="1fa88-123">Hello emin olun **konumu** seçili *Orta ABD*, ardından **Varolanı seç** altında **kaynak grubu**, ardından**Kaynak grubu** yeniden, ardından *TestRG*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Temel Bilgiler dikey penceresi](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="1fa88-125">Merhaba, **bir boyutu seçin** dikey penceresinde, select **A1 standart**ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="1fa88-127">İçinde **ayarları** dikey penceresinde, aşağıdaki özelliklere yapma emin hello ayarlanır aşağıdaki hello değerleri ile ayarlanır ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="1fa88-128">-**Depolama hesabı**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="1fa88-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="1fa88-129">**Ağ**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="1fa88-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="1fa88-130">**Alt ağ**: *ön uç*</span><span class="sxs-lookup"><span data-stu-id="1fa88-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Bir boyut dikey penceresi seçin](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="1fa88-132">Merhaba, **Özet** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="1fa88-133">Panonuzda görüntülenen bildirim hello döşeme aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="1fa88-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="1fa88-135">Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi</span><span class="sxs-lookup"><span data-stu-id="1fa88-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="1fa88-136">VM yukarıdaki hello adımları ile oluşturulan tooview hello statik özel IP adresi bilgileri hello hello adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="1fa88-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="1fa88-137">Hello Azure Azure Portalı'ndan tıklatın **TÜMÜNE Gözat** > **sanal makineleri** > **DNS01** > **tüm ayarları** > **ağ arabirimleri** ve listelenen hello yalnızca ağ arabirimi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1fa88-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="1fa88-139">Merhaba, **ağ arabirimi** dikey penceresinde tıklatın **tüm ayarları** > **IP adreslerini** ve bildirim hello **atama** ve **IP adresi** değerleri.</span><span class="sxs-lookup"><span data-stu-id="1fa88-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![VM döşeme dağıtma](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="1fa88-141">Nasıl tooadd statik özel IP adresi VM varolan tooan</span><span class="sxs-lookup"><span data-stu-id="1fa88-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="1fa88-142">tooadd bir statik özel IP adresi toohello hello yukarıdaki adımları kullanarak oluşturulan VM hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1fa88-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="1fa88-143">Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **statik** altında **atama**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="1fa88-144">Tür *192.168.1.101* için **IP adresi**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Azure Portalı'nda VM oluşturma](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="1fa88-146">' I tıklattıktan sonra IF **kaydetmek** hello atama hala çok ayarlandığına dikkat edin**dinamik**, yazdığınız başlangıç IP adresi zaten kullanımda olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1fa88-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="1fa88-147">Farklı bir IP adresi deneyin.</span><span class="sxs-lookup"><span data-stu-id="1fa88-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="1fa88-148">Nasıl tooremove bir statik özel IP adresi bir sanal makineden</span><span class="sxs-lookup"><span data-stu-id="1fa88-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="1fa88-149">tooremove hello statik özel IP adresinden yukarıda, VM oluşturduğunuz hello adım aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="1fa88-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="1fa88-150">Merhaba gelen **IP adreslerini** , yukarıda gösterilen dikey tıklayın **dinamik** altında **atama**ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1fa88-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fa88-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1fa88-151">Next steps</span></span>
* <span data-ttu-id="1fa88-152">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="1fa88-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1fa88-153">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="1fa88-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1fa88-154">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fa88-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

