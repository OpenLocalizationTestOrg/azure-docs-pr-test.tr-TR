---
title: "bir Azure Resource Manager şablonu aaaVirtual makinelerinizde | Microsoft Azure"
description: "Merhaba sanal makine kaynak bir Azure Resource Manager şablonu nasıl tanımlanır hakkında daha fazla bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu içindeki sanal makineler

Bu makalede toovirtual makineler geçerli bir Azure Resource Manager şablonu yönleri açıklanmaktadır. Bu makalede, bir sanal makine oluşturmak için tam bir şablonu açıklamaz; için depolama hesapları, ağ arabirimleri, ortak IP adresleri ve sanal ağlar için kaynak tanımı gerekir. Bu kaynakların nasıl birlikte tanımlanabilir hakkında daha fazla bilgi için bkz: Merhaba [Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Vardır birçok [hello galeri şablonlarında](https://azure.microsoft.com/documentation/templates/?term=VM) hello VM kaynak içerir. Bir şablona dahil tüm öğeleri burada açıklanmıştır.

Bu örnek belirtilen sayıda sanal makineleri oluşturmak için bir şablonu tipik kaynak bölümünü gösterir:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Bu örnek daha önce oluşturulmuş bir depolama hesabı kullanır. Merhaba şablondan dağıtarak hello depolama hesabı oluşturabilirsiniz. Merhaba örneği aynı zamanda bir ağ arabirimi ve hello şablonda tanımlanan kaynaklarına bağımlı kullanır. Bu kaynaklar hello örnekte gösterilmez.
>
>

## <a name="api-version"></a>API sürümü

Bir şablonu kullanarak kaynak dağıttığınızda, toospecify hello API toouse bir sürümüne sahip. Merhaba, bu apiVersion öğesi kullanılarak hello sanal makine kaynağı örnektir:

```
"apiVersion": "2016-04-30-preview",
```

Merhaba hello şablonunuzda belirttiğiniz API sürümü hello şablonda tanımlayabilirsiniz hangi özelliklerin etkiler. Genel olarak, şablonları oluştururken hello en son API sürümü seçmeniz gerekir. Var olan şablonları için önceki bir API sürümü kullanarak toocontinue istediğiniz veya şablonunuz hello en son sürüm tootake yeni özelliklerden için güncelleştirme olup olmadığını karar verebilirsiniz.

Merhaba son API sürümü almak için bu fırsatları kullanın:

- REST API - [tüm kaynak sağlayıcıları Listele](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Azure CLI 2.0 - [az sağlayıcısı Göster](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parametreler ve değişkenler

[Parametreleri](../../resource-group-authoring-templates.md) çalıştırdığınızda, toospecify değerleri hello şablonu için kolaylaştırır. Bu Parametreler bölümünden hello örnekte kullanılır:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Merhaba örnek şablonu dağıttığınızda, değerleri hello adı ve parola hello yönetici hesabının her VM'ler toocreate VM ve hello sayısına girin. Merhaba şablonuyla yönetilebilir ayrı bir dosyada parametre değerleri belirtme veya istendiğinde değerleri sağlayarak hello seçeneğiniz vardır.

[Değişkenleri](../../resource-group-authoring-templates.md) sizin için değerleri tooset kullanılan art arda onu veya zamanla değiştirebilirsiniz hello şablonunda kolaylaştırır. Bu değişkenler bölümü hello örnekte kullanılır:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Merhaba örnek şablonu dağıttığınızda, değişken değerleri hello adı ve daha önce oluşturduğunuz hello depolama hesabının tanımlayıcısı için kullanılır. Ayrıca hello tanılama uzantı için kullanılan tooprovide hello ayarları değişkenlerdir. Kullanım hello [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../../resource-manager-template-best-practices.md) toohelp karar toostructure hello parametreler ve değişkenler şablonunuzda nasıl istiyor.

## <a name="resource-loops"></a>Kaynak döngüler

Uygulamanız için birden fazla sanal makine gerektiğinde bir şablonda bir kopya öğesi kullanabilirsiniz. Bu isteğe bağlı öğe, bir parametre olarak belirtilen VM hello sayısı oluşturmada size döngü:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Ayrıca, bazı hello belirtme hello kaynak için değerleri döngü dizini hello Merhaba örneği bildiriminde kullanılır. Örneğin, üç, hello adlarını hello işletim sistemi disklerinde örnek sayısı girdiyseniz myOSDisk1, myOSDisk2 ve myOSDisk3 şunlardır:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>Bu örnek yönetilen diskleri hello sanal makineler için kullanır.
>
>

Bir kaynak için bir döngü hello şablonunda oluşturma oluştururken veya diğer kaynaklara erişme, toouse hello döngü gerektirebilecek göz önünde bulundurun. Örneğin, birden çok VM de oluşturmada size döngü gereken üç VM'ler oluşturmada size şablonunuzu döngüler, üç ağ arabirimleri için aynı ağ arabirimi, hello kullanamazsınız. Bir ağ arabirimi tooa VM atarken hello döngü kullanılan tooidentify dizinidir onu:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Bağımlılıklar

En fazla kaynak diğer kaynakları toowork doğru bağlıdır. Sanal makineler bir sanal ağ ve ağ arabirimi ihtiyaç duyduğu toodo ile ilişkilendirilmiş olması gerekir. Merhaba [dependsOn](../../resource-group-define-dependencies.md) öğesidir kullanılan toomake hello ağ arabirimini hello VM'ler oluşturulmadan önce kullanılan hazır toobe olmasını:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager dağıtılan başka bir kaynağa bağımlı olmayan tüm kaynakları paralel olarak dağıtır. Gereksiz bağımlılıkları belirterek dağıtımınızı yanlışlıkla yavaşlatabileceği için bağımlılıkları ayarlarken dikkatli olun. Bağımlılıklar birden fazla kaynak zincir. Örneğin, hello ağ arabirimi hello genel IP adresi ve sanal ağ kaynaklarına bağlıdır.

Bir bağımlılık gerekli olup olmadığını nasıl bilebilirsiniz? Merhaba şablonda ayarlanan hello değerleri bakın. Öğenin hello sanal makine kaynak tanımı'nda hello dağıtılan tooanother kaynak gösteriyorsa aynı şablonu, bir bağımlılık gerekir. Örneğin, örnek sanal makine bir ağ profili tanımlar:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset bu özelliğin hello ağ arabirimi var olması gerekir. Bu nedenle, bir bağımlılık gerekir. Bir kaynak (alt) içindeki başka bir kaynak (üst) tanımlandığında tooset bir bağımlılık da gerekir. Örneğin, hello tanılama ayarlarını ve özel betik uzantılarının her ikisi de hello sanal makine alt kaynaklar olarak tanımlanır. Merhaba sanal makine var. Bunlar oluşturulamaz. Bu nedenle, her iki kaynağın hello sanal makineye bağlı olarak işaretlenir.

## <a name="profiles"></a>Profiller

Birkaç profil öğeler, bir sanal makine kaynağı tanımlarken kullanılır. Bazı gereklidir ve bazı isteğe bağlıdır. Örneğin, hello hardwareProfile, osProfile, storageProfile ve networkProfile öğeleri gerekiyor, ancak hello diagnosticsProfile isteğe bağlıdır. Bu profiller ayarları gibi tanımlayın:
   
- [boyutu](sizes.md)
- [ad](/architecture/best-practices/naming-conventions) ve kimlik bilgileri
- disk ve [işletim sistemi ayarları](cli-ps-findimage.md)
- [Ağ arabirimi](../../virtual-network/virtual-networks-multiple-nics.md) 
- Önyükleme tanılaması

## <a name="disks-and-images"></a>Diskleri ve görüntüleri
   
Azure'da, vhd dosyaları gösterebilir [disk veya görüntü](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bir vhd dosyasının Hello işletim sisteminde özel toobe belirli bir VM'yi olduğunda, başvurulan tooas bir disk olur. Bir vhd dosyasının Hello işletim sisteminde genelleştirilmiş toobe toocreate birçok VM kullanılan, başvurulan tooas bir görüntü değil.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Yeni sanal makineler ve yeni diskler bir platform görüntüsünden oluşturma

Bir VM oluşturduğunuzda, hangi işletim sistemi toouse karar vermeniz gerekir. Merhaba Imagereference kullanılan toodefine hello işletim sisteminin yeni bir VM öğedir. Merhaba, bir Windows Server işletim sistemi için bir tanım örnektir:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Linux işletim sistemi toocreate istiyorsanız, bu tanımı kullanabilirsiniz:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Merhaba işletim sistemi diski için yapılandırma ayarlarını hello osDisk öğeyle atanır. Merhaba örnek yeni bir yönetilen disk mod kümesi çok önbelleğe alma hello tanımlar**ReadWrite** ve o hello disk alanından oluşturuluyor bir [platform görüntüsü](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Mevcut yönetilen diskleri yeni sanal makineler oluşturun

Var olan disklerin toocreate sanal makinelerden istiyorsanız, hello Imagereference ve hello osProfile öğeleri kaldırın ve bu disk ayarları tanımlayın:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Yönetilen bir görüntüden yeni sanal makineler oluşturun

Toocreate istiyorsanız, yönetilen bir görüntüden sanal makine hello Imagereference öğesi değiştirin ve bu disk ayarlarını tanımlayın:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Veri diskleri ekleme

Veri diskleri toohello VM'ler isteğe bağlı olarak ekleyebilirsiniz. Merhaba [diskleri sayısı](sizes.md) hello kullandığınız işletim sistemi disk boyutuna bağlıdır. Merhaba ile tooStandard_DS1_v2, bunları iki toohello eklenemedi veri diski maksimum sayısı hello hello VM'ler boyutunu ayarlayın. Merhaba örnekte, bir yönetilen veri diski tooeach VM ekleniyor:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Uzantılar

Ancak [uzantıları](extensions-features.md) ayrı bir kaynak, yakından bağlı tooVMs oldukları. Uzantıları hello VM alt kaynak veya farklı bir kaynak olarak eklenebilir. Merhaba örnek gösterir hello [tanılama uzantısını](extensions-diagnostics-template.md) toohello VM'ler eklenmekte olan:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Bu uzantı kaynak hello storageName değişkeni ve hello tanılama değişkenleri tooprovide değerleri kullanır. Bu uzantı tarafından toplanan toochange hello verilerin istiyorsanız, daha fazla performans sayaçları toohello wadperfcounters değişken ekleyebilirsiniz. Merhaba VM diskleri depolandığı daha farklı bir depolama hesabı içine tooput hello tanılama verilerini de seçebilirsiniz.

Bir VM'ye yükleyebilirsiniz birçok uzantıları vardır, ancak en yararlı hello büyük olasılıkla hello [özel betik uzantısının](extensions-customscript.md). İlk başladığında hello örnekte, her VM start.ps1 adlı bir PowerShell komut dosyasını çalıştırır:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

Merhaba start.ps1 betik birçok yapılandırma görevleri gerçekleştirebilirsiniz. Örneğin, toohello VM'ler hello örnekte eklenen hello veri diskleri başlatılamadı; özel bir komut dosyası tooinitialize kullanabileceğiniz bunları. Birden çok başlangıç görevleri toodo varsa, Azure depolama alanında hello start.ps1 dosya toocall diğer PowerShell komut dosyalarını kullanabilirsiniz. Merhaba örnek PowerShell kullanır, ancak hello işletim sisteminde, kullanmakta olduğunuz kullanılabilir herhangi bir komut dosyası yöntemini kullanabilirsiniz.

Merhaba portalındaki hello uzantıları ayarları yüklü hello uzantılardan hello durumunu görebilirsiniz:

![Uzantı durumunu Al](./media/template-description/virtual-machines-show-extensions.png)

Hello kullanarak uzantısı bilgi edinebilirsiniz **Get-AzureRmVMExtension** PowerShell komutunu hello **vm uzantısı get** Azure CLI 2.0 komut veya hello **uzantısı bilgi alma**  REST API.

## <a name="deployments"></a>Dağıtımlar

Bir şablonu, bir grup olarak ve otomatik olarak dağıtılan Azure parçaları hello kaynakları dağıttığınızda bir adı dağıtılan toothis Grup atar. Merhaba dağıtım Hello adı olduğu hello hello şablonu hello adı ile aynı.

Hello dağıtımda kaynakların hello durumuyla ilgili merak ediyorsanız hello kaynak grubu dikey hello Azure portalını kullanabilirsiniz:

![Dağıtım bilgileri alma](./media/template-description/virtual-machines-deployment-info.png)
    
Bir sorun toouse değil hello aynı şablon toocreate kaynakları veya tooupdate mevcut kaynakları. Komutları toodeploy şablonlarını kullandığınızda, hello fırsat toosay sahip olduğu [modu](../../resource-group-template-deploy.md) toouse istiyor. başlangıç modu tooeither ayarlanabilir **tam** veya **artımlı**. Merhaba, toodo artımlı güncelleştirmeler varsayılandır. Merhaba kullanırken dikkatli olun **tam** modu kaynakları yanlışlıkla silebilir olduğundan. Ayarladığınızda hello modu çok**tam**, Resource Manager hello şablonunda olmayan tüm kaynaklar hello kaynak grubunda siler.

## <a name="next-steps"></a>Sonraki Adımlar

- Kendi şablonunu kullanarak oluşturduğunuz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).
- Kullanılarak oluşturulan hello şablonu dağıtmak [Resource Manager şablonu ile Windows sanal makine oluşturma](ps-template.md).
- Nasıl toomanage hello gözden geçirerek oluşturulan VM'ler öğrenin [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
