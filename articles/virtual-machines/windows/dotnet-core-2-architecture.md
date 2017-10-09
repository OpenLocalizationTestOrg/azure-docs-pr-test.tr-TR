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
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Windows sanal makineleri için Azure Resource Manager şablonları ile uygulama mimarisi

Bir Azure Resource Manager dağıtım geliştirirken, hesaplama gereksinimleri eşlenen toobe tooAzure kaynaklarını ve Hizmetleri gerekir. Bir uygulama birkaç http uç noktaları, bir veritabanı ve bir veri hizmeti önbelleğe alma oluşuyorsa, hello bu bileşenlerin her birini barındıran Azure kaynaklarını gerekiyor ayrıştıran toobe. Örneğin, Merhaba örnek müzik deposu uygulaması sanal bir makinede barındırılan bir web uygulaması ve Azure SQL veritabanı'nda barındırılan bir SQL veritabanı içerir. 

Bu belge hello müzik deposu işlem kaynakları hello örnek Azure Resource Manager şablonunda nasıl yapılandırılacağını ayrıntıları verilmektedir. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın. Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Sanal Makine
Merhaba müzik deposu uygulama burada müşteriler göz atın ve Müzik satın alma bir web uygulaması içerir. Bu örnek için web uygulamalarını barındırabilir birkaç Azure Hizmetleri varken bir sanal makine kullanılır. Merhaba örnek müzik deposu şablonu kullanarak bir sanal makinenin dağıtıldığı, bir web sunucusu yüklemek ve hello müzik deposu Web sitesine yüklenir ve yapılandırılır. Bu makalede Hello artırmak amacıyla için yalnızca hello sanal makine dağıtımı ayrıntılı olarak gösterilmiştir. Merhaba web sunucusu ve Merhaba uygulaması Hello yapılandırmasını bir sonraki makalesinde ayrıntılı olarak gösterilmiştir.

Bir sanal makine hello Visual Studio yeni kaynak Ekleme Sihirbazı, ya geçerli bir JSON hello Dağıtım şablonuna ekleyerek kullanarak tooa şablonunu eklenebilir. Bir sanal makineyi dağıtırken bazı ilgili kaynaklar de gereklidir. Visual Studio toocreate hello şablonu kullanıyorsanız, bu kaynakları sizin için oluşturulur. El ile Merhaba şablon oluşturma, bu kaynakları eklenen ve yapılandırılmış toobe gerekir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

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

Uygulama dağıtıldıktan sonra hello sanal makine özellikleri hello Azure portal görülebilir.

![Sanal Makine](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Depolama Hesabı
Depolama hesapları, çok sayıda depolama seçenekleri ve özelliklere sahip. Azure sanal makineleri Hello bağlamının hello hello sanal makinenin sanal sabit sürücüler ve ek diskleri bir depolama hesabı tutar. Merhaba müzik deposu örnek bir depolama hesabı toohold hello sanal sabit sürücü, her bir sanal makinenin hello dağıtımda içerir. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [depolama hesabı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

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

İlişkilendirme hello Resource Manager şablonu bildirimi hello sanal makinenin içindeki bir sanal makine ile bir depolama hesabıdır. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine ve depolama hesabı ilişkisi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

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

Dağıtımdan sonra hello depolama hesabı hello Azure portal görüntülenebilir.

![Depolama Hesabı](./media/dotnet-core-2-architecture/storacct-win.png)

Merhaba depolama hesabı blob kapsayıcıya tıklatarak, hello hello şablonla dağıtılan her bir sanal makine için sanal sabit disk dosyası görülebilir.

![Sanal sabit disk sürücüler](./media/dotnet-core-2-architecture/vhd-win.png)

Azure Storage hakkında daha fazla bilgi için bkz: [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Sanal Ağ
Bir sanal makinenin diğer sanal makineler ve Azure kaynakları ile Merhaba özelliği toocommunicate gibi iç ağ gerektiriyorsa, bir Azure sanal ağı gereklidir.  Bir sanal ağ hello sanal makine üzerinden erişilebilir yapmaz Internet hello. Genel bağlantı daha sonra bu dizide ayrıntılı bir genel IP adresi gerektirir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal ağ ve alt ağları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

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

Hello Azure portal hello sanal ağ görüntü aşağıdaki hello gibi görünüyor. Merhaba şablonla dağıtılan tüm sanal makineleri ekli toohello sanal ağ olduğuna dikkat edin.

![Sanal Ağ](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Ağ arabirimi
 Bir ağ arabirimi bir sanal makine tooa sanal ağ, hello sanal ağ içinde tanımlanan daha açık belirtmek gerekirse tooa alt ağa bağlanır. 

 Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [ağ arabirimi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

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

Her sanal makine kaynağı bir ağ profili içerir. Hello ağ arabirimi, bu profilde hello sanal makine ile ilişkilidir.  

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine ağ profili](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

Azure portal Hello görüntü aşağıdaki hello gibi hello ağ arabirimi arar. Merhaba iç IP adresi ve hello sanal makine ilişkilendirme hello ağ arabirimi kaynakta görülebilir.

![Ağ arabirimi](./media/dotnet-core-2-architecture/nic-win.png)

Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure sanal ağ belgeleri](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Azure SQL Database
Ayrıca tooa sanal makine hello müzik deposu Web sitesi, bir Azure SQL veritabanı barındırma dağıtılan toohost hello müzik deposu veritabanıdır. Azure SQL veritabanı burada kullanarak hello avantajı, ikinci bir kümede sanal makinelerin gerekli değildir ve ölçek ve kullanılabilirlik hello hizmetinde yerleşik olmasıdır.

Bir Azure SQL veritabanı hello Visual Studio yeni kaynak Ekleme Sihirbazı, veya bir şablona geçerli JSON ekleyerek kullanılarak eklenebilir. Merhaba SQL Server Kaynak, bir kullanıcı adı ve hello SQL örneğinde yönetici hakları verilen parola içerir. Ayrıca, bir SQL güvenlik duvarı kaynak eklenir. Varsayılan olarak, Azure üzerinde barındırılan hello SQL örneğiyle mümkün tooconnect uygulamalardır. tooallow dış uygulama böyle bir SQL Server Management studio tooconnect toohello SQL örneği, yapılandırılmış toobe hello güvenlik duvarı gerekir. Merhaba varsayılan yapılandırma hello müzik deposu demo Hello artırmak amacıyla için uygundur. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

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

Merhaba SQL server ve hello Azure portal görülen MusicStore veritabanı görünümü.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Azure SQL veritabanı dağıtma hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı belgeleri](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Sonraki adım
<hr>

[2. adım - Azure Resource Manager şablonları güvenlik ve erişim](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

