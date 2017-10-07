---
title: "Azure mikro aaaChange ReliableDictionaryActorStateProvider ayarlarında | Microsoft Docs"
description: "Durum bilgisi olan Azure Service Fabric aktör türü ReliableDictionaryActorStateProvider yapılandırma hakkında bilgi edinin."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Güvenilir aktörler--ReliableDictionaryActorStateProvider yapılandırma
Merhaba Visual Studio Paketi kök hello belirtilen aktör hello yapılandırma klasörü altında oluşturulan hello settings.xml dosyasını değiştirerek ReliableDictionaryActorStateProvider hello varsayılan yapılandırmasını değiştirebilirsiniz.

Hello Azure Service Fabric çalışma zamanı hello settings.xml dosyasında tanımlanmış bölüm adları arar ve çalışma zamanı bileşenleri için temel alınan hello oluşturulurken hello yapılandırma değerlerini kullanır.

> [!NOTE]
> Yapmak **değil** silebilir veya yapılandırmaları hello Visual Studio çözümü oluşturulan hello settings.xml dosyasında aşağıdaki hello hello bölüm adlarını değiştirebilirsiniz.
> 
> 

ReliableDictionaryActorStateProvider hello yapılandırmasını etkileyen genel ayarlar da vardır.

## <a name="global-configuration"></a>Genel yapılandırma
Merhaba genel yapılandırma hello küme bildiriminde hello KtlLogger bölümü altında hello kümesi için belirtilir. Merhaba Günlükçü tarafından kullanılan paylaşılan hello günlük konumu ve boyutu artı hello genel bellek sınırları yapılandırmanızı sağlar. Değişiklikleri hello küme bildiriminde ReliableDictionaryActorStateProvider kullanan tüm hizmetleri ve durum bilgisi olan güvenilir hizmetler etkileyeceğini unutmayın.

Merhaba küme bildirimi ayarlarını ve tooall düğümlerini ve hello küme Hizmetleri'nde geçerli yapılandırmaları tutan tek bir XML dosyasıdır. Merhaba dosyası genellikle ClusterManifest.xml çağrılır. Gördüğünüz hello Get-ServiceFabricClusterManifest powershell komutunu kullanarak, kümeniz için hello küme bildirimi.

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobayt |8388608 |KB tooallocate hello Günlükçü için çekirdek modunda en az sayıda arabellek bellek havuzu yazma. Bu bellek havuzundaki toodisk yazmadan önce durum bilgilerini önbelleğe almak için kullanılır. |
| WriteBufferMemoryPoolMaximumInKB |Kilobayt |Sınırsız |En büyük boyutu toowhich hello Günlükçü yazma arabelleği bellek havuzundaki büyüyebilir. |
| SharedLogId |GUID |"" |Merhaba SharedLogId hizmet belirli yapılandırmalarında belirtmeyin hello kümedeki tüm düğümlere tüm güvenilir hizmetler tarafından kullanılan hello varsayılan paylaşılan günlük dosyası tanımlamak için benzersiz bir GUID toouse belirtir. SharedLogId belirtilirse, SharedLogPath de belirtilmelidir. |
| SharedLogPath |Tam yol adı |"" |Merhaba hello SharedLogPath hizmet belirli yapılandırmalarında belirtmeyin hello kümedeki tüm düğümlere tüm güvenilir hizmetler tarafından kullanılan günlük dosyası olduğu paylaşılan hello tam yolunu belirtir. SharedLogPath belirtilirse, ancak ardından SharedLogId de belirtilmesi gerekir. |
| SharedLogSizeInMB |Megabayt |8192 |Merhaba numarasını belirtir MB disk alanı toostatically ayırmak için hello paylaşılan günlüğü. Merhaba değeri 2048 veya daha büyük olmalıdır. |

### <a name="sample-cluster-manifest-section"></a>Örnek Küme bildirim bölümü
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Açıklamalar
Merhaba Günlükçü toohello ayrılmış günlük hello güvenilir hizmet çoğaltma ile ilişkili yazılmadan önce durumu verileri önbelleğe alma için kullanılabilir tooall güvenilir hizmetler bir düğümde alınamayan çekirdek bellek gelen ayrılmış bellek genel havuzu vardır. Merhaba havuz boyutu hello WriteBufferMemoryPoolMinimumInKB ve WriteBufferMemoryPoolMaximumInKB ayarları tarafından denetlenir. Her ikisi de bu bellek havuzunun ilk boyutu hello ve hello en düşük boyut toowhich hello bellek havuzundaki küçültülebilir WriteBufferMemoryPoolMinimumInKB belirtir. WriteBufferMemoryPoolMaximumInKB hello en yüksek boyutu toowhich hello bellek havuzundaki büyümesine ' dir. Açılan her güvenilir hizmet çoğaltma tarafından belirlenen sistem tutarı tooWriteBufferMemoryPoolMaximumInKB oluşturan hello bellek havuzu hello boyutunu artırabilir. Kullanılabilenden hello bellek havuzundaki bellek için daha fazla isteğe bağlı ise, istekleri bellek için bellek kullanılabilir oluncaya kadar geciktirilir. Merhaba yazma arabelleği bellek havuzu için belirli bir yapılandırma çok küçük ise, bu nedenle sonra performans düşebilir.

Merhaba SharedLogId ve SharedLogPath ayarlarını her zaman kullanılan birlikte toodefine hello GUID ve hello varsayılan konumu hello kümedeki tüm düğümler için günlük paylaşılan verilebilir. Merhaba varsayılan paylaşılan günlük hello ayarları hello settings.xml hello belirli hizmet belirtmediği tüm güvenilir hizmetler için kullanılır. En iyi performans için paylaşılan günlük dosyaları yalnızca paylaşılan hello günlük dosyası tooreduce Çekişme için kullanılan diskler yerleştirilmelidir.

SharedLogSizeInMB tüm düğümlerde hello varsayılan paylaşılan günlüğü için disk alanı toopreallocate hello miktarını belirtir.  SharedLogId ve SharedLogPath SharedLogSizeInMB toobe belirtilen sırada belirtilen toobe gerekmez.

## <a name="replicator-security-configuration"></a>Çoğaltıcı güvenlik yapılandırması
Çoğaltıcı güvenlik çoğaltma sırasında kullanılan kullanılan toosecure hello iletişim kanalını bağlantılardır. Bunun anlamı Hizmetleri birbirlerinin çoğaltma trafiğini göremiyorum, yüksek oranda kullanılabilir hale getirileceğini sağlama hello verileri de güvenlidir.
Varsayılan olarak, bir boş güvenlik yapılandırması bölümü çoğaltma güvenlik engeller.

### <a name="section-name"></a>Bölüm adı
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Çoğaltıcı yapılandırma
Çoğaltıcı, hello aktör durumu sağlayıcısı durumu yüksek oranda güvenilir çoğaltmak ve hello durumu yerel olarak kalıcı yapmaktan sorumlu kullanılan tooconfigure hello çoğaltıcı bağlantılardır.
Merhaba varsayılan yapılandırması hello Visual Studio şablon tarafından oluşturulan ve yeterli olacaktır. Bu bölümde, kullanılabilir tootune hello çoğaltıcı hakkında ek yapılandırmaları açıklanmaktadır.

### <a name="section-name"></a>Bölüm adı
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Saniye |0.015 |Bir dönemde hangi hello çoğaltıcı için geri bildirim toohello birincil göndermeden önce bir işlem aldıktan sonra hello ikincil bekler. Bu aralık dahilinde işlenen işlemleri için gönderilen diğer onayları toobe bir yanıt olarak gönderilir. |
| ReplicatorEndpoint |Yok |Varsayılan yok--gerekli parametre |IP adresi ve birincil/ikincil çoğaltıcı hello bağlantı noktası toocommunicate hello yineleme kümesindeki diğer çoğaltıcılar kullanır. Bu, bir TCP kaynak uç noktası hello hizmet bildiriminde başvuruda bulunmalıdır. Çok başvuran[Service manifest kaynakları](service-fabric-service-manifest-resources.md) tooread endpoint kaynakları hizmet bildiriminde tanımlama hakkında daha fazla bilgi. |
| MaxReplicationMessageSize |Bayt |50 MB |Tek bir iletiye iletilen çoğaltma verilerinin en büyük boyutu. |
| MaxPrimaryReplicationQueueSize |İşlem sayısı |8192 |Merhaba birincil kuyruk işlemlerinde maksimum sayısı. Merhaba birincil çoğaltıcı tüm hello ikincil çoğaltıcılar alındısı sonra bir işlem yukarı serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |
| MaxSecondaryReplicationQueueSize |İşlem sayısı |16384 |Merhaba ikincil sıra işlemlerinde maksimum sayısı. Bir işlem yukarı durumuna Kalıcılık üzerinden yüksek oranda kullanılabilir yaptıktan sonra serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |
| CheckpointThresholdInMB |MB |200 |Sonra hello durumu belirttiğinizde günlük dosyasındaki boş alan miktarı. |
| MaxRecordSizeInKB |KB |1024 |Çoğaltıcı hello kayıt en büyük boyutu hello günlüğüne yazabilir. Bu değer birden fazla 4 ve 16'den büyük olmalıdır. |
| OptimizeLogForLowerDiskUsage |Boole değeri |TRUE |Doğru olduğunda, hello günlük Hello yinelemenin ayrılmış günlük dosyası bir NTFS seyrek dosya kullanılarak oluşturulan şekilde yapılandırılır. Hello dosya için hello gerçek disk alanı kullanımını azaltır. Yanlış olduğunda, hello dosyası hello iyi yazma performansı sağlamak sabit ayırma ile oluşturulur. |
| SharedLogId |GUID |"" |Bu çoğaltma ile kullanılan hello paylaşılan günlük dosyası tanımlamak için benzersiz bir GUID toouse belirtir. Genellikle, hizmetleri, bu ayar kullanmamalısınız. SharedLogId belirtilirse, ancak ardından SharedLogPath de belirtilmesi gerekir. |
| SharedLogPath |Tam yol adı |"" |Bu çoğaltma için paylaşılan günlük dosyası hello oluşturulacağı hello tam yolunu belirtir. Genellikle, hizmetleri, bu ayar kullanmamalısınız. SharedLogPath belirtilirse, ancak ardından SharedLogId de belirtilmesi gerekir. |

## <a name="sample-configuration-file"></a>Örnek yapılandırma dosyası
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
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

## <a name="remarks"></a>Açıklamalar
Merhaba BatchAcknowledgementInterval parametre çoğaltma gecikmesi denetler. (Daha fazla bildirim iletileri gerekir gönderilmesine ve işlenen her daha az onayları içeren gibi) '0' değeri sn'ye hello maliyetle hello düşük olası gecikme sonuçlanır.
Merhaba BatchAcknowledgementInterval, büyük hello değeri hello yüksek hello genel yüksek işlem gecikme hello maliyetle çoğaltma işleme. Bu işlem yürütme toohello gecikme doğrudan dönüşür.

Merhaba CheckpointThresholdInMB parametresi denetimleri hello çoğaltıcı hello disk alanı miktarını hello yinelemenin ayrılmış bir günlük dosyasında toostore durum bilgilerini kullanabilirsiniz. Yeni bir çoğaltma toohello kümesi eklendiğinde daha hızlı yeniden yapılandırma süresi Hello varsayılan sonuçlanabilir daha bu tooa daha yüksek değer artırma. Merhaba günlüğünde işlemlerinin daha fazla geçmiş toohello kullanılabilirliği nedeniyle gerçekleşir toohello kısmi durum transfer son budur. Bu gibi durumlarda bu bir çoğaltma hello kurtarma süresi olası kilitlenme sonrasında artırabilir.

OptimizeForLowerDiskUsage tootrue ayarlarsanız, etkin olmayan çoğaltmalar daha az disk alanı kullanırken etkin çoğaltmaları günlük dosyalarına daha fazla durum bilgilerini depolayabileceğiniz günlük dosyası alanının aşırı sağlanan olacaktır. Bu, olası toohost kolaylaştırır bir düğüm üzerinde daha fazla yineleme. OptimizeForLowerDiskUsage toofalse ayarlarsanız, hello durum bilgilerini toohello günlük dosyalarını daha hızlı yazılır.

Merhaba MaxRecordSizeInKB ayarı hello hello çoğaltıcı tarafından hello günlük dosyasına yazılabilir bir kayıt en büyük boyutunu tanımlar. Çoğu durumda, hello varsayılan 1024-KB kayıt boyutu idealdir. Ancak, Hello hizmeti daha büyük veri öğeleri toobe parçası hello durum bilgilerini neden oluyorsa bu değer artan toobe gerekebilir. Daha küçük kayıtları yalnızca hello küçük kayıt için gereken hello alanı kullanırken, 1024'ten MaxRecordSizeInKB küçülterek az avantajı vardır. Bu değer yalnızca nadir durumlarda değiştirilen toobe gerektiğini bekliyoruz.

Merhaba SharedLogId ve SharedLogPath her zaman kullanılan birlikte toomake hello düğümü için bir hizmet kullanım hello varsayılan paylaşılan günlük ayrı bir paylaşılan günlüğünden ayarlardır. En iyi verimlilik için mümkün olduğunca çok Hizmetleri hello belirtmelidir aynı günlük paylaşılan. Paylaşılan günlük dosyaları yalnızca hello paylaşılan günlük dosyası için tooreduce baş taşıma Çekişme kullanılan diskler yerleştirilmelidir. Bu değerleri yalnızca nadir durumlarda değiştirilen toobe gerektiğini bekliyoruz.

