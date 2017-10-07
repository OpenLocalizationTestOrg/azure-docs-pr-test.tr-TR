---
title: Service Fabric uygulama izleme deposu olarak Elasticsearch aaaUsing | Microsoft Docs
description: "Service Fabric uygulamaları Elasticsearch ve Kibana toostore, dizin ve arama uygulama izlemelerini (günlükleri) ile nasıl kullanabileceğiniz açıklanır"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Kullanım Elasticsearch Service Fabric uygulama izleme olarak depolama
## <a name="introduction"></a>Giriş
Bu makalede nasıl [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) uygulamalar kullanabilir **Elasticsearch** ve **Kibana** uygulama izleme depolama, dizin oluşturma ve arama. [Elasticsearch](https://www.elastic.co/guide/index.html) bu görev için oldukça uygun olan bir açık kaynaklı, dağıtılmış ve ölçeklenebilir gerçek zamanlı arama ve analizi altyapısıdır. Windows ve Linux sanal makinelerde Microsoft Azure'da çalışan yüklenebilir. Elasticsearch verimli bir şekilde işleyebilir *yapılandırılmış* gibi teknolojileri kullanmayı üretilen izlemeleri **olay izleme için Windows (ETW)**.

ETW Service Fabric çalışma zamanı toosource tanılama bilgileriyle (izlemeler) kullanılır. Bu tanılama bilgilerini Service Fabric uygulamaları toosource yöntemi hello çok önerilen olur. Çalışma zamanı tarafından sağlanan ve uygulama tarafından sağlanan izlemeleri ve sorun gidermeyi kolaylaştırır arasında bağıntı aynı mekanizmayı sağlar hello kullanma. Visual Studio Proje şablonları Service Fabric dahil günlük API (.NET hello üzerinde temel **EventSource** sınıfı), varsayılan olarak ETW izlemeleri yayar. Service Fabric uygulaması genel bir bakış için bkz: ETW, kullanarak izleme [izleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Merhaba izlemeleri tooshow için Elasticsearch içinde gerçek zamanlı hello Service Fabric küme düğümleri (Merhaba uygulaması çalışırken) yakalanan ve tooan Elasticsearch endpoint gönderilen toobe ihtiyaç duyar. İzleme yakalamak için iki ana seçeneğiniz vardır:

* **İşlemdeki izleme yakalama**  
  Merhaba uygulaması veya hizmeti işlemi daha hassas bir şekilde hello tanılama veri toohello izleme deposu (Elasticsearch) göndermekten sorumludur.
* **İşlem dışı izleme yakalama**  
  Ayrı bir aracı hello hizmet işlemin veya işlemlerin izlemeleri yakalamak ve toohello izleme deposu gönderme.

Aşağıda, nasıl Azure üzerinde Elasticsearch yukarı tooset hello uzmanları ele almaktadır ve dezavantajlarını her ikisi için de seçenekleri yakalayabilir ve nasıl tooconfigure Service Fabric hizmet toosend veri tooElasticsearch açıklama açıklanmaktadır.

## <a name="set-up-elasticsearch-on-azure"></a>Azure üzerinde Elasticsearch ayarlama
Merhaba up hello Elasticsearch hizmeti Azure ile ilgili en kolay yolu tooset aracılığıyladır [ **Azure Resource Manager şablonları**](../azure-resource-manager/resource-group-overview.md). Kapsamlı bir [Elasticsearch için hızlı başlangıç Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) Azure hızlı başlangıç şablonlarını depodan kullanılabilir. Bu şablon, ayrı depolama hesapları için ölçek birimlerinizi (düğümler grupları) kullanır. Ayrıca, ayrı istemci ve sunucu düğümleri farklı yapılandırmaları olan ve çeşitli numaraları bağlı veri disklerin sağlayabilirsiniz.

Adlı başka bir şablonu burada kullandığımız **ES-MultiNode** hello gelen [Azure tanılama araçları depo](https://github.com/Azure/azure-diagnostics-tools). Bu şablonu daha kolay toouse ise ve HTTP temel kimlik doğrulaması tarafından korunan bir Elasticsearch kümesi oluşturur. Devam etmeden önce hello deposu (Merhaba depo kopyalama veya bir zip dosyası indiriliyor) GitHub tooyour makineden indirilemedi. Merhaba ES MultiNode şablonu hello hello klasörüyle bulunduğu aynı adı.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Bir makine toorun Elasticsearch yükleme betikleri hazırlama
Merhaba en kolay yolu toouse hello ES-MultiNode adlı sağlanan bir Azure PowerShell Betiği şablonudur `CreateElasticSearchCluster`. toouse bu komut, tooinstall PowerShell modülleri ve adlı bir aracı ihtiyacınız **openssl**. Merhaba ikinci kullanılan tooadminister olabilir bir SSH anahtarı Elasticsearch kümenizi uzaktan oluşturmak için gereklidir.

`CreateElasticSearchCluster`komut dosyası bir Windows makineden hello ES MultiNode şablonuyla kullanım kolaylığı için tasarlanmıştır. Olası toouse hello Windows olmayan makine şablonunda, ancak bu senaryo, bu makalenin kapsamı dışındadır hello gelir.

1. Bunları henüz yüklemediyseniz yüklemek [ **Azure PowerShell modülleri**](http://aka.ms/webpi-azps). İstendiğinde, tıklatın **çalıştırmak**, ardından **yükleme**. 1.3 ya da daha yeni Azure PowerShell gereklidir.
2. Merhaba **openssl** aracı hello dağıtımlarında dahil [ **Windows için Git**](http://www.git-scm.com/downloads). Henüz yapmadıysanız, yükleme [Windows için Git](http://www.git-scm.com/downloads) şimdi. (Merhaba varsayılan yükleme Tamam seçenekleridir.)
3. Git yüklendi ancak hello sistem yolunda yer almayan varsayılarak, bir Microsoft Azure PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Hello yerine `<Git installation folder>` makinenizde; hello Git konumla hello Yardımı'nı varsayılandır **"C:\Program Files\Git"**. Merhaba noktalı virgül karakterini hello ilk yol hello başında unutmayın.
4. TooAzure üzerinde oturum açtığınızdan emin olun (aracılığıyla [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) ve toocreate esnek arama kümenizi kullanılan olmalıdır hello abonelik seçtiniz. Kullanarak, doğru aboneliğin seçildiğini doğrulayın `Get-AzureRmContext` ve `Get-AzureRmSubscription` cmdlet'leri.
5. Henüz yapmadıysanız, hello geçerli dizin toohello ES-MultiNode klasörü değiştirin.

### <a name="run-hello-createelasticsearchcluster-script"></a>Merhaba CreateElasticSearchCluster komut dosyasını çalıştır
Merhaba betiği çalıştırmadan önce hello açmak `azuredeploy-parameters.json` dosya ve doğrulamak veya hello betik parametreleri için değerler sağlayın. şu parametreler hello sağlanır:

| Parametre Adı | Açıklama |
| --- | --- |
| dnsNameForLoadBalancerIP |kullanılan toocreate hello hello esnek arama küme için herkese görünür DNS adını (hello Azure bölgesi etki alanı sağlanan toohello adı eklenerek) hello adı. Örneğin, bu parametre değeri "myBigCluster" ve seçilen hello Azure bölgesi Batı ABD ise hello ortaya çıkan DNS hello küme myBigCluster.westus.cloudapp.azure.com adıdır. <br /><br />Bu ad, aynı zamanda veri düğümü adları gibi hello esnek arama kümesi ile ilişkili birçok yapıları için kök adı olarak görev yapar. |
| adminUsername |Merhaba esnek arama küme yönetmek için hello hello yönetici hesabının adını (ilgili SSH anahtarları otomatik olarak oluşturulur). |
| dataNodeCount |Merhaba hello esnek arama kümedeki düğüm sayısı. Merhaba geçerli sürümü hello komut dosyası, veri ve sorgu düğümler arasında ayrım yapmaz; tüm düğümleri her iki rol oynar. Varsayılanları too3 düğümleri. |
| dataDiskSize |Her veri düğüm için ayrılan hello boyutu (GB)'ndeki veri disklerinin. Her düğüm 4 veri diskleri, özel olarak ayrılmış tooElastic arama hizmeti alır. |
| Bölge |Burada hello esnek arama küme yerleştirilmelidir Azure bölgesi Hello adı. |
| esUserName |Merhaba hello kullanıcı kullanıcı adını toohave erişim tooES küme (konu tooHTTP temel kimlik doğrulaması) yapılandırılmış. Merhaba parola parametrelerini dosyasının bir parçası değil ve ne zaman sağlanmalıdır `CreateElasticSearchCluster` komut dosyası çağrılır. |
| vmSizeDataNodes |Merhaba esnek arama küme düğümleri için Azure sanal makine boyutu. Varsayılanları tooStandard_D2. |

Hazır toorun hello betik sunulmuştur. Merhaba aşağıdaki komutu yürütün:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

Burada 

| Komut parametre adı | Açıklama |
| --- | --- |
| `<es-group-name>` |Tüm esnek arama küme kaynakları içerecek hello Azure kaynak grubu adı Hello. |
| `<azure-region>` |Merhaba hello esnek arama küme nerede oluşturulacağını Azure bölgesi Hello adı. |
| `<es-password>` |Merhaba esnek arama kullanıcının parolasını Hello. |

> [!NOTE]
> NullReferenceException hello Test-AzureResourceGroup cmdlet'i alırsanız, tooAzure üzerinde toolog unuttuysanız (`Add-AzureRmAccount`).
> 
> 

Merhaba betik çalıştıran bir hata alıyorsunuz ve yanlış şablon parametre değeri tarafından hello hata neden oldu belirlerseniz hello parametre dosyası düzeltin ve hello betik farklı bir kaynak grubu adı ile yeniden çalıştırın. Aynı zamanda yeniden kullanabilirsiniz hello aynı kaynak grubu adı ve hello ekleyerek hello betik hello eskisinin temizleme sahip `-RemoveExistingResourceGroup` parametresi toohello betik çağırma.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Merhaba CreateElasticSearchCluster betik çalıştırma sonucu
Merhaba çalıştırdıktan sonra `CreateElasticSearchCluster` komut dosyası, ana yapıları aşağıdaki hello oluşturulur. Bu örnekte "myBigCluster" Merhaba hello değeri olarak kullanmış olan varsayıyoruz `dnsNameForLoadBalancerIP` parametresi hello küme oluşturulduğu bu hello bölge ise Batı ABD.

| Yapı | Adını, konumunu ve açıklamalar |
| --- | --- |
| Uzaktan Yönetim için SSH anahtarı |myBigCluster.key dosyasında (Merhaba dizin) hangi hello CreateElasticSearchCluster çalıştırın. <br /><br />Bu anahtar dosyası kullanılan tooconnect toohello yönetici düğüm olabilir ve (düğümünden hello yönetici) hello kümedeki toodata düğümler. |
| Yönetim düğümü |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Dış SSH bağlantılarına izin veren bir adanmış VM için Uzak Elasticsearch küme yönetim--hello yalnızca bir tane. Elasticsearch hizmetlerin çalıştırmamanız tüm hello Elasticsearch küme düğümleri, ancak aynı sanal ağ mu hello üzerinde çalışır. |
| Veri düğümler |myBigCluster1... myBigCluster*N* <br /><br />Elasticsearch ve Kibana hizmetlerinin çalıştığından veri düğümlerini. SSH tooeach düğümü aracılığıyla, ancak yalnızca hello yönetim düğümü üzerinden bağlanabilirsiniz. |
| Elasticsearch küme |http://myBigCluster.westus.cloudapp.Azure.com/ES/ <br /><br />Merhaba hello Elasticsearch küme (Not hello /es sonek) uç noktasının birincil. Temel HTTP kimlik doğrulaması tarafından korunur (Merhaba kimlik bilgileri olan hello belirtilen hello ES MultiNode şablonu esUserName/esPassword parametrelerinin). Merhaba küme yüklü hello head Eklentisi (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) temel küme yönetimi için de vardır. |
| Kibana hizmeti |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />Merhaba Kibana hizmet tooshow verileri Elasticsearch küme oluşturulan hello ayarlanır. Merhaba tarafından korunan aynı kimlik doğrulama kimlik bilgileri hello olarak küme kendisi. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>İşlemdeki işlem dışı izleme yakalama karşılaştırması
Merhaba, biz Tanılama verileri toplama iki temel yolu girişte: işlem içi ve işlem dışı. Her güçlü ve zayıf vardır.

Merhaba avantajları **işlemdeki izleme yakalama** içerir:

1. *Kolay yapılandırma ve dağıtma*
   
   * tanılama veri toplama Hello yapılandırmasının değil yalnızca hello uygulama yapılandırması parçası. "Hello ile eşitleme", rest hello uygulamasının kolay tooalways Canlı olur.
   * Her uygulama veya hizmet başına yapılandırma kolayca elde edilebilir.
   * İşlem dışı izleme yakalama genellikle ayrı bir dağıtım ve bir ek yönetim görevini ve hataların olası kaynak hello Tanılama Aracı yapılandırmasını gerektirir. Merhaba belirli Aracısı teknoloji genellikle hello aracı sanal makine (düğüm) başına yalnızca bir örneğini sağlar. Bu hello tanılama yapılandırması hello koleksiyonunu tüm uygulamalar arasında paylaşılır ve o düğümde çalışan hizmetler, yapılandırmayı anlamına gelir.
2. *Esneklik*
   
   * toogo, gereken her yerde hedeflenen hello veri depolama sistemi destekleyen bir istemci kitaplığı var olduğu sürece Merhaba uygulaması hello veriler gönderebilir. Yeni havuzlarını eklenebilir istenen şekilde.
   * Karmaşık yakalama, filtreleme ve veri toplama kuralları uygulanabilir.
   * Bir işlem dışı izleme yakalama Aracısı destekler hello hello veri havuzlarını tarafından çoğunlukla sınırlıdır. Bazı aracılar genişletilebilir.
3. *Erişim toointernal uygulama verilerini ve içeriği*
   
   * Merhaba uygulama/hizmet işlemi içinde çalışan hello tanılama alt sistemi kolayca hello izlemeleri bağlamsal bilgi ile genişletebilirsiniz.
   * Merhaba işlem dışı yaklaşım, Windows için olay izleme gibi bazı işlemler arası iletişim mekanizması aracılığıyla tooan Aracısı hello veri gönderilmelidir. Bu mekanizma ek sınırlamalar zorunlu tuttukları.

Merhaba avantajları **işlem dışı izleme yakalama** içerir:

1. *Merhaba özelliği toomonitor uygulama hello ve kilitlenme bilgi dökümleri toplama*
   
   * Merhaba uygulaması toostart başarısız veya çöküyor işlemdeki izleme yakalama başarısız olabilir. Bağımsız bir aracı önemli sorun giderme bilgileri yakalama kadar şansı vardır.<br /><br />
2. *Olgunluk, sağlamlık ve kanıtlanmış performansı*
   
   * Bir platform satıcı (örneğin, bir Microsoft Azure Tanılama Aracı) tarafından geliştirilen bir aracı test ve var olma Savaşının sağlamlaştırma konu toorigorous olmuştur.
   * Yakalama işlemi izleme ile bir uygulama işleminden Tanılama verileri gönderme hello etkinlik değil hello uygulamanın ana görevleri ile müdahale veya zamanlama veya performans sorunlarına oluşabileceğini tooensure dikkatli olunması gerekir. Bağımsız olarak çalışan bir aracının potansiyeli daha az toothese sorunlarını ve özel olarak tasarlanmış toolimit hello sistem üzerindeki etkisini.

Bu olası toocombine ve her iki yaklaşımın düzeyinden yararlanın olur. Aslında, pek çok uygulama hello en iyi çözüm olabilir.

Merhaba burada kullandığımız **Microsoft.Diagnostic.Listeners Kitaplığı** ve Service Fabric uygulaması tooan Elasticsearch kümesinden toosend veri yakalamayı hello işlemdeki izleme.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Merhaba dinleyicileri kitaplığı toosend tanılama veri tooElasticsearch kullanın
Merhaba Microsoft.Diagnostic.Listeners kitaplığı PartyCluster örnek Service Fabric uygulaması bir parçasıdır. toouse onu:

1. Karşıdan [hello PartyCluster örnek](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) github'dan.
2. Merhaba Microsoft.Diagnostics.Listeners ve Microsoft.Diagnostics.Listeners.Fabric projeleri (tüm klasörleri) hello PartyCluster örnek dizin toohello çözüm klasöründen toosend hello veri tooElasticsearch beklenen hello uygulamasının kopyalayın .
3. Merhaba hedef çözümü açın, hello Çözüm Gezgini hello çözüm düğümüne sağ tıklayın ve seçin **Varolan Proje Ekle**. Merhaba Microsoft.Diagnostics.Listeners proje toohello çözümü ekleyin. Yineleme hello aynı hello Microsoft.Diagnostics.Listeners.Fabric projesi için.
4. Proje başvurusu, hizmet proje toohello iki eklenen projelerden ekleyin. (Toosend veri tooElasticsearch beklenen her hizmet Microsoft.Diagnostics.EventListeners ve Microsoft.Diagnostics.EventListeners.Fabric başvuruda bulunmalıdır).
   
    ![Proje başvuruları tooMicrosoft.Diagnostics.EventListeners ve Microsoft.Diagnostics.EventListeners.Fabric kitaplıkları][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Service Fabric genel kullanılabilirlik sürümü ve Microsoft.Diagnostics.Tracing Nuget paketi
Service Fabric genel kullanılabilirlik sürüm (31 Mart 2016 yayımlanan 2.0.135) ile oluşturulan uygulamalar hedef **.NET Framework 4.5.2**. Merhaba .NET Framework hello GA sürümü hello sırasında Azure tarafından desteklenen en yüksek sürümü hello sürümüdür. Ne yazık ki, hello framework'ün bu sürümünde belirli EventListener API'leri bu hello kitaplığı gereken Microsoft.Diagnostics.Listeners eksik. EventSource (Merhaba temelini API'leri doku uygulamalarda oturum hello bileşeni) ve EventListener sıkı şekilde bağlı olduğundan, hello Microsoft.Diagnostics.Listeners kitaplığını kullanan her proje, alternatif bir uygulama kullanması gerekir EventSource. Bu uygulama hello tarafından sağlanan **Microsoft.Diagnostics.Tracing Nuget paketi**, Microsoft tarafından yazılmış. Merhaba paketi hiçbir kod değişiklikleri başvurulan ad alanı değişikliklerinden başka gerekli nedenle hello Framework'te dahil EventSource ile tam olarak geriye dönük olarak uyumlu değil.

toostart kullanarak hello Microsoft.Diagnostics.Tracing uygulama hello EventSource sınıfının toosend veri tooElasticsearch gereken her hizmet projesi için şu adımları izleyin:

1. Merhaba hizmet projeye sağ tıklayın ve seçin **Nuget paketlerini Yönet**.
2. (Henüz seçili değilse) toohello nuget.org paket kaynağı ve aramak için anahtar "**Microsoft.Diagnostics.Tracing**".
3. Merhaba yüklemek `Microsoft.Diagnostics.Tracing.EventSource` paketi (ve bağımlılıklarını).
4. Açık hello **ServiceEventSource.cs** veya **ActorEventSource.cs** dosya hizmet projenizdeki ve hello yerine `using System.Diagnostics.Tracing` hello hello dosyasıyla üstünde yönerge `using Microsoft.Diagnostics.Tracing` yönergesi.

Bu adımları gerekmeyecektir kez hello **.NET Framework 4.6** Microsoft Azure tarafından desteklenir.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch dinleyicisi örnek oluşturma ve yapılandırma
Merhaba tanılama veri tooElasticsearch göndermek için son adım toocreate örneği olan `ElasticSearchListener` ve Elasticsearch bağlantı verileri ile yapılandırın. Merhaba dinleyicisi hello hizmet proje tanımlanan EventSource sınıfları aracılığıyla başlatılan tüm olayları otomatik olarak yakalar. En iyi Hello yerleştirin şekilde hello hizmet başlatma kodu olan toocreate toobe hello hizmet hello ömrü sırasında Canlı gerekir. İşte bir durum bilgisi olmayan hizmetin hello başlatma kodu sonra gerekli değişiklikleri hello nasıl görünebilir (başlayarak açıklamalarında eklemeleri işaret `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Elasticsearch bağlantı verileri koyun hello hizmet yapılandırma dosyası ayrı bir bölümde (**PackageRoot\Config\Settings.xml**). Hello ad hello bölümünün gerekir, karşılık gelen toohello geçirilen toohello değeri `FabricConfigurationProvider` oluşturucusu, örneğin:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Merhaba değerlerini `serviceUri`, `userName` ve `password` parametreleri karşılık gelen toohello Elasticsearch küme uç noktası adresi, Elasticsearch kullanıcı adı ve parola, sırasıyla. `indexNamePrefix`Elasticsearch dizinleri Hello önektir; Merhaba Microsoft.Diagnostics.Listeners kitaplığı günlük verileri için yeni bir dizin oluşturur.

### <a name="verification"></a>Doğrulama
İşte bu kadar! Şimdi, Hello hizmetin çalıştığı her hello yapılandırmasında belirtilen izlemeleri toohello Elasticsearch servis gönderme başlar. Bu Kibana UI hello hedef Elasticsearch örneği ile ilişkili açılış hello tarafından doğrulayabilirsiniz. Bizim örneğimizde, http://myBigCluster.westus.cloudapp.azure.com/ hello sayfasının adresidir. Merhaba seçilen hello adı öneki ile dizinler onay `ElasticSearchListener` örneği gerçekten oluşturulmuş ve verilerle doldurulur.

![Kibana gösteren PartyCluster uygulama olayları][2]

## <a name="next-steps"></a>Sonraki adımlar
* [Tanılama ve bir Service Fabric hizmeti izleme hakkında daha fazla bilgi edinin](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
