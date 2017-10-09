---
title: Windows Azure Diagnostics Service Fabric olay toplama aaaAzure | Microsoft Docs
description: "Toplama ve izleme ve tanılama Azure Service Fabric kümeleri için WAD kullanarak olay toplama hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Olay toplama ve Windows Azure Tanılama'yı kullanarak koleksiyonu
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur. Merhaba günlüklerini merkezi bir konumda sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hello uygulamaları ve Hizmetleri sorunları gidermenize yardımcı olur.

Bir yolu tooupload ve toplama günlükleri günlükleri tooAzure depolama yükler ve ayrıca hello seçeneği toosend günlükleri tooAzure Application Insights veya olay hub'ları içeren toouse hello Windows Azure tanılama (WAD) uzantısı olur. Ayrıca bir dış işlem tooread hello olayları depolama biriminden kullanın ve analiz platformu üründe gibi yerleştirin [OMS günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma.

## <a name="prerequisites"></a>Ön koşullar
Bu araçları kullanılan tooperform olan bazı bu belgedeki hello işlemlerinin:

* [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) (tooAzure bulut Hizmetleri ancak sahip iyi bilgi ve örnekler ilgili)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager istemci](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager şablonu](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Günlük ve olay kaynakları

### <a name="service-fabric-platform-events"></a>Service Fabric platform olayları
' Da anlatıldığı gibi [bu makalede](service-fabric-diagnostics-event-generation-infra.md), Service Fabric ayarlayan, birkaç Giden kutusu günlük kanalları, hangi Merhaba aşağıdaki kanallar kolayca WAD toosend izleme ve tanılama veri tooa depolama tablosu ile yapılandırılmış olan veya başka bir yerde:
  * Çalışma olaylarını: hizmet platform uygular doku hello üst düzey işlem. Örnek uygulamalar ve hizmetler, düğüm durumu değişiklikleri ve yükseltme bilgileri oluşturulmasını verilebilir. Bu olay için Windows izleme (ETW) günlükleri olarak gösterilen
  * [Reliable Actors programlama modelini olayları](service-fabric-reliable-actors-diagnostics.md)
  * [Programlama modeli olaylarının güvenilir hizmetler](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Uygulama olayları
 Uygulamaların ve hizmetlerin koddan yayılan ve hello EventSource yardımcı sınıfı kullanılarak yazılan olaylar hello Visual Studio şablonları sağlanmıştır. Toowrite EventSource uygulamanızdan nasıl günlüğe yazacağını daha fazla bilgi için bkz: [İzleyici ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Merhaba tanılama uzantısını dağıtma
günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır. Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler. Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp biraz göre farklılık gösterir. Merhaba adımlar da hello dağıtım küme oluşturmanın bir parçası değil veya zaten bir küme için göre değişir. Her senaryo için hello adımları bakalım.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Azure portal ile küme oluşturma bir parçası olarak Hello tanılama uzantısını dağıtma
Küme oluşturma bir parçası olarak hello kümedeki toodeploy hello tanılama uzantısını toohello VM'ler, hello aşağıda gösterildiği hello tanılama ayarları bölmesini kullanın görüntü - tanılama çok ayarlandığından emin olun**üzerinde** (Merhaba varsayılan ayar) . Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarları değiştiremezsiniz.

![Küme oluşturma hello portalındaki Azure tanılama ayarları](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Merhaba portalını kullanarak bir küme oluştururken, hello şablonunu indirebilir öneririz **Tamam'ı tıklatmadan önce** toocreate hello küme. Ayrıntılar için çok başvurun[bir Azure Resource Manager şablonu kullanarak bir Service Fabric kümesi ayarlayın](service-fabric-cluster-creation-via-arm.md). Merhaba portalını kullanarak bazı değişiklik yapılamıyor çünkü hello şablonu toomake değişiklikleri daha sonra gerekir.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Azure Kaynak Yöneticisi'ni kullanarak küme oluşturmanın bir parçası olarak Hello tanılama uzantısını dağıtma
Merhaba küme oluşturmadan önce toocreate Kaynak Yöneticisi'ni kullanarak bir küme, tooadd hello tanılama yapılandırması JSON toohello tam küme Resource Manager şablonu gerekir. Eklenen tanılama yapılandırması bir örnek beş VM küme Resource Manager şablonu sağladığımız tooit Resource Manager şablonu örneklerimizi bir parçası olarak. Bu konumda hello Azure Örnekleri Galerisi bkz: [beş düğümlü kümeyi tanılama Resource Manager şablonu örneği ile](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

toosee hello tanılama ayarını hello Resource Manager şablonu, açık hello azuredeploy.json dosyasını ve arama **IaaSDiagnostics**. Bu şablon, select hello'ı kullanarak bir küme toocreate **tooAzure dağıtmak** düğmesini hello önceki bağlantıda kullanılabilir.

Alternatif olarak, hello Resource Manager örnek indirebilir, değişiklikleri tooit olun ve hello kullanarak hello değiştirilmiş şablonu ile bir küme oluşturma `New-AzureRmResourceGroupDeployment` bir Azure PowerShell penceresinde komutu. Kod toohello komutta geçirdiğiniz hello parametreleri için aşağıdaki hello bakın. Merhaba makale toodeploy bir kaynak grup PowerShell kullanarak nasıl hakkında ayrıntılı bilgi için bkz [hello Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Merhaba tanılama uzantısını tooan var olan küme dağıtma
Dağıtılan tanılama yok varolan bir kümeye varsa veya toomodify var olan yapılandırmasını istiyorsanız, ekleyebilir veya güncelleştirebilir. Kullanılan toocreate hello var olan kümesinin hello Resource Manager şablonu değiştirin veya daha önce açıklandığı gibi hello portalından hello şablonu indirin. Merhaba aşağıdaki görevleri gerçekleştirerek Hello template.json dosyasını değiştirin.

Yeni bir depolama kaynak toohello şablonu toohello kaynakları bölümü ekleme.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Ardından, toohello parametreleri yalnızca hello depolama hesabı tanımlarını sonra arasında bölüm eklemek `supportLogStorageAccountName` ve `vmNodeType0Name`. Merhaba yer tutucu metni değiştirmek *depolama hesabı adı buraya* hello depolama hesabı hello adı.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Ardından, hello güncelleştirin `VirtualMachineProfile` hello uzantıları dizi koddan hello ekleyerek hello template.json dosyasının bölümü. Emin tooadd hello başındaki veya burada eklenen bağlı olarak hello son virgül olabilir.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Açıklandığı gibi hello template.json dosyasını değiştirdikten sonra hello Resource Manager şablonunu yeniden yayımlayın. Merhaba şablonu dışarı aktarılmışsa çalışan hello deploy.ps1 dosyasını hello şablonu yeniden yayımlar. Dağıttıktan sonra emin **ProvisioningState** olan **başarılı**.

## <a name="collect-health-and-load-events"></a>Sistem durumu toplama ve olayları yükleme

Service Fabric Hello 5.4 sürümünden başlayarak, sistem durumu ve yük ölçüm olayları koleksiyonu için kullanılabilir. Bu olaylar hello durumu kullanarak hello sistemi veya kodunuzu tarafından oluşturulan olayları yansıtmak veya Raporlama API'leri gibi yük [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) veya [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Bu, toplama ve zaman içinde sistem durumu görüntüleme ve sistem durumu veya yük olaylara dayanarak uyarı verme sağlar. Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW sağlayıcılar listesi.

toocollect hello olaylar, değişiklik hello Resource Manager şablonu tooinclude

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Ters proxy olaylarını Topla

Service Fabric Hello 5.7 sürümünden başlayarak [ters proxy](service-fabric-reverseproxy.md) olayları koleksiyonu için kullanılabilir.
Ters proxy iki kanallarına bir içeren hata olayları yayar yansıtma olayları istek işleme hataları ve başka bir hello ters proxy işlenen tüm hello istekler hakkında ayrıntılı olayları içeren hello. 

1. Hatası olaylarını Topla: Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000010" toohello ETW sağlayıcılar listesi.
Azure kümeleri toocollect hello olaylarından hello Resource Manager şablonu tooinclude değiştirme

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Toplama tüm olayları işlemeyi istek: Visual Studio'da 's Tanılama Olay Görüntüleyicisi'ni güncelleştirme hello Microsoft ServiceFabric girişi hello ETW sağlayıcı listesi çok "Microsoft-ServiceFabric:4:0x4000000000000020".
Azure Service Fabric kümeleri için hello resource manager şablonu tooinclude değiştirme

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Bu tüm trafiğini hello ters proxy üzerinden toplar ve depolama kapasitesini hızlıca tüketebileceği toojudiciously etkinleştir toplama olayları bu kanal önerilir.

Azure Service Fabric kümeleri için tüm hello düğümlerinden hello olayları toplanır ve hello SystemEventTable bir araya getirilir.
Ayrıntılı Hello ters proxy olaylarını sorun giderme için hello başvuran [ters proxy tanılama Kılavuzu](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Yeni EventSource kanaldan Topla

tooupdate tanılama toocollect toodeploy hakkında olduğunuz yeni bir uygulama temsil eden yeni EventSource kanallar günlüklerinden tanılama hello Kurulum var olan bir küme için için aynı adımları daha önce açıklandığı gibi hello gerçekleştirir.

Merhaba güncelleştirme `EtwEventSourceProviderConfiguration` hello kullanarak hello yapılandırma uygulamadan önce hello yeni EventSource kanallar güncelleştirmek için hello template.json dosyasını tooadd girişlerinde bölümünde `New-AzureRmResourceGroupDeployment` PowerShell komutu. Merhaba olay kaynağı Hello adını hello ServiceEventSource.cs Visual Studio tarafından oluşturulan dosya kodunuzda bir parçası olarak tanımlanır.

Olay kaynağı Eventsource My olarak adlandırılmışsa, örneğin, kod tooplace hello olayları Eventsource My MyDestinationTableName adlı bir tabloya aşağıdaki hello ekleyin.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

toocollect performans sayaçlarını veya olay günlükleri, değişiklik hello Resource Manager şablonu sağlanan hello örnekleri kullanarak [bir Azure Resource Manager şablonukullanılarakizlemeveTanılamaileWindowssanalmakineoluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ardından, hello Resource Manager şablonunu yeniden yayımlayın.

## <a name="collect-performance-counters"></a>Performans sayaçlarını Topla

Kümenizde toocollect performans ölçümleri kümenizin hello Resource Manager şablonunda hello performans sayaçları tooyour "WadCfg > DiagnosticMonitorConfiguration" ekleyin. Bkz: [Service Fabric performans sayaçları](service-fabric-diagnostics-event-generation-perf.md) performans sayaçları için toplama öneririz.

Örneğin, burada örneklenen 15 dakikada bir performans sayacı ayarlarız (Bu değiştirilebilir ve aşağıdaki biçimi hello "PT\<zaman >\<birim >", PT3M üç dakikalık aralıklarla Örneğin, örnek) ve toohello aktarıldı uygun depolama tablo her bir dakika.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Application Insights havuz hello aşağıdaki bölümde açıklandığı gibi kullanıyorsanız ve bu ölçümleri tooshow Application Insights'ta istediğiniz, emin tooadd hello havuz adı yukarıda gösterildiği gibi hello "havuzlarını" bölümünde olun. Bunlar hello yönelik kitle olmayan şekilde Ayrıca, performans sayaçları için ayrı bir tablo toosend oluşturmayı düşünün gelen veri hello etkinleştirdiğiniz diğer günlük kanalları.


## <a name="send-logs-tooapplication-insights"></a>Gönderme tooApplication Öngörüler günlüğe kaydeder

İzleme ve tanılama veri tooApplication Öngörüler (AI) gönderme hello WAD yapılandırmasının bir parçası yapılabilir. Olay çözümleme ve görselleştirme için AI toouse karar verirseniz, okuma [olay çözümleme ve görselleştirme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md) tooset AI havuz, "WadCfg" nın bir parçası olarak ayarlama.

## <a name="next-steps"></a>Sonraki adımlar

Azure tanılama doğru şekilde yapılandırdıktan sonra hello ETW ve EventSource günlükler, depolama tablolardaki verileri görürsünüz. Toouse OMS seçerseniz, Kibana ya da doğrudan hello Resource Manager şablonunda yapılandırılmamış başka bir veri analizi ve görselleştirme platform olun, seçim tooread hello platformunu oluşturan emin tooset bu depolama tablolardan hello verilerdeki. Bunu yapmak için OMS görece önemsiz ve içinde açıklanan [OMS olay ve Günlük çözümlemesi](service-fabric-diagnostics-event-analysis-oms.md). Application Insights biraz bu bağlamda bir özel durum, hello tanılama uzantı yapılandırmasını bir parçası olarak yapılandırıldıktan sonra bu nedenle toohello başvuran [uygun makale](service-fabric-diagnostics-event-analysis-appinsights.md) toouse AI seçerseniz.

>[!NOTE]
>Şu anda toohello tablo gönderilen yolu toofilter veya Temizle hello olayı yok. Bir işlem tooremove olaylarını hello tablosundan uygularsanız yok hello tablo toogrow devam eder. Şu anda hello çalışan bir veri temizleme hizmet örneği yoktur [izleme örnek](https://github.com/Azure-Samples/service-fabric-watchdog-service), ve olmadığı sürece, 30 veya 90 günlük süre toostore kaydettiği iyi nedeni için kendiniz bir tane de yazma önerilir.

* [Tanılama uzantısını toocollect performans sayaçlarını veya kullanarak günlükleri nasıl hello öğrenin](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Olay çözümleme ve görselleştirme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Olay çözümleme ve OMS Görselleştirme](service-fabric-diagnostics-event-analysis-oms.md)