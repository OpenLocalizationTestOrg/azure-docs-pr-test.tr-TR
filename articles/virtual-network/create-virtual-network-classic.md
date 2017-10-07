---
title: "bir Azure sanal ağ (Klasik) birden fazla alt ağı aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir sanal ağ (Klasik) Azure içinde birden fazla alt ağı."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="d0b7a-103">Bir sanal ağ ile birden fazla alt ağ (Klasik) oluşturun</span><span class="sxs-lookup"><span data-stu-id="d0b7a-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0b7a-104">Azure sahip iki [farklı dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) oluşturmak ve kaynaklarla çalışmak için: Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="d0b7a-105">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d0b7a-106">Microsoft önerir hello üzerinden çoğu yeni sanal ağlar oluşturma [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="d0b7a-107">Bu öğreticide, nasıl toocreate olan bir temel Azure sanal ağ (Klasik) ayrı ortak ve özel alt ağlar hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="d0b7a-108">Sanal makineler ve bir alt ağdaki bulut Hizmetleri gibi Azure kaynaklarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="d0b7a-109">Sanal ağları (Klasik) oluşturulan kaynakları birbirleriyle ve diğer ağ bağlantılı tooa sanal ağınızdaki kaynaklara ile iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="d0b7a-110">Tüm hakkında daha fazla bilgi [sanal ağ](virtual-network-manage-network.md) ve [alt](virtual-network-manage-subnet.md) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="d0b7a-111">Sanal ağları (Klasik), Azure tarafından hemen silinir, bir [abonelik devre dışı](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="d0b7a-112">Sanal ağları (Klasik) kaynakları hello sanal ağında mevcut bağımsız olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="d0b7a-113">Daha sonra hello aboneliği yeniden etkinleştirirseniz, hello sanal ağında varolan kaynakları yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="d0b7a-114">Hello kullanarak bir sanal ağ (Klasik) oluşturabilirsiniz [Azure portal](#portal), hello [Azure komut satırı arabirimi (CLI) 1.0](#azure-cli), veya [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="d0b7a-115">Portal</span><span class="sxs-lookup"><span data-stu-id="d0b7a-115">Portal</span></span>

1. <span data-ttu-id="d0b7a-116">Bir Internet tarayıcısında toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d0b7a-117">Kullanarak oturum açın, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="d0b7a-118">Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="d0b7a-119">Tıklatın **+ yeni** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="d0b7a-120">Girin *sanal ağ* hello içinde **arama hello Market** kutusunu hello hello üstündeki **yeni** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="d0b7a-121">Tıklatın **sanal ağ** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="d0b7a-122">Seçin **Klasik** hello içinde **dağıtım modeli seçin** hello kutusunda **sanal ağ** görünür, ardından dikey **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="d0b7a-123">Değerler üzerinde hello aşağıdaki hello girin **sanal ağ oluştur (Klasik)** dikey ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="d0b7a-124">Ayar</span><span class="sxs-lookup"><span data-stu-id="d0b7a-124">Setting</span></span>|<span data-ttu-id="d0b7a-125">Değer</span><span class="sxs-lookup"><span data-stu-id="d0b7a-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="d0b7a-126">Ad</span><span class="sxs-lookup"><span data-stu-id="d0b7a-126">Name</span></span>|<span data-ttu-id="d0b7a-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="d0b7a-127">myVnet</span></span>|
    |<span data-ttu-id="d0b7a-128">Adres alanı</span><span class="sxs-lookup"><span data-stu-id="d0b7a-128">Address space</span></span>|<span data-ttu-id="d0b7a-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d0b7a-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="d0b7a-130">Alt ağ adı</span><span class="sxs-lookup"><span data-stu-id="d0b7a-130">Subnet name</span></span>|<span data-ttu-id="d0b7a-131">Genel</span><span class="sxs-lookup"><span data-stu-id="d0b7a-131">Public</span></span>|
    |<span data-ttu-id="d0b7a-132">Alt ağ adres aralığı</span><span class="sxs-lookup"><span data-stu-id="d0b7a-132">Subnet address range</span></span>|<span data-ttu-id="d0b7a-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d0b7a-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="d0b7a-134">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="d0b7a-134">Resource group</span></span>|<span data-ttu-id="d0b7a-135">Bırakın **Yeni Oluştur** seçili yazıp enter **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="d0b7a-136">Abonelik ve konum</span><span class="sxs-lookup"><span data-stu-id="d0b7a-136">Subscription and location</span></span>|<span data-ttu-id="d0b7a-137">Abonelik ve konum seçin.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-137">Select your subscription and location.</span></span>

    <span data-ttu-id="d0b7a-138">Yeni tooAzure değilseniz, hakkında daha fazla bilgi [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (tooas ya da *bölgeleri*).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="d0b7a-139">Bir sanal ağ oluşturduğunuzda, hello Portalı'nda, yalnızca bir alt ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="d0b7a-140">Merhaba sanal ağ oluşturduktan sonra Bu öğreticide, ikinci bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="d0b7a-141">Daha sonra Internet'ten erişilebilen kaynaklara hello oluşturacağınız **ortak** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="d0b7a-142">Merhaba hello Internet üzerinden erişilebilir olmayan kaynakları de oluşturabilir **özel** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="d0b7a-143">toocreate ikinci alt ağ Merhaba, girin **myVnet** hello içinde **arama kaynakları** hello sayfanın üst kısmındaki hello kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="d0b7a-144">Tıklatın **myVnet** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="d0b7a-145">Tıklatın **alt ağlar** (Merhaba içinde **ayarları** bölüm) hello üzerinde **sanal ağ oluştur (Klasik)** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="d0b7a-146">Tıklatın **+ Ekle** hello üzerinde **myVnet - alt ağlar** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="d0b7a-147">Girin **özel** için **adı** hello üzerinde **alt ağ Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="d0b7a-148">Girin **10.0.1.0/24** için **adres aralığı**.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="d0b7a-149">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-149">Click **OK**.</span></span>
8. <span data-ttu-id="d0b7a-150">Merhaba üzerinde **myVnet - alt ağlar** dikey penceresinde hello görebilirsiniz **ortak** ve **özel** oluşturduğunuz alt ağlar.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="d0b7a-151">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi yok, oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="d0b7a-152">Tıklatın **genel bakış** hello üzerinde **myVnet** dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="d0b7a-153">Merhaba tıklatın **silmek** hello simgesine **myVnet** dikey.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="d0b7a-154">tooconfirm hello silme tıklatın **Evet** hello içinde **Delete sanal ağ** kutusu.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="d0b7a-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d0b7a-155">Azure CLI</span></span>

1. <span data-ttu-id="d0b7a-156">Seçebilir ya da [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), veya hello Azure bulut Kabuk içinde hello CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="d0b7a-157">Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="d0b7a-158">Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="d0b7a-159">CLI komutları için tooget Yardım yazın `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="d0b7a-160">CLI oturumunda, aşağıdaki hello komutuyla tooAzure kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="d0b7a-161">Tıklatırsanız **deneyin** hello kutuya bir bulut Kabuğu'nu açar.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="d0b7a-162">Komutu aşağıdaki hello girmeden tooyour Azure aboneliği kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="d0b7a-163">CLI Hizmet Yönetimi modundaysa tooensure hello hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="d0b7a-164">Bir sanal ağ ile özel bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="d0b7a-165">Ortak bir alt ağ içinde hello sanal ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="d0b7a-166">Merhaba sanal ağ ve alt ağları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="d0b7a-167">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="d0b7a-168">Hello CLI kullanarak bir kaynak grubu toocreate bir sanal ağ (Klasik) belirtemezsiniz olsa, Azure hello sanal ağ içinde adlı bir kaynak grubu oluşturur. *varsayılan ağ*.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="d0b7a-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0b7a-169">PowerShell</span></span>

1. <span data-ttu-id="d0b7a-170">Merhaba PowerShell Hello en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) modülü.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="d0b7a-171">Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="d0b7a-172">Bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="d0b7a-173">PowerShell'de tooAzure içinde hello girerek oturum `Add-AzureAccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="d0b7a-174">Değiştirme hello şu yol ve dosya adı, uygun şekilde sonra varolan ağ yapılandırma dosyanızı aktarın:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="d0b7a-175">toocreate ortak ve özel alt ağları, sanal ağ kullanan herhangi bir metin düzenleyicisi tooadd hello **VirtualNetworkSite** toohello ağ yapılandırma dosyası izleyen öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="d0b7a-176">Gözden geçirme hello tam [ağ yapılandırma dosyası şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="d0b7a-177">Merhaba ağ yapılandırma dosyasını içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="d0b7a-178">Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="d0b7a-179">Yalnızca hello önceki sanal ağ ekleme ve yok değiştirdiğinizde veya var olan tüm sanal ağları aboneliğinizden kaldırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="d0b7a-180">Merhaba sanal ağ ve alt ağları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="d0b7a-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="d0b7a-181">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz toodelete hello kaynakları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="d0b7a-182">toodelete hello sanal ağ, tam adımlar 4-6 yeniden, bu zaman kaldırma hello **VirtualNetworkSite** 5. adımda eklediğiniz öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="d0b7a-183">Azure PowerShell kullanarak bir kaynak grubu toocreate bir sanal ağ (Klasik) belirtemezsiniz olsa adlı bir kaynak grubunda hello sanal ağ oluşturur *varsayılan ağ*.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="d0b7a-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0b7a-184">Next steps</span></span>

- <span data-ttu-id="d0b7a-185">tüm sanal ağ ve alt ağ ayarları hakkında toolearn bkz [sanal ağlarını yönetmeleri](virtual-network-manage-network.md) ve [sanal ağ alt ağlarını yönetin](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="d0b7a-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="d0b7a-186">Sanal ağlar ve alt ağlar, bir üretim ortamında toomeet farklı gereksinimleri kullanmaya yönelik çeşitli seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="d0b7a-187">gelen ve giden toofilter alt ağ trafiği, oluşturma ve uygulama [ağ güvenlik grubu](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="d0b7a-188">Oluşturma bir [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine ve tooan varolan sanal ağa bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="d0b7a-189">tooconnect iki sanal ağlar olarak Merhaba aynı Azure konumunda, oluşturma bir [sanal ağ eşlemesi](create-peering-different-deployment-models.md) hello sanal ağlar arasında.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="d0b7a-190">Bir sanal ağ (Resource Manager) tooa sanal ağ (Klasik) eşi, ancak iki sanal ağ (Klasik) arasında eşleme oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="d0b7a-191">Kullanarak Hello sanal ağ tooan şirket ağına bağlanan bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hattı.</span><span class="sxs-lookup"><span data-stu-id="d0b7a-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
