---
title: "aaaAzure tanılama uzantı yapılandırmasını şema sürümleri ve geçmiş | Microsoft Docs"
description: "Azure sanal makineler, VM ölçek kümesi, Service Fabric ve Cloud Services ilgili toocollecting performans sayaçları."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Azure tanılama uzantı yapılandırmasını şema sürümleri ve geçmişi
Bu sayfa dizinlerinin Azure tanılama uzantı şema sürümleri hello Microsoft Azure SDK'sı bir parçası olarak gönderilir.  

> [!NOTE]
> Hello Azure tanılama uzantısını hello bileşen toocollect performans sayaçları ve diğer istatistiklerine kullanılır:
> - Azure Sanal Makineler 
> - Sanal Makine Ölçek Kümeleri
> - Service Fabric 
> - Cloud Services 
> - Ağ Güvenlik Grupları
> 
> Bu sayfa, yalnızca bu hizmetlerden biri kullanıyorsanız geçerlidir.

Hello Azure tanılama uzantısını Azure monitör, Application Insights ve günlük analizi gibi diğer Microsoft tanılama ürünlerle kullanılır. Daha fazla bilgi için bkz: [Microsoft izleme araçlarına genel bakış](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Grafik sevkiyat azure SDK ve tanılama sürümleri  

|Azure SDK sürümü | Tanılama genişletme sürümü | modeli|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |eklentisi|  
|2.0 - 2.4         |1.0                            |eklentisi|  
|2.5               |1.2                            |Uzantısı|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2.9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Azure tanılama sürüm 1.0 ilk hello Azure SDK'sı yüklendiğinde hello Azure Tanılama ile birlikte gelen sürümünü aldı yani bir eklenti modeli--geliyordu.  

 SDK 2.5 (tanılama sürüm 1.2) ile Azure tanılama başlatılıyor tooan uzantısı model geçti. Merhaba araçları tooutilize yeni özellikler yalnızca yeni Azure SDK'ları içinde kullanılabilir, ancak Azure Tanılama'yı kullanarak herhangi bir hizmeti hello son sevkiyat sürüm doğrudan Azure'dan çekme. Örneğin, hala SDK 2.5 kullanan herkes hello yeni özellikleri kullanıyorsanız hello önceki tabloda bakılmaksızın gösterilen hello en son sürümünü yüklemeye.  

## <a name="schemas-index"></a>Şemalar dizini  
Azure tanılama farklı sürümlerini farklı yapılandırma şemaları kullanabilir. 

[Tanılama 1.0 yapılandırma şeması](azure-diagnostics-schema-1dot0.md)  

[Tanılama 1.2 yapılandırma şeması](azure-diagnostics-schema-1dot2.md)  

[Tanılama 1.3 ve daha sonra yapılandırma şeması](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Sürüm geçmişi


### <a name="diagnostics-extension-19"></a>Tanılama uzantısını 1.9 
Docker desteği eklendi.


### <a name="diagnostics-extension-181"></a>Tanılama uzantısını 1.8.1 
Bir depolama hesabı anahtarı yerine bir SAS belirteci hello özel yapılandırma dosyasında belirtebilirsiniz. Bir SAS belirteci sağlanırsa, hello depolama hesabı anahtarı göz ardı edilir.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Tanılama uzantısını 1,8 
Eklenen depolama türü tooPublicConfig. StorageType olabilir *tablo*, *Blob*, *TableAndBlob*. *Tablo* hello varsayılandır.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Tanılama uzantısını 1.7 
Eklenen hello özelliği tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>Tanılama uzantısını 1.5
Merhaba öğesi ve hello özelliği toosend tanılama verilerini çok iç havuzlar eklenen[Application Insights](../application-insights/app-insights-cloudservices.md) daha kolay toodiagnose sorunları, uygulamanın yanı sıra arasında hello sistem ve altyapı düzeyinde yapma.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 ve tanılama uzantısı 1.3 
Visual Studio bulut hizmeti projeleri için hello aşağıdaki değişiklikler yapıldı. (Bu değişikliklerin Azure SDK'ın toolater sürümleri de geçerlidir.)

* Merhaba yerel öykünücüsü artık tanılama destekler. Bu tanılama verilerini toplamak ve geliştirme ve Visual Studio'da test ederken, uygulamanızın doğru izlemeleri hello oluşturuyor olun anlamına gelir. Merhaba bağlantı dizesi `UseDevelopmentStorage=true` hello Azure storage öykünücüsü kullanarak bulut hizmeti projenizi Visual Studio'da çalıştırıyorsanız tanılama veri toplamayı etkinleştirir. Tüm tanılama verilerini hello (geliştirme depolama) depolama hesabında toplanır.
* Merhaba tanılama depolama hesabı bağlantı dizesi (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) bir kez daha hello hizmet yapılandırma (.cscfg) dosyasında depolanır. Azure SDK 2.5 hello diagnostics.wadcfgx dosyasında hello tanılama depolama hesabı belirtilmedi.

Azure SDK 2.4 ve önceki hello bağlantı dizesini nasıl çalıştığı ve nasıl Azure SDK 2.6 ve daha sonra çalıştığı arasında önemli bazı farklar vardır.

* Azure SDK 2.4 ve önceki sürümlerinde, hello bağlantı dizesi çalışma zamanı tanılama günlükleri aktarmak için hello tanılama eklentisi tooget hello depolama hesabı bilgilerini tarafından kullanıldı.
* Azure SDK 2.6 ve daha sonra hello tanılama bağlantı dizesi Visual Studio tooconfigure hello tanılama uzantısını yayımlama sırasında hello uygun depolama hesabı bilgileri ile tarafından kullanılır. Merhaba bağlantı dizesi, Visual Studio yayımlama için kullanacağı farklı hizmet yapılandırması için farklı depolama hesapları tanımlamanıza olanak sağlar. Ancak, Hello tanılama eklentisi artık (sonra Azure SDK 2.5) kullanılabilir olmadığından, hello .cscfg dosyası tek başına hello tanılama uzantısını etkinleştiremezsiniz. Tooenable hello uzantısı ayrı olarak Visual Studio veya PowerShell gibi araçlar aracılığıyla var.
* PowerShell ile Merhaba tanılama uzantısını yapılandırma toosimplify hello işlemi, hello paket çıktı Visual Studio'dan hello genel yapılandırması XML hello tanılama uzantısını her rol için de içerir. Visual Studio hello tanılama bağlantı dizesi toopopulate hello depolama hesabı bilgilerini hello ortak yapılandırmada mevcut kullanır. Merhaba ortak yapılandırma dosyaları hello Uzantıları klasöründe oluşturulur ve hello düzeni PaaSDiagnostics izleyin. <RoleName>. PubConfig.xml. Tüm temel PowerShell dağıtımları her yapılandırma tooa rolü bu deseni toomap kullanabilirsiniz.
* hello görüntülenebilir hello hello .cscfg dosyasında bağlantı dizesini de Azure portal tooaccess hello tanılama verilerini hello tarafından kullanılan **izleme** sekmesini hello bağlantı dizesidir, gerekli tooconfigure hello hizmet tooshow ayrıntılı izleme verilerini hello Portalı'nda.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Geçirme projeleri tooAzure SDK 2.6 ve sonrası
Ardından Azure SDK 2.5 tooAzure SDK 2.6 den geçirme veya daha sonra hello .wadcfgx dosyasında belirtilen tanılama depolama hesabı olsaydı var. kalır. farklı depolama yapılandırmaları için farklı depolama kullanmanın hello esneklik tootake avantajlarından hesapları, hello bağlantı dizesi tooyour projesi eklemek toomanually sahip olacaksınız. Azure SDK 2.4 veya önceki tooAzure SDK 2.6 proje geçiş, bağlantı dizeleri korunur tanılama hello. Ancak, nasıl bağlantı dizeleri Azure SDK 2.6 belirtildiği şekilde hello önceki bölümde davranılır hello değişiklikler lütfen unutmayın.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Visual Studio hello tanılama depolama hesabı nasıl belirler
* Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilmediği takdirde, Visual Studio tooconfigure hello tanılama uzantısını yayımlarken ve hello ortak yapılandırma xml dosyalarını paketlemesi sırasında oluştururken kullanır.
* Bir tanılama bağlantı dizesi hello .cscfg dosyasında belirtilirse, ardından Visual Studio geri yayımlama ve hello ortak oluşturma hello .wadcfgx dosya tooconfigure hello tanılama uzantısını belirtilen toousing hello depolama hesabı döner paketleme yapılandırma xml dosyaları.
* Merhaba tanılama bağlantı dizesi hello .cscfg dosyasında hello depolama hesabı hello .wadcfgx dosyasında daha önceliklidir. Bir tanılama bağlantı dizesi ise hello .cscfg dosyasında belirtilen sonra Visual Studio kullanan ve .wadcfgx hello depolama hesabında yok sayar.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Ne "geliştirme storage bağlantı dizelerini güncelleştir..." Merhaba onay kutusu musunuz?
onay kutusunu hello **güncelleştirme geliştirme storage bağlantı dizelerini tanılama ve önbelleğe alma için Microsoft Azure depolama hesabı kimlik bilgilerinizle tooMicrosoft Azure yayımlarken** herhangi bir yöntemdir tooupdate sağlar Yayımlama sırasında belirtilen hello Azure depolama hesabı ile geliştirme depolama hesabı bağlantı dizeleri.

Örneğin, bu onay kutusunu seçin ve hello tanılama bağlantı dizesini belirtir varsayalım `UseDevelopmentStorage=true`. Merhaba proje tooAzure yayımladığınızda, Visual Studio hello tanılama bağlantı dizesi hello Yayımlama Sihirbazı'nda belirtilen hello depolama hesabıyla otomatik olarak güncelleştirir. Gerçek depolama hesabı hello tanılama bağlantı dizesi olarak belirtilmişse, ancak, ardından o hesabı yerine kullanılır.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Tanılama işlevleri farklılıkları Azure SDK 2.4 ve önceki ve Azure SDK 2,5 ve üzeri
Projenizi Azure SDK 2.4 tooAzure SDK 2.5 veya sonraki ' yükseltiyorsanız, Tanılama işlevleri farklılıkları aşağıdaki göz hello bulundurmanız gerekir.

* **Yapılandırma API'leri dışıdır** – tanılama program yapılandırması Azure SDK 2.4 veya önceki sürümlerde kullanılabilir, ancak Azure SDK 2.5 ve daha sonra kullanım dışı bırakılmıştır. Tanılama yapılandırmanızı kodda şu anda tanımlanmış olması durumunda, bu ayarları hello geçirilen proje sırada tanılama tookeep çalışmak için en baştan tooreconfigure gerekir. Merhaba tanılama yapılandırması için Azure SDK 2.4 diagnostics.wadcfg ve diagnostics.wadcfgx ve sonraki sürümler için Azure SDK 2.5 dosyasıdır.
* **Bulut hizmeti uygulamaları için tanılama hello rol düzeyinde hello örnek düzeyinde değil yalnızca yapılandırılabilir.**
* **Uygulamanızı dağıtma her zaman hello tanılama yapılandırması güncelleştirilir** – tanılama yapılandırmanızı Server Explorer'dan değiştirirseniz ve uygulamanızı yeniden dağıtın bu eşlik sorunlara neden olabilir.
* **Azure SDK 2.5 ve daha sonra kilitlenme bilgi dökümleri değil kodda hello tanılama yapılandırma dosyasındaki yapılandırılan** – kodda yapılandırılmış kilitlenme bilgi dökümleri varsa, kodu toohello yapılandırma dosyasından toomanually aktarımı hello yapılandırma gerekir. Merhaba kilitlenme dökümleri çünkü hello geçiş tooAzure SDK 2.6 sırasında aktarılmaz.

