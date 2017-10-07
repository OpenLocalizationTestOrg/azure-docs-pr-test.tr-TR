---
title: "bir Azure sanal ağ (Klasik) - ağ yapılandırma dosyası aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl toocreate ve dışarı aktarma, değiştirme ve bir ağ yapılandırma dosyasını içeri sanal ağları (Klasik) değiştirin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="314ba-103">Bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="314ba-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="314ba-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="314ba-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="314ba-105">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="314ba-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="314ba-106">Microsoft, en yeni dağıtımların hello Resource Manager dağıtım modeli kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="314ba-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="314ba-107">Oluşturun ve bir ağ yapılandırma dosyası hello Azure komut satırı arabirimi (CLI) 1.0 veya Azure PowerShell kullanarak bir sanal ağ (Klasik) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="314ba-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="314ba-108">Oluşturma veya bir ağ yapılandırma dosyası kullanarak hello Azure Resource Manager dağıtım modeli aracılığıyla bir sanal ağ değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="314ba-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="314ba-109">Hello Azure portal toocreate kullanın veya bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik) değiştirme, kullanabilirsiniz ancak Azure portal toocreate olmadan bir ağ yapılandırma dosyası kullanarak bir sanal ağ (Klasik), hello olamaz.</span><span class="sxs-lookup"><span data-stu-id="314ba-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="314ba-110">Oluşturma ve bir ağ yapılandırma dosyası ile bir sanal ağ (Klasik) yapılandırma dışarı aktarma, değiştirme ve hello dosya alma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="314ba-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="314ba-111"><a name="export"></a>Bir ağ yapılandırma dosyası dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="314ba-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="314ba-112">PowerShell veya hello Azure CLI tooexport bir ağ yapılandırma dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="314ba-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="314ba-113">Hello Azure CLI bir json dosyası verirken PowerShell bir XML dosyasına dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="314ba-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="314ba-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="314ba-114">PowerShell</span></span>
 
1. <span data-ttu-id="314ba-115">[Azure PowerShell'i yükleyin ve tooAzure içinde oturum](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="314ba-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="314ba-116">Değiştirme hello dizin (ve onu var olduğundan emin olun) ve hello filename aşağıdaki komut istenen sonra çalışma hello komutu tooexport hello ağ yapılandırma dosyası olarak:</span><span class="sxs-lookup"><span data-stu-id="314ba-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="314ba-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="314ba-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="314ba-118">[Hello Azure CLI 1.0 yüklemek](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="314ba-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="314ba-119">Azure CLI 1.0 komut isteminden adımları kalan hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="314ba-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="314ba-120">İçinde tooAzure hello girerek oturum `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="314ba-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="314ba-121">Merhaba girerek asm modunda olduğunuzdan emin olun `azure config mode asm` komutu.</span><span class="sxs-lookup"><span data-stu-id="314ba-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="314ba-122">Değiştirme hello dizin (ve onu var olduğundan emin olun) ve hello filename aşağıdaki komut istenen sonra çalışma hello komutu tooexport hello ağ yapılandırma dosyası olarak:</span><span class="sxs-lookup"><span data-stu-id="314ba-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="314ba-123">Oluşturma veya bir ağ yapılandırma dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="314ba-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="314ba-124">Bir ağ yapılandırma XML dosyasını (PowerShell kullanırken) veya bir json dosyası (hello Azure CLI kullanırken) dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="314ba-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="314ba-125">Merhaba dosyasını bir metin veya XML/json düzenleyicide düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="314ba-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="314ba-126">Merhaba [ağ yapılandırma dosyası şeması ayarları](https://msdn.microsoft.com/library/azure/jj157100.aspx) makale tüm ayarları için ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="314ba-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="314ba-127">Hello ayarları ek açıklaması için bkz: [sanal ağlar ve ayarları görüntüle](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="314ba-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="314ba-128">Merhaba değişiklikleri toohello dosya yapın:</span><span class="sxs-lookup"><span data-stu-id="314ba-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="314ba-129">Uymalıdır hello şema veya içeri aktarma hello ağ yapılandırma dosyası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="314ba-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="314ba-130">Aboneliğiniz için var olan tüm ağ ayarlarını üzerine yazma, bu nedenle değişiklikler yaparken dikkatli.</span><span class="sxs-lookup"><span data-stu-id="314ba-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="314ba-131">Örneğin, izleyin hello örnek ağ yapılandırması dosyaları başvuru.</span><span class="sxs-lookup"><span data-stu-id="314ba-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="314ba-132">Merhaba özgün dosya bulunan iki söyleyin **VirtualNetworkSite** örnekleri ve değişti, hello örneklerde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="314ba-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="314ba-133">Merhaba dosyasını içe aktardığınızda, Azure hello için sanal ağ hello siler **VirtualNetworkSite** hello dosyasında kaldırdığınız örneği.</span><span class="sxs-lookup"><span data-stu-id="314ba-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="314ba-134">Hiçbir kaynak yoktu hello sanal ağında Basitleştirilmiş bu senaryo varsayar gibi olsaydı, hello sanal ağ silinemedi ve hello alma başarısız olurdu.</span><span class="sxs-lookup"><span data-stu-id="314ba-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="314ba-135">Azure göz önünde bulundurur bir şey sahip bir alt tooit olarak dağıtılan **kullanımda**.</span><span class="sxs-lookup"><span data-stu-id="314ba-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="314ba-136">Bir alt ağ kullanımdayken değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="314ba-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="314ba-137">Ağ yapılandırma dosyasında alt ağ bilgilerini değiştirmeden önce değiştirilen değil toohello alt tooa farklı alt dağıtmış olan herhangi bir şey taşıyın.</span><span class="sxs-lookup"><span data-stu-id="314ba-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="314ba-138">Bkz: [bir VM veya rol örneğine tooa farklı alt taşıma](virtual-networks-move-vm-role-to-subnet.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="314ba-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="314ba-139">PowerShell ile kullanılmak üzere XML örneği</span><span class="sxs-lookup"><span data-stu-id="314ba-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="314ba-140">Merhaba aşağıdaki örnek ağ yapılandırma dosyası adlı bir sanal ağ oluşturur *myVirtualNetwork* bir adres alanı ile *10.0.0.0/16* hello içinde *Doğu ABD* Azure bölge.</span><span class="sxs-lookup"><span data-stu-id="314ba-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="314ba-141">Merhaba sanal ağ içeren bir alt ağ *mySubnet* bir adres öneki ile *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="314ba-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="314ba-142">Merhaba ağ yapılandırma dosyasını dışarı aktardığınız hiç içerik içeriyorsa, hello XML hello önceki örnekte kopyalayın ve yeni bir dosyaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="314ba-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="314ba-143">Örnek JSON hello Azure CLI 1.0 ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="314ba-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="314ba-144">Merhaba aşağıdaki örnek ağ yapılandırma dosyası adlı bir sanal ağ oluşturur *myVirtualNetwork* bir adres alanı ile *10.0.0.0/16* hello içinde *Doğu ABD* Azure bölge.</span><span class="sxs-lookup"><span data-stu-id="314ba-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="314ba-145">Merhaba sanal ağ içeren bir alt ağ *mySubnet* bir adres öneki ile *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="314ba-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="314ba-146">Merhaba ağ yapılandırma dosyasını dışarı aktardığınız hiç içerik içeriyorsa, hello json hello önceki örnekte kopyalayın ve yeni bir dosyaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="314ba-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="314ba-147"><a name="import"></a>Ağ yapılandırma dosyasını içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="314ba-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="314ba-148">PowerShell veya hello Azure CLI tooimport bir ağ yapılandırma dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="314ba-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="314ba-149">PowerShell Hello Azure CLI bir json dosyası alırken bir XML dosyası içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="314ba-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="314ba-150">Merhaba alma başarısız olursa, o hello dosya hello ile uyumlu onaylayın [ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="314ba-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="314ba-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="314ba-151">PowerShell</span></span>
 
1. <span data-ttu-id="314ba-152">[Azure PowerShell'i yükleyin ve tooAzure içinde oturum](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="314ba-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="314ba-153">Başlangıç dizini ve gerektiğinde komutu aşağıdaki hello dosya değiştirin, ardından hello komutu tooimport hello ağ yapılandırma dosyasını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="314ba-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="314ba-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="314ba-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="314ba-155">[Hello Azure CLI 1.0 yüklemek](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="314ba-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="314ba-156">Azure CLI 1.0 komut isteminden adımları kalan hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="314ba-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="314ba-157">İçinde tooAzure hello girerek oturum `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="314ba-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="314ba-158">Merhaba girerek asm modunda olduğunuzdan emin olun `azure config mode asm` komutu.</span><span class="sxs-lookup"><span data-stu-id="314ba-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="314ba-159">Başlangıç dizini ve gerektiğinde komutu aşağıdaki hello dosya değiştirin, ardından hello komutu tooimport hello ağ yapılandırma dosyasını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="314ba-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
