---
title: "aaaConfigure güvenilir Azure mikro | Microsoft Docs"
description: "Durum bilgisi olan güvenilir hizmetler Azure Service Fabric yapılandırma hakkında bilgi edinin."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Durum bilgisi olan güvenilir hizmetler yapılandırın
Güvenilir hizmetler için yapılandırma ayarlarını iki kümesi vardır. Merhaba başka bir küme belirli tooa belirli bir güvenilir hizmet ederken bir hello kümedeki tüm güvenilir hizmetler için genel kümesidir.

## <a name="global-configuration"></a>Genel yapılandırma
Merhaba genel güvenilir hizmet yapılandırmasını hello küme bildiriminde hello KtlLogger bölümü altında hello kümesi için belirtilir. Merhaba Günlükçü tarafından kullanılan paylaşılan hello günlük konumu ve boyutu artı hello genel bellek sınırları yapılandırmanızı sağlar. Merhaba küme bildirimi ayarlarını ve tooall düğümlerini ve hello küme Hizmetleri'nde geçerli yapılandırmaları tutan tek bir XML dosyasıdır. Merhaba dosyası genellikle ClusterManifest.xml çağrılır. Gördüğünüz hello Get-ServiceFabricClusterManifest powershell komutunu kullanarak, kümeniz için hello küme bildirimi.

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobayt |8388608 |KB tooallocate hello Günlükçü için çekirdek modunda en az sayıda arabellek bellek havuzu yazma. Bu bellek havuzundaki toodisk yazmadan önce durum bilgilerini önbelleğe almak için kullanılır. |
| WriteBufferMemoryPoolMaximumInKB |Kilobayt |Sınırsız |En büyük boyutu toowhich hello Günlükçü yazma arabelleği bellek havuzundaki büyüyebilir. |
| SharedLogId |GUID |"" |Merhaba SharedLogId hizmet belirli yapılandırmalarında belirtmeyin hello kümedeki tüm düğümlere tüm güvenilir hizmetler tarafından kullanılan hello varsayılan paylaşılan günlük dosyası tanımlamak için benzersiz bir GUID toouse belirtir. SharedLogId belirtilirse, SharedLogPath de belirtilmelidir. |
| SharedLogPath |Tam yol adı |"" |Merhaba hello SharedLogPath hizmet belirli yapılandırmalarında belirtmeyin hello kümedeki tüm düğümlere tüm güvenilir hizmetler tarafından kullanılan günlük dosyası olduğu paylaşılan hello tam yolunu belirtir. SharedLogPath belirtilirse, ancak ardından SharedLogId de belirtilmesi gerekir. |
| SharedLogSizeInMB |Megabayt |8192 |Merhaba numarasını belirtir MB disk alanı toostatically ayırmak için hello paylaşılan günlüğü. Merhaba değeri 2048 veya daha büyük olmalıdır. |

Azure ARM veya şirket içi JSON şablonunu, aşağıdaki hello örnek alır toochange hello hello paylaşılan işlem günlüğü tooback durum bilgisi olan hizmetler için herhangi bir güvenilir koleksiyonu nasıl oluşturulacağını gösterir.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Örnek yerel geliştirici küme bildirim bölümü
Toochange bu yerel geliştirme ortamınızı isterseniz, tooedit hello yerel clustermanifest.xml dosyası gerekir.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Açıklamalar
Merhaba Günlükçü toohello ayrılmış günlük hello güvenilir hizmet çoğaltma ile ilişkili yazılmadan önce durumu verileri önbelleğe alma için kullanılabilir tooall güvenilir hizmetler bir düğümde alınamayan çekirdek bellek gelen ayrılmış bellek genel havuzu vardır. Merhaba havuz boyutu hello WriteBufferMemoryPoolMinimumInKB ve WriteBufferMemoryPoolMaximumInKB ayarları tarafından denetlenir. Her ikisi de bu bellek havuzunun ilk boyutu hello ve hello en düşük boyut toowhich hello bellek havuzundaki küçültülebilir WriteBufferMemoryPoolMinimumInKB belirtir. WriteBufferMemoryPoolMaximumInKB hello en yüksek boyutu toowhich hello bellek havuzundaki büyümesine ' dir. Açılan her güvenilir hizmet çoğaltma tarafından belirlenen sistem tutarı tooWriteBufferMemoryPoolMaximumInKB oluşturan hello bellek havuzu hello boyutunu artırabilir. Kullanılabilenden hello bellek havuzundaki bellek için daha fazla isteğe bağlı ise, istekleri bellek için bellek kullanılabilir oluncaya kadar geciktirilir. Merhaba yazma arabelleği bellek havuzu için belirli bir yapılandırma çok küçük ise, bu nedenle sonra performans düşebilir.

Merhaba SharedLogId ve SharedLogPath ayarlarını her zaman kullanılan birlikte toodefine hello GUID ve hello varsayılan konumu hello kümedeki tüm düğümler için günlük paylaşılan verilebilir. Merhaba varsayılan paylaşılan günlük hello ayarları hello settings.xml hello belirli hizmet belirtmediği tüm güvenilir hizmetler için kullanılır. En iyi performans için paylaşılan günlük dosyaları yalnızca paylaşılan hello günlük dosyası tooreduce Çekişme için kullanılan diskler yerleştirilmelidir.

SharedLogSizeInMB tüm düğümlerde hello varsayılan paylaşılan günlüğü için disk alanı toopreallocate hello miktarını belirtir.  SharedLogId ve SharedLogPath SharedLogSizeInMB toobe belirtilen sırada belirtilen toobe gerekmez.

## <a name="service-specific-configuration"></a>Hizmet belirli yapılandırma
Merhaba yapılandırma paketi (yapılandırma) kullanarak durum bilgisi olan güvenilir hizmetler varsayılan yapılandırmaları değiştirme veya hizmet uygulaması (kod) hello.

* **Config** -hello yapılandırma paketi aracılığıyla yapılandırmaya hello Microsoft Visual Studio Paketi kök hello uygulamadaki her hizmet için hello yapılandırma klasörü altında oluşturulan hello Settings.xml dosyasını değiştirerek gerçekleştirilir.
* **Kod** -kod aracılığıyla yapılandırmaya hello uygun seçenekleri kümesiyle ReliableStateManagerConfiguration nesnesi kullanılarak bir ReliableStateManager oluşturarak gerçekleştirilir.

Varsayılan olarak, hello Azure Service Fabric çalışma zamanı hello Settings.xml dosyasında tanımlanmış bölüm adları arar ve çalışma zamanı bileşenleri için temel alınan hello oluşturulurken hello yapılandırma değerlerini kullanır.

> [!NOTE]
> Yapmak **değil** hizmetinizde kod tooconfigure planlamıyorsanız hello Visual Studio çözümünde oluşturulan hello Settings.xml dosyasını yapılandırmalarında aşağıdaki hello hello bölüm adlarını silin.
> Merhaba yapılandırma paketi veya bölüm adları yeniden adlandırma bir kod değişikliği hello ReliableStateManager yapılandırırken gerektirir.
> 
> 

### <a name="replicator-security-configuration"></a>Çoğaltıcı güvenlik yapılandırması
Çoğaltıcı güvenlik çoğaltma sırasında kullanılan kullanılan toosecure hello iletişim kanalını bağlantılardır. Bu hizmetler yüksek oranda kullanılabilir hale getirileceğini hello verileri de olduğundan emin olmanın birbirlerinin çoğaltma trafiği güvenli mümkün toosee olmayacak anlamına gelir. Varsayılan olarak, bir boş güvenlik yapılandırması bölümü çoğaltma güvenlik engeller.

### <a name="default-section-name"></a>Varsayılan bölüm adı
ReplicatorSecurityConfig

> [!NOTE]
> toochange Bu bölüm adı, bu hizmet için hello ReliableStateManager oluşturulurken geçersiz kılma hello replicatorSecuritySectionName parametresi toohello ReliableStateManagerConfiguration Oluşturucusu.
> 
> 

### <a name="replicator-configuration"></a>Çoğaltıcı yapılandırma
Çoğaltıcı yapılandırmaları hello durum bilgisi olan güvenilir hizmetinin durumunu yüksek oranda güvenilir çoğaltmak ve hello durumu yerel olarak kalıcı yapmaktan sorumlu hello çoğaltıcı yapılandırın.
Merhaba varsayılan yapılandırması hello Visual Studio şablon tarafından oluşturulan ve yeterli olacaktır. Bu bölümde, kullanılabilir tootune hello çoğaltıcı hakkında ek yapılandırmaları açıklanmaktadır.

### <a name="default-section-name"></a>Varsayılan bölüm adı
ReplicatorConfig

> [!NOTE]
> toochange Bu bölüm adı, bu hizmet için hello ReliableStateManager oluşturulurken geçersiz kılma hello replicatorSettingsSectionName parametresi toohello ReliableStateManagerConfiguration Oluşturucusu.
> 
> 

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Saniye |0.015 |Bir dönemde hangi hello çoğaltıcı için geri bildirim toohello birincil göndermeden önce bir işlem aldıktan sonra hello ikincil bekler. Bu aralık dahilinde işlenen işlemleri için gönderilen diğer onayları toobe bir yanıt olarak gönderilir. |
| ReplicatorEndpoint |Yok |Varsayılan yok--gerekli parametre |IP adresi ve birincil/ikincil çoğaltıcı hello bağlantı noktası toocommunicate hello yineleme kümesindeki diğer çoğaltıcılar kullanır. Bu, bir TCP kaynak uç noktası hello hizmet bildiriminde başvuruda bulunmalıdır. Çok başvuran[Service manifest kaynakları](service-fabric-service-manifest-resources.md) tooread bir hizmet bildirimi uç noktası kaynakları tanımlama hakkında daha fazla bilgi. |
| MaxPrimaryReplicationQueueSize |İşlem sayısı |8192 |Merhaba birincil kuyruk işlemlerinde maksimum sayısı. Merhaba birincil çoğaltıcı tüm hello ikincil çoğaltıcılar alındısı sonra bir işlem yukarı serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |
| MaxSecondaryReplicationQueueSize |İşlem sayısı |16384 |Merhaba ikincil sıra işlemlerinde maksimum sayısı. Bir işlem yukarı durumuna Kalıcılık üzerinden yüksek oranda kullanılabilir yaptıktan sonra serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |
| CheckpointThresholdInMB |MB |50 |Sonra hello durumu belirttiğinizde günlük dosyasındaki boş alan miktarı. |
| MaxRecordSizeInKB |KB |1024 |Çoğaltıcı hello kayıt en büyük boyutu hello günlüğüne yazabilir. Bu değer birden fazla 4 ve 16'den büyük olmalıdır. |
| MinLogSizeInMB |MB |0 (belirlenen sistem) |Merhaba işlem günlüğü minimum boyutu. Merhaba günlük tootruncate tooa boyutunun bu ayarı altında izin verilmiyor. 0, o hello çoğaltıcı hello minimum oturum boyutu belirleyecek gösterir. Bu değer artırıldığında kısmi kopyalar ve artımlı yedeklemeler kesilmesine azaltıldığı ilgili günlük kayıtları olasılığını itibaren yapmanın hello olasılığı artar. |
| TruncationThresholdFactor |Faktörü |2 |Hangi hello günlük boyutta kesilmesi tetiklenecek belirler. Kesme eşiği tarafından TruncationThresholdFactor çarpılan MinLogSizeInMB tarafından belirlenir. TruncationThresholdFactor 1'den büyük olmalıdır. MinLogSizeInMB * TruncationThresholdFactor MaxStreamSizeInMB daha az olmalıdır. |
| ThrottlingThresholdFactor |Faktörü |4 |Hangi hello günlük boyutta karşılaşıldığı hello çoğaltma başlar belirler. Azaltma eşiği (MB) cinsinden en büyük tarafından belirlenir ((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)). Azaltma eşiği (MB) cinsinden (MB) cinsinden kesilmesi eşik değerinden büyük olmalıdır. Kesme eşiği (MB) cinsinden MaxStreamSizeInMB daha az olmalıdır. |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |En büyük boyutunu (MB) verilen yedek günlüğü zinciri yedekleme günlüklerinde toplanan. Merhaba artımlı yedekleme birikmiş hello yedekleme günlükleri hello ilgili tam yedekleme toobe bu boyuttan daha büyük itibaren neden olacak bir yedekleme günlüğü oluşturur bir artımlı yedekleme istekleri başarısız olur. Böyle durumlarda, kullanıcı gerekli tootake tam yedekleme ' dir. |
| SharedLogId |GUID |"" |Bu çoğaltma ile kullanılan hello paylaşılan günlük dosyası tanımlamak için benzersiz bir GUID toouse belirtir. Genellikle, hizmetleri, bu ayar kullanmamalısınız. SharedLogId belirtilirse, ancak ardından SharedLogPath de belirtilmesi gerekir. |
| SharedLogPath |Tam yol adı |"" |Bu çoğaltma için paylaşılan günlük dosyası hello oluşturulacağı hello tam yolunu belirtir. Genellikle, hizmetleri, bu ayar kullanmamalısınız. SharedLogPath belirtilirse, ancak ardından SharedLogId de belirtilmesi gerekir. |
| SlowApiMonitoringDuration |Saniye |300 |İzleme aralığı yönetilen API çağrıları için hello ayarlar. Örnek: kullanıcı tarafından sağlanan yedekleme geri çağırma işlevi. Merhaba aralığı geçtikten sonra bir uyarı sistem durumu raporu toohello sistem durumu Yöneticisi gönderilir. |

### <a name="sample-configuration-via-code"></a>Kod aracılığıyla örnek yapılandırma
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Örnek yapılandırma dosyası
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```


### <a name="remarks"></a>Açıklamalar
Çoğaltma gecikmesi BatchAcknowledgementInterval denetler. (Daha fazla bildirim iletileri gerekir gönderilmesine ve işlenen her daha az onayları içeren gibi) '0' değeri sn'ye hello maliyetle hello düşük olası gecikme sonuçlanır.
Merhaba BatchAcknowledgementInterval, büyük hello değeri hello yüksek hello genel yüksek işlem gecikme hello maliyetle çoğaltma işleme. Bu işlem yürütme toohello gecikme doğrudan dönüşür.

CheckpointThresholdInMB denetimleri hello çoğaltıcı hello disk alanı miktarını Hello değeri hello yinelemenin ayrılmış bir günlük dosyasında toostore durum bilgilerini kullanabilirsiniz. Yeni bir çoğaltma toohello kümesi eklendiğinde daha hızlı yeniden yapılandırma süresi Hello varsayılan sonuçlanabilir daha bu tooa daha yüksek değer artırma. Merhaba günlüğünde işlemlerinin daha fazla geçmiş toohello kullanılabilirliği nedeniyle gerçekleşir toohello kısmi durum transfer son budur. Bu gibi durumlarda bu bir çoğaltma hello kurtarma süresi olası kilitlenme sonrasında artırabilir.

Merhaba MaxRecordSizeInKB ayarı hello hello çoğaltıcı tarafından hello günlük dosyasına yazılabilir bir kayıt en büyük boyutunu tanımlar. Çoğu durumda, hello varsayılan 1024-KB kayıt boyutu idealdir. Ancak, Hello hizmeti daha büyük veri öğeleri toobe parçası hello durum bilgilerini neden oluyorsa bu değer artan toobe gerekebilir. Daha küçük kayıtları yalnızca hello küçük kayıt için gereken hello alanı kullanırken, 1024'ten MaxRecordSizeInKB küçülterek az avantajı vardır. Bu değer yalnızca nadir durumlarda değiştirilen toobe gerektiğini bekliyoruz.

Merhaba SharedLogId ve SharedLogPath her zaman kullanılan birlikte toomake hello düğümü için bir hizmet kullanım hello varsayılan paylaşılan günlük ayrı bir paylaşılan günlüğünden ayarlardır. En iyi verimlilik için mümkün olduğunca çok Hizmetleri hello belirtmelidir aynı günlük paylaşılan. Paylaşılan günlük dosyaları yalnızca paylaşılan hello günlük dosyası tooreduce baş taşıma için Çekişme kullanılan diskler yerleştirilmelidir. Bu değer yalnızca nadir durumlarda değiştirilen toobe gerektiğini bekliyoruz.

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric uygulamanızı Visual Studio'da hata ayıklama](service-fabric-debugging-your-application.md)
* [Güvenilir hizmetler için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/dn706529.aspx)

