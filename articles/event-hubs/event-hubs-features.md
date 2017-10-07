---
title: "aaaAzure Event Hubs özellikleri genel bakış | Microsoft Docs"
description: "Genel bakış ve Azure Event Hubs özellikleri hakkında ayrıntılı bilgileri"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Olay hub'ları özelliklere genel bakış

Azure Event Hubs işleme alır ve düşük gecikme süreli ve yüksek güvenilirlikle olayları ve verileri, büyük miktarlarda işleyen hizmeti ölçeklenebilir bir olaydır. Bkz: [Event Hubs nedir?](event-hubs-what-is-event-hubs.md) hello hizmet üst düzey bir genel bakış için.

Bu makalede hello hello bilgileri derlemeler [genel bakış](event-hubs-what-is-event-hubs.md)ve Event Hubs bileşenleri ve özellikleri hakkında teknik ve uygulama ayrıntılar sağlar.

## <a name="event-publishers"></a>Olay yayımcıları

Veri tooan olay hub'ı olan bir olay üretici gönderen herhangi bir varlık veya *olay yayımcısı*. Olay yayımcıları HTTPS veya AMQP 1.0 kullanarak olayları yayımlayabilir. Olay yayımcıları kendilerini bir paylaşılan erişim imzası (SAS) belirteci tooidentify tooan olay hub'ı kullanın ve benzersiz bir kimliğe sahip veya ortak bir SAS belirteci kullanın.

### <a name="publishing-an-event"></a>Olay yayımlama

Bir olayı AMQP 1.0 veya HTTPS üzerinden yayımlayabilirsiniz. Event Hubs sağlar [istemci kitaplıkları ve sınıfları](event-hubs-dotnet-framework-api-overview.md) olayları tooan olay hub'ı .NET istemcilerinden yayımlama. Diğer çalışma zamanları ve platformlar için [Apache Qpid](http://qpid.apache.org/) gibi herhangi bir AMQP 1.0 istemcisi kullanabilirsiniz. Olayları ayrı ayrı veya toplu olarak yayımlayabilirsiniz. Tek bir yayın (olay verileri örneği), tek bir olay ya da toplu işlem olmasına bakılmaksızın 256 KB sınırlamaya sahiptir. Bu bir hata eşiği sonuçlarında büyük yayımlama olaylar. Yayımcılar toobe ındaki bölümleri hello olay hub'ı için en iyi yöntem olduğu ve tooonly belirtin bir *bölüm anahtarı* (Merhaba sonraki bölümde açıklanmıştır) ya da kimliklerini SAS belirteci üzerinden.

Merhaba seçim toouse AMQP veya HTTPS belirli toohello kullanım senaryodur. AMQP toplama tootransport düzeyi güvenliği (TLS) veya SSL/TLS kalıcı çift yönlü yuva hello kurulmasını gerektirir. HTTPS ek SSL yükü her istek için gerektirir ancak AMQP hello oturumu başlatılırken daha yüksek ağ maliyetleri vardır. Daha sık yayımcılar için AMQP daha yüksek performans sunar.

![Event Hubs](./media/event-hubs-features/partition_keys.png)

Olay hub'ları sağlar bir bölüm anahtarı değerini paylaşan tüm olayların sırası ve toohello aynı teslim edilmesini bölüm. Bölüm anahtarlarını yayımcı ilkeleriyle kullandıysanız, hello yayımcı kimliğini hello ve hello hello bölüm anahtarı değerinin eşleşmesi gerekir. Aksi takdirde bir hata oluşur.

### <a name="publisher-policy"></a>Yayımcı ilkesi

Event Hubs, *yayımcı ilkeleri* aracılığıyla olay yayımcıları üzerinde ayrıntılı denetim sağlar. Yayımcı, çalışma zamanı özellikleri tasarlanmış toofacilitate çok sayıda bağımsız olay yayımcıları ilkelerdir. Yayımcı ilkeleriyle her yayımcı benzersiz tanımlayıcısını olayları tooan event hub'ı seçin, yayımlarken mekanizması aşağıdaki hello kullanarak kullanır:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Toocreate yayımcı adlarını önceden yoksa, ancak sıra tooensure bağımsız yayımcı kimlikleri bir olayı yayımlarken kullanılan SAS belirteci hello eşleşmesi gerekir. Yayımcı ilkelerini kullanırken hello **PartitionKey** değerini toohello yayımcı adını ayarlayın. toowork düzgün bir şekilde, bu değerlerin eşleşmesi gerekir.

## <a name="capture"></a>Capture

[Olay hub'ları yakalama](event-hubs-capture-overview.md) olay hub'ları veri akış tooautomatically yakalama hello sağlar ve bir Blob storage hesabı veya bir Azure Data Lake hizmeti hesabının tooyour seçimi kaydedin. Azure portal hello yakalamayı etkinleştirme ve en küçük boyut ve zaman penceresini tooperform hello yakalama belirtin. Olay hub'ları yakalama kullanarak, kendi Azure Blob Storage hesabı ve kapsayıcı belirtin ya da kullanılan toostore hello Azure Data Lake Service hesap, yakalanan verileri. Yakalanan veriler hello Apache Avro biçiminde yazılır.

## <a name="partitions"></a>Bölümler

Event Hubs, her bir tüketici yalnızca belirli alt ya da bölümü hello ileti akışı okur bölümlenmiş tüketici modeli aracılığıyla ileti akışı sağlar. Bu model, olay işleme için yatay ölçek sağlar ve kuyruklar ile konularda kullanılamayan diğer akış odaklı özellikleri sunar.

Bölüm bir olay hub'ında tutulan olayların sıralı dizisidir. Yeni olaylar geldikçe bunlar toohello bu dizinin sonuna eklenir. Bölüm bir "yürütme günlüğü" olarak düşünülebilir.

![Event Hubs](./media/event-hubs-features/partition.png)

Olay hub'ları hello event hub'ındaki tüm bölümler arasında geçerli bir yapılandırılan saklama süresi için verileri saklar. Olayların süresi saat bazında dolar; bunları açıkça silemezsiniz. Bölümler birbirinden bağımsız olup kendi veri dizisini içerdiğinden genellikle farklı hızlarda büyürler.

![Event Hubs](./media/event-hubs-features/multiple_partitions.png)

bölüm sayısı Hello oluşturma sırasında belirtilir ve 2 ile 32 arasında olmalıdır. Merhaba bölüm sayısı değiştirilemez, olmadığından, uzun vadeli ölçek bölüm sayısı ayarlanırken dikkate almanız gerekir. Bölümler toohello aşağı akış paralellik uygulamalar gerekli ilişkili bir veri düzenleme mekanizmasıdır. Merhaba bir event hub'ındaki bölüm sayısı doğrudan toohello numarası ilişkili toohave beklediğiniz eşzamanlı okuyucu. Bölüm 32 ötesinde hello sayısı hello olay hub'ları ekibine başvurarak artırabilirsiniz.

Bölümler tanımlanabilir ve toodirectly gönderilebilir olsa da, doğrudan tooa bölüm göndererek önerilmez. Bunun yerine, hello sunulan daha yüksek düzeyli yapıları kullanabilirsiniz [olay yayımcısı](#event-publishers) ve [kapasite](#capacity) bölümler. 

Bölümler hello olay hello gövdesini, kullanıcı tanımlı özellik paketi ve hello bölümdeki sapması ve hello akış dizisindeki numarası gibi meta veriler içeren olay verileri dizisi ile doldurulur.

Merhaba bölümler ve kullanılabilirliği ve güvenilirliği arasındaki hello dengelemeyi hakkında daha fazla bilgi için bkz: [Event Hubs Programlama Kılavuzu](event-hubs-programming-guide.md#partition-key) ve hello [kullanılabilirlik ve Event Hubs tutarlılık](event-hubs-availability-and-consistency.md) makale .

### <a name="partition-key"></a>Bölüm anahtarı

Kullanabileceğiniz bir [bölüm anahtarı](event-hubs-programming-guide.md#partition-key) toomap gelen olay verilerini veri düzenleme hello amacı için belirli bölümlere. Merhaba bölüm anahtarı bir olay hub'ına geçirilen bir gönderen tarafından belirtilip değerdir. Merhaba bölüm ataması oluşturan bir statik karma işlevi ile işlenir. Bir olayı yayımlarken bölüm anahtarı belirtmezseniz hepsini bir kez deneme ataması kullanılır.

Merhaba olay yayımcısı yalnızca bölüm anahtarını bilir, farkındadır değil hello bölüm toowhich hello olayları yayımlanır. Bu anahtar ile bölümün kesilmesi hello aşağı akış işleme hakkında çok fazla tooknow gerek gelen hello gönderen korunmasını sağlar. Aygıt Başına veya kullanıcı kimlik iyi bir bölüm anahtarı oluşturur, ancak coğrafi konum gibi diğer öznitelikler de kullanılan toogroup olabilir benzersiz olayları tek bir bölümde ilgili.

## <a name="sas-tokens"></a>SAS belirteçleri

Event Hubs kullanan *paylaşılan erişim imzaları*, hangi kullanılabilir hello ad alanı ve olay hub'ı düzeyinde. SAS belirteci bir SAS anahtarından oluşturulur ve belirli bir biçimde kodlanmış bir URL’nin SHA karmasıdır. Merhaba adını hello anahtar (ilke) ve hello belirteci kullanarak, olay hub'ları hello karmayı yeniden ve böylece hello gönderenin kimliğini doğrular. Normalde, olay yayımcıları için SAS belirteci yalnızca belirli bir olay hub'ı üzerindeki **gönder** ayrıcalıkları ile oluşturulur. Bu SAS belirteci URL mekanizması hello hello yayımcı ilkesinde sunulan yayımcı kimliğinin temelini oluşturur. SAS ile çalışma hakkında daha fazla bilgi için bkz. [Service Bus ile Paylaşılan Erişim İmzası Kimlik Doğrulaması](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Olay tüketicileri

Bir olay hub'ından olay verilerini okuyan herhangi bir varlık *olay tüketicisidir*. Tüm Event Hubs tüketicileri hello AMQP 1.0 oturumu üzerinden bağlanır ve çıktıklarında olaylar hello oturumu aracılığıyla teslim edilir. Merhaba istemci toopoll veri kullanılabilirliği için gerekli değildir.

### <a name="consumer-groups"></a>Tüketici grupları

Olay hub'larını Hello yayımlama/abonelik mekanizması aracılığıyla etkin *tüketici grupları*. Tüketici grubu tüm olay hub'ının bir görünümüdür (durum, konum veya uzaklık). Tüketici grupları tooeach hello olay akışının ve tooread hello akışı kendi hızlarında bağımsız olarak ayrı bir görünüm ve kendi ile kaydırır birden çok tüketen uygulamayı etkinleştirin.

Bir akış işleme mimarisinde her bir aşağı akış uygulaması tooa tüketici grubu karşılık gelir. Toowrite olay toolong dönemli saklama istiyorsanız, ardından bu depolama yazma uygulaması bir tüketici grubudur. Bundan sonra karmaşık olay işlemesi başka ve ayrı bir tüketici grubu tarafından gerçekleştirilebilir. Bölümlere yalnızca bir tüketici grubu üzerinden erişebilirsiniz. Olabilir en fazla 5 eşzamanlı okuyucu tüketici grubu başına bir bölüme; ancak **olduğundan yalnızca bir etkin alıcı tüketici grubu başına bir bölüme önerilir**. Bir event hub'ında her zaman varsayılan bir tüketici grubu vardır ve bir standart katmanı olay hub'ına yönelik too20 tüketici grupları oluşturabilirsiniz.

Merhaba, hello tüketici grubu URI kuralının örnekleri şunlardır:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Merhaba aşağıdaki şekilde hello olay hub'ları akış işleme mimarisi gösterilmektedir:

![Event Hubs](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Akış uzaklıkları

Bir *uzaklık* bir olayın bölüm içindeki hello konumudur. Uzaklığı istemci tarafındaki bir imleç olarak düşünebilirsiniz. Merhaba bir bayt uzaklığı hello olayı numaralandırma. Bu uzaklık olay tüketicisinin (Okuyucu) toospecify hello olay akışında olayları okumaya toobegin istedikleri noktası sağlar. Başlangıç uzaklığı bir zaman damgası veya bir uzaklık değeri olarak belirtebilirsiniz. Tüketiciler, kendi uzaklık değerlerini hello Event Hubs hizmetinin dışında saklamaktan sorumludur. Bir bölüm içinde her olay bir uzaklık içerir.

![Event Hubs](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Denetim noktası oluşturma

*Denetim noktası oluşturma*, okuyucuların bir bölüm olay dizisindeki konumlarını işaretledikleri veya uyguladıkları bir işlemdir. Denetim noktası oluşturma hello tüketici hello sorumluluğundadır ve bir tüketici grubundaki bölüm başına temelinde gerçekleşir. Bu sorumluluğu her bir tüketici grubu için her bölüm okuyucusu geçerli konumunu hello olay akışında izlemek gerekir ve hello veri akışının tamamlandığını düşündüğünde hello hizmeti bilgilendirebilir anlamına gelir.

Okuyucu bağlandığında bir bölümün dışında keser varsa hello ilgili tüketici grubundaki o bölümün son okuyucusu tarafından daha önce gönderilen hello denetim noktası okumaya başlar. Merhaba okuyucu bağlandığında bu uzaklık toohello olay hub'ı toospecify hello konumda hangi toostart okuma geçirir. Bu şekilde denetim noktası oluşturma tooboth işareti olayları "tamamlandı" olarak aşağı akış uygulamaları tarafından kullanabilirsiniz ve tooprovide dayanıklılık bir yük devretme durumunda farklı makinelerde çalışan okuyucular arasında oluşur. Bu olası tooreturn tooolder bu denetim noktası oluşturma işleminden daha düşük bir uzaklık belirterek verilerdir. Bu mekanizmayla denetim noktası oluşturma özelliği hem yük devretme esnekliği hem de olay akışı yeniden yürütmesi sağlar.

### <a name="common-consumer-tasks"></a>Ortak tüketici görevleri

Tüm Event Hubs tüketicileri durumu algılayan çift yönlü iletişim kanalını bir AMQP 1.0 oturumu üzerinden bağlanır. Her bölümde bölüme göre ayrılmış olayların hello aktarım kolaylaştıran bir AMQP 1.0 oturumu var.

#### <a name="connect-tooa-partition"></a>Tooa bölüm bağlanma

Toopartitions bağlanırken bir kiralama yaygın yöntem toouse olan mekanizması toocoordinate okuyucu bağlantıları toospecific bölümler. Bu şekilde, her bir tüketici grubu toohave yalnızca bir etkin okuyucuya bölümün mümkündür. Kiralama ve yönetme denetim noktası oluşturma, okuyucuların Basitleştirilmiş hello kullanarak [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) .NET istemcileri için sınıfı. Merhaba olay işleyicisi konağı bir akıllı bir tüketici aracısıdır.

#### <a name="read-events"></a>Olayları okuma

Belirli bir bölüm için bir AMQP 1.0 oturumu ve bağlantı açıldıktan sonra olaylar Event Hubs hizmeti hello tarafından toohello AMQP 1.0 istemcisi teslim edilir. Bu teslim mekanizması, HTTP GET gibi çekme tabanlı mekanizmalardan daha yüksek verimlilik ve daha düşük gecikme sağlar. Olayları toohello istemci gönderilen gibi her bir olay verisi örneği hello olay dizisinde denetim noktası kullanılan toofacilitate hello uzaklık ve dizi numarası gibi önemli meta veriler içerir.

Olay verileri:
* Uzaklık
* Sıra numarası
* Gövde
* Kullanıcı özellikleri
* Sistem özellikleri

Bu, sorumluluk toomanage başlangıç uzaklığı.

## <a name="capacity"></a>Kapasite

Olay hub'ları sahip yüksek oranda ölçeklenebilen paralel bir mimaridir ve boyutlandırma ve ölçeklendirme birkaç anahtar Etkenler tooconsider vardır.

### <a name="throughput-units"></a>İşleme birimleri

Olay hub'ları Hello işleme kapasitesi tarafından denetlenir *üretilen iş birimleri*. İşleme birimleri önceden satın alınan kapasite birimleridir. Tek bir işleme birimi kapasite aşağıdaki hello içerir:

* Giriş: ikinci ya da 1000 olayları (hangisi önce gerçekleşirse) saniye başına başına too1 MB
* Çıkış: saniye başına too2 MB

Üretilen iş birimleri satın hello Hello kapasitesini giriş azaltılır ve [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) döndürülür. Çıkış azaltma özel durumları oluşturmaz, ancak işleme birimi satın hello hala sınırlı toohello kapasitesi. Yayımlama hızı özel durumları alırsanız veya toosee daha yüksek çıkış bekleniyor, emin toocheck hello ad alanı için satın aldığınız kaç tane işleme birimi olabilir. Üretilen iş birimleri hello üzerinde yönetebilirsiniz **ölçek** hello hello ad alanları dikey [Azure portal](https://portal.azure.com). Üretilen iş birimleri program aracılığıyla hello kullanarak da yönetebilirsiniz [olay hub'ları API'leri](event-hubs-api-overview.md).

İşleme birimleri saat başına faturalandırılır ve önceden satın alınır. Satın alındıktan sonra işleme birimleri en az bir saat için faturalandırılır. Too20 üretilen iş birimleri için bir olay hub'ları ad alanı satın alınabilir ve hello ad alanındaki tüm Event Hubs arasında paylaşılır.

Daha fazla işleme birimi too100 üretilen iş birimleri 20 blokları Azure desteğine başvurarak satın alınabilir. Bundan sonraki miktarlar için 100 işleme biriminden oluşan bloklar satın alabilirsiniz.

Üretilen iş birimleri ile bölümleri tooachieve en iyi ölçeği Bakiye öneririz. Tek bir bölüm en fazla bir işleme biriminden oluşan ölçeğe sahiptir. Merhaba işleme birimlerinin sayısı küçük veya buna eşit olmalıdır toohello bir olay hub'ındaki bölüm sayısı.

Ayrıntılı olay fiyatlandırma bilgileri hub için bkz: [Event Hubs fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Sonraki adımlar

Event Hubs hakkında daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin:

* [Event Hubs öğreticisi][Event Hubs tutorial] ile çalışmaya başlama
* [Event Hubs programlama kılavuzu](event-hubs-programming-guide.md)
* [Event Hubs’da kullanılabilirlik ve tutarlılık](event-hubs-availability-and-consistency.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)
* [Olay hub'ları örnekleri][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Olay hub'ları örnekleri]: https://github.com/Azure/azure-event-hubs/tree/master/samples
