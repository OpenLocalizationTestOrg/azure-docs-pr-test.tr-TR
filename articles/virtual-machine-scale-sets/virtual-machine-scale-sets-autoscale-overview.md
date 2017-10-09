---
title: "aaaAutomatic ölçekleme ve sanal makine ölçekleme kümeleri | Microsoft Docs"
description: "Tanılama ve otomatik ölçeklendirme kaynakları tooautomatically ölçek sanal makine ölçek kümesindeki kullanma hakkında bilgi edinin."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Nasıl toouse otomatik ölçeklendirme ve sanal makine ölçekleme kümeleri
Ölçek kümesindeki sanal makinelerin otomatik ölçeklendirmeyi hello oluşturma ya da toomatch performans gereksinimlerini yap hello makinelerinizde silinmesini gerekli. Merhaba toplu iş büyüdükçe, bir uygulama ek kaynaklar tooenable gerektirebilir onu tooeffectively görevleri gerçekleştirebilir.

Otomatik ölçeklendirme yardımcı yönetim yükünü kolaylaştırır otomatik bir işlem var. Ek yükünü azaltarak, yok toocontinually sistem performansını izleme gerekir veya karar nasıl toomanage kaynakları. Ölçeklendirme esnek bir işlemdir. Daha fazla kaynak hello yük arttıkça eklenebilir. Ve isteğe bağlı azalıyor, kaynakları kaldırılan toominimize maliyetleri kullanılabilir ve performans düzeylerini sağlamaya.

Otomatik bir Azure Resource Manager şablonu, Azure PowerShell, Azure CLI veya hello Azure portal kullanarak bir ölçekte ölçeklendirmeyi ayarlayın.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Resource Manager şablonları kullanarak ölçeklendirmeyi ayarlayın
Dağıtma ve her bir kaynağın, uygulamanızın ayrı ayrı yönetmek yerine, tüm kaynakları tek ve eşgüdümlü bir işlemle dağıtan bir şablon kullanın. Merhaba şablonunda uygulama kaynakları tanımlanır ve farklı ortamlar için dağıtım parametresi belirtilmemiş. JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur. daha fazlasını toolearn bakabilir [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Merhaba şablonunda hello kapasite öğesi belirtin:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Kapasite hello kümesindeki sanal makineleri hello sayısını tanımlar. Farklı bir değere sahip bir şablon dağıtarak hello kapasite el ile değiştirebilirsiniz. Bir şablon tooonly değişiklik hello kapasite dağıtıyorsanız, güncelleştirilmiş hello kapasiteyle yalnızca hello SKU öğe içerebilir.

Merhaba, Ölçek kümesi kapasitesi otomatik olarak hello birleşimini kullanarak ayarlanabilir **autoscaleSettings** kaynak ve hello tanılama uzantısını.

### <a name="configure-hello-azure-diagnostics-extension"></a>Hello Azure tanılama uzantısını Yapılandır
Ölçümleri toplama hello ölçek kümesindeki sanal makinelerin her başarılı olursa otomatik ölçeklendirmeyi yalnızca yapılabilir. Hello Azure tanılama uzantısını hello ölçümleri toplama hello otomatik ölçeklendirme kaynak ihtiyaçlarını karşılayan hello izleme ve tanılama olanakları sağlar. Merhaba uzantısı hello Resource Manager şablonu bir parçası olarak yükleyebilirsiniz.

Bu örnekte kullanılan hello değişkenleri hello şablonu tooconfigure hello tanılama uzantısı'nda gösterir:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Merhaba şablon dağıtıldığında parametreler sağlanır. Bu örnek, hello (verilerinin depolandığı) hello depolama hesabı adını ve hello (burada verileri toplanır) hello ölçek kümesinin adını sağlanır. Ayrıca bu Windows Server örnekte yalnızca hello iş parçacığı sayısı performans sayacı toplanır. Tüm kullanılabilir performans sayaçları Windows hello veya Linux kullanılan toocollect tanılama bilgilerini olabilir ve hello uzantısı yapılandırmasında eklenebilir.

Bu örnek hello şablonunda hello hello uzantısı tanımını gösterir:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Merhaba tanılama uzantısını çalıştığında hello veriler depolanır ve belirttiğiniz hello depolama hesabındaki bir tabloda, toplanan. Merhaba, **WADPerformanceCounters** tablo, toplanan hello veri bulabilirsiniz:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Merhaba autoScaleSettings kaynak yapılandırın
sanal makineler hello ölçeğinde azaltın veya tooincrease hello sayısını ayarlayın yapıp hello autoscaleSettings kaynak hello tanılama uzantısını toodecide hello bilgileri kullanır.

Bu örnek hello şablonunda hello kaynak hello yapılandırması gösterilmektedir:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

Merhaba yukarıdaki örnekte, iki kural hello otomatik ölçeklendirme eylemleri tanımlamak için oluşturulur. Merhaba ilk kural hello ölçeklendirme eylemi tanımlar ve ölçek eylemi hello hello ikinci kuralı tanımlar. Bu değerleri hello kurallarında sağlanır:

| Kural | Açıklama |
| ---- | ----------- |
| metricName        | Bu değer olan hello hello wadperfcounter değişken hello tanılama uzantısını için tanımlanan hello performans sayacı ile aynı. Merhaba yukarıdaki örnekte, hello iş parçacığı sayısı sayacını kullanılır.    |
| metricResourceUri | Bu değer hello sanal makine ölçek kümesinin hello kaynak tanımlayıcısı değil. Bu tanımlayıcı hello hello kaynak grubunun adını, hello hello kaynak sağlayıcısının adını ve hello ölçek kümesi tooscale hello adını içerir. |
| timeGrain         | Bu değer toplanan hello ölçümleri hello kesinliği olur. Hello örnek önceki bir dakikalık bir aralıkta verileri toplanır. Bu değer timeWindow ile kullanılır. |
| İstatistiği         | Bu değer hello ölçümleri birleşik tooaccommodate hello ölçeklendirme eylemi otomatik şeklini belirler. Merhaba olası değerler şunlardır: ortalama, Min, maks. |
| timeWindow        | Bu değer hello örnek veriler toplanır zaman aralığıdır. 5 dakika ile 12 saat arasında olmalıdır. |
| timeAggregation   | Bu değer, toplanan hello veri zaman içinde nasıl birleştirileceğini belirler. Ortalama Hello varsayılan değerdir. Merhaba olası değerler şunlardır: ortalama, Minimum, maksimum, son, toplam, sayısı. |
| işleci          | Bu değer kullanılan toocompare hello ölçüm verileri ve hello eşiğin hello işlecidir. Merhaba olası değerler şunlardır: NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual eşittir. |
| Eşik         | Bu değer hello ölçek eylemi tetikler hello değerdir. Merhaba eşik değerleri hello için yeterli birbirinden emin tooprovide olması **genişleme** ve **ölçek bileşenini** eylemler. Her iki eylemler için aynı değerlere hello ayarlarsanız, bir ölçeklendirme eylemi uygulama engeller sabit değişiklik hello sistem düşünmektedir. Örneğin, her iki too600 iş parçacıkları örnek önceki hello ayarı çalışmaz. |
| Yönü         | Bu değer hello eşik değeri elde edilir, alınır hello eylemi belirler. Merhaba olası artış veya Azalış değerlerdir. |
| type              | Bu değer, gerçekleşeceğini ve tooChangeCount ayarlanmalıdır eylemin hello türüdür. |
| değer             | Bu değer, sanal makinelerin hello ölçek kümesinden kaldırıldı tooor eklenen hello sayıdır. Bu değer, 1 veya daha büyük olmalıdır. |
| cooldown          | Merhaba bir sonraki eylem oluşmadan önce bu değer hello zaman toowait hello son ölçeklendirme eylemi itibaren miktarıdır. Bu değer, bir hafta ve bir dakika arasında olmalıdır. |

Merhaba performans sayacı, bağlı olarak, kullanmakta olduğunuz, bazı hello şablon Yapılandırması'ndaki hello öğelerin farklı şekilde kullanılır. Merhaba, örnek önceki hello performans sayacı iş parçacığı sayısıdır ve hello eşik değeridir 650 bir ölçeklendirme eylemi için hello ölçek eylemi için 550 hello eşik değeri şudur. % İşlemci zamanı gibi bir sayaç kullanırsanız, hello eşik değeri bir ölçeklendirme eylemi belirler CPU kullanım yüzdesini toohello ayarlanır.

Yüksek yük gibi bir ölçeklendirme eylemi tetiklendiğinde hello kapasite hello kümesinin hello şablon hello değerinde göre artar. Örneğin, burada hello kapasite too3 ayarlanır ve hello ölçeklendirme eylemi değeri too1 bir ölçek kümesindeki:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Ne zaman geçerli yük nedenler hello ortalama iş parçacığı sayısı toogo 650 hello eşiğinin üstünde hello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A **genişleme** eylem nedenler birden artan hello kümesi toobe kapasitesini hello tetiklenir:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

Merhaba sonuç bir sanal makine ölçek kümesini toohello eklenir:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Merhaba ortalama hello makinelerde iş parçacığı sayısı üzerinde 600 kalırsa beş dakika sonra bir cooldown süre, başka bir makine toohello eklenir. Merhaba ortalama iş parçacığı sayısı 550 altında kalırsa, hello kapasitesi hello ölçek kümesi tarafından azaltılır ve bir makine hello kümesinden kaldırılır.

## <a name="set-up-scaling-using-azure-powershell"></a>Azure PowerShell kullanarak ölçeklendirme ayarlayın

PowerShell tooset otomatik ölçeklendirmeyi yukarı kullanma toosee örnekleri bakabilir [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Azure CLI kullanarak ölçeklendirme ayarlayın

Azure CLI tooset otomatik ölçeklendirmeyi yukarı kullanma toosee örnekleri bakabilir [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Hello Azure portal kullanarak ölçeklendirmeyi ayarlayın

toosee kullanma örneği hello Azure portal tooset otomatik ölçeklendirmeyi yukarı arama sırasında [hello Azure portal kullanarak bir sanal makine ölçek kümesi oluşturma](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Ölçeklendirme eylemleri araştırın

* **Azure portal**  
Şu anda sınırlı miktarda bilgiyi hello portal kullanarak elde edebilirsiniz.

* **Azure Kaynak Gezgini**  
Merhaba, Ölçek kümesini geçerli durumunu incelemek için en iyi hello aracıdır. Bu yolu izleyin ve oluşturduğunuz kümesi hello örnek görünümü hello ölçeğin görmeniz gerekir:  
**Abonelikler > {aboneliğinizi} > resourceGroups > {kaynak grubunuz} > sağlayıcıları > Microsoft.Compute > virtualMachineScaleSets > {Ölçek kümesi} > virtualMachines**

* **Azure PowerShell**  
Bu komut tooget bazı bilgileri kullanın:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Toohello jumpbox sanal makine, yalnızca diğer herhangi bir makine olur ve ardından uzaktan hello ölçek kümesi toomonitor tek tek işlemleri hello sanal makinelere erişmek gibi bağlanın.

## <a name="next-steps"></a>Sonraki Adımlar
* Bakmak [otomatik olarak bir sanal makine ölçek kümesindeki makineleri ölçekleme](virtual-machine-scale-sets-windows-autoscale.md) toosee toocreate yapılandırılmış otomatik ölçeklendirmeyi ile nasıl bir ölçek kümesi örnek.

* Azure özellikleri izleme monitör örnekleri Bul [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md)

* Bildirim özellikler hakkında bilgi edinin [otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri Azure İzleyicisi'nde kullanmayı](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Çok hakkında bilgi edinin[Azure İzleyicisi'nde kullanım denetim günlüklerini toosend e-posta ve Web kancası uyarı bildirimleri](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Hakkında bilgi edinin [Gelişmiş otomatik ölçeklendirme senaryoları](virtual-machine-scale-sets-advanced-autoscale.md).
