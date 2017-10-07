---
title: "aaaAdd özel Service Fabric sistem durumu raporlarının | Microsoft Docs"
description: "Nasıl tooAzure Service Fabric sistem durumu varlıkları toosend özel durumu raporları açıklar. Tasarlama ve kalite sistem durumu raporlarının uygulamak için öneriler sağlar."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Özel Service Fabric durum raporları ekleme
Azure Service Fabric tanıtır bir [sistem durumu modeli](service-fabric-health-introduction.md) tasarlanmış tooflag sağlıksız küme ve uygulama koşullara belirli varlıklar. Merhaba sistem durumu modeli kullanan **sistem durumu reporters** (sistem bileşenleri ve watchdogs). Merhaba kolay ve hızlı tanı ve onarım hedeftir. Sistem durumu hakkında önceden toothink beklemeleri gerekir. Özellikle, toohello kök kapatmak bayrağı sorunları yardımcı olur, sistem durumu etkileyebilir herhangi bir koşul, bildirilmelidir. Merhaba sistem durumu bilgileri, hata ayıklama ve araştırma zaman ve çaba kaydedebilirsiniz. Merhaba hizmet hello bulutta ölçekte da çalışır durumda bir kez hello yararlılığını özellikle Temizle (özel veya Azure).

Merhaba Service Fabric reporters İzleyici faiz koşullarını tanımlanmış. Kendi yerel bir görünümü temel alarak bu koşullara bildirin. Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) varlıklar genel sağlıklı olup tüm reporters toodetermine tarafından gönderilen sistem durumu verileri toplar. Merhaba, hedeflenen toobe zengin, esnek ve kolay toouse modelidir. Merhaba sistem durumu raporlarının Hello kalitesini hello küme hello sistem durumu görünümünü hello doğruluğunu belirler. Yanlış sağlıksız sorunları göstermek hatalı pozitif sonuç, yükseltme veya sistem durumu verileri kullanan diğer hizmetler olumsuz yönde etkileyebilir. Bu tür hizmetlerin onarım hizmetleri ve uyarı mekanizmaları gösterilebilir. Bu nedenle, bazı düşünce hello ilgi koşullarını yakalama gerekli tooprovide raporları olan en iyi olası yol.

toodesign ve uygulama sistem durumu raporlaması, watchdogs ve sistem bileşenleri gerekir:

* İlginizi hello koşulu tanımlamak, izlenip hello yolu ve hello hello küme veya uygulamanın işlevselliğini etkileyebilir. Bu bilgilere dayanarak hello rapor özelliği ve sistem durumu hakkında karar verin.
* Merhaba belirlemek [varlık](service-fabric-health-introduction.md#health-entities-and-hierarchy) hello rapor için geçerlidir.
* Merhaba raporlama burada yapılır belirlemek için hizmet veya bir iç veya dış izleme içinden hello.
* Bir kaynak kullanılan tooidentify hello Raporlayıcı tanımlayın.
* Bir raporlama stratejisi geçişleri veya düzenli aralıklarla seçin. Merhaba daha basit kod gerektirir ve potansiyeli daha az tooerrors şekilde, düzenli aralıklarla önerilir.
* Ne kadar süreyle hello rapor sağlıksız koşullar hello health store içinde kalmalı ve onu temizlenmelidir nasıl belirler. Bu bilgileri kullanarak hello raporun süresi toolive ve kaldırma üzerinde süre sonu davranışını karar verin.

Belirtildiği gibi raporlama den yapılabilir:

* Merhaba Service Fabric hizmeti çoğaltma izlenen.
* İç watchdogs Service Fabric hizmeti (koşullar izler ve raporları sorunları Örneğin, bir Service Fabric durum bilgisiz hizmet) dağıtılmış. Merhaba watchdogs olabilir tüm düğümlere dağıtılan veya izlenen Benzetilen toohello hizmet olabilir.
* Merhaba Service Fabric düğümlerinde çalıştırın, ancak olan iç watchdogs *değil* Service Fabric Hizmetleri olarak uygulanır.
* Bu araştırma hello kaynaktan dış watchdogs *dışında* hello Service Fabric kümesi (örneğin, izleme hizmeti Gomez gibi).

> [!NOTE]
> Merhaba kutudan çıktığında, hello küme hello sistem bileşenleri tarafından gönderilen durum raporları ile doldurulur. Ayrıntılı bilgi için [kullanarak sistem durumu raporları sorun giderme için](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Merhaba kullanıcı raporları gönderilmelidir [durumu varlıklarını](service-fabric-health-introduction.md#health-entities-and-hierarchy) , önceden oluşturulmuş hello sistem tarafından.
> 
> 

Bir kez hello sistem durumu raporlama tasarım sistem durumu raporları kolayca gönderilebilir, işaretlenmemiştir. Kullanabileceğiniz [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) hello küme değilse tooreport durumu [güvenli](service-fabric-cluster-security.md) veya hello doku istemci yönetim ayrıcalıkları varsa. Raporlama yapılabilir hello API tarafından aracılığıyla kullanarak [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), PowerShell veya REST aracılığıyla. Yapılandırma düğmelerini performansı için raporları toplu.

> [!NOTE]
> Rapor durumu zaman uyumlu ve yalnızca hello doğrulama iş hello istemci tarafında temsil eder. Merhaba rapor hello olgu hello sistem istemci veya hello tarafından kabul edilen `Partition` veya `CodePackageActivationContext` nesneleri değil anlamına hello deposunda uygulanır. Zaman uyumsuz olarak gönderilir ve büyük olasılıkla diğer raporlarla toplu. Merhaba sunucuda işleme hello yine başarısız olabilir: hello sıra numarası eski olabilir, hangi hello üzerinde rapor uygulanmalıdır hello varlık silindi, vb..
> 
> 

## <a name="health-client"></a>İstemci sistem durumu
Merhaba sistem durumu raporlarının toohello sistem durumu deposu hello doku istemci içinde bulunduğu bir sistem durumu istemcisi aracılığıyla gönderilir. Merhaba sistem istemci ayarları aşağıdaki hello ile yapılandırılabilir:

* **HealthReportSendInterval**: hello süresi hello raporu arasında hello gecikme, eklenen toohello istemci ve hello süre toohello sistem durumu deposu gönderilir. Her rapor için gönderen bir ileti yerine tek bir ileti kullanılan toobatch raporlar. Merhaba toplu performansı artırır. Varsayılan: 30 saniyedir.
* **HealthReportRetrySendInterval**: hello aralığı sırasında hangi hello sistem istemci yeniden gönderir birikmiş sistem durumu raporları toohello sistem durumu deposu. Varsayılan: 30 saniyedir.
* **HealthOperationTimeout**: hello zaman aşımı süresi bir rapor iletisi için gönderilen toohello sistem durumu deposu. Bir ileti zaman aşımına uğrarsa, hello rapor işlenmiş hello sistem durumu deposu onaylayıncaya kadar hello sistem istemci bunu yeniden dener. Varsayılan: iki dakika.

> [!NOTE]
> Merhaba raporları toplu hale zaman hello doku istemci için Canlı tutulması gereken en az, gönderilmeden HealthReportSendInterval tooensure hello. Canlı uzun toogive hello doku istemci selamlama iletisine kaybolur veya hello sistem durumu deposu olamaz uygularsanız bunları tootransient hatalar tutulmalıdır onu fırsat tooretry.
> 
> 

Merhaba hello istemcide arabelleğe alma hello raporları hello benzersizliğini dikkate alır. Belirli bir hatalı Raporlayıcı 100 raporlama, örneğin, saniyede hello üzerinde aynı rapor hello özelliği aynı varlık, hello raporları hello son sürümü ile değiştirilir. En çok bir tür rapor hello istemci sırada yok. Toplu işleme yapılandırılmışsa, rapor hello sayısı toohello sistem durumu deposu gönderme aralığı başına yalnızca bir tanesini gönderilir. Bu rapor hello en güncel duruma hello varlığın yansıtan hello son eklenen raporudur.
Yapılandırma parametrelerini belirtin, `FabricClient` geçirerek oluşturulan [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) ile Merhaba istenen değerlerini sistem durumu ile ilgili girdileri.

Merhaba aşağıdaki örnekte bir doku istemci oluşturur ve eklendiklerinde hello raporları gönderilmesi gerektiğini belirtir. Zaman aşımları ve yeniden denenebilir hata, yeniden deneme 40 saniyede gerçekleşir.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Merhaba varsayılan doku ayarlamak istemci ayarları tutma öneririz `HealthReportSendInterval` too30 saniye. Bu ayar en iyi performans sağlar son toobatching. Mümkün olan en kısa sürede gönderilmesi gereken kritik raporlar için `HealthReportSendOptions` hemen ile `true` içinde [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API. Hemen raporları aralığı toplu işleme hello atlama. Bu bayrak dikkatli kullanın; mümkün olduğunda toplu işleme hello sistem istemci tootake avantajlarından istiyoruz. Hemen gönder yararlıdır da hello doku istemci kapatırken (örneğin, hello işlemi geçersiz durum belirledi ve tooshut tooprevent yan etkileri aşağı gerekir). En yüksek çaba gönderme birikmiş hello raporlar sağlar. Bir rapor anlık bayrağı ile eklendiğinde, hello sistem istemci tüm toplanan hello raporları itibaren son gönderme toplu işlemleri.

PowerShell aracılığıyla bağlantı tooa küme oluşturulduğunda, aynı parametreleri belirtilebilir. Aşağıdaki örnek hello bağlantı tooa yerel küme başlar:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Benzer şekilde tooAPI, raporları kullanarak gönderilebilir `-Immediate` hemen hello bağımsız olarak gönderilen toobe geçiş `HealthReportSendInterval` değeri.

KALAN için bir iç doku istemci toohello Service Fabric gateway hello raporlar gönderilir. Varsayılan olarak, bu, her 30 saniyede toplu yapılandırılmış toosend raporları istemcidir. Merhaba küme yapılandırma ayarı ile Merhaba toplu aralığını değiştirebilirsiniz `HttpGatewayHealthReportSendInterval` üzerinde `HttpGateway`. Belirtildiği gibi bir toosend hello raporları ile daha iyi seçenektir `Immediate` true. 

> [!NOTE]
> Sistem durumu Hizmetleri yetkisiz tooensure rapor veremez hello kümedeki hello varlıklar karşı hello sunucu tooaccept istekleri yalnızca güvenli istemcilerden gelen yapılandırın. Merhaba `FabricClient` gerekir sahip güvenliği etkinleştirilmiş toobe mümkün toocommunicate hello kümeyle (örneğin, Kerberos veya sertifika kimlik doğrulaması) ile raporlama için kullanılır. Daha fazla bilgi edinin [küme güvenlik](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Gelen düşük ayrıcalıklı Hizmetleri içinde rapor
Service Fabric Hizmetleri yönetici erişimi toohello küme yoksa hello geçerli bağlamdan varlıklar üzerinde sistem durumu bildirebilirsiniz `Partition` veya `CodePackageActivationContext`.

* Durum bilgisi olmayan hizmetler için kullanmak [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport hello geçerli hizmet örneği üzerinde.
* Durum bilgisi olan hizmetler için kullanmak [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport geçerli çoğaltma.
* Kullanım [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport hello geçerli bölüm varlığı.
* Kullanım [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport geçerli uygulama üzerinde.
* Kullanım [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport hello geçerli düğümde dağıtılan hello geçerli uygulama üzerinde.
* Kullanım [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport hello geçerli düğümde dağıtılan hello uygulaması için bir hizmet paketi üzerinde.

> [!NOTE]
> Dahili olarak, hello `Partition` ve hello `CodePackageActivationContext` varsayılan ayarlarla yapılandırılan bir sistem durumu istemcisi tutun. Merhaba açıklandığı gibi [sistem istemci](service-fabric-report-health.md#health-client), raporları toplu hale ve bir süreölçer gönderilir. Merhaba nesneleri olmalıdır Canlı toohave bir fırsat toosend hello rapor tutulurlar.
> 
> 

Belirleyebileceğiniz `HealthReportSendOptions` raporlarda gönderirken `Partition` ve `CodePackageActivationContext` sistem durumu API'leri. Mümkün olan en kısa sürede gönderilmesi gereken kritik raporlarınız varsa, kullanmak `HealthReportSendOptions` hemen ile `true`. Hemen raporları hello iç sistem istemci aralığını toplu işleme hello atlama. Önceden belirtildiği gibi bu bayrak dikkatli kullanın; mümkün olduğunda toplu işleme hello sistem istemci tootake avantajlarından istiyoruz.

## <a name="design-health-reporting"></a>Sistem durumu raporlama tasarlama
Merhaba yüksek kaliteli raporları üretme ilk adımı hello hizmetinin hello durumunun etkileyebilir hello koşulları tanımlamak için kullanılır. Başlatıldığında--veya hatta daha iyi bir sorun gerçekleşmeden önce--olası olabilir, hello hizmet veya küme bayrağı sorunlarını yardımcı olabilecek herhangi bir koşul ABD Doları milyarlarca kaydedin. Merhaba kesinti daha az yararları, daha az gece saat araştırma ve sorunları ve daha yüksek müşteri memnuniyetini onarma harcanan.

Merhaba koşullar tanımlandıktan sonra izleme yazıcılarının kendileri için ek yükü ve yararlılığını arasında dengeleyin hello en iyi şekilde toomonitor çıkışı toofigure gerekir. Örneğin, bazı geçici dosyaları paylaşımındaki kullanmak karmaşık hesaplamalar yapan bir hizmet göz önünde bulundurun. Bir izleme yeterli alan vardır hello paylaşımı tooensure izleyebilir. Dosya veya dizin değişiklik bildirimleri için dinleme. Bir ön eşik ulaşıldığında ve hello paylaşımı doluysa bir hata raporu bir uyarı rapor edilemedi. Bir uyarı üzerinde bir onarım sistem hello paylaşımındaki eski dosyalar temizleniyor başlayamadı. Bir hata üzerinde bir onarım sistem hello hizmet çoğaltma tooanother düğümü taşıyabilirsiniz. Merhaba koşul durumlarını bakımından sistem durumu nasıl açıklanan unutmayın: Merhaba durumunu hello (Tamam) sağlıklı kabul edilebilir koşul veya sağlıksız (uyarı veya hata).

Merhaba İzleme Ayrıntıları ayarladıktan sonra bir izleme yazıcısı nasıl tooimplement hello İzleme çıkışı toofigure gerekir. Merhaba koşullar hello Hizmeti'nde belirlenebilir hello izleme hello izlenen hizmetin kendisini parçası olabilir. Örneğin, hello hizmet kod hello paylaşım kullanımını denetleyin ve toowrite bir dosya çalışır her zaman ardından raporlar. Bu yaklaşımın avantajı Hello raporlama kolay olmasıdır. Merhaba hizmeti işlevselliğini etkileyen gelen tooprevent izleme hatalar dikkatli olunması gerekir.

Kullanarak izlenen hello Hizmeti'nde raporlama her zaman bir seçenek değil. İzleme olaylarını hello hizmet içinde mümkün toodetect hello koşullar olmayabilir. Merhaba mantığı ya da veri toomake hello belirleme olmayabilir. Merhaba koşullarını izleme hello yükünü yüksek olabilir. Merhaba koşullar da belirli tooa hizmet olmaması, ancak bunun yerine Hizmetleri arasındaki etkileşimler etkiler. Başka bir seçenek toohave watchdogs hello kümedeki ayrı işlemleri olarak olur. Hello watchdogs hello koşullar ve rapor, herhangi bir şekilde hello ana Hizmetleri etkilemeden izleyin. Örneğin, bu watchdogs hello durum bilgisiz Hizmetleri'nde olarak uygulanabilir veya hello tüm düğümler üzerinde dağıtılan aynı uygulama aynı düğümleri hello hizmet olarak.

Bazı durumlarda, hello kümede çalışan bir izleme seçeneği ya da değil. Kullanıcıların gördüğünüz hello kullanılabilirlik veya hello hizmet işlevselliğini izlenen hello koşul ise, en iyi toohave hello watchdogs aynı hello kullanıcı istemcileri olarak yerleştirin hello içinde var. Burada, hello işlemleri sınayabilirsiniz hello aynı şekilde, kullanıcılar bunları çağırın. Örneğin, hello küme dışında yaşar, istekleri toohello hizmet veren ve hello gecikme süresi ve hello sonuç doğruluğunu denetler bir izleme olabilir. (Hesaplayıcı hizmeti için örneğin, 2 + 2 4 makul bir sürede return mu?)

Merhaba İzleme Ayrıntıları sonlandırıldıktan sonra benzersiz olarak tanımlayan bir kaynak kimliği karar vermeniz gerekir. Aynı türde yaşayan Merhaba, birden çok watchdogs küme hello gerekir farklı varlıklarını rapor, veya, hakkında rapor varsa aynı varlık, kullanım farklı kaynak kimliği veya özellik hello. Bu şekilde raporlarının bulunabilir. Merhaba sistem durumu raporu Hello özelliği izlenen hello koşul yakalama. (Merhaba yukarıdaki örnekte, hello özellik olabilir **ShareSize**.) Birden çok rapor toohello uygularsanız aynı, hello koşul özelliği raporları toocoexist sağlayan bazı dinamik bilgileri içermelidir. Örneğin, birden çok paylaşımı izlenen toobe gerekiyorsa, hello özellik adı olabilir **ShareSize sharename**.

> [!NOTE]
> Yapmak *değil* hello sistem durumu deposu tookeep durum bilgisini kullanın. Yalnızca sistem durumu ile ilgili bilgileri sistem durumu, bu bilgileri etkileri hello sistem durumu değerlendirmesi bir varlık olarak raporlanır. Merhaba sistem durumu depolama genel amaçlı bir depolama alanı olarak tasarlanmamıştır. Tüm veriler sistem durumu değerlendirme mantığı tooaggregate hello sistem durumu kullanır. Sistem durumu (gibi bir sistem durumu Tamam durumuyla raporlama) ilgisiz toohealth hello etkilemez bilgileri gönderme bir araya getirilir ancak hello sistem durumu deposu hello performansını olumsuz yönde etkileyebilir.
> 
> 

Merhaba sonraki karar noktası hangi varlık tooreport açıktır. Çoğu hello süreyi hello koşulu idetifies varlık açıkça hello. Merhaba varlık ile olası en iyi ayrıntı düzeyi seçin. Bir koşul bir bölümdeki tüm çoğaltmaları etkiliyorsa hello hizmet üzerinde hello bölüm raporlama. Burada daha fazla düşünce, ancak gerekli köşe durumlar vardır. Merhaba koşul bir varlık etkiliyorsa hello bölüme bildirilmesi sonra bir çoğaltma ancak hello gibi desire çoğaltma ömrü hello süresinden daha fazla bilgi için işaretlenen toohave hello durumdur. Aksi takdirde, Hello çoğaltma silindiğinde, hello sistem durumu depolama, tüm raporları siler. İzleme yazıcılarının hello ömrü hello varlık ve hello raporu hakkında düşünmeniz gerekir. Mağaza (örneğin, bir varlık üzerinde bildirdiği bir hata artık uygulanmadığında) bir rapor temizlenmelidir zaman açık olması gerekir.

Birlikte ı açıklanan hello noktaları koyan bir örneğe bakalım. Bir durum bilgisi olan kalıcı hizmet ana ve tüm düğümleri (görevinin her türü için bir ikincil hizmet türü) dağıtılan ikincil durum bilgisi olmayan hizmetler Service Fabric uygulaması oluşan göz önünde bulundurun. Hello Yöneticisi ikinciller tarafından yürütülen komutları toobe içeren bir işleme sırası vardır. Merhaba ikinciller hello gelen isteklerin yürütülebilmesi ve geri bildirim sinyalleri gönderin. İzlenen bir koşul hello hello ana işleme sırası uzunluğu ' dir. Hello Yöneticisi sırası uzunluğu eşiği ulaşırsa, bir uyarı bildirilir. Merhaba uyarı hello ikinciller hello yük işleyemiyor gösterir. Hello sıra hello en fazla uzunluk ulaştığında ve komutları bırakılan bir hata bildirdi, hizmet hello kurtaramazsınız. Merhaba raporları hello özellikte olabilir **QueueStatus**. Merhaba izleme hello hizmet içinde yaşar ve hello ana birincil Çoğaltmada düzenli aralıklarla gönderilir. Merhaba süresi toolive iki dakikadır ve her 30 saniyede düzenli aralıklarla gönderilir. Merhaba birincil kullanılamaz hale gelirse hello rapor Mağazası'ndan otomatik olarak temizlenir. Merhaba hizmet çoğaltma çalışıyor, ancak karşılıklı veya diğer sorunlar oluşmuş hello rapor hello health store içinde süresi dolar. Bu durumda, hello varlık hatasında değerlendirilir.

İzlenebilir başka bir koşul görev yürütme süresi ' dir. Hello Yöneticisi dağıtır görevleri toohello ikinciller hello görev türüne bağlı. Merhaba tasarım bağlı olarak, hello ana hello ikinciller görev durumu için yoklama. Bunlar bittiğinde ikinciller toosend geri bildirim sinyalleri için de bekleyin. Merhaba ikinci durumda, ikincil kopya dökme veya iletileri burada kaybolur toodetect durumlarda dikkatli olunması gerekir. Bir seçenek hello ana toosend ping isteği toohello ikincil durumunu geri gönderen aynıdır. Durum yok aldıysanız hello ana bir hata olarak değerlendirir ve hello görev reschedules. Bu davranış, başlangıç görevleri ıdempotent olduğunu varsayar.

izlenen hello koşul dönüştürülür uyarı olarak hello görev belirli bir süre içinde yapmadıysanız (**t1**, örneğin 10 dakika). Merhaba görev zamanında tamamlanmazsa (**t2**, örneğin 20 dakika), izlenen hello koşul hata olarak çevrilmiş. Bu raporlama birden çok yolla yapılabilir:

* Hello Yöneticisi birincil çoğaltma kendisini düzenli aralıklarla bildirir. Tüm Bekleyen görevler için bir özellik hello sıraya sahip olabilir. En az bir daha uzun sürer hello rapor durumu hello özellikte görev **PendingTasks** bir uyarı veya hata uygun olarak. Bekleyen görev yok veya tüm görevler yürütme başladı hello rapor durumu Tamam olur. Merhaba görevleri kalıcıdır. Merhaba birincil kullanılamaz hale gelirse, yeni yükseltilmiş hello birincil tooreport düzgün bir şekilde devam edebilirsiniz.
* Başka bir izleme işlemde (Merhaba Bulut veya dış) hello görevleri denetler (gelen dışında istenen hello görev sonucuna bağlı olarak) bunlar tamamladıysanız toosee. Merhaba eşikleri uymaz, bir rapor hello ana hizmette gönderilir. Bir raporu da gibi hello görev tanımlayıcısı içeren her görev için gönderilen **PendingTask + Taskıd**. Raporları yalnızca sağlıksız durumlarına gönderilmelidir. Birkaç dakika zaman toolive tooa ayarlayın ve tooensure temizleme sona erdiğinde kaldırılan hello raporları toobe işaretleyin.
* Bu beklenen toorun uzun sürer olduğunda bir görev yürütme ikincil hello bildirir. Merhaba özellikte hello hizmet örneği üzerinde raporları **PendingTasks**. Merhaba rapor sorunları var. hello hizmet örneği soruna neden olan, ancak burada hello örneği sonlandıktan hello durumu yakalamaz. Merhaba raporları sonra temizlenir. Merhaba ikincil hizmette rapor edilemedi. Merhaba ikincil hello görev tamamlarsa, hello ikincil örneği hello rapor hello deposundan temizler. Merhaba rapor burada hello bildirim iletisi kaybolur ve hello görev hello Yöneticisi'nin açısından bakıldığında bitmedi hello durumu yakalamaz.

Yukarıda açıklanan hello durumlarda Hello raporlama yapılır ancak sistem durumu değerlendirmesinde hello raporları uygulama sağlığını yakalanır.

## <a name="report-periodically-vs-on-transition"></a>Raporda düzenli aralıklarla ve geçiş
Merhaba sistem durumu modeli raporlama kullanarak watchdogs raporları düzenli aralıklarla veya geçişleri gönderebilirsiniz. Hello kod çok daha basit ve potansiyeli daha az tooerrors olduğundan hello raporlama izleme yolu, düzenli aralıklarla önerilir. Merhaba watchdogs toobe yanlış raporları tetiklemek olası tooavoid hata olarak basit çaba gerekir. Yanlış *sağlıksız* raporları, sistem durumu değerlendirmesini ve yükseltmeleri dahil olmak üzere sistem durumu hakkında temel senaryoları etkileyen. Yanlış *sağlıklı* raporları istenmediği hello kümedeki sorunları gizle.

Dönemsel raporlama için hello izleme ile bir süreölçer uygulanabilir. Bir zamanlayıcı geri hello izleme hello durumunu denetleyin ve hello geçerli durumunu temel alan bir rapor gönderin. Hangi raporun daha önce gönderilen veya Mesajlaşma bakımından herhangi iyileştirmeler olun hiçbir gerek toosee yoktur. Toplu işleme mantığı toohelp performans Hello sistem durumu istemcinin olur. Merhaba sistem istemci Canlı tutulur, ancak bu dahili hello rapor hello sistem durumu mağaza tarafından onaylanan veya hello izleme hello sahip yeni bir rapor oluşturur kadar yeniden deneme aynı varlık, özellik ve kaynak.

Geçişleri üzerinde raporlama durumunun dikkatli işleme gerektirir. Merhaba izleme bazı koşullar izler ve yalnızca hello koşullar değiştiğinde raporlar. Bu yaklaşımın ters Merhaba, daha az raporları gerekli olan ' dir. Merhaba dezavantajı hello izleme hello mantığını karmaşık olmasıdır. Böylece incelenen toodetermine durum değişiklikleri olabilir hello izleme hello koşullar veya hello raporları bulundurmanız gerekir. Yük devretme, eklediğiniz, ancak henüz toohello sistem durumu deposu gönderilen raporlarla dikkatli olunması gerekir. Başlangıç sıra numarası, gitgide artan olması gerekir. Aksi durumda, hello raporları eski olarak reddedilir. Veri kaybı burada ücrete hello nadir durumlarda, eşitleme hello Raporlayıcı hello durumunu ve hello sistem durumu deposu hello durumunu arasında gerekli olabilir.

Geçişleri üzerinde raporlama anlamlı kendilerini üzerinde aracılığıyla reporting services için `Partition` veya `CodePackageActivationContext`. Ne zaman, yerel nesnesi hello (çoğaltma veya dağıtılmış hizmet paketi / dağıtılan uygulama) olan kaldırıldı, tüm raporları da kaldırılır. Bu otomatik temizleme Raporlayıcı ve sistem durumu deposu arasındaki eşitleme hello gereksinimini rahatlatır. Merhaba rapor için üst bölüm veya üst uygulama ise, yük devretme tooavoid eski raporlarda hello health store içinde dikkatli olunması gerekir. Mantığı toomaintain hello doğru durumda ve Temizle hello rapor artık gerekmeyen zaman deposundan eklenmesi gerekir.

## <a name="implement-health-reporting"></a>Sistem durumu raporlamasını Uygula
Merhaba varlık ve rapor ayrıntıları Temizle olduktan sonra sistem durumu raporları gönderme hello API'si, PowerShell veya REST yapılabilir.

### <a name="api"></a>API
tooreport hello API aracılığıyla toocreate üzerinde tooreport istedikleri bir sistem durumu raporu belirli toohello varlık türü gerekir. Merhaba rapor tooa sistem istemci verin. Alternatif olarak, bir sistem durumu bilgisi oluşturmak ve yöntemleri raporlama toocorrect geçirin `Partition` veya `CodePackageActivationContext` tooreport geçerli varlıklar üzerinde.

Merhaba aşağıdaki örnek hello küme içindeki izleme olaylarını kullanarak raporlama düzenli gösterir. Merhaba izleme, dış kaynak gelen bir düğümde erişilip erişilemeyeceğini denetler. Merhaba kaynak hello uygulama içinde bir hizmet bildirimi tarafından gereklidir. Merhaba kaynak kullanılamıyorsa, hello Merhaba uygulaması içindeki diğer hizmetler hala düzgün bir şekilde çalışabilir. Bu nedenle, hello rapor dağıtılan hello hizmet paketi varlıkta her 30 saniyede bir gönderilir.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Sistem durumu raporları ile Gönder * *gönderme ServiceFabric*EntityType*HealthReport **.

Merhaba aşağıdaki örnek bir düğüm üzerindeki CPU değerleri raporlama düzenli gösterir. Merhaba raporları her 30 saniyede gönderilmesi gerektiğini ve birer iki dakikalık toolive sahiptir. Bunlar zaman aşımına uğrarsa hello Raporlayıcı sorunları sahiptir, böylece hello düğüm hatası değerlendirilir. Merhaba CPU bir eşiğin olduğunda uyarı sistem durumu hello rapor vardır. Merhaba CPU yapılandırılmış başlangıç saatinden daha fazla bilgi için bir eşiğin üstünde kaldığında hata olarak bildirilir. Aksi takdirde hello Raporlayıcı Tamam sistem durumunu gönderir.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Merhaba aşağıdaki örnek geçici bir uyarı bir çoğaltma üzerinde raporlar. İlk hello bölüm kimliği alır ve bunu ilgilendiği hello hizmeti için çoğaltma kimliği hello. Ardından bir rapordan gönderir **PowershellWatcher** hello özellikte **ResourceDependency**. Merhaba ilgi yalnızca iki dakika rapordur ve hello Mağazası'ndan otomatik olarak kaldırılır.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
İstenen toohello varlık gidin ve hello gövde hello sistem durumu raporu açıklamasında POST istekleri REST kullanarak sistem durumu raporları gönder. Örneğin, nasıl toosend REST bkz [küme sistem durumu raporlarının](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) veya [hizmet sistem durumu raporlarının](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Tüm varlıklar desteklenir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba sistem durumu verilerini temel alarak hizmeti yazıcılarını ve küme/uygulama yöneticileri, yolları tooconsume hello bilgilerinin düşünebilirsiniz. Örneğin, bunlar kesintilere yol açabilirsiniz önce sistem durumu toocatch ciddi sorunları hakkında temel Uyarıları ayarlayın. Yöneticiler ayrıca otomatik olarak onarma sistemleri toofix sorunları ayarlayabilirsiniz.

[Giriş tooService doku sistem durumu izleme](service-fabric-health-introduction.md)

[Service Fabric sistem durumu raporlarını görüntüle](service-fabric-view-entities-aggregated-health.md)

[Nasıl tooreport ve onay sistem durumu hizmeti](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Sorunlarını gidermek için sistem durumu raporlarını kullanma](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[İzleme ve Hizmetleri yerel olarak tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)

