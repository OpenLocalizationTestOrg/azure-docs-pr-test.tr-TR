---
title: "Azure tanılama kullanarak aaaCollect günlükleri | Microsoft Docs"
description: "Bu makalede, Azure'da çalışan Service Fabric kümesinden Azure tanılama toocollect yukarı tooset nasıl günlüğe yazacağını açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Azure Tanılama’yı kullanarak günlük toplama
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Azure Service Fabric kümesi çalıştırdığınız bir fikir toocollect hello günlüklerini merkezi bir konumda tüm hello düğümlerinden olur. Merhaba günlüklerini merkezi bir konumda sahip çözümlemek ve sorunları kümenizdeki veya bu kümede çalışan hello uygulamaları ve Hizmetleri sorunları gidermenize yardımcı olur.

Bir yolu tooupload toplama günlükleri ise toouse hello Azure tanılama uzantısını, hangi yüklemeleri tooAzure depolama, Azure Application Insights ya da Azure Event Hubs günlüğe kaydeder. Merhaba günlükleri doğrudan depolama veya olay hub'ları bu kullanışlı değildir. Ancak bir dış işlem tooread hello olayları depolama biriminden kullanın ve bunları bir üründe gibi yerleştirmek [günlük analizi](../log-analytics/log-analytics-service-fabric.md) veya başka bir çözüm günlük ayrıştırma. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) bir kapsamlı günlük arama ve analizi hizmeti ile yerleşik gelir.

## <a name="prerequisites"></a>Ön koşullar
Bu araçlar tooperform kullandığınız hello işlemlerin bu belgede:

* [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) (tooAzure bulut Hizmetleri ancak sahip iyi bilgi ve örnekler ilgili)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Resource Manager istemci](https://github.com/projectkudu/ARMClient)
* [Azure Resource Manager şablonu](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Günlük kaynakları toocollect isteyebilirsiniz
* **Service Fabric günlükleri**: hello platform toostandard olay izleme için Windows (ETW) ve EventSource kanaldan yayılan. Günlükleri birkaç türlerden biri olabilir:
  * Çalışma olaylarını: hizmet platform uygular doku hello işlemleri için günlükleri. Örnek uygulamalar ve hizmetler, düğüm durumu değişiklikleri ve yükseltme bilgileri oluşturulmasını verilebilir.
  * [Reliable Actors programlama modelini olayları](service-fabric-reliable-actors-diagnostics.md)
  * [Programlama modeli olaylarının güvenilir hizmetler](service-fabric-reliable-services-diagnostics.md)
* **Uygulama olaylarını**: hizmetinizin koddan yayılan ve hello Visual Studio şablonları sağlanan hello EventSource yardımcı sınıfı kullanılarak yazılan olaylar. Toowrite uygulamanızdan nasıl günlüğe yazacağını daha fazla bilgi için bkz: [İzleyici ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Merhaba tanılama uzantısını dağıtma
günlükleri toplamayı hello ilk toodeploy hello tanılama uzantısını her hello VM'ler hello Service Fabric kümesindeki bir adımdır. Merhaba tanılama uzantısını her VM günlükleri toplar ve bunları belirttiğiniz toohello depolama hesabı yükler. Merhaba adımlar hello Azure portalında veya Azure Resource Manager kullanıp biraz göre farklılık gösterir. Merhaba adımlar da hello dağıtım küme oluşturmanın bir parçası değil veya zaten bir küme için göre değişir. Her senaryo için hello adımları bakalım.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Küme oluşturma hello portal aracılığıyla bir parçası olarak Hello tanılama uzantısını dağıtma
Küme oluşturma bir parçası olarak hello kümedeki toodeploy hello tanılama uzantısını toohello VM'ler, görüntü aşağıdaki hello gösterilen hello tanılama Ayarları panelini kullanın. tooenable Reliable Actors veya güvenilir hizmetler olay toplama olun tanılama çok ayarlandığını**üzerinde** (Merhaba varsayılan ayar). Merhaba kümeyi oluşturduktan sonra hello portalını kullanarak bu ayarları değiştiremezsiniz.

![Küme oluşturma hello portalındaki Azure tanılama ayarları](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Azure destek ekibinin hello *gerektirir* destek oluşturduğunuz hiç destek isteği toohelp çözümleme günlüğe kaydeder. Bu günlükler gerçek zamanlı olarak toplanır ve hello kaynak grubunda oluşturduğunuz hello depolama hesaplarından birini depolanır. Uygulama düzeyi olaylarını Hello tanılama ayarlarını yapılandırın. Bu olayları dahil [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) olayları [Reliable Services](service-fabric-reliable-services-diagnostics.md) olaylar ve Azure Storage'da depolanan bazı sistem düzeyinde Service Fabric olayları toobe.

Ürünler gibi [Elasticsearch](https://www.elastic.co/guide/index.html) veya kendi işlem hello depolama hesabından hello olayları alabilirsiniz. Şu anda toohello tablo gönderilen yolu toofilter veya Temizle hello olayı yok. Bir işlem tooremove olaylarını hello tablosundan uygularsanız yok hello tablo toogrow devam eder.

Merhaba portalını kullanarak bir küme oluştururken, hello şablonunu indirebilir öneririz **Tamam'ı tıklatmadan önce** toocreate hello küme. Ayrıntılar için çok başvurun[bir Azure Resource Manager şablonu kullanarak bir Service Fabric kümesi ayarlayın](service-fabric-cluster-creation-via-arm.md). Merhaba portalını kullanarak bazı değişiklik yapılamıyor çünkü hello şablonu toomake değişiklikleri daha sonra gerekir.

Merhaba aşağıdaki adımları kullanarak şablonları hello Portalı'ndan dışarı aktarabilirsiniz. Ancak, gerekli bilgiler eksik null değerler olabileceği için bu şablonları daha zor toouse olabilir.

1. Kaynak grubu açın.
2. Seçin **ayarları** toodisplay hello Ayarları panelini.
3. Seçin **dağıtımları** toodisplay hello dağıtım Geçmiş paneli.
4. Merhaba dağıtım dağıtım toodisplay hello ayrıntılarını seçin.
5. Seçin **şablonu dışarı aktar** toodisplay hello şablon paneli.
6. Seçin **toofile kaydetmek** tooexport hello şablonu, parametre ve PowerShell dosyalarını içeren bir .zip dosyası.

Merhaba dosyaları dışarı aktardıktan sonra toomake değişiklik gerekir. Merhaba parameters.json dosyasını düzenleyin ve hello kaldırmak **Admınpassword** öğesi. Merhaba dağıtım betiğini çalıştırdığınızda bu hello parola için bir isteme neden olur. Merhaba dağıtım betiği çalıştırırken toofix null parametre değerleri olabilir.

toouse hello bir yapılandırma şablonu tooupdate yüklenen:

1. Yerel bilgisayarınızdaki Hello içeriği tooa klasöre ayıklayın.
2. Merhaba içeriği tooreflect hello yeni yapılandırmasını değiştirin.
3. PowerShell'i başlatın ve hello içeriği ayıkladığınız toohello klasöre değiştirin.
4. Çalıştırma **deploy.ps1** ve hello abonelik kimliği hello kaynak grubu adı girin (kullanım hello aynı adı tooupdate hello yapılandırma) ve benzersiz dağıtım adı.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Azure Kaynak Yöneticisi'ni kullanarak küme oluşturmanın bir parçası olarak Hello tanılama uzantısını dağıtma
Merhaba küme oluşturmadan önce toocreate Kaynak Yöneticisi'ni kullanarak bir küme, tooadd hello tanılama yapılandırması JSON toohello tam küme Resource Manager şablonu gerekir. Eklenen tanılama yapılandırması bir örnek beş VM küme Resource Manager şablonu sağladığımız tooit Resource Manager şablonu örneklerimizi bir parçası olarak. Bu konumda hello Azure Örnekleri Galerisi bkz: [beş düğümlü kümeyi tanılama Resource Manager şablonu örneği ile](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

toosee hello tanılama ayarını hello Resource Manager şablonu, açık hello azuredeploy.json dosyasını ve arama **IaaSDiagnostics**. Bu şablon, select hello'ı kullanarak bir küme toocreate **tooAzure dağıtmak** düğmesini hello önceki bağlantıda kullanılabilir.

Alternatif olarak, hello Resource Manager örnek indirebilir, değişiklikleri tooit olun ve hello kullanarak hello değiştirilmiş şablonu ile bir küme oluşturma `New-AzureRmResourceGroupDeployment` bir Azure PowerShell penceresinde komutu. Kod toohello komutta geçirdiğiniz hello parametreleri için aşağıdaki hello bakın. Merhaba makale toodeploy bir kaynak grup PowerShell kullanarak nasıl hakkında ayrıntılı bilgi için bkz [hello Azure Resource Manager şablonu ile bir kaynak grubu dağıtma](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Tanılama toocollect sistem durumu ve yükleme olaylarını güncelleştir

Service Fabric Hello 5.4 sürümünden başlayarak, sistem durumu ve yük ölçüm olayları koleksiyonu için kullanılabilir. Bu olaylar hello durumu kullanarak hello sistemi veya kodunuzu tarafından oluşturulan olayları yansıtmak veya Raporlama API'leri gibi yük [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) veya [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Bu, toplama ve zaman içinde sistem durumu görüntüleme ve sistem durumu veya yük olaylara dayanarak uyarı verme sağlar. Visual Studio'nun Tanılama Olay Görüntüleyicisi'nde bu olayları eklemek tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW sağlayıcılar listesi.

toocollect hello olaylar, değişiklik hello resource manager şablonu tooinclude

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Tanılama toocollect güncelleştirin ve yeni EventSource kanallar günlükleri karşıya yükleme
tooupdate tanılama toocollect toodeploy hakkında olduğunuz yeni bir uygulama temsil eden yeni EventSource kanallar günlüklerinden gerçekleştirmek hello olduğu gibi aynı adımları hello [önceki bölümde](#deploywadarm) mevcut bir tanılama kurulumu için Küme.

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

## <a name="next-steps"></a>Sonraki adımlar
daha ayrıntılı toounderstand, görünmelidir sorunlarını giderme sırasında hangi olayların görmek için gösterilen hello tanılama olayları [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) ve [Reliable Services](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>İlgili makaleler
* [Tanılama uzantısını toocollect performans sayaçlarını veya kullanarak günlükleri nasıl hello öğrenin](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Service Fabric çözümde günlük analizi](../log-analytics/log-analytics-service-fabric.md)

