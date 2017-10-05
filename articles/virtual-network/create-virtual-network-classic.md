---
title: "Bir Azure sanal ağı ile birden fazla alt ağ (Klasik) oluşturun | Microsoft Docs"
description: "Bir sanal ağ (Klasik) Azure içinde birden fazla alt ağı oluşturmayı öğrenin."
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
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="47456-103">Bir sanal ağ ile birden fazla alt ağ (Klasik) oluşturun</span><span class="sxs-lookup"><span data-stu-id="47456-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47456-104">Azure sahip iki [farklı dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) oluşturmak ve kaynaklarla çalışmak için: Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="47456-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="47456-105">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="47456-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="47456-106">Microsoft önerir üzerinden çoğu yeni sanal ağlar oluşturma [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="47456-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="47456-107">Bu öğreticide, ayrı ortak ve özel alt ağları olan bir temel Azure sanal ağ (Klasik) oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="47456-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="47456-108">Sanal makineler ve bir alt ağdaki bulut Hizmetleri gibi Azure kaynaklarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47456-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="47456-109">Sanal ağları (Klasik) oluşturulan kaynakları birbirleriyle ve diğer ağlarda, sanal bir ağa bağlı kaynaklar ile iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="47456-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="47456-110">Tüm hakkında daha fazla bilgi [sanal ağ](virtual-network-manage-network.md) ve [alt](virtual-network-manage-subnet.md) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="47456-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="47456-111">Sanal ağları (Klasik), Azure tarafından hemen silinir, bir [abonelik devre dışı](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="47456-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="47456-112">Sanal ağları (Klasik) kaynakları sanal ağında mevcut bağımsız olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="47456-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="47456-113">Daha sonra aboneliği yeniden etkinleştirirseniz, sanal ağ içinde var olan kaynakların yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47456-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="47456-114">Bir sanal ağ (Klasik) kullanarak oluşturabileceğiniz [Azure portal](#portal), [Azure komut satırı arabirimi (CLI) 1.0](#azure-cli), veya [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="47456-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="47456-115">Portal</span><span class="sxs-lookup"><span data-stu-id="47456-115">Portal</span></span>

1. <span data-ttu-id="47456-116">Bir Internet tarayıcısında Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47456-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="47456-117">Kullanarak oturum açın, [Azure hesabı](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="47456-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="47456-118">Bir Azure hesabınız yoksa, oturum açabileceğiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="47456-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="47456-119">Tıklatın **+ yeni** Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="47456-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="47456-120">Girin *sanal ağ* içinde **Market arama** kutusunun üstündeki **yeni** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="47456-121">Tıklatın **sanal ağ** arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="47456-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="47456-122">Seçin **Klasik** içinde **dağıtım modeli seçin** kutusunda **sanal ağ** görünür, ardından dikey **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="47456-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="47456-123">Aşağıdaki değerleri girin **sanal ağ oluştur (Klasik)** dikey ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="47456-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="47456-124">Ayar</span><span class="sxs-lookup"><span data-stu-id="47456-124">Setting</span></span>|<span data-ttu-id="47456-125">Değer</span><span class="sxs-lookup"><span data-stu-id="47456-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="47456-126">Ad</span><span class="sxs-lookup"><span data-stu-id="47456-126">Name</span></span>|<span data-ttu-id="47456-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="47456-127">myVnet</span></span>|
    |<span data-ttu-id="47456-128">Adres alanı</span><span class="sxs-lookup"><span data-stu-id="47456-128">Address space</span></span>|<span data-ttu-id="47456-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="47456-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="47456-130">Alt ağ adı</span><span class="sxs-lookup"><span data-stu-id="47456-130">Subnet name</span></span>|<span data-ttu-id="47456-131">Genel</span><span class="sxs-lookup"><span data-stu-id="47456-131">Public</span></span>|
    |<span data-ttu-id="47456-132">Alt ağ adres aralığı</span><span class="sxs-lookup"><span data-stu-id="47456-132">Subnet address range</span></span>|<span data-ttu-id="47456-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="47456-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="47456-134">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="47456-134">Resource group</span></span>|<span data-ttu-id="47456-135">Bırakın **Yeni Oluştur** seçili yazıp enter **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="47456-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="47456-136">Abonelik ve konum</span><span class="sxs-lookup"><span data-stu-id="47456-136">Subscription and location</span></span>|<span data-ttu-id="47456-137">Abonelik ve konum seçin.</span><span class="sxs-lookup"><span data-stu-id="47456-137">Select your subscription and location.</span></span>

    <span data-ttu-id="47456-138">Hakkında daha fazla bilgi için Azure yeniyseniz, [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (olarak da adlandırılan *bölgeleri*).</span><span class="sxs-lookup"><span data-stu-id="47456-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="47456-139">Bir sanal ağ oluşturduğunuzda, portalda, yalnızca bir alt ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47456-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="47456-140">Sanal ağ oluşturduktan sonra Bu öğreticide, ikinci bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47456-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="47456-141">Daha sonra Internet'ten erişilebilen kaynaklara oluşturabilirsiniz **ortak** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="47456-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="47456-142">Internet'ten erişilemez kaynakları de oluşturabilir **özel** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="47456-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="47456-143">İkinci alt ağ oluşturmak için girin **myVnet** içinde **arama kaynakları** sayfanın üst kısmındaki kutusu.</span><span class="sxs-lookup"><span data-stu-id="47456-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="47456-144">Tıklatın **myVnet** arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="47456-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="47456-145">Tıklatın **alt ağlar** (içinde **ayarları** bölüm) üzerinde **sanal ağ oluştur (Klasik)** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="47456-146">Tıklatın **+ Ekle** üzerinde **myVnet - alt ağlar** görünür dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="47456-147">Girin **özel** için **adı** üzerinde **alt ağ Ekle** dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="47456-148">Girin **10.0.1.0/24** için **adres aralığı**.</span><span class="sxs-lookup"><span data-stu-id="47456-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="47456-149">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="47456-149">Click **OK**.</span></span>
8. <span data-ttu-id="47456-150">Üzerinde **myVnet - alt ağlar** dikey penceresinde görebilirsiniz **ortak** ve **özel** oluşturduğunuz alt ağlar.</span><span class="sxs-lookup"><span data-stu-id="47456-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="47456-151">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi yok, oluşturduğunuz kaynakları silmek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47456-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="47456-152">Tıklatın **genel bakış** üzerinde **myVnet** dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="47456-153">Tıklatın **silmek** simgesine **myVnet** dikey.</span><span class="sxs-lookup"><span data-stu-id="47456-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="47456-154">Silme işlemini onaylamak için tıklatın **Evet** içinde **Delete sanal ağ** kutusu.</span><span class="sxs-lookup"><span data-stu-id="47456-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="47456-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="47456-155">Azure CLI</span></span>

1. <span data-ttu-id="47456-156">Seçebilir ya da [Azure CLI'yi yükleme ve yapılandırma](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), veya Azure bulut kabuktan CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="47456-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="47456-157">Azure Cloud Shell doğrudan Azure portalının içinde çalıştırabileceğiniz ücretsiz bir Bash kabuğudur.</span><span class="sxs-lookup"><span data-stu-id="47456-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="47456-158">Azure CLI, kabuğa önceden yüklenmiştir ve kabuk, hesabınızla birlikte kullanılacak şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="47456-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="47456-159">CLI komutları için Yardım almak için yazın `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="47456-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="47456-160">CLI oturumunda, Azure için aşağıdaki komutu ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="47456-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="47456-161">Tıklatırsanız **deneyin** kutuya bir bulut Kabuğu'nu açar.</span><span class="sxs-lookup"><span data-stu-id="47456-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="47456-162">Azure aboneliğiniz için aşağıdaki komutu girmeden oturum:</span><span class="sxs-lookup"><span data-stu-id="47456-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="47456-163">CLI Hizmet Yönetimi modunda olduğundan emin olmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="47456-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="47456-164">Bir sanal ağ ile özel bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="47456-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="47456-165">Sanal ağ içindeki ortak bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="47456-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="47456-166">Sanal ağ ve alt ağları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="47456-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="47456-167">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz kaynakları silmek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47456-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="47456-168">CLI kullanarak bir sanal ağ (Klasik) oluşturmak için bir kaynak grubu belirtemezsiniz olsa, Azure sanal ağ içinde adlı bir kaynak grubu oluşturur. *varsayılan ağ*.</span><span class="sxs-lookup"><span data-stu-id="47456-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="47456-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47456-169">PowerShell</span></span>

1. <span data-ttu-id="47456-170">PowerShell'ın en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) modülü.</span><span class="sxs-lookup"><span data-stu-id="47456-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="47456-171">Azure PowerShell'i kullanmaya yeni başladıysanız [Azure PowerShell'e genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) sayfasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="47456-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="47456-172">Bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="47456-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="47456-173">PowerShell'de `Add-AzureAccount` komutunu girerek Azure oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="47456-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="47456-174">Aşağıdaki yolunu ve dosya adı, uygun şekilde değiştirme sonra mevcut ağ yapılandırma dosyasını dışarı aktar:</span><span class="sxs-lookup"><span data-stu-id="47456-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="47456-175">Ortak ve özel alt ağları ile bir sanal ağ oluşturmak için eklemek için herhangi bir metin düzenleyicisi kullanın **VirtualNetworkSite** ağ yapılandırma dosyasına aşağıdaki öğesi.</span><span class="sxs-lookup"><span data-stu-id="47456-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

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

    <span data-ttu-id="47456-176">Tam gözden [ağ yapılandırma dosyası şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="47456-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="47456-177">Ağ yapılandırma dosyasını içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="47456-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="47456-178">Değiştirilen ağ yapılandırma dosyasını içeri varolan sanal ağlar (aboneliğinizde Klasik) yapılan değişiklikler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="47456-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="47456-179">Yalnızca önceki sanal ağ ekleyin ve verme değiştirir veya var olan tüm sanal ağları aboneliğinizden kaldırırsanız, emin olun.</span><span class="sxs-lookup"><span data-stu-id="47456-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="47456-180">Sanal ağ ve alt ağları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="47456-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="47456-181">**İsteğe bağlı**: Bu öğreticiyi tamamladığınızda, böylece kullanım ücretlerine tabi olmayan oluşturduğunuz kaynakları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47456-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="47456-182">Sanal ağı silmek için 4-6 yeniden, bu zaman kaldırma adımları tamamlayın **VirtualNetworkSite** 5. adımda eklediğiniz öğesi.</span><span class="sxs-lookup"><span data-stu-id="47456-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="47456-183">PowerShell kullanarak bir sanal ağ (Klasik) oluşturmak için bir kaynak grubu belirtemezsiniz olsa, Azure sanal ağ içinde adlı bir kaynak grubu oluşturur. *varsayılan ağ*.</span><span class="sxs-lookup"><span data-stu-id="47456-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="47456-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47456-184">Next steps</span></span>

- <span data-ttu-id="47456-185">Tüm sanal ağ ve alt ağ ayarları hakkında bilgi edinmek için bkz: [sanal ağlarını yönetmeleri](virtual-network-manage-network.md) ve [sanal ağ alt ağlarını yönetin](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="47456-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="47456-186">Sanal ağlar ve alt ağları farklı gereksinimlerini karşılamak için bir üretim ortamında kullanmadan yönelik çeşitli seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="47456-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="47456-187">Alt ağa gelen ve giden trafiği filtrelemek, oluşturmak ve uygulamak için [ağ güvenlik grubu](virtual-networks-nsg.md) alt ağlara.</span><span class="sxs-lookup"><span data-stu-id="47456-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="47456-188">Oluşturma bir [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal makine ve mevcut bir sanal ağa bağlayın.</span><span class="sxs-lookup"><span data-stu-id="47456-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="47456-189">İki sanal ağ ile aynı konumda Azure bağlanmak için oluşturmanız bir [sanal ağ eşlemesi](create-peering-different-deployment-models.md) sanal ağlar arasında.</span><span class="sxs-lookup"><span data-stu-id="47456-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="47456-190">Sanal ağ (Klasik) için bir sanal ağ (Resource Manager) eşi, ancak eşlemesi iki sanal ağ arasında (Klasik) oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="47456-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="47456-191">Sanal ağ kullanarak bir şirket ağına bağlanan bir [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) veya [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hattı.</span><span class="sxs-lookup"><span data-stu-id="47456-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
