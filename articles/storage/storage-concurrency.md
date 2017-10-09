---
title: "aaaManaging eşzamanlılık Microsoft Azure depolama"
description: "Nasıl toomanage eşzamanlılık hello Blob, kuyruk, tablo ve Dosya Hizmetleri"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Microsoft Azure Depolama'da Eşzamanlılığı Yönetme
## <a name="overview"></a>Genel Bakış
Modern Internet tabanlı uygulamalar genellikle görüntüleme ve verileri aynı anda güncelleştirme birden çok kullanıcı sahiptir. Bu uygulama geliştiricilerin toothink dikkatli bir şekilde nasıl tooprovide öngörülebilir bir deneyim tootheir son kullanıcılar, hakkında özellikle birden çok kullanıcı burada güncelleştirebilirsiniz senaryoları aynı hello için gerektirir veri. Geliştiriciler genellikle değerlendirir üç ana veri eşzamanlılık stratejisi vardır:  

1. İyimser eşzamanlılık – bir güncelleştirme, güncelleştirme bir parçası olarak hello veri Merhaba uygulaması itibaren değişip değişmediğini doğrulayın gerçekleştiren bir uygulama bu verileri son okuyun. Bir wiki sayfa görüntüleme iki kullanıcı bir güncelleştirme toohello yaparsanız, örneğin, aynı hello wiki platform hello ikinci güncelleştirmenin hello ilk güncelleştirmesi – üzerine yazmaz emin olmalısınız ve her iki kullanıcı kendi güncelleştirme başarılı olup olmadığını anlamak daha sonra sayfa. Bu strateji, web uygulamaları en sık kullanılır.
2. Eşzamanlılık – tooperform bir güncelleştirme arayan bir uygulama, diğer kullanıcıların hello kilidi serbest kadar hello verileri güncelleştirme engelleyen bir nesne üzerinde bir kilit olur. Merhaba veri tooensure hiç kimsenin zamanında uzun bir süre güncelleştirmek için örneğin, yalnızca hello ana güncelleştirmeleri nerede gerçekleştirecek ana/bağımlı veri çoğaltma senaryoda hello ana genellikle özel bir kilit tutar.
3. Son yazıcı WINS – tüm güncelleştirme işlemleri tooproceed Merhaba uygulaması ilk hello veri okuma beri hello verileri başka bir uygulama güncelleştirdi, doğrulamadan sağlayan bir yaklaşımdır. Bu strateji (veya bir resmi stratejisi eksikliği) genellikle veri birden çok kullanıcı hello erişecek hiçbir olasılığı olan yolu burada bölümlenmiş kullanılan aynı veri. Bu da kısa süreli veri akışlarını burada işlenen yararlı olabilir.  

Bu makalede bu eşzamanlılık stratejileri üçü için birinci sınıf destek sağlayarak hello Azure Storage platform geliştirme nasıl basitleştirir genel bir bakış sağlar.  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure Storage – bulut geliştirme basitleştirir
tasarlanmış tooembrace olduğunda garanti bir güçlü tutarlılık modeli olduğundan iyimser ve kötümser eşzamanlılık için kendi yeteneği tooprovide tam destek farklı olmasına rağmen tüm üç stratejileri, hello Azure depolama hizmeti destekler veri ekleme veya güncelleştirme işlemi tüm başka toothat verilere erişir son güncelleştirme hello görürsünüz depolama hizmeti işlemeleri hello. Nihai tutarlılık modelini kullanan depolama platformları yazma bir kullanıcı tarafından ne zaman gerçekleştirilen arasında bir gecikme olması ve hello güncelleştirildiği veri böylece sipariş tooprevent tutarsızlıklar istemci uygulamalarını geliştirme karmaşıklaştırarak diğer kullanıcılar tarafından görülebilir. Son kullanıcıları etkileyen.  

Ayrıca tooselecting uygun eşzamanlılık stratejisi geliştiriciler ayrıca bir depolama platform değişiklikleri – özellikle aynı işlemleri arasında nesne değişiklikleri toohello nasıl yalıtır bilmeniz gerekir. Hello Azure depolama hizmeti işlemleri toohappen yazma işlemlerini tek bir bölüm aynı anda okuma anlık görüntü yalıtım tooallow kullanır. Diğer yalıtım düzeyleri farklı olarak, anlık görüntü yalıtımı bile güncelleştirmeler – aslında bir güncelleştirme işlemi gerçekleştirilirken hello son kabul edilen değerler döndüren tarafından yaşanan sırada tüm okuma hello verilerin tutarlı bir anlık görüntü bkz güvence altına alır.  

## <a name="managing-concurrency-in-blob-storage"></a>Blob depolama alanına eşzamanlılık yönetme
İyimser veya kötümser eşzamanlılık toomanage erişim tooblobs modeller ve blob hizmeti kapsayıcılarında hello toouse tercih edebilirsiniz. Bir strateji açıkça belirtmezseniz, son WINS hello varsayılan yazar.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>BLOB'ları ve kapsayıcıları için iyimser eşzamanlılık
Merhaba depolama hizmeti depolanan bir tanımlayıcı tooevery nesne atar. Bu tanımlayıcı, bir nesne üzerinde her bir güncelleştirme işlemi gerçekleştirildiğinde güncelleştirilir. Merhaba tanıtıcısı toohello istemci hello HTTP Protokolü içinde tanımlanan hello (varlık etiketi) ETag üstbilgisi kullanarak bir HTTP GET yanıtında bir parçası olarak döndürülür. Böyle bir nesne üzerinde bir güncelleştirme gönderebilirsiniz gerçekleştiren bir kullanıcı, bir güncelleştirme yalnızca oluşur belirli bir koşulun yerine – bu durumda hello hello depolama gerektiren bir "If-Match" üst bilgisi bir durumdur, koşullu üstbilgi tooensure birlikte özgün ETag hello Hizmet tooensure hello değeri hello hello güncelleştirme isteğinde belirtilen ETag olduğu hello hello depolama hizmeti depolanan aynıdır.  

Bu işlemin Hello anahat aşağıdaki gibidir:  

1. Bir blob hello Depolama hizmetinden alın, hello yanıt hello nesnesinin geçerli sürümü, hello hello depolama hizmetindeki tanımlayan bir HTTP ETag üstbilgi değeri içeriyor.
2. Merhaba blob güncelleştirdiğinizde hello de 1. adımda alınan hello ETag değeri içeren **IF-Match** toohello hizmet gönderdiğiniz hello isteğinin koşullu üstbilgi.
3. Merhaba hizmet hello istekteki hello ETag değeri hello hello blob geçerli ETag değeri ile karşılaştırır.
4. Merhaba geçerli ETag değeri hello BLOB ETag hello hello daha farklı bir sürümü ise **IF-Match** hello isteğindeki hello hizmet koşullu üstbilgi toohello istemci 412 hata döndürür. Bu, başka bir işlem hello istemci, alınan bu yana hello blob güncelleştirdi toohello istemci gösterir.
5. Merhaba geçerli hello blob değeri ETag aynı sürümde Merhaba, ETag hello hello **IF-Match** hello isteğindeki hello hizmet koşullu üstbilgi gerçekleştirir hello istenen işlemi ve güncelleştirmeleri hello hello blob geçerli ETag değeri tooshow yeni bir sürümü oluşturdu.  

Merhaba (Merhaba istemci depolama kitaplığı 4.2.0 kullanarak) aşağıdaki C# kod parçası nasıl basit bir örneği gösterir tooconstruct bir **IF-Match AccessCondition** hello hello olan blob özelliklerinden erişilen ETag değeri göre daha önce alınan ya da eklenen. Ardından hello kullanır **AccessCondition** nesne zaman onu hello blob güncelleştiriliyor: hello **AccessCondition** nesnesi ekler hello **IF-Match** üstbilgi toohello isteği. Başka bir işlem hello blob güncelleştirdi, hello blob hizmeti bir HTTP 412 (önkoşul başarısız oldu) durum iletisi döndürür. Merhaba tam örnek buradan indirebilirsiniz: [Azure Storage kullanarak eşzamanlılık yönetme](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Merhaba depolama hizmeti için de destek içerir ek koşullu üstbilgileri gibi **If-Modified-Since**, **IF-Unmodified-Since** ve **If-None-Match** yanı bunların bileşimleri. Daha fazla bilgi için bkz: [Blob hizmeti işlemleri için koşullu üstbilgileri belirtme](http://msdn.microsoft.com/library/azure/dd179371.aspx) konusuna bakın.  

Merhaba aşağıdaki tabloda özetlenmiştir koşullu üstbilgileri gibi kabul hello kapsayıcı işlemleri **IF-Match** hello istek ve hello yanıt ETag değeri döndürür.  

| İşlem | Kapsayıcı ETag değeri döndürür | Koşullu üstbilgileri kabul eder |
|:--- |:--- |:--- |
| Kapsayıcı oluşturma |Evet |Hayır |
| Kapsayıcı özellikleri Al |Evet |Hayır |
| Kapsayıcı meta verileri alma |Evet |Hayır |
| Kapsayıcı meta verileri ayarlama |Evet |Evet |
| Kapsayıcı ACL Al |Evet |Hayır |
| Kapsayıcı ACL ayarlayın |Evet |Evet (*) |
| Kapsayıcısını silmek |Hayır |Evet |
| Kira kapsayıcısı |Evet |Evet |
| Liste BLOB'ları |Hayır |Hayır |

Merhaba SetContainerACL tarafından tanımlanan (*) izinleri önbelleğe alınır ve güncelleştirmeleri toothese izinleri hangi dönemde güncelleştirmeleri değildir toopropagate toobe tutarlı garanti 30 saniye sürebilir.  

Merhaba aşağıdaki tabloda özetlenmiştir koşullu üstbilgileri gibi kabul hello blobu işlemleri **IF-Match** hello istek ve hello yanıt ETag değeri döndürür.

| İşlem | ETag değeri döndürür | Koşullu üstbilgileri kabul eder |
|:--- |:--- |:--- |
| BLOB yerleştirme |Evet |Evet |
| BLOB alma |Evet |Evet |
| BLOB özelliklerini alma |Evet |Evet |
| Blob özelliklerini ayarlama |Evet |Evet |
| BLOB meta verileri alma |Evet |Evet |
| BLOB meta verileri ayarlama |Evet |Evet |
| Kira blob'u (*) |Evet |Evet |
| Anlık görüntü Blob |Evet |Evet |
| BLOB kopyalama |Evet |Evet (kaynak ve hedef blob için) |
| Kopya Blob Durdur |Hayır |Hayır |
| BLOB Sil |Hayır |Evet |
| Blok yerleştirme |Hayır |Hayır |
| Engelleme listesi yerleştirme |Evet |Evet |
| Engelleme listesi al |Evet |Hayır |
| Sayfa yerleştirin |Evet |Evet |
| Sayfa aralıklarını alma |Evet |Evet |

(*) Kira blob'u blob üzerinde hello ETag değiştirmez.  

### <a name="pessimistic-concurrency-for-blobs"></a>Eşzamanlılık BLOB'lar için
elde toolock özel kullanım için bir blob, bir [kira](http://msdn.microsoft.com/library/azure/ee691972.aspx) üzerindeki. Bir kira aldığınızda, ne kadar süreyle kira hello belirtin: Bu için 15 too60 saniye arasında bir değer veya sonsuz hangi tutarlar tooan özel kullanım kilidi olabilir. İle işiniz bittiğinde ve tüm kira serbest bırakabilirsiniz sınırlı kira tooextend yenileyebilirsiniz. Bunlar sona erdiğinde hello blob hizmeti otomatik olarak sınırlı kira serbest bırakır.  

Kira desteklenen farklı eşitleme stratejileri toobe özel yazma dahil olmak üzere etkinleştir / okuma, özel yazma paylaşılan / özel okuma ve yazma paylaşılan / özel okuyun. Bir kira var. burada hello Depolama Birimi Hizmeti (put, ayarlayın ve silme işlemleri) yazma hello Geliştirici tooensure tüm istemci uygulamaları aynı anda yalnızca bir istemci ve bir kira kimliği kullanın gerektirir ancak exclusivity okuma işlemleri için sağlama özel zorlar. Geçerli bir kira kimliği vardır. Bir kira kimliği sonucu paylaşılan okuma içermez okuma işlemleri.  

Merhaba aşağıdaki C# kod parçacığında 30 saniye kadar bir blob için özel bir kira alınırken, hello blob Merhaba içeriğine güncelleştirme ve hello kira serbest bırakma bir örneği gösterir. Zaten varsa geçerli bir kira hello blob üzerindeki tooacquire yeni bir kira çalıştığınızda, hello blob hizmeti bir "HTTP (409) çakışma" durum sonucunu döndürür. kullandığı aşağıdaki Hello kod parçacığını bir **AccessCondition** hello depolama hizmetinde bir istek tooupdate hello blob yaptığında tooencapsulate hello kiralama bilgilerini nesnesi.  Merhaba tam örnek buradan indirebilirsiniz: [Azure Storage kullanarak eşzamanlılık yönetme](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Hello kira kimliği geçmeden bir yazma işlemi kiralık blob çalışırsanız hello istek 412 bir hata ile başarısız olur. Merhaba, kiralama hello çağırmadan önce süresi Not **UploadText** yöntem, ancak hala hello kira kimliği geçişi, hello isteği ayrıca başarısız olan bir **412** hata. Merhaba kira bitiş zamanları ve kira kimlikleri yönetme hakkında daha fazla bilgi için bkz: [kira blob'u](http://msdn.microsoft.com/library/azure/ee691972.aspx) REST belgeleri.  

Merhaba aşağıdaki blobu işlemleri kiraları toomanage eşzamanlılık kullanabilirsiniz:  

* BLOB yerleştirme
* BLOB alma
* BLOB özelliklerini alma
* Blob özelliklerini ayarlama
* BLOB meta verileri alma
* BLOB meta verileri ayarlama
* BLOB Sil
* Blok yerleştirme
* Engelleme listesi yerleştirme
* Engelleme listesi al
* Sayfa yerleştirin
* Sayfa aralıklarını alma
* Anlık görüntü Blob - kira kimliği bir kira varsa, isteğe bağlı
* BLOB - bir kira hello hedef blob üzerindeki var olup olmadığını kimliği gerekli kira kopyalama
* Sonsuz bir kira hello hedef blob üzerindeki var olup olmadığını kira kimliği durdurma kopyalama Blob - gerekli
* Kira blob'u  

### <a name="pessimistic-concurrency-for-containers"></a>Eşzamanlılık kapsayıcıları için
Kiraları kapsayıcılarına hello BLOB'lar gibi aynı eşitleme stratejileri toobe desteklenmiyor etkinleştirmek (özel yazma / okuma, özel yazma paylaşılan / özel okuma ve yazma paylaşılan / özel okuma) ancak BLOB'lar hello depolama hizmeti yalnızca exclusivity zorlar üzerinde silme işlemleri. toodelete etkin bir kira ile bir kapsayıcı, bir istemci hello etkin kira hello silme isteği Kimliğiyle eklemeniz gerekir. Hello kira kimliği dahil olmak üzere diğer tüm kapsayıcı işlemleri kiralık bir kapsayıcıda başarılı durumda olduklarını işlemleri paylaşılan. Güncelleştirme (put veya kümesi) veya okuma işlemleri exclusivity gerekliyse, ardından geliştiriciler aynı anda bir istemci geçerli bir kira kimliğe sahip yalnızca bir kira kimliği ve, tüm istemcilerin kullanın emin olmalısınız  

Merhaba aşağıdaki kapsayıcı işlemleri kiraları toomanage eşzamanlılık kullanabilirsiniz:  

* Kapsayıcısını silmek
* Kapsayıcı özellikleri Al
* Kapsayıcı meta verileri alma
* Kapsayıcı meta verileri ayarlama
* Kapsayıcı ACL Al
* Kapsayıcı ACL ayarlayın
* Kira kapsayıcısı  

Daha fazla bilgi için bkz:  

* [Blob hizmeti işlemleri için koşullu üstbilgileri belirtme](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Kira kapsayıcısı](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Kira blob'u](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Eşzamanlılık hello tablo hizmeti yönetme
Merhaba tablo hizmeti iyimser eşzamanlılık burada açıkça tooperform iyimser eşzamanlılık denetimleri seçmelisiniz hello blob hizmeti aksine varlıklarla çalışırken hello varsayılan davranış olarak denetler kullanır. Merhaba diğer hello tablo ve blob hizmetleri arasında hello blob hizmeti ile Merhaba kapsayıcılara ve blob'lara eşzamanlılığı yönetebilir ancak hello eşzamanlılık varlıkların davranışlarındaki yalnızca yönetebilir farktır.  

toouse iyimser eşzamanlılık ve başka bir işlem hello tablo Depolama hizmetinden alınan bu yana bir varlık değiştirilirse toocheck, hello tablo hizmeti bir varlık döndürdüğünde aldığınız hello ETag değeri kullanabilirsiniz. Bu işlemin Hello anahat aşağıdaki gibidir:  

1. Bir varlık hello tablo Depolama hizmetinden alın, hello yanıt hello depolama hizmetindeki varlık ile ilişkili hello geçerli tanımlayıcı tanımlayan bir ETag değeri içeriyor.
2. Merhaba varlık güncelleştirdiğinizde hello zorunlu de 1. adımda alınan hello ETag değeri içeren **IF-Match** toohello hizmet gönderdiğiniz hello isteği üstbilgisi.
3. Merhaba hizmet hello istekteki hello ETag değeri hello varlık hello geçerli ETag değeri ile karşılaştırır.
4. Merhaba geçerli ETag değeri hello varlığın hello zorunlu hello ETag farklı ise **IF-Match** hello isteği, hello hizmet üstbilgisinde toohello istemci 412 hata döndürür. Bu, başka bir işlem hello istemci, alınan bu yana hello varlık güncelleştirdi toohello istemci gösterir.
5. Merhaba varlık Hello geçerli ETag değeri olan hello varsa ETag hello zorunlu hello aynı **IF-Match** hello istek veya hello üstbilgisinde **IF-Match** üstbilgisi hello joker karakter (*) hello hizmeti içerir gerçekleştirir hello istenen işlemi ve güncelleştirmeleri hello hello varlık tooshow güncelleştirilmiş geçerli ETag değeri.  

Not Hello blob hizmeti hello istemci tooinclude hello tablo hizmeti gerektiren bir **IF-Match** güncelleştirme isteği başlığı. Ancak, olası tooforce bir koşulsuz olur (son yazıcı WINS stratejisi) güncelleştirin ve hello istemci hello ayarlarsa eşzamanlılık denetimlerini atlamak **IF-Match** üstbilgi toohello joker karakter (*) hello isteği.  

C# kod parçacığında aşağıdaki hello ya da daha önce oluşturulmuş veya güncelleştirilmiş kendi e-posta adresi alınan bir müşteri varlığı gösterir. Merhaba ilk ekleme işlemi depoları hello ETag değeri veya hello müşteri nesnesindeki ve hello örnek kullandığından hello hello yürüttüğünde aynı nesne örneğini değiştirme işlemi, hello ETag değeri geri toohello tablo hizmeti otomatik olarak gönderir Merhaba hizmet toocheck eşzamanlılık ihlalleri için etkinleştiriliyor. Başka bir işlem tablo depolama hello varlık güncelleştirdi, hello hizmeti bir HTTP 412 (önkoşul başarısız oldu) durum iletisi döndürür.  Merhaba tam örnek buradan indirebilirsiniz: [Azure Storage kullanarak eşzamanlılık yönetme](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly hello eşzamanlılık denetimi devre dışı bırakmak, hello ayarlamalısınız **ETag** hello özelliğinin **çalışan** çok nesne "*" Merhaba değiştirme işlemini yürütmeden önce.  

```csharp
customer.ETag = "*";  
```

Merhaba aşağıdaki tabloda hello tablo varlık işlemleri ETag değerleri kullanma özetlenmektedir:

| İşlem | ETag değeri döndürür | IF-Match istek üstbilgisi gerektirir |
|:--- |:--- |:--- |
| Sorgu varlıklar |Evet |Hayır |
| Varlık ekleme |Evet |Hayır |
| Varlık güncelleştir |Evet |Evet |
| Varlık birleştirme |Evet |Evet |
| Varlığı silme |Hayır |Evet |
| Ekleme veya değiştirme varlık |Evet |Hayır |
| INSERT veya birleştirme varlık |Evet |Hayır |

Bu hello unutmayın **ekleme veya değiştirme varlık** ve **ekleme veya birleştirme varlık** işlemleri yapıp *değil* bir ETag değeri toohello göndermeyin her eşzamanlılık denetim gerçekleştirilemiyor Tablo hizmeti.  

Genel tabloları kullanarak geliştiricilerin ölçeklenebilir uygulamalar geliştirirken üzerinde iyimser eşzamanlılık yararlanmalıdır. Kötümser kilitleme gerekirse bir yaklaşım geliştiriciler tabloları erişme tooassign her tablo için atanmış bir blob olduğunda götürün ve hello tablosunda işletim önce tootake hello blob üzerinde bir kira deneyin. Bu yaklaşım hello uygulama tooensure tüm veri erişim gerektiren yolları elde hello kira önceki toooperating hello tablosunda. Ayrıca, ölçeklenebilirlik için dikkat gerektiren hello minimum kira süresi 15 saniye olduğuna dikkat edin.  

Daha fazla bilgi için bkz:  

* [Varlıklar üzerinde işlemler](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Eşzamanlılık hello sıra hizmeti yönetme
Hangi eşzamanlılık hello Çağrısı hizmetindeki bir sorun olduğu bir senaryo, burada birden çok istemciye iletilerin bir kuyruktan alıyor ' dir. Merhaba kuyruktan bir ileti alındığında hello yanıt selamlama iletisine ve gerekli toodelete hello iletisi pop giriş değeri içeriyor. Selamlama iletisine hello sıradan otomatik olarak silinmez, ancak bunu alındıktan sonra görünür tooother istemcileri hello visibilitytimeout parametresi tarafından belirtilen zaman aralığı hello olmadığı. Merhaba iletiyi alır hello istemci beklenen toodelete hello işlendikten sonra hello önce zaman hello tarafından TimeNextVisible öğesi yanıtının hello değerine göre hello visibilitytimeout hesaplanan Merhaba, belirtilen iletisidir parametre. visibilitytimeout Hello değeri toodetermine hello TimeNextVisible değerini toohello zaman hangi hello ileti alınan eklenir.  

Merhaba sıra hizmeti iyimser veya kötümser eşzamanlılık desteği yok ve bir ıdempotent şekilde işlenen iletileri bir sıradan alınan iletileri işleme neden istemcileri bu için emin olmalısınız. Bir son yazıcı WINS stratejisi SetQueueServiceProperties, SetQueueMetaData, SetQueueACL ve UpdateMessage gibi güncelleştirme işlemleri için kullanılır.  

Daha fazla bilgi için bkz:  

* [Kuyruk hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [İletileri alma](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Eşzamanlılık hello dosya hizmeti yönetme
Merhaba dosya hizmeti, iki farklı protokol uç noktalarını – SMB ve REST kullanarak erişilebilir. Merhaba REST hizmeti İyimser kilitleme veya kötümser kilitleme için destek yok ve tüm güncelleştirmeleri bir son yazıcı WINS stratejisi izler. Dosya paylaşımları bağlama SMB istemcileri hello özelliği tooperform kötümser kilitleme dahil olmak üzere dosya sistemi kilitleme mekanizmaları toomanage erişim tooshared dosya – yararlanabilirsiniz. SMB istemcisi bir dosya açıldığında hello dosya erişim ve Paylaşım belirtir modu. Bir dosya erişimi seçeneğiyle "Yazma" veya "Okuma/yazma", "None" dosya paylaşımı modu ayarı hello dosya kapatılana kadar bir SMB istemci tarafından kilitleniyor hello dosyasında neden olur. SMB istemcisi kilitli hello dosya sahip olduğu bir dosyada REST işlemini denenirse hello REST hizmeti hata kodu SharingViolation durum koduyla 409 (Çakışma) döndürür.  

SMB istemcisi silme için bir dosya açıldığında, bu dosyada açık tanıtıcıların bekleyen silme diğer tüm SMB istemci kadar kapalı olarak hello dosyayı işaretler. Bir dosya bekleyen silme olarak işaretlenmiş, ancak bu dosya üzerinde herhangi bir REST işlemi hata kodu SMBDeletePending durum koduyla 409 (Çakışma) döndürür. Merhaba SMB istemci tooremove hello bekleyen silme bayrağı önceki tooclosing hello dosya mümkün olduğundan, durum kodu 404 (bulunamadı) döndürülmez. Diğer bir deyişle, durum kodu 404 (bulunamadı), yalnızca Hello dosya kaldırıldığında beklenir. Delete durumu bekleyen bir SMB dosya olarak kullanılırken, sonuçları liste dosyaları hello katılmaz olduğunu unutmayın. Ayrıca hello REST Dosya Sil ve REST dizin silme işlemlerini otomatik olarak uygulanır ve bekleyen yol açmamasını Not durumu silin.  

Daha fazla bilgi için bkz:  

* [Dosya Yönetimi kilitler](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Özet ve sonraki adımlar
Merhaba Microsoft Azure depolama hizmeti toomeet hello hello en karmaşık çevrimiçi uygulamalar ihtiyaçlarını tootake gelmiş geliştiriciler toocompromise veya zorlanıyor temel tasarım varsayımları eşzamanlılık ve veri tutarlılığı gibi zorlamadan tasarlanmış verilen için.  

Merhaba, bu Web Günlüğü'ndeki başvurulan örnek uygulama tamamlayın:  

* [Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Azure Storage bakın hakkında daha fazla bilgi için:  

* [Microsoft Azure depolama giriş sayfası](https://azure.microsoft.com/services/storage/)
* [Giriş tooAzure depolama](storage-introduction.md)
* Başlarken depolama [Blob](storage-dotnet-how-to-use-blobs.md), [tablo](storage-dotnet-how-to-use-tables.md), [sıraları](storage-dotnet-how-to-use-queues.md), ve [dosyaları](storage-dotnet-how-to-use-files.md)
* Depolama mimarisi – [Azure Storage: güçlü tutarlılık sahip yüksek oranda kullanılabilir bulut depolama hizmeti](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

