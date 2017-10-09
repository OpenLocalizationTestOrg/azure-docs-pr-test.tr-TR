---
title: "Windows işlem kaynakları Azure Resource Manager şablonları ile aaaDeploying | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="b0fad-103">Windows sanal makineleri için Azure Resource Manager şablonları ile uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="b0fad-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="b0fad-104">Bir Azure Resource Manager dağıtım geliştirirken, hesaplama gereksinimleri eşlenen toobe tooAzure kaynaklarını ve Hizmetleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="b0fad-105">Bir uygulama birkaç http uç noktaları, bir veritabanı ve bir veri hizmeti önbelleğe alma oluşuyorsa, hello bu bileşenlerin her birini barındıran Azure kaynaklarını gerekiyor ayrıştıran toobe.</span><span class="sxs-lookup"><span data-stu-id="b0fad-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="b0fad-106">Örneğin, Merhaba örnek müzik deposu uygulaması sanal bir makinede barındırılan bir web uygulaması ve Azure SQL veritabanı'nda barındırılan bir SQL veritabanı içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="b0fad-107">Bu belge hello müzik deposu işlem kaynakları hello örnek Azure Resource Manager şablonunda nasıl yapılandırılacağını ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="b0fad-108">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="b0fad-109">Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b0fad-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="b0fad-110">Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="b0fad-110">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="b0fad-111">Sanal Makine</span><span class="sxs-lookup"><span data-stu-id="b0fad-111">Virtual Machine</span></span>
<span data-ttu-id="b0fad-112">Merhaba müzik deposu uygulama burada müşteriler göz atın ve Müzik satın alma bir web uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="b0fad-113">Bu örnek için web uygulamalarını barındırabilir birkaç Azure Hizmetleri varken bir sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="b0fad-114">Merhaba örnek müzik deposu şablonu kullanarak bir sanal makinenin dağıtıldığı, bir web sunucusu yüklemek ve hello müzik deposu Web sitesine yüklenir ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="b0fad-115">Bu makalede Hello artırmak amacıyla için yalnızca hello sanal makine dağıtımı ayrıntılı olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="b0fad-116">Merhaba web sunucusu ve Merhaba uygulaması Hello yapılandırmasını bir sonraki makalesinde ayrıntılı olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="b0fad-117">Bir sanal makine hello Visual Studio yeni kaynak Ekleme Sihirbazı, ya geçerli bir JSON hello Dağıtım şablonuna ekleyerek kullanarak tooa şablonunu eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="b0fad-118">Bir sanal makineyi dağıtırken bazı ilgili kaynaklar de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="b0fad-119">Visual Studio toocreate hello şablonu kullanıyorsanız, bu kaynakları sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b0fad-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="b0fad-120">El ile Merhaba şablon oluşturma, bu kaynakları eklenen ve yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="b0fad-121">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="b0fad-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

<span data-ttu-id="b0fad-122">Uygulama dağıtıldıktan sonra hello sanal makine özellikleri hello Azure portal görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Sanal Makine](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="b0fad-124">Depolama Hesabı</span><span class="sxs-lookup"><span data-stu-id="b0fad-124">Storage Account</span></span>
<span data-ttu-id="b0fad-125">Depolama hesapları, çok sayıda depolama seçenekleri ve özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="b0fad-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="b0fad-126">Azure sanal makineleri Hello bağlamının hello hello sanal makinenin sanal sabit sürücüler ve ek diskleri bir depolama hesabı tutar.</span><span class="sxs-lookup"><span data-stu-id="b0fad-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="b0fad-127">Merhaba müzik deposu örnek bir depolama hesabı toohold hello sanal sabit sürücü, her bir sanal makinenin hello dağıtımda içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="b0fad-128">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [depolama hesabı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="b0fad-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="b0fad-129">İlişkilendirme hello Resource Manager şablonu bildirimi hello sanal makinenin içindeki bir sanal makine ile bir depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="b0fad-130">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine ve depolama hesabı ilişkisi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="b0fad-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="b0fad-131">Dağıtımdan sonra hello depolama hesabı hello Azure portal görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Depolama Hesabı](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="b0fad-133">Merhaba depolama hesabı blob kapsayıcıya tıklatarak, hello hello şablonla dağıtılan her bir sanal makine için sanal sabit disk dosyası görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Sanal sabit disk sürücüler](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="b0fad-135">Azure Storage hakkında daha fazla bilgi için bkz: [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="b0fad-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="b0fad-136">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="b0fad-136">Virtual Network</span></span>
<span data-ttu-id="b0fad-137">Bir sanal makinenin diğer sanal makineler ve Azure kaynakları ile Merhaba özelliği toocommunicate gibi iç ağ gerektiriyorsa, bir Azure sanal ağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="b0fad-138">Bir sanal ağ hello sanal makine üzerinden erişilebilir yapmaz Internet hello.</span><span class="sxs-lookup"><span data-stu-id="b0fad-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="b0fad-139">Genel bağlantı daha sonra bu dizide ayrıntılı bir genel IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="b0fad-140">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal ağ ve alt ağları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="b0fad-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="b0fad-141">Hello Azure portal hello sanal ağ görüntü aşağıdaki hello gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="b0fad-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="b0fad-142">Merhaba şablonla dağıtılan tüm sanal makineleri ekli toohello sanal ağ olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b0fad-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Sanal Ağ](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="b0fad-144">Ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="b0fad-144">Network Interface</span></span>
 <span data-ttu-id="b0fad-145">Bir ağ arabirimi bir sanal makine tooa sanal ağ, hello sanal ağ içinde tanımlanan daha açık belirtmek gerekirse tooa alt ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="b0fad-146">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [ağ arabirimi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="b0fad-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="b0fad-147">Her sanal makine kaynağı bir ağ profili içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="b0fad-148">Hello ağ arabirimi, bu profilde hello sanal makine ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="b0fad-149">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine ağ profili](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="b0fad-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="b0fad-150">Azure portal Hello görüntü aşağıdaki hello gibi hello ağ arabirimi arar.</span><span class="sxs-lookup"><span data-stu-id="b0fad-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="b0fad-151">Merhaba iç IP adresi ve hello sanal makine ilişkilendirme hello ağ arabirimi kaynakta görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Ağ arabirimi](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="b0fad-153">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure sanal ağ belgeleri](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="b0fad-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="b0fad-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b0fad-154">Azure SQL Database</span></span>
<span data-ttu-id="b0fad-155">Ayrıca tooa sanal makine hello müzik deposu Web sitesi, bir Azure SQL veritabanı barındırma dağıtılan toohost hello müzik deposu veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="b0fad-156">Azure SQL veritabanı burada kullanarak hello avantajı, ikinci bir kümede sanal makinelerin gerekli değildir ve ölçek ve kullanılabilirlik hello hizmetinde yerleşik olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="b0fad-157">Bir Azure SQL veritabanı hello Visual Studio yeni kaynak Ekleme Sihirbazı, veya bir şablona geçerli JSON ekleyerek kullanılarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="b0fad-158">Merhaba SQL Server Kaynak, bir kullanıcı adı ve hello SQL örneğinde yönetici hakları verilen parola içerir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="b0fad-159">Ayrıca, bir SQL güvenlik duvarı kaynak eklenir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="b0fad-160">Varsayılan olarak, Azure üzerinde barındırılan hello SQL örneğiyle mümkün tooconnect uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="b0fad-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="b0fad-161">tooallow dış uygulama böyle bir SQL Server Management studio tooconnect toohello SQL örneği, yapılandırılmış toobe hello güvenlik duvarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0fad-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="b0fad-162">Merhaba varsayılan yapılandırma hello müzik deposu demo Hello artırmak amacıyla için uygundur.</span><span class="sxs-lookup"><span data-stu-id="b0fad-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="b0fad-163">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="b0fad-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="b0fad-164">Merhaba SQL server ve hello Azure portal görülen MusicStore veritabanı görünümü.</span><span class="sxs-lookup"><span data-stu-id="b0fad-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="b0fad-166">Azure SQL veritabanı dağıtma hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı belgeleri](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="b0fad-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="b0fad-167">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="b0fad-167">Next step</span></span>
<hr>

[<span data-ttu-id="b0fad-168">2. adım - Azure Resource Manager şablonları güvenlik ve erişim</span><span class="sxs-lookup"><span data-stu-id="b0fad-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

