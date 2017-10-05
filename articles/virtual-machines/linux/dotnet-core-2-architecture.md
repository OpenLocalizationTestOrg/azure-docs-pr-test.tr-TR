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
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>Linux VM'ler için Azure Resource Manager şablonları ile uygulama mimarisi

Bir Azure Resource Manager dağıtım geliştirirken, hesaplama gereksinimleri Azure kaynaklarını ve Hizmetleri için eşlenmesi gerekir. Bir uygulama birkaç http uç noktaları, bir veritabanı ve bir veri hizmeti önbelleğe alma oluşuyorsa, Azure kaynaklarını barındıran her bu bileşenlerin ayrıştıran gerekir. Örneğin, örnek müzik deposu uygulaması sanal bir makinede barındırılan bir web uygulaması ve Azure SQL veritabanı'nda barındırılan bir SQL veritabanı içerir. 

Bu belge, müzik deposu işlem kaynakları örnek Azure Resource Manager şablonunda nasıl yapılandırılacağını ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın. Tam veri şablonunun burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="virtual-machine"></a>Sanal Makine
Müzik deposu uygulama burada müşteriler göz atın ve Müzik satın alma bir web uygulaması içerir. Bu örnek için web uygulamalarını barındırabilir birkaç Azure Hizmetleri varken bir sanal makine kullanılır. Örnek Müzik deposu şablonu kullanarak bir sanal makinenin dağıtıldığı, bir web sunucusu yüklemek ve müzik deposu Web sitesine yüklenir ve yapılandırılır. Bu makalede amacıyla, yalnızca sanal makine dağıtımı ayrıntılı olarak gösterilmiştir. Web sunucusu ve uygulama yapılandırmasını bir sonraki makalesinde ayrıntılı olarak gösterilmiştir.

Bir sanal makine, Visual Studio yeni kaynak Ekleme Sihirbazı'nı kullanarak bir şablonla ya da geçerli JSON Dağıtım şablonuna ekleyerek eklenebilir. Bir sanal makineyi dağıtırken bazı ilgili kaynaklar de gereklidir. Visual Studio şablonu oluşturmak için kullanıyorsanız, bu kaynakları sizin için oluşturulur. El ile şablon oluşturmak, bu kaynakları eklenen ve yapılandırılmış olması gerekir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).

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

Uygulama dağıtıldıktan sonra sanal makine özelliklerini Azure portalında görülebilir.

![Sanal Makine](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>Depolama hesabı
Depolama hesapları, çok sayıda depolama seçenekleri ve özelliklere sahip. Azure sanal makineleri bağlam için bir depolama hesabı olan ek veri disklerinin ile sanal makine ve sanal sabit disk sürücüler tutar. Müzik deposu örnek dağıtımda, her bir sanal makinenin sanal sabit sürücü tutmak için bir depolama hesabını içerir. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [depolama hesabı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).

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

Resource Manager şablonu bildirimi sanal makinenin içindeki bir sanal makine ile ilişkilendirilecek bir depolama hesabıdır. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine ve depolama hesabı ilişkisi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).

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

Dağıtım sonrasında, Azure Portal'da depolama hesabı görüntülenebilir.

![Depolama hesabı](./media/dotnet-core-2-architecture/storacct.png)

Depolama hesabı blob kapsayıcısı tıklatarak, şablonla dağıtılan her bir sanal makine için sanal sabit disk dosyası görülebilir.

![Sanal sabit disk sürücüler](./media/dotnet-core-2-architecture/vhd.png)

Azure Storage hakkında daha fazla bilgi için bkz: [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Sanal Ağ
Bir sanal makinenin diğer sanal makineler ve Azure kaynakları ile iletişim kurmasına olanak gibi iç ağ gerektiriyorsa, bir Azure sanal ağı gereklidir.  Bir sanal ağ sanal makine internet üzerinden erişilebilir değil. Genel bağlantı daha sonra bu dizide ayrıntılı bir genel IP adresi gerektirir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal ağ ve alt ağları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).

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

Azure portalından, sanal ağ aşağıdaki görüntü gibi görünüyor. Şablonla dağıtılan tüm sanal makineleri sanal ağa takılı olduğunu dikkat edin.

![Sanal Ağ](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>Ağ arabirimi
 Bir ağ arabirimi bir sanal makinenin sanal ağ içinde tanımlanan daha belirgin bir alt ağ için sanal bir ağa bağlanır. 

 Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [ağ arabirimi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).

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

Her sanal makine kaynağı bir ağ profili içerir. Bu profildeki sanal makineyle ilişkilendirilmiş Ağ arabirimidir.  

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine ağ profili](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

Azure portalından, ağ arabiriminin aşağıdaki görüntü gibi görünüyor. İç IP adresi ve sanal makine ilişkilendirme ağ arabirimi kaynakta görülebilir.

![Ağ arabirimi](./media/dotnet-core-2-architecture/nic.png)

Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure sanal ağ belgeleri](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Azure SQL Database
Bir müzik deposu Web sitesi barındırma ek olarak sanal makine, müzik deposu veritabanını barındırmak için bir Azure SQL veritabanı dağıtıldı. Azure SQL veritabanı burada kullanmanın avantajı, ikinci bir kümede sanal makinelerin gerekli değildir ve ölçek ve kullanılabilirlik hizmete yerleşik ' dir.

Visual Studio yeni kaynak Ekleme Sihirbazı, veya bir şablona geçerli JSON ekleyerek kullanarak Azure SQL veritabanına eklenebilir. SQL Server Kaynak, bir kullanıcı adı ve SQL örneğinde yönetici hakları verilen parola içerir. Ayrıca, bir SQL güvenlik duvarı kaynak eklenir. Varsayılan olarak, Azure üzerinde barındırılan uygulamalar SQL örneğine bağlanamıyor. Dış uygulama izin vermek için bir tür SQL Server Management studio güvenlik duvarını SQL örneğine bağlanmak için yapılandırılması gerekir. Müzik deposu tanıtım amacıyla varsayılan yapılandırmayı uygundur. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).

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

SQL server ve Azure portalında göründüğü gibi MusicStore veritabanı görünümü.

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

Azure SQL veritabanı dağıtma hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı belgeleri](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Sonraki adım
<hr>

[2. adım - Azure Resource Manager şablonları güvenlik ve erişim](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

