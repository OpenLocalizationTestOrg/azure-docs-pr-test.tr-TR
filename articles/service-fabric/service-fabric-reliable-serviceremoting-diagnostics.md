---
title: "aaaAzure ServiceFabric tanılama ve izleme | Microsoft Docs"
description: "Bu makalede, performans sayaçları tarafından gösterilen gibi hello Service Fabric güvenilir ServiceRemoting çalışma zamanında hello performans izleme özelliklerini açıklar."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Tanılama ve güvenilir hizmeti uzaktan iletişim için performans izleme
Merhaba güvenilir ServiceRemoting çalışma zamanı yayar [performans sayaçları](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Bunlar hello ServiceRemoting nasıl çalıştığını içine bilgiler ve sorun giderme ve performans izleme ile yardımcı.


## <a name="performance-counters"></a>Performans sayaçları
Merhaba güvenilir ServiceRemoting çalışma zamanı performans sayacı kategorileri aşağıdaki hello tanımlar:

| Kategori | Açıklama |
| --- | --- |
| Yapı Hizmeti |Belirli tooAzure Service Fabric hizmeti Remoting sayaçları, örneğin, geçen ortalama süre tooprocess istek |
| Service Fabric hizmeti yöntemi |Sayaçları belirli toomethods ne sıklıkta bir hizmet yöntemi çağrılır doku uzaktan iletişim hizmeti tarafından Örneğin, uygulanmadı. |

Her kategori önceki hello bir veya daha fazla sayaca sahiptir.

Merhaba [Windows Performans İzleyicisi'ni](https://technet.microsoft.com/library/cc749249.aspx) varsayılan hello Windows işletim sisteminde kullanılabilir uygulama kullanılan toocollect ve görünüm performans sayacı verilerini olabilir. [Azure tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) performans sayaç verileri toplayan ve tooAzure tabloları karşıya yükleme için başka bir seçenektir.

### <a name="performance-counter-instance-names"></a>Performans sayacı örneği adları
Çok sayıda ServiceRemoting Hizmetleri veya bölümleri olan bir küme, çok sayıda performans sayacı örnekleri vardır. Bu hello performans sayacı örneği ilişkili hello performans sayacı örneği adları hello belirli bir bölüm ve hizmet yöntemi (varsa) belirlemenize yardımcı olabilir.

#### <a name="service-fabric-service-category"></a>Service Fabric hizmeti kategorisi
Merhaba kategorisi için `Service Fabric Service`, hello sayaç örneği adlardır, biçim şu hello:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* hello dize performans sayacı örneği hello Service Fabric bölüm kimliği ile ilişkili hello gösterimidir. Merhaba bölüm kimliği bir GUID olan ve dize gösterimi hello oluşturulan [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) biçim belirticisi "D" yöntemiyle.

*ServiceReplicaOrInstanceId* hello dize performans sayacı örneği hello Service Fabric çoğaltma/örnek kimliği ile ilişkili hello gösterimidir.

*ServiceRuntimeInternalID* hello dize iç kullanımı için hello Fabric hizmeti çalışma zamanı tarafından oluşturulan bir 64-bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

Merhaba toohello ait bir sayacın sayaç örneği adı örneği aşağıdadır `Service Fabric Service` kategorisi:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Örnek, önceki hello içinde `2740af29-78aa-44bc-a20b-7e60fb783264` hello dize hello Service Fabric bölüm kimliği, gösterimidir `635650083799324046` çoğaltma/InstanceId dize gösterimidir ve `5008379932` hello çalışma zamanı iç için oluşturan hello 64-bit kimliği kullanın.

#### <a name="service-fabric-service-method-category"></a>Service Fabric hizmeti yöntemi kategorisi
Merhaba kategorisi için `Service Fabric Service Method`, hello sayaç örneği adlardır, biçim şu hello:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* performans sayacı örneği hello hello hizmet yönteminin hello adı ile ilişkili değil. hello yöntemi adı Hello biçiminde hello performans sayacı örneği adları en fazla uzunluğu hello kısıtlamalar Windows hello adıyla hello okunabilirliğini dengeleyen hello Fabric hizmeti çalışma zamanı bazı mantığında göre belirlenir.

*ServiceRuntimeMethodId* hello dize iç kullanımı için hello Fabric hizmeti çalışma zamanı tarafından oluşturulan bir 32 bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

*ServiceFabricPartitionID* hello dize performans sayacı örneği hello Service Fabric bölüm kimliği ile ilişkili hello gösterimidir. Merhaba bölüm kimliği bir GUID olan ve dize gösterimi hello oluşturulan [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) biçim belirticisi "D" yöntemiyle.

*ServiceReplicaOrInstanceId* hello dize performans sayacı örneği hello Service Fabric çoğaltma/örnek kimliği ile ilişkili hello gösterimidir.

*ServiceRuntimeInternalID* hello dize iç kullanımı için hello Fabric hizmeti çalışma zamanı tarafından oluşturulan bir 64-bit tamsayı gösterimidir. Bu eklenmiştir hello performans sayacı örneği benzersizliğini tooensure adlandırın ve diğer performans sayacı örneği adları çakışıyor kaçının. Kullanıcıların toointerpret hello performans sayacı örneği adı bu kısmı denemelisiniz değil.

Merhaba toohello ait bir sayacın sayaç örneği adı örneği aşağıdadır `Service Fabric Service Method` kategorisi:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Örnek, önceki hello içinde `ivoicemailboxservice.leavemessageasync` hello yöntem adı `2` hello çalışma zamanı iç için oluşturulan 32-bit Kimliğini kullanın, hello olan `89383d32-e57e-4a9b-a6ad-57c6792aa521` hello dize hello Service Fabric bölüm kimliği, gösterimidir`635650083804480486` hello dizesi Merhaba Service Fabric çoğaltma/örnek kimliği gösterimini ve `5008380` hello çalışma zamanı iç için oluşturulan hello 64-bit Kimliğini kullanın.

## <a name="list-of-performance-counters"></a>Performans sayaçlarının listesi
### <a name="service-method-performance-counters"></a>Hizmet yöntemi performans sayaçları

Merhaba güvenilir hizmet çalışma zamanı performans sayaçları ilgili toohello hizmet yöntemleri yürütülmesinin hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Service Fabric hizmeti yöntemi |Çağrıları/sn |Merhaba hizmet yöntemi, saniye başına çağrılma sayısı |
| Service Fabric hizmeti yöntemi |Çağrı başına ortalama milisaniye |Milisaniye cinsinden tooexecute hello hizmet yöntemi harcanan süre |
| Service Fabric hizmeti yöntemi |Oluşturulan özel durum/sn |Hizmet yöntemi hello sayısını saniye başına özel durum oluşturdu |

### <a name="service-request-processing-performance-counters"></a>Hizmet isteği işleme performans sayaçları
Bir istemci bir hizmet proxy nesnesi yöntemiyle çalıştırdığında, hello ağ toohello uzaktan iletişim hizmeti üzerinden gönderilen bir istek iletisi sonuçlanır. Merhaba hizmeti hello İstek iletisini işler ve bir yanıtı geri toohello istemci gönderir. Merhaba güvenilir ServiceRemoting çalışma zamanı performans sayaçları ilgili tooservice isteği işleme aşağıdaki hello yayımlar.

| Kategori adı | Sayaç adı | Açıklama |
| --- | --- | --- |
| Yapı Hizmeti |Beklemedeki istek sayısı |Merhaba hizmetinde işlenmekte olan istek sayısı |
| Yapı Hizmeti |İstek başına ortalama milisaniye |(Milisaniye cinsinden) bir istek hello hizmet tooprocess tarafından harcanan süre |
| Yapı Hizmeti |İsteğin seri durumdan çıkarılması için geçen ortalama süre (milisaniye) |Hello hizmeti tarafından alındığında süresi (milisaniye cinsinden) çekildiği toodeserialize hizmet istek iletisi |
| Yapı Hizmeti |Yanıtın serileştirilmesi için geçen ortalama süre (milisaniye) |Süre (milisaniye cinsinden) çekildiği tooserialize hello hizmet yanıt iletisi hello yanıt toohello istemci gönderilmeden önce hello hizmetine |

## <a name="next-steps"></a>Sonraki adımlar
* [Örnek kod](https://github.com/Azure/servicefabric-samples)
* [PerfView EventSource sağlayıcıları](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
