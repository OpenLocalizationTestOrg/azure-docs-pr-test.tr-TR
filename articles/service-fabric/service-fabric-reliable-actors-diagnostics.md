---
title: "aaaActors tanılama ve izleme | Microsoft Docs"
description: "Bu makalede hello tanılama ve performans izleme hello olaylar ve performans sayaçları tarafından gösterilen dahil olmak üzere hello Service Fabric Reliable Actors çalışma zamanında özelliklerini açıklar."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Reliable Actors için tanılama ve performans izlemesi
Merhaba Reliable Actors çalışma zamanı yayar [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) olayları ve [performans sayaçları](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Bunlar hello çalışma zamanı nasıl çalıştığını içine bilgiler ve sorun giderme ve performans izleme ile yardımcı.

## <a name="eventsource-events"></a>EventSource olaylarını
Merhaba EventSource sağlayıcısı hello Reliable Actors çalışma zamanı için "Microsoft-ServiceFabric-aktörler" adıdır. Bu olay kaynağı olaylarından görünür hello [tanılama olayları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) hello aktör uygulama yüklenirken pencere [Visual Studio'da hata ayıklaması](service-fabric-debugging-your-application.md).

Araçlar ve toplama ve/veya EventSource olaylarını görüntüleme içinde yardımcı teknolojiler örnekleri [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md), [semantik günlük](https://msdn.microsoft.com/library/dn774980.aspx)ve hello [ Microsoft TraceEvent Kitaplığı](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Anahtar sözcükler
Güvenilir aktörler EventSource toohello ait tüm olayları bir veya daha fazla ile ilişkili anahtar sözcükler. Bu, toplanan olayları filtreleme sağlar. anahtar sözcüğü BITS aşağıdaki hello tanımlanır.

| bit | Açıklama |
| --- | --- |
| 0x1 |Merhaba işlemi hello Fabric aktör zamanının özetleyen önemli olaylar ayarlayın. |
| 0x2 |Aktör yöntem çağrılarını açıklayan olaylar kümesi. Daha fazla bilgi için bkz: Merhaba [aktörler giriş konuda](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Olaylar ilgili tooactor durumunu ayarlayın. Daha fazla bilgi için hello üzerinde konusuna [aktör durum yönetimi](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Olaylar ilgili tooturn tabanlı eşzamanlılık hello aktör kümesi. Daha fazla bilgi için hello üzerinde konusuna [eşzamanlılık](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Performans sayaçları
Merhaba Reliable Actors çalışma zamanı performans sayacı kategorileri aşağıdaki hello tanımlar.

| Kategori | Açıklama |
| --- | --- |
| Service Fabric aktör |Belirli tooAzure Service Fabric aktör, örneğin toosave aktör durumunun geçen süre sayaçları |
| Service Fabric aktör metodu |Örneğin Service Fabric aktör tarafından uygulanan belirli toomethods sayaçları ne sıklıkta bir aktör yöntemi çağrılır |

Merhaba kategorileri yukarıda her bir veya daha fazla sayaca sahiptir.

Merhaba [Windows Performans İzleyicisi'ni](https://technet.microsoft.com/library/cc749249.aspx) varsayılan hello Windows işletim sisteminde kullanılabilir uygulama kullanılan toocollect ve görünüm performans sayacı verilerini olabilir. [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) performans sayaç verileri toplayan ve tooAzure tabloları karşıya yükleme için başka bir seçenektir.

### <a name="performance-counter-instance-names"></a>Performans sayacı örneği adları
Çok sayıda aktör Hizmetleri veya aktör hizmeti bölümleri olan bir küme, çok sayıda aktör performans sayacı örnekleri sahip olur. Hello performans sayacı örneği adları hello özel tanımlanmasına yardımcı olabilecek [bölüm](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) ve aktör yöntemi (varsa) bu hello performans sayacı örneği ilişkilendirilmiştir.

#### <a name="service-fabric-actor-category"></a>Service Fabric aktör kategorisi
Merhaba kategorisi için `Service Fabric Actor`, hello sayaç örneği adlardır, biçim şu hello:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* hello dize performans sayacı örneği hello Service Fabric bölüm kimliği ile ilişkili hello gösterimidir. Merhaba bölüm kimliği bir GUID olan ve dize gösterimi hello oluşturulan [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) biçim belirticisi "D" yöntemiyle.

*ActorRuntimeInternalID* hello dize iç kullanımı için hello Fabric aktör çalışma zamanı tarafından oluşturulan bir 64-bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

Merhaba toohello ait bir sayacın sayaç örneği adı örneği aşağıdadır `Service Fabric Actor` kategorisi:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

Yukarıdaki hello örnekte `2740af29-78aa-44bc-a20b-7e60fb783264` hello Service Fabric bölüm kimliği, hello dize gösterimi ise ve `635650083799324046` hello çalışma zamanı iç için oluşturan hello 64-bit kimliği kullanın.

#### <a name="service-fabric-actor-method-category"></a>Service Fabric aktör metodu kategorisi
Merhaba kategorisi için `Service Fabric Actor Method`, hello sayaç örneği adlardır, biçim şu hello:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* performans sayacı örneği hello hello aktör yönteminin hello adı ile ilişkili değil. Merhaba yöntemi adı Hello biçiminde hello performans sayacı örneği adları en fazla uzunluğu hello kısıtlamalar Windows hello adıyla hello okunabilirliğini dengeleyen hello Fabric aktör çalışma zamanında bazı mantığı göre belirlenir.

*ActorsRuntimeMethodId* hello dize iç kullanımı için hello Fabric aktör çalışma zamanı tarafından oluşturulan bir 32 bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

*ServiceFabricPartitionID* hello dize performans sayacı örneği hello Service Fabric bölüm kimliği ile ilişkili hello gösterimidir. Merhaba bölüm kimliği bir GUID olan ve dize gösterimi hello oluşturulan [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) biçim belirticisi "D" yöntemiyle.

*ActorRuntimeInternalID* hello dize iç kullanımı için hello Fabric aktör çalışma zamanı tarafından oluşturulan bir 64-bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

Merhaba toohello ait bir sayacın sayaç örneği adı örneği aşağıdadır `Service Fabric Actor Method` kategorisi:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

Yukarıdaki hello örnekte `ivoicemailboxactor.leavemessageasync` hello yöntem adı `2` hello çalışma zamanı iç için oluşturulan 32-bit Kimliğini kullanın, hello olan `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello Service Fabric bölüm kimliği, hello dize gösterimi ise ve `635650083804480486` hello 64-bit kimliği Başlangıç zamanının iç kullanım için oluşturulur.

## <a name="list-of-events-and-performance-counters"></a>Olaylar ve performans sayaçları listesi
### <a name="actor-method-events-and-performance-counters"></a>Aktör yöntemi olaylar ve performans sayaçları
Merhaba Reliable Actors çalışma zamanı yayar çok ilgili olayları aşağıdaki hello[aktör yöntemleri](service-fabric-reliable-actors-introduction.md).

| Olay adı | Olay Kimliği | Düzey | Anahtar sözcüğü | Açıklama |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Ayrıntılı |0x2 |Aktör çalışma zamanı hakkında tooinvoke bir aktör yöntemidir. |
| ActorMethodStop |8 |Ayrıntılı |0x2 |Aktör yöntemi yürütülmesi tamamlandı. Diğer bir deyişle, başlangıç zamanının zaman uyumsuz çağrı toohello aktör yöntemi döndürdü ve hello aktör yöntemi tarafından döndürülen hello görevi tamamlandı. |
| ActorMethodThrewException |9 |Uyarı |0x3 |Aktör yöntemi hello yürütülmesi sırasında hello zamanının zaman uyumsuz çağrı toohello aktör yöntemi sırasında veya hello görev hello yürütülmesi sırasında hello aktör yöntemi tarafından döndürülen özel durum oluştu. Bu olay araştırma gerektiren hello aktör kodda hata çeşit gösterir. |

Merhaba Reliable Actors çalışma zamanı performans sayaçları ilgili toohello aktör yöntemleri yürütülmesinin hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric aktör metodu |Çağrıları/sn |Merhaba aktör hizmeti metodunu saniye başına çağrılma sayısı |
| Service Fabric aktör metodu |Çağrı başına ortalama milisaniye |Geçen süre tooexecute hello aktör hizmeti metodunu milisaniye |
| Service Fabric aktör metodu |Oluşturulan özel durum/sn |Aktör hizmeti metodunu hello sayısını saniye başına özel durum oluşturdu |

### <a name="concurrency-events-and-performance-counters"></a>Eşzamanlılık olaylar ve performans sayaçları
Merhaba Reliable Actors çalışma zamanı yayar çok ilgili olayları aşağıdaki hello[eşzamanlılık](service-fabric-reliable-actors-introduction.md#concurrency).

| Olay adı | Olay Kimliği | Düzey | Anahtar sözcüğü | Açıklama |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Ayrıntılı |0x8 |Bu olay, her yeni bir aktör sırayla hello başlangıcı sırasında yazılır. Bırakma tabanlı eşzamanlılık uygulayan tooacquire hello başına kilit almayı bekleyen aktör çağrısı sayısı bekleyen hello sayısını içerir. |

Merhaba Reliable Actors çalışma zamanı performans sayaçları ilgili tooconcurrency aşağıdaki hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric aktör |Aktör kilidi için bekleyen aktör çağrısı sayısı |Bırakma tabanlı eşzamanlılık uygulayan tooacquire hello başına kilit almayı bekleyen aktör çağrısı sayısı bekleyen sayısı |
| Service Fabric aktör |Kilit bekleme işlemi başına ortalama süre (milisaniye) |Bırakma tabanlı eşzamanlılık zorlar süresi (milisaniye cinsinden) çekildiği tooacquire hello aktör başına kilit |
| Service Fabric aktör |Aktör kilidinin ortalama tutulma süresi (milisaniye) |Hangi Merhaba aktör başına kilit tutulan süre (milisaniye cinsinden) |

### <a name="actor-state-management-events-and-performance-counters"></a>Aktör durumunu yönetim olaylar ve performans sayaçları
Merhaba Reliable Actors çalışma zamanı yayar çok ilgili olayları aşağıdaki hello[aktör durum yönetimi](service-fabric-reliable-actors-state-management.md).

| Olay adı | Olay Kimliği | Düzey | Anahtar sözcüğü | Açıklama |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Ayrıntılı |0x4 |Aktör çalışma zamanı toosave hello aktör hakkında durumudur. |
| ActorSaveStateStop |11 |Ayrıntılı |0x4 |Aktör çalışma zamanı hello aktör durumunu kaydetmek bitirdi. |

Merhaba Reliable Actors çalışma zamanı performans sayaçları ilgili tooactor durum yönetimi aşağıdaki hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric aktör |Durum kaydetme işlemi başına ortalama süre (milisaniye) |Milisaniye cinsinden toosave aktör durumunun harcanan süre |
| Service Fabric aktör |Durum yükleme işlemi başına ortalama süre (milisaniye) |Milisaniye cinsinden tooload aktör durumunun harcanan süre |

### <a name="events-related-tooactor-replicas"></a>Olaylar ilgili tooactor çoğaltmaları
Merhaba Reliable Actors çalışma zamanı yayar çok ilgili olayları aşağıdaki hello[aktör çoğaltmaları](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Olay adı | Olay Kimliği | Düzey | Anahtar sözcüğü | Açıklama |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Bilgilendirme |0x1 |Aktör çoğaltma rolü tooPrimary değiştirildi. Bu, bu bölüm hello aktörler Bu çoğaltma içinde oluşturulacak anlamına gelir. |
| ReplicaChangeRoleFromPrimary |2 |Bilgilendirme |0x1 |Aktör çoğaltma rolü toonon birincil değiştirildi. Bu, bu bölüm hello aktörler içinde bu çoğaltma artık oluşturulacak anlamına gelir. Yeni İstek zaten bu çoğaltma içinde oluşturulan tooactors teslim edilecek. Tüm Süren istekleri tamamlandıktan sonra hello aktörler yok. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Aktör etkinleştirme ve devre dışı bırakma olaylar ve performans sayaçları
Merhaba Reliable Actors çalışma zamanı yayar çok ilgili olayları aşağıdaki hello[aktör etkinleştirme ve devre dışı bırakma](service-fabric-reliable-actors-lifecycle.md).

| Olay adı | Olay Kimliği | Düzey | Anahtar sözcüğü | Açıklama |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Bilgilendirme |0x1 |Bir oyuncu etkinleştirildi. |
| ActorDeactivated |6 |Bilgilendirme |0x1 |Bir oyuncu devre dışı bırakıldı. |

Merhaba Reliable Actors çalışma zamanı yayımlar hello performans sayaçlarını izleyerek ilgili tooactor etkinleştirme ve devre dışı bırakma.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric aktör |Ortalama OnActivateAsync milisaniye |Milisaniye cinsinden tooexecute OnActivateAsync metodunun harcanan süre |

### <a name="actor-request-processing-performance-counters"></a>Aktör isteği işleme performans sayaçları
Bir istemci bir aktör proxy nesnesi yöntemiyle çalıştırdığında, hello ağ toohello aktör hizmeti üzerinden gönderilen bir istek iletisi sonuçlanır. Merhaba hizmeti hello İstek iletisini işler ve bir yanıtı geri toohello istemci gönderir. Merhaba Reliable Actors çalışma zamanı performans sayaçları ilgili tooactor isteği işleme aşağıdaki hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric aktör |Beklemedeki istek sayısı |Merhaba hizmetinde işlenmekte olan istek sayısı |
| Service Fabric aktör |İstek başına ortalama milisaniye |(Milisaniye cinsinden) bir istek hello hizmet tooprocess tarafından harcanan süre |
| Service Fabric aktör |İsteğin seri durumdan çıkarılması için geçen ortalama süre (milisaniye) |Merhaba hizmeti tarafından alındığında süresi (milisaniye cinsinden) çekildiği toodeserialize aktör istek iletisi |
| Service Fabric aktör |Yanıtın serileştirilmesi için geçen ortalama süre (milisaniye) |Süre (milisaniye cinsinden) çekildiği tooserialize hello aktör yanıt iletisi hello yanıt toohello istemci gönderilmeden önce hello hizmetine |

## <a name="next-steps"></a>Sonraki adımlar
* [Reliable Actors hello Service Fabric platformundan kullanma](service-fabric-reliable-actors-platform.md)
* [Aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Örnek kod](https://github.com/Azure/servicefabric-samples)
* [PerfView EventSource sağlayıcıları](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
