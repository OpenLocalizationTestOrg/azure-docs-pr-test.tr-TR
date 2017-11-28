---
title: "Azure Resource Manager şablonları ile Linux işlem kaynaklarını dağıtma | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c3f9f98079e0c89d1231f9c3e62e82c33ad18236
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="e1bb1-103">Linux VM'ler için Azure Resource Manager şablonları ile uygulama mimarisi</span><span class="sxs-lookup"><span data-stu-id="e1bb1-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="e1bb1-104">Bir Azure Resource Manager dağıtım geliştirirken, hesaplama gereksinimleri Azure kaynaklarını ve Hizmetleri için eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="e1bb1-105">Bir uygulama birkaç http uç noktaları, bir veritabanı ve bir veri hizmeti önbelleğe alma oluşuyorsa, Azure kaynaklarını barındıran her bu bileşenlerin ayrıştıran gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="e1bb1-106">Örneğin, örnek müzik deposu uygulaması sanal bir makinede barındırılan bir web uygulaması ve Azure SQL veritabanı'nda barındırılan bir SQL veritabanı içerir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="e1bb1-107">Bu belge, müzik deposu işlem kaynakları örnek Azure Resource Manager şablonunda nasıl yapılandırılacağını ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="e1bb1-108">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="e1bb1-109">En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="e1bb1-110">Tam veri şablonunun burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-110">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="e1bb1-111">Sanal Makine</span><span class="sxs-lookup"><span data-stu-id="e1bb1-111">Virtual Machine</span></span>
<span data-ttu-id="e1bb1-112">Müzik deposu uygulama burada müşteriler göz atın ve Müzik satın alma bir web uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="e1bb1-113">Bu örnek için web uygulamalarını barındırabilir birkaç Azure Hizmetleri varken bir sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="e1bb1-114">Örnek Müzik deposu şablonu kullanarak bir sanal makinenin dağıtıldığı, bir web sunucusu yüklemek ve müzik deposu Web sitesine yüklenir ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="e1bb1-115">Bu makalede amacıyla, yalnızca sanal makine dağıtımı ayrıntılı olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="e1bb1-116">Web sunucusu ve uygulama yapılandırmasını bir sonraki makalesinde ayrıntılı olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="e1bb1-117">Bir sanal makine, Visual Studio yeni kaynak Ekleme Sihirbazı'nı kullanarak bir şablonla ya da geçerli JSON Dağıtım şablonuna ekleyerek eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="e1bb1-118">Bir sanal makineyi dağıtırken bazı ilgili kaynaklar de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="e1bb1-119">Visual Studio şablonu oluşturmak için kullanıyorsanız, bu kaynakları sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="e1bb1-120">El ile şablon oluşturmak, bu kaynakları eklenen ve yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="e1bb1-121">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
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

<span data-ttu-id="e1bb1-122">Uygulama dağıtıldıktan sonra sanal makine özelliklerini Azure portalında görülebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Sanal Makine](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="e1bb1-124">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="e1bb1-124">Storage Account</span></span>
<span data-ttu-id="e1bb1-125">Depolama hesapları, çok sayıda depolama seçenekleri ve özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="e1bb1-126">Azure sanal makineleri bağlam için bir depolama hesabı olan ek veri disklerinin ile sanal makine ve sanal sabit disk sürücüler tutar.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="e1bb1-127">Müzik deposu örnek dağıtımda, her bir sanal makinenin sanal sabit sürücü tutmak için bir depolama hesabını içerir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="e1bb1-128">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [depolama hesabı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

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

<span data-ttu-id="e1bb1-129">Resource Manager şablonu bildirimi sanal makinenin içindeki bir sanal makine ile ilişkilendirilecek bir depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="e1bb1-130">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine ve depolama hesabı ilişkisi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

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

<span data-ttu-id="e1bb1-131">Dağıtım sonrasında, Azure Portal'da depolama hesabı görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Depolama hesabı](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="e1bb1-133">Depolama hesabı blob kapsayıcısı tıklatarak, şablonla dağıtılan her bir sanal makine için sanal sabit disk dosyası görülebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Sanal sabit disk sürücüler](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="e1bb1-135">Azure Storage hakkında daha fazla bilgi için bkz: [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="e1bb1-136">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="e1bb1-136">Virtual Network</span></span>
<span data-ttu-id="e1bb1-137">Bir sanal makinenin diğer sanal makineler ve Azure kaynakları ile iletişim kurmasına olanak gibi iç ağ gerektiriyorsa, bir Azure sanal ağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="e1bb1-138">Bir sanal ağ sanal makine internet üzerinden erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="e1bb1-139">Genel bağlantı daha sonra bu dizide ayrıntılı bir genel IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="e1bb1-140">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal ağ ve alt ağları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

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

<span data-ttu-id="e1bb1-141">Azure portalından, sanal ağ aşağıdaki görüntü gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="e1bb1-142">Şablonla dağıtılan tüm sanal makineleri sanal ağa takılı olduğunu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Sanal Ağ](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="e1bb1-144">Ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="e1bb1-144">Network Interface</span></span>
 <span data-ttu-id="e1bb1-145">Bir ağ arabirimi bir sanal makinenin sanal ağ içinde tanımlanan daha belirgin bir alt ağ için sanal bir ağa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="e1bb1-146">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [ağ arabirimi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="e1bb1-147">Her sanal makine kaynağı bir ağ profili içerir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="e1bb1-148">Bu profildeki sanal makineyle ilişkilendirilmiş Ağ arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="e1bb1-149">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine ağ profili](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="e1bb1-150">Azure portalından, ağ arabiriminin aşağıdaki görüntü gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="e1bb1-151">İç IP adresi ve sanal makine ilişkilendirme ağ arabirimi kaynakta görülebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Ağ arabirimi](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="e1bb1-153">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure sanal ağ belgeleri](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="e1bb1-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e1bb1-154">Azure SQL Database</span></span>
<span data-ttu-id="e1bb1-155">Bir müzik deposu Web sitesi barındırma ek olarak sanal makine, müzik deposu veritabanını barındırmak için bir Azure SQL veritabanı dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="e1bb1-156">Azure SQL veritabanı burada kullanmanın avantajı, ikinci bir kümede sanal makinelerin gerekli değildir ve ölçek ve kullanılabilirlik hizmete yerleşik ' dir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="e1bb1-157">Visual Studio yeni kaynak Ekleme Sihirbazı, veya bir şablona geçerli JSON ekleyerek kullanarak Azure SQL veritabanına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="e1bb1-158">SQL Server Kaynak, bir kullanıcı adı ve SQL örneğinde yönetici hakları verilen parola içerir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="e1bb1-159">Ayrıca, bir SQL güvenlik duvarı kaynak eklenir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="e1bb1-160">Varsayılan olarak, Azure üzerinde barındırılan uygulamalar SQL örneğine bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="e1bb1-161">Dış uygulama izin vermek için bir tür SQL Server Management studio güvenlik duvarını SQL örneğine bağlanmak için yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="e1bb1-162">Müzik deposu tanıtım amacıyla varsayılan yapılandırmayı uygundur.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="e1bb1-163">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="e1bb1-164">SQL server ve Azure portalında göründüğü gibi MusicStore veritabanı görünümü.</span><span class="sxs-lookup"><span data-stu-id="e1bb1-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="e1bb1-166">Azure SQL veritabanı dağıtma hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı belgeleri](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="e1bb1-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="e1bb1-167">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e1bb1-167">Next step</span></span>
<hr>

[<span data-ttu-id="e1bb1-168">2. adım - Azure Resource Manager şablonları güvenlik ve erişim</span><span class="sxs-lookup"><span data-stu-id="e1bb1-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

