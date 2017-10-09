---
title: "aaaScheduler kavramları, terimleri ve varlıkları | Microsoft Docs"
description: "İşler ve iş koleksiyonları dahil Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi.  Zamanlanan bir işin kapsamlı bir örneği gösterilmektedir."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Scheduler kavramları ve terminolojisi + varlık hiyerarşisi
## <a name="scheduler-entity-hierarchy"></a>Scheduler varlık hiyerarşisi
Merhaba aşağıdaki tabloda gösterilen ya da hello Scheduler API'si tarafından kullanılan hello ana kaynaklar açıklanır:

| Kaynak | Açıklama |
| --- | --- |
| **İş koleksiyonu** |İş koleksiyonu, bir grup işi içerir ve ayarlar, kotalar ve hello koleksiyondaki işler tarafından paylaşılan kısıtlamaları tutar. İş koleksiyonu abonelik sahibi tarafından oluşturulur ve işleri kullanım veya uygulama sınırlarına göre gruplandırır. Kısıtlanmış tooone bölgedir. Ayrıca hello zorlama kotaları koleksiyonda tooconstrain hello tüm işlerin kullanımını sağlar. Merhaba kotalar MaxJobs ve maxrecurrence değerlerini içerir. |
| **İş** |Bir iş, yürütmek üzere basit ya da karmaşık stratejilerle tek bir yinelenen eylemi tanımlar. Eylemler HTTP, depolama kuyruğu, hizmet veri yolu kuyruğu ya da hizmet veri yolu konusu isteklerini içerebilir. |
| **İş geçmişi** |İş geçmişi bir işin yürütülmesine ilişkin ayrıntılarını temsil eder. Bu başarılı ve hatalı karşılaştırmasının yanı sıra tüm yanıt ayrıntılarını içerir. |

## <a name="scheduler-entity-management"></a>Scheduler varlık yönetimi
Yüksek bir düzeyde hello kaynaklar üzerinde işlem aşağıdaki hello hello Zamanlayıcı ve hello Hizmet Yönetimi API'si ortaya çıkarır:

| Özellik | Açıklama ve URI adresi |
| --- | --- |
| **İş koleksiyonu yönetimi** |Al koy ve Sil desteği oluşturma ve iş koleksiyonları ve burada yer alan hello işleri değiştirme. İş koleksiyonu işleri için bir kapsayıcıdır ve tooquotas ve paylaşılan ayarları eşler. İleride açıklanan kota örnekleri, maksimum iş sayısı ve en küçük yineleme aralığıdır. <p>KOY ve SİL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>AL: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **İş yönetimi** |İşleri oluşturma ve değiştirmeye yönelik AL, KOY, YAYIMLA, DÜZELTME EKİ UYGULA ve SİL desteği. Açık oluşturma böylece tüm işleri zaten var, tooa iş koleksiyonu ait olmalıdır. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **İş geçmişi yönetimi** |İş geçen süresi ve iş yürütme sonuçları gibi, 60 günlük iş yürütme geçmişi getirmek üzere AL desteği. Durum ve duruma göre filtreleme için sorgu dizesi parametresi desteği ekler. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>İş türleri
Birden çok iş türü vardır: HTTP işleri (SSL destekleyen HTTPS işleri dahil), depolama kuyruğu işleri, hizmet veri yolu kuyruğu işleri ve hizmet veri yolu konusu işleri. HTTP işleri, mevcut bir iş yükünde ya da hizmette uç noktaya sahipseniz idealdir. Bu işleri depolama kuyrukları kullanan iş yükleri için ideal; bu nedenle depolama kuyruğu işleri toopost iletileri toostorage kuyrukları kullanabilirsiniz. Benzer şekilde, hizmet veri yolu işleri hizmet veri yolu kuyrukları ve konuları kullanan iş yükleri için idealdir.

## <a name="hello-job-entity-in-detail"></a>Merhaba ayrıntılı "job" varlığı
Temel düzeyde, zamanlanan bir iş birkaç bölümden oluşur:

* Merhaba iş Zamanlayıcı başlatıldığında hello eylem tooperform  
* (İsteğe bağlı) hello süresi toorun hello işi  
* (İsteğe bağlı) Zaman ve ne sıklıkta toorepeat hello işi  
* (İsteğe bağlı) Merhaba birincil eylem başarısız olursa eylem toofire  

Dahili olarak, zamanlanmış bir işi hello sonraki zamanlanan yürütme zamanı gibi sistem tarafından sağlanan verileri de içerir.

koddan hello zamanlanan bir işin kapsamlı bir örnek sağlar. Ayrıntılar sonraki bölümlerde verilmiştir.

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

Merhaba örnek zamanlanan İşte yukarıdaki görüldüğü gibi bir iş tanımı birkaç bölümden oluşur:

* Başlangıç zamanı ("startTime")  
* Hata eylemi ("errorAction") içeren eylem ("eylem")
* Yineleme ("recurrence")  
* Durum ("state")  
* Durum ("status")  
* Yeniden deneme ilkesi ("retryPolicy")  

Şimdi bunların her birini ayrıntılı inceleyelim:

## <a name="starttime"></a>startTime
Merhaba "startTime" Merhaba başlangıç saati ve hello arayan toospecify hello hat üzerinde uzaklığı bir saat dilimi sağlar [ISO 8601 biçiminde](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action ve errorAction
Merhaba "action" her meydana Gelişte çağrılan hello eylemdir ve hizmet başlatma türünü açıklar. Merhaba zamanlama sağlanan hello üzerinde yürütülecek eylemdir. Scheduler, HTTP, depolama kuyruğu, hizmet veri yolu konusu ve hizmet veri yolu kuyruğu eylemlerini destekler.

Yukarıdaki hello örnekte Hello eylem bir HTTP eylemdir. Bir depolama kuyruğu eylemi örneği aşağıdadır:

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

Bir hizmet veri yolu konusu eylemi örneği aşağıdadır:

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

Bir hizmet veri yolu kuyruğu eylemi örneği aşağıdadır:

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // netMessaging ya da AMQP olabilir "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Merhaba "errorAction" Merhaba hata hello eylemin hello birincil eylem başarısız olduğunda çağrılan işleyicisidir. Bu değişken toocall bir hata işleme uç nokta kullanın veya bir kullanıcı bildirimi gönderebilirsiniz. Bu kullanılabilir o hello hello durumda ikincil uç noktaya ulaşmak için birincil kullanılabilir (örneğin, bir olağanüstü durum hello uç noktanın sitede durumunu hello) değil veya bir hata işleme uç noktasını bildirmek için kullanılabilir. Yalnızca hello birincil eylemde olduğu gibi hello hata eylemi diğer eylemler temelinde basit ya da birleşik mantıklı olabilir. toocreate bir SAS belirteci başvurmak çok nasıl toolearn[oluşturmak ve paylaşılan erişim imzası kullanmak](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>yineleme
Yineleme birkaç bölümden oluşur:

* Sıklık: Dakika, saat, gün, hafta, ay, yıldan biri  
* Aralığı: Merhaba yinelemesi sıklığı verilen hello aralıkta  
* Belirtilen zamanlama: dakika, saat, hafta, ay ve ayın günü hello yinelenme belirtin  
* Sayı: Yineleme sayısı  
* Bitiş saati: hello belirtilen bitiş zamanından sonra hiç iş yürütülmez  

Bir iş, JSON tanımında belirtilen yinelenen nesneye sahipse yinelenendir. Sayı ve endTime belirtilmişse, önce gerçekleşirse hello tamamlama kuralı uygulanır.

## <a name="state"></a>durum
hello iş Hello durumu dört değerden biridir: etkin, devre dışı, tamamlandı ya da hatalı. KOYABİLİRSİNİZ veya düzeltme eki işler bunu tooupdate bunları toohello etkin veya devre dışı durumu. Bir işi tamamlandı ya da hatalı ise (Merhaba iş hala silinebilir) güncelleştirilemiyor son durum olmasıdır. Merhaba state özelliği örneği aşağıdaki gibidir:

        "state": "disabled", // enabled, disabled, completed, or faulted
Tamamlanan ve hatalı işler 60 gün sonra silinir.

## <a name="status"></a>durum
Scheduler işi başladıktan sonra hello geçerli hello işin durumu hakkında bilgi döndürülür. Bu nesne hello kullanıcı tarafından ayarlanamaz değildir — hello sistem tarafından ayarlanır. Ancak, böylece bir hello işin durumunu kolayca edinebileceği hello iş nesnesi (yerine ayrı bağlantılı bir kaynak) dahil.

İş durumu içerir hello önceki yürütme (varsa), başlangıç zamanı hello hello sonraki zamanlanan yürütmeyi (devam eden işler) süresi ve hello iş hello yürütme sayısı.

## <a name="retrypolicy"></a>retryPolicy
Scheduler işi başarısız olursa, olası toospecify olup olmadığını ve nasıl hello eylemin yeniden denenip bir yeniden deneme ilkesi toodetermine olur. Bu hello tarafından belirlenir **retryType** nesne — çok ayarlamak**hiçbiri** varsa yeniden deneme ilkesi, yukarıda gösterildiği gibi. Çok ayarlamak**sabit** bir yeniden deneme ilkesi varsa.

tooset bir yeniden deneme ilkesi iki ek ayar belirtilebilir: yeniden deneme aralığını (**Retryınterval**) ve yeniden deneme sayısı hello (**retryCount**).

Merhaba, Hello ile belirtilen yeniden deneme aralığı **Retryınterval** nesne, hello yeniden denemeler arasındaki aralıktır. Varsayılan değer 30 saniye, minimum yapılandırılabilir değeri 15 saniye, ve maksimum değeri 18 aydır. Ücretsiz iş koleksiyonlarındaki işleri 1 saat şeklinde minimum yapılandırabilir değere sahiptir.  Merhaba ISO 8601 biçiminde tanımlıdır. Yeniden deneme sayısı hello hello değerini hello ile benzer şekilde, belirtilen **retryCount** nesne; hello kaç kez yeniden değil. Varsayılan değer 4'tür ve maksimum değeri 20\ olduğu. Her ikisi de **Retryınterval** ve **retryCount** isteğe bağlıdır. Bunlar varsayılan değerlerine verilir **retryType** çok ayarlanır**sabit** ve açıkça değer belirtilmemiş.

## <a name="see-also"></a>Ayrıca bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile](scheduler-advanced-complexity.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

