---
title: "Azure mikro aaaChange KVSActorStateProvider ayarlarında | Microsoft Docs"
description: "Durum bilgisi olan Azure Service Fabric aktör türü KVSActorStateProvider yapılandırma hakkında bilgi edinin."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Güvenilir aktörler--KVSActorStateProvider yapılandırma
Merhaba Microsoft Visual Studio Paketi kök hello belirtilen aktör hello yapılandırma klasörü altında oluşturulan hello settings.xml dosyasını değiştirerek KVSActorStateProvider hello varsayılan yapılandırmasını değiştirebilirsiniz.

Hello Azure Service Fabric çalışma zamanı hello settings.xml dosyasında tanımlanmış bölüm adları arar ve çalışma zamanı bileşenleri için temel alınan hello oluşturulurken hello yapılandırma değerlerini kullanır.

> [!NOTE]
> Yapmak **değil** silebilir veya yapılandırmaları hello Visual Studio çözümü oluşturulan hello settings.xml dosyasında aşağıdaki hello hello bölüm adlarını değiştirebilirsiniz.
> 
> 

## <a name="replicator-security-configuration"></a>Çoğaltıcı güvenlik yapılandırması
Çoğaltıcı güvenlik çoğaltma sırasında kullanılan kullanılan toosecure hello iletişim kanalını bağlantılardır. Bu hizmetler yüksek oranda kullanılabilir hale getirileceğini hello verileri de güvenli olduğundan emin olmanın birbirlerinin çoğaltma trafiği, göremeyeceği anlamına gelir.
Varsayılan olarak, bir boş güvenlik yapılandırması bölümü çoğaltma güvenlik engeller.

### <a name="section-name"></a>Bölüm adı
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Çoğaltıcı yapılandırma
Çoğaltıcı yapılandırmaları hello aktör durumu sağlayıcısı durumu yüksek oranda güvenilir yapmaktan sorumlu hello çoğaltıcı yapılandırın.
Merhaba varsayılan yapılandırması hello Visual Studio şablon tarafından oluşturulan ve yeterli olacaktır. Bu bölümde, kullanılabilir tootune hello çoğaltıcı hakkında ek yapılandırmaları açıklanmaktadır.

### <a name="section-name"></a>Bölüm adı
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Saniye |0.015 |Bir dönemde hangi hello çoğaltıcı için geri bildirim toohello birincil göndermeden önce bir işlem aldıktan sonra hello ikincil bekler. Bu aralık dahilinde işlenen işlemleri için gönderilen diğer onayları toobe bir yanıt olarak gönderilir. |
| ReplicatorEndpoint |Yok |Varsayılan yok--gerekli parametre |IP adresi ve birincil/ikincil çoğaltıcı hello bağlantı noktası toocommunicate hello yineleme kümesindeki diğer çoğaltıcılar kullanır. Bu, bir TCP kaynak uç noktası hello hizmet bildiriminde başvuruda bulunmalıdır. Çok başvuran[Service manifest kaynakları](service-fabric-service-manifest-resources.md) tooread endpoint kaynakları hello hizmet bildiriminde tanımlama hakkında daha fazla bilgi. |
| Retryınterval |Saniye |5 |Hangi hello çoğaltıcı yeniden aktaran bir işlem için bir onay almazsa iletisi sonra süre. |
| MaxReplicationMessageSize |Bayt |50 MB |Tek bir iletiye iletilen çoğaltma verilerinin en büyük boyutu. |
| MaxPrimaryReplicationQueueSize |İşlem sayısı |1024 |Merhaba birincil kuyruk işlemlerinde maksimum sayısı. Merhaba birincil çoğaltıcı tüm hello ikincil çoğaltıcılar alındısı sonra bir işlem yukarı serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |
| MaxSecondaryReplicationQueueSize |İşlem sayısı |2048 |Merhaba ikincil sıra işlemlerinde maksimum sayısı. Bir işlem yukarı durumuna Kalıcılık üzerinden yüksek oranda kullanılabilir yaptıktan sonra serbest bırakılır. Bu değer 64 ve 2'in büyük olmalıdır. |

## <a name="store-configuration"></a>Depolama yapılandırması
Mağaza, çoğaltılmakta olan kullanılan toopersist hello durumu kullanılan tooconfigure hello yerel deposu bağlantılardır.
Merhaba varsayılan yapılandırması hello Visual Studio şablon tarafından oluşturulan ve yeterli olacaktır. Bu bölümde, kullanılabilir tootune hello yerel deposu hakkında ek yapılandırmaları açıklanmaktadır.

### <a name="section-name"></a>Bölüm adı
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Yapılandırma adları
| Ad | Birim | Varsayılan değer | Açıklamalar |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |milisaniye |200 |Dayanıklı yerel depo yürütme için aralığı toplu işleme hello maksimum ayarlar. |
| MaxVerPages |Sayfa sayısı |16384 |Merhaba yerel sürüm sayfalarına Hello sayısının veritabanına depolar. Bekleyen işlemlerin hello sayısını belirler. |

## <a name="sample-configuration-file"></a>Örnek yapılandırma dosyası
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
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

