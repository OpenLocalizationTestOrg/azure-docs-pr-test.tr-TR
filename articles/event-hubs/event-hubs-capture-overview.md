---
title: "Azure olay hub'ları yakalama aaaOverview | Microsoft Docs"
description: "Olay hub'ları yakalama telemetri verilerini yakalama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Azure Event Hubs yakalama

Azure olay hub'ları yakalama sağlar, olay hub'ları tooan veri akış tooautomatically teslim hello [Azure Blob Depolama](https://azure.microsoft.com/services/storage/blobs/) veya [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hello ile tercih ettiğiniz hesabına esneklik eklenen bir kez veya boyut aralığı belirterek. Yakalama kurduğunuzda ayardır hızlı ve bunu ölçeklendirir otomatik olarak Event Hubs ile hiçbir yönetim maliyetleri toorun [üretilen iş birimleri](event-hubs-features.md#capacity). Olay hub'ları yakalama akış verileri Azure'da hello en kolay yolu tooload ve toofocus veri işleme yerine veri yakalamayı etkinleştirir.

Toplu işlem tabanlı ardışık düzen üzerinde aynı akış hello ve olay hub'ları yakalama tooprocess gerçek zamanlı sağlar. Bu, zaman içinde gereksinimlerinizi ile büyümesine çözümleri oluşturmanıza anlamına gelir. Toplu işlem tabanlı sistemleriyle bugün gelecekteki gerçek zamanlı işleme doğru bir göz oluşturmakta olduğunuz ya tooadd etkin yolunuzda tooan varolan gerçek zamanlı çözümü istiyor da olsanız, olay hub'ları yakalama daha kolay veri akış ile çalışma hale getirir.

## <a name="how-event-hubs-capture-works"></a>Olay hub'ları yakalama nasıl çalışır

Olay hub'ları telemetri giriş, benzer tooa dağıtılmış günlük bir bekletme süresi dayanıklı arabellek olur. Olay hub'ın anahtar tooscaling Hello olduğu hello [bölümlenmiş tüketici modelinin](event-hubs-features.md#partitions). Her bölüm veri bağımsız bir parçasıdır ve bağımsız olarak kullanılır. Bu verileri kapalı eskir zamanla hello yapılandırılabilir saklama dönemi temel. Sonuç olarak, belirli olay hub'ı hiçbir zaman "dolu." alır

Olay hub'ları yakalama, toospecify kendi Azure Blob Depolama hesabı ve kapsayıcı ya da kullanılan toostore hello yakalanan verileri Azure Data Lake Store hesabını etkinleştirir. Bu hesapları hello olabilir aynı bölgede olay hub'ınızı ya da başka bir bölgede hello olay hub'ları yakalama özelliği toohello esnekliğini ekleme.

Yakalanan verileri yazılmış [Apache Avro] [ Apache Avro] biçimi: satır içi şeması ile zengin veri yapılarını sağlar compact, hızlı ve ikili biçimi. Bu biçim hello Hadoop ekosistemi, akış analizi ve Azure Data Factory yaygın olarak kullanılır. Avro ile çalışma hakkında daha fazla bilgi, bu makalenin sonraki bölümlerinde kullanılabilir.

### <a name="capture-windowing"></a>Pencereleme yakalama

Olay hub'ları yakalama pencere yakalanıyor toocontrol yukarı tooset sağlar. Bu, en küçük boyut ve zaman yapılandırma İlkesi'yle "yakalama işlemi, ilk tetikleyici karşılaşılan nedenleri hello yani ilk WINS," penceredir. On beş dakikalık varsa, 100 MB Yakalama penceresinin ve 1 MB saniye başına hello boyutu penceresi Tetikleyicileri hello zaman penceresi önce gönderin. Her bölüm bağımsız olarak yakalar ve tamamlanan blok blobu, yakalama, başlangıç sırasında hangi hello yakalama aralığı karşılaşıldı hello süredir adlı yazar. Merhaba depolama adlandırma kuralı aşağıdaki gibidir:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Toothroughput birimleri ölçeklendirme

Olay hub'ları trafiği tarafından denetlenir [üretilen iş birimleri](event-hubs-features.md#capacity). Tek bir işleme birimi, ikinci veya 1000 olayları giriş ve çıkış miktarı iki kez saniyede başına 1 MB sağlar. Standart olay hub'ları 1-20 işleme birimleri ile yapılandırılabilir ve daha fazla satın alma ile kota artırma [destek isteği][support request]. Kullanım, satın alınan işleme birimlerine ötesinde kısıtlanır. Olay hub'ları yakalama verileri doğrudan hello İç olay hub'ları depolama biriminden, işleme birimi çıkış kotaları atlayarak ve akış analizi veya Spark gibi diğer işleme okuyucular için çıkış kaydetme kopyalar.

Olay hub'ları yakalama yapılandırdıktan sonra ilk olay gönderdiğinizde, otomatik olarak çalışır ve çalışmaya devam eder. hiçbir veri olduğunda toomake hello işlemin çalıştığını, aşağı akış işleme tooknow için olay hub'ları daha kolaydır boş dosyaları yazar. Bu işlem, tahmin edilebilir tempoyla ve toplu işlemciler besleyebilecek işaret sunar.

## <a name="setting-up-event-hubs-capture"></a>Olay hub'ları yakalama ayarlama

Yakalama hello kullanarak hello olay hub'ı oluşturma zamanında yapılandırabilirsiniz [Azure portal](https://portal.azure.com), veya Azure Resource Manager şablonları kullanarak. Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Olay hub'ları hello Azure portal kullanarak yakalama etkinleştir](event-hubs-capture-enable-through-portal.md)
- [Bir event hub ile Event Hubs ad alanı oluşturmak ve bir Azure Resource Manager şablonu kullanarak yakalamayı etkinleştirme](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Yakalanan hello dosyaları keşfetme ve Avro ile çalışma

Olay hub'ları yakalama Avro biçiminde hello yapılandırılmış zaman penceresi belirtildiği gibi dosyalar oluşturur. Bu dosyaları gibi herhangi bir aracı görüntüleyebilirsiniz [Azure Storage Gezgini][Azure Storage Explorer]. İndirebilirsiniz hello dosyaları yerel olarak toowork bunlar üzerinde.

Olay hub'ları yakalama tarafından üretilen hello dosyaları Avro şemasının aşağıdaki hello sahiptir:

![][3]

Kolay bir yolu tooexplore Avro dosyalarının olduğu hello kullanarak [Avro Araçları] [ Avro Tools] Apache gelen jar. Bu jar indirdikten sonra komutu aşağıdaki hello çalıştırarak belirli bir Avro dosya hello şeması görebilirsiniz:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Bu komut döndürür

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Avro araçları tooconvert hello dosya tooJSON biçimini kullanın ve başka bir işlem gerçekleştirin.

daha gelişmiş işleme, karşıdan yüklenip Avro için tercih ettiğiniz platformun tooperform. Bu yazma Hello anda uygulamaları C, C++, C için kullanılabilir olduğundan\#, Java, NodeJS, Perl, PHP, Python ve Ruby.

Apache Avro için tam Başlarken kılavuzları sahip [Java] [ Java] ve [Python][Python]. Ayrıca, hello okuyabilirsiniz [olay hub'ları yakalama ile çalışmaya başlama](event-hubs-capture-python.md) makalesi.

## <a name="how-event-hubs-capture-is-charged"></a>Olay hub'ları yakalama nasıl doludur

Olay hub'ları yakalama ölçülen benzer şekilde toothroughput birimler: saatlik giderleri olarak. Merhaba ücret orantılı toohello hello ad alanı için satın alınan işleme birimi sayısıdır. Üretilen iş birimleri artırılır ve azaltılır gibi olay hub'ları yakalama ölçümler artırın ve performans eşleşen tooprovide azaltın. Merhaba ölçümler dağıtımınızla oluşur. Fiyatlandırma ayrıntıları için bkz: [Event Hubs fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Sonraki adımlar

Olay hub'ları yakalama hello en kolay yolu tooget Azure içine verilerdir. Azure Data Lake, Azure Data Factory ve Azure Hdınsight kullanarak toplu işleme gerçekleştirebilir ve herhangi bir ölçekte tanıdık Araçlar ve seçtiğiniz platformlar kullanarak diğer analytics gerekir.

Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Gönderme ve alma olayları kullanmaya başlama](event-hubs-dotnet-framework-getstarted-send.md)
* [Event Hubs kullanan bir örnek uygulamanın][sample application that uses Event Hubs] tamamı
* [Event Hubs'a genel bakış][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
