---
title: "Bir sanal ağ geçidini silmek: PowerShell: Azure Klasik | Microsoft Docs"
description: "Klasik dağıtım modelinde PowerShell kullanarak bir sanal ağ geçidini silin."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="b1b65-103">PowerShell (Klasik) kullanarak bir sanal ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="b1b65-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1b65-104">Resource Manager - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="b1b65-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="b1b65-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b65-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="b1b65-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b65-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="b1b65-107">Bu makalede PowerShell kullanarak bir VPN ağ geçidi Klasik dağıtım modelinde silmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b1b65-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="b1b65-108">Sanal ağ geçidi silindikten sonra artık kullanmadığınız öğeleri kaldırmak için ağ yapılandırma dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1b65-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="b1b65-109"><a name="connect"></a>1. adım: Azure'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="b1b65-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="b1b65-110">1. En son PowerShell cmdlet'lerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1b65-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="b1b65-111">Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü yükleyip yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="b1b65-112">Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b1b65-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="b1b65-113">2. Azure hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="b1b65-114">PowerShell konsolunuzu yükseltilmiş haklarla açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="b1b65-115">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="b1b65-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="b1b65-116"><a name="export"></a>2. adım: Dışarı aktarma ve ağ yapılandırma dosyasını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="b1b65-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="b1b65-117">Bilgisayarınızda bir dizin oluşturun ve sonra ağ yapılandırma dosyasını dizine aktarın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="b1b65-118">Bu dosya geçerli yapılandırma bilgilerini hem görünümüne ve ağ yapılandırmasını değiştirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="b1b65-119">Bu örnekte, ağ yapılandırma dosyası C:\AzureNet dizinine aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b1b65-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="b1b65-120">Dosyayı bir metin düzenleyicisiyle açın ve klasik sanal ağınızı adını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="b1b65-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="b1b65-121">Azure portalında VNet oluşturduğunuzda, Azure kullandığı tam adı portalda görünür değil.</span><span class="sxs-lookup"><span data-stu-id="b1b65-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="b1b65-122">Örneğin, 'ClassicVNet1' Azure portalında adlandırılması görünür bir VNet olabilir kadar uzun ad ağ yapılandırma dosyasında.</span><span class="sxs-lookup"><span data-stu-id="b1b65-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="b1b65-123">Adı şöyle görünebilir: 'Grup ClassicRG1 ClassicVNet1'.</span><span class="sxs-lookup"><span data-stu-id="b1b65-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="b1b65-124">Sanal ağ adları olarak listelenen **' VirtualNetworkSite adı ='**.</span><span class="sxs-lookup"><span data-stu-id="b1b65-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="b1b65-125">Adları PowerShell cmdlet'lerini çalıştırırken ağ yapılandırma dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="b1b65-126"><a name="delete"></a>3. adım: sanal ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="b1b65-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="b1b65-127">Bir sanal ağ geçidini sildiğinizde, ağ geçidi üzerinden vnet'e tüm bağlantılar kesilir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="b1b65-128">Vnet'e bağlı P2S istemcileriniz varsa, uyarı olmadan kesilir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="b1b65-129">Bu örnek, sanal ağ geçidini siler.</span><span class="sxs-lookup"><span data-stu-id="b1b65-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="b1b65-130">Ağ yapılandırma dosyasından sanal ağın tam adı kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b1b65-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="b1b65-131">Başarılı olursa, dönüş gösterir:</span><span class="sxs-lookup"><span data-stu-id="b1b65-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="b1b65-132"><a name="modify"></a>4. adım: ağ yapılandırma dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="b1b65-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="b1b65-133">Bir sanal ağ geçidini sildiğinizde, cmdlet ağ yapılandırma dosyası değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="b1b65-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="b1b65-134">Artık kullanılmayan öğeleri kaldırmak için dosyasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="b1b65-135">Aşağıdaki bölümlerde indirdiğiniz ağ yapılandırma dosyasını değiştirme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b1b65-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="b1b65-136"><a name="lnsref"></a>Yerel ağ sitesi başvuruları</span><span class="sxs-lookup"><span data-stu-id="b1b65-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="b1b65-137">Site başvuru bilgileri kaldırmak için yapılandırma değişiklikleri yapmanız **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="b1b65-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="b1b65-138">Bir yerel site başvuru Tetikleyicileri tünel silmek için Azure kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="b1b65-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="b1b65-139">Oluşturduğunuz yapılandırmasına bağlı olarak, olmayabilir bir **LocalNetworkSiteRef** listelenir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="b1b65-140">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b1b65-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="b1b65-141"><a name="lns"></a>Yerel ağ sitesi</span><span class="sxs-lookup"><span data-stu-id="b1b65-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="b1b65-142">Artık kullanmadığınız yerel siteleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="b1b65-143">Oluşturduğunuz yapılandırmasına bağlı olarak, yoksa olası bir **LocalNetworkSite** listelenir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="b1b65-144">Bu örnekte, yalnızca Site3 kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="b1b65-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="b1b65-145"><a name="clientaddresss"></a>İstemci adres havuzu</span><span class="sxs-lookup"><span data-stu-id="b1b65-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="b1b65-146">P2S bağlantısı Vnet'iniz olsaydı olacaktır bir **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="b1b65-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="b1b65-147">Sildiğiniz sanal ağ geçidi karşılık gelen istemci adres havuzları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b1b65-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="b1b65-148">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b1b65-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="b1b65-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="b1b65-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="b1b65-150">Silme **GatewaySubnet** Vnet'e karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="b1b65-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="b1b65-151">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b1b65-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="b1b65-152"><a name="upload"></a>5. adım: ağ yapılandırma dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="b1b65-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="b1b65-153">Yaptığınız değişiklikleri kaydedin ve ağ yapılandırma dosyasını Azure'a yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1b65-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="b1b65-154">Ortamınız için gerektiği gibi dosya yolu değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b1b65-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="b1b65-155">Başarılı olursa, dönüş bu örneğe benzer bir şey gösterir:</span><span class="sxs-lookup"><span data-stu-id="b1b65-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded