---
title: "aaaUsing paylaşılan erişim imzaları (SAS) Azure storage'da | Microsoft Docs"
description: "BLOB, kuyruklar, tablolar ve dosyaları da dahil olmak üzere toouse paylaşılan erişim imzaları (SAS) toodelegate erişim tooAzure, depolama kaynaklarını öğrenin."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Paylaşılan erişim imzaları (SAS) kullanma

Paylaşılan erişim imzası (SAS) depolama hesabınızdaki bir şekilde toogrant sınırlı erişim tooobjects tooother istemciler, hesap anahtarınızı sokmadan sağlar. Bu makalede, biz hello SAS modeline genel bakış sağlayan, SAS en iyi uygulamaları incelemek ve bazı örneklere bakın.

Burada sunulan olanlar SAS kullanarak ek kod örnekleri için bkz: [.NET içinde Azure Blob Storage ile çalışmaya başlama](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) ve diğer örnekler hello kullanılabilir [Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=storage) kitaplığı. Merhaba örnek uygulamaları indir ve bunları çalıştırma veya hello kodu github'da göz atın.

## <a name="what-is-a-shared-access-signature"></a>Paylaşılan erişim imzası nedir?
Paylaşılan erişim imzası depolama hesabınızda atanmış erişim tooresources sağlar. Bir SAS ile hesap anahtarlarınızı paylaşmadan tooresources depolama hesabınızdaki istemciler erişim izni verebilir. Bu, uygulamalarınızı--SAS paylaşılan erişim imzaları kullanma hello anahtar noktasıdır hesap anahtarlarınızı tehlikeye olmadan depolama kaynaklarınıza güvenli şekilde tooshare olduğu.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

Bir SAS hello dahil olmak üzere SAS sahip tooclients vermek erişim hello türü üzerinde ayrıntılı denetim sağlar:

* hello aralığı hangi hello SAS hello başlangıç saati ve hello sona erme saati dahil olmak üzere, geçerli değil.
* SAS Hello tarafından hello izinler. Örneğin, bir blob için bir SAS okuma izni ve izinleri toothat blob yazma, ancak izinleri silmemeniz.
* İsteğe bağlı bir IP adresi veya Azure Storage kabul edeceği IP adresleri aralığı SAS hello. Örneğin, tooyour kuruluş ait bir IP adresi aralığı belirtebilirsiniz.
* Merhaba protokolü üzerinden Azure Storage hello SAS kabul eder. HTTPS kullanarak bu isteğe bağlı bir parametre toorestrict erişim tooclients kullanabilirsiniz.

## <a name="when-should-you-use-a-shared-access-signature"></a>Ne zaman bir paylaşılan erişim imzası kullanmalısınız?
Depolama hesabınızın erişim anahtarlarını işlediği değil, depolama hesabı tooany istemcisinde tooprovide erişim tooresources istediğinizde bir SAS kullanabilirsiniz. Depolama hesabınızı hem her ikisi de yönetici erişimi tooyour hesaba verin bir birincil ve ikincil erişim anahtarını ve içerdiği tüm kaynaklar içerir. Bu anahtarları birini gösterme, kötü amaçlı ya da ihmalkar kullanım hesap toohello olasılığını açılır. Paylaşılan erişim imzaları tooread, yazma ve silme verilerini açıkça verilen toohello izinlerine göre depolama hesabınızda ve hesap anahtarı gereksinimi olmadan istemcilerin güvenli bir alternatif sunar.

Bir SAS yararlı olduğu yaygın bir senaryo, kullanıcıların okuma ve yazma kendi veri tooyour depolama hesabı bir hizmettir. Bir depolama hesabı kullanıcı verilerini depoladığı bir senaryoda, iki tipik tasarım modeli vardır:

1. İstemciler, indirin ve kimlik doğrulaması yapan bir ön uç proxy hizmeti aracılığıyla veri yükleyin. Bu ön uç proxy hizmeti iş kuralları doğrulanması izin vererek hello avantajına sahiptir, ancak büyük miktarlarda veri veya yüksek hacimli işlemleri için toomatch talep ölçeklenebilen bir hizmet oluşturuluyor pahalı ya da zor olabilir.

  ![Senaryo diyagramı: ön uç proxy hizmeti](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Basit bir hizmet hello istemci gerektiği şekilde doğrular ve ardından bir SAS oluşturur. Merhaba SAS Hello istemci aldıktan sonra doğrudan hello SAS tarafından ve SAS hello tarafından izin verilen hello aralığı için tanımlanan hello izinlerine sahip depolama hesabı kaynaklarına erişebilir. Merhaba SAS hello ön uç proxy hizmeti üzerinden tüm verileri yönlendirme hello gereksinimini azaltır.

  ![Senaryo diyagramı: SAS sağlayıcı hizmeti](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

Pek çok gerçek dünya hizmet bu iki yaklaşımdan karma kullanabilir. Örneğin, bazı veriler işlenen ve diğer verileri kaydedilen ve/veya SAS kullanarak doğrudan okuma sırasında hello ön uç proxy doğrulanabilir.

Ayrıca, belirli senaryolarda bir kopyalama işleminde SAS tooauthenticate hello kaynak nesne toouse gerekir:

* Farklı depolama hesabında bulunduğu bir blob tooanother blob kopyaladığınızda, SAS tooauthenticate hello kaynak blob kullanmanız gerekir. İsteğe bağlı olarak bir SAS tooauthenticate hello hedef blob de kullanabilirsiniz.
* Farklı depolama hesabında bulunduğu bir dosya tooanother dosya kopyaladığınızda, SAS tooauthenticate hello kaynak dosyası kullanmanız gerekir. İsteğe bağlı olarak bir SAS tooauthenticate hello hedef dosya de kullanabilirsiniz.
* Bir blob tooa dosyası veya dosya tooa blob kopyaladığınızda, hello kaynak ve hedef nesneler hello içinde aynı bulunurlar olsa bile bir SAS tooauthenticate hello kaynak nesnesi kullanmalısınız depolama hesabı.

## <a name="types-of-shared-access-signatures"></a>Paylaşılan erişim imzaları türleri
İki tür paylaşılan erişim imzası oluşturabilirsiniz:

* **Hizmet SAS.** Merhaba hizmet SAS temsilciler erişim tooa kaynak yalnızca bir hello depolama hizmetleri: Blob, kuyruk, tablo veya dosya hizmeti hello. Bkz: [hizmet SAS oluşturma](https://msdn.microsoft.com/library/dn140255.aspx) ve [hizmet SAS örnekler](https://msdn.microsoft.com/library/dn140256.aspx) hello hizmet SAS belirteci oluşturma hakkında ayrıntılı bilgi.
* **Hesap SAS.** bir veya daha fazla hello depolama hizmet tooresources Hello hesap SAS temsilcileri erişin. Tüm hizmet SAS kullanılabilir hello işlemlerinin de hesap SAS kullanılabilir. Ayrıca, hello hesap SAS ile hizmeti gibi verilen tooa uygulamak erişim toooperations devredebilirsiniz **Get/Set hizmet özellikleri** ve **hizmeti istatistikleri almak**. Ayrıca, erişim tooread, yazma ve silme işlemleri blob kapsayıcılar, tablolar, kuyruklar ve hizmet SAS ile izin verilmiyor dosya paylaşımları üzerinde devredebilirsiniz. Bkz: [bir hesap SAS oluşturma](https://msdn.microsoft.com/library/mt584140.aspx) hello hesap SAS belirteci oluşturma hakkında ayrıntılı bilgi.

## <a name="how-a-shared-access-signature-works"></a>Paylaşılan erişim imzası nasıl çalışır?
Paylaşılan erişim imzası tooone ya da daha fazla depolama kaynaklarını işaret ve özel bir sorgu parametreleri kümesini içeren bir belirteç içeren imzalı bir URI değil. Merhaba belirteci nasıl hello istemci tarafından hello kaynaklara erişebilir gösterir. Merhaba sorgu parametrelerden biri, imza Merhaba, hello SAS parametrelerinden oluşturulur ve hello hesap anahtarı ile imzalanmış. Bu imza Azure Storage tooauthenticate hello SAS tarafından kullanılır.

Bir SAS URI'sini, gösteren hello kaynak URI'si ve hello SAS belirteci bir örneği burada verilmiştir:

![SAS URI'sini bileşenleri](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

Merhaba SAS belirteci hello üzerinde oluşturduğunuz bir dizedir *istemci* yan (Merhaba bkz [SAS örnekler](#sas-examples) bölüm kod örnekleri için). Merhaba depolama istemci kitaplığı ile oluşturduğunuz bir SAS belirteci Örneğin, Azure Storage tarafından herhangi bir şekilde izlenmez. SAS belirteci sınırsız sayıda hello istemci tarafında oluşturabilirsiniz.

Bir istemci isteğinin bir parçası bir SAS URI'sini tooAzure depolama sağladığında, hello hizmeti hello SAS parametreleri ve imza tooverify hello isteği kimlik doğrulaması için geçerli olduğunu denetler. Merhaba hizmeti bu hello imza geçerli doğrularsa hello isteği doğrulanır. Aksi takdirde, 403 (Yasak) hata koduyla hello isteği reddedildi.

## <a name="shared-access-signature-parameters"></a>Paylaşılan erişim imzası parametreleri
Hello hesap SAS ve hizmet SAS belirteci bazı ortak parametreler içerir ve ayrıca bazı parametreler farklı alın.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Parametreleri ortak tooaccount SAS ve hizmet SAS belirteci
* **API sürümü** hello depolama hizmeti sürüm toouse tooexecute hello isteğini belirten isteğe bağlı bir parametre.
* **Hizmet sürümünü** hello depolama hizmeti sürüm toouse tooauthenticate hello isteğini belirten gerekli bir parametre.
* **Başlangıç zamanı.** Bu hangi hello SAS geçerli hale geldiği hello zamandır. paylaşılan erişim imzası için Hello başlangıç saati isteğe bağlıdır. Bir başlangıç saati atlanırsa hello SAS hemen etkili olur. Merhaba başlangıç saati UTC (Eşgüdümlü Evrensel Saat), bir özel UTC göstergesi ("Z") ile örneğin ifade edilmesi gerekir `1994-11-05T13:15:30Z`.
* **Sona erme saati.** Bu sonra hello SAS artık geçerli olmayan hello zamandır. En iyi uygulamalar için bir SAS bir sona erme saati belirtin veya bir saklı erişim ilkesi ile ilişkilendirebilirsiniz öneririz. Merhaba sona erme saati UTC (Eşgüdümlü Evrensel Saat), bir özel UTC göstergesi ("Z") ile örneğin ifade edilmesi gerekir `1994-11-05T13:15:30Z` (daha aşağıya bakın).
* **İzinler.** SAS Hello üzerinde belirtilen hello izinlerini hello istemci hello depolama kaynağı karşı hello SAS kullanarak gerçekleştirebilirsiniz hangi işlemleri gösterir. İzinleri hesap SAS ve hizmet SAS için farklıdır.
* **IP.** Bir IP adresi veya bir IP adresi aralığı Azure dışında belirten isteğe bağlı bir parametre (Merhaba bölümüne bakın [yönlendirme oturum yapılandırma durumu](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) hızlı rota için) hangi tooaccept istekler.
* **Protokol.** Hello protokolü belirten isteğe bağlı parametresi bir istek için izin verilir. Olası değerler şunlardır: HTTPS ve HTTP (`https,http`), olduğu hello varsayılan değer veya HTTPS yalnızca (`https`). HTTP yalnızca izin verilen değeri olmadığını unutmayın.
* **İmza.** Merhaba imza hello oluşturulan diğer parametreleri bölümü belirteci olarak belirtilen ve sonra da şifrelenir. Tooauthenticate hello SAS kullandı.

### <a name="parameters-for-a-service-sas-token"></a>Hizmet SAS belirteci için parametreler
* **Depolama kaynağı.** Bir hizmeti ile erişim devredebilirsiniz depolama kaynaklarını SAS şunlardır:
  * Kapsayıcılar ve bloblar
  * Dosya paylaşımları ve dosyaları
  * Kuyruklar
  * Tabloları ve tablo varlıkları aralıkları.

### <a name="parameters-for-an-account-sas-token"></a>Bir hesap SAS belirteci için parametreler
* **Hizmet veya hizmetleri.** Hesap SAS erişim tooone veya daha fazla hello depolama hizmet devredebilirsiniz. Örneğin, temsilciler toohello Blob ve dosya hizmetine erişim hesap SAS oluşturabilirsiniz. Veya temsilciler tooall dört Hizmetleri (Blob, kuyruk, tablo ve dosya) erişim SAS oluşturabilirsiniz.
* **Depolama kaynak türleri.** Hesap SAS tooone veya belirli bir kaynak yerine depolama kaynaklarını daha fazla sınıflar için geçerlidir. Bir hesap SAS toodelegate erişim oluşturabilirsiniz:
  * Hizmet düzeyi API'leri karşı hello depolama hesabı kaynağı olarak adlandırılır. Örnekler **Get/Set hizmet özellikleri**, **alma hizmeti istatistikleri**, ve **kapsayıcıları/sıraları/tablolar/paylaşımları**.
  * Her hizmet için hello kapsayıcı nesneleri karşı çağrılan kapsayıcı düzeyi API'leri: blob kapsayıcılar, kuyruklar, tablolar ve dosya paylaşımları. Örnekler **oluşturma/silme kapsayıcı**, **oluşturma/silme sıra**, **oluşturma/silme tablo**, **oluşturma/silme paylaşımı**, ve **listesi BLOB'lar/dosyaları ve dizinleri**.
  * BLOB, kuyruk iletileri, tablo varlıkları ve dosyaları karşı adlı nesne düzeyinde API'leri. Örneğin, **Put Blob**, **sorgu varlık**, **iletileri almak**, ve **dosyası oluştur**.

## <a name="examples-of-sas-uris"></a>SAS URI'ler örnekleri

### <a name="service-sas-uri-example"></a>Hizmet SAS URİ'si örneği

Bir hizmet sağlar SAS URI'sini okuma ve yazma izinleri tooa blob bir örneği burada verilmiştir. Merhaba tablo nasıl toohello SAS katkıda bulunan hello URI toounderstand her parçası keser:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Ad | SAS bölümü | Açıklama |
| --- | --- | --- |
| BLOB URI'si |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |Merhaba blob Hello adresi. HTTPS kullanarak önerilir unutmayın. |
| Depolama Hizmetleri sürümü |`sv=2015-04-05` |Depolama Hizmetleri sürüm 2012-02-12 ve daha sonra bu parametre hello sürüm toouse gösterir. |
| Başlangıç zamanı |`st=2015-04-29T22%3A18%3A26Z` |UTC saati belirtilmiş. Merhaba SAS toobe geçerli hemen isterseniz, hello başlangıç saati atlayın. |
| Sona erme saati |`se=2015-04-30T02%3A23%3A26Z` |UTC saati belirtilmiş. |
| Kaynak |`sr=b` |Merhaba, bir blob kaynaktır. |
| İzinler |`sp=rw` |SAS Hello tarafından hello izinler ve yazma (w) Read (r) içerir. |
| IP aralığı |`sip=168.1.5.60-168.1.5.70` |bir isteği kabul edilecek hello IP adresleri aralığı. |
| Protokol |`spr=https` |Yalnızca HTTPS kullanarak isteklerine izin verilir. |
| İmza |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Tooauthenticate erişim toohello blobu kullanılır. Merhaba imza dize oturum ve hello SHA256 algoritmasını kullanarak anahtarı üzerinden hesaplanır ve Base64 kodlama kullanılarak kodlanan bir HMAC değil. |

### <a name="account-sas-uri-example"></a>Hesap SAS URI'sini örneği

Hesap SAS kullandığı aynı ortak parametreler hello belirtecine hello örneği aşağıda verilmiştir. Bu parametreler, yukarıda açıklanan olduğundan, burada açıklanmamaktadır. Yalnızca Merhaba, SAS hello aşağıdaki tabloda açıklanan belirli tooaccount parametreleridir.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Ad | SAS bölümü | Açıklama |
| --- | --- | --- |
| Kaynak URI'si |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Merhaba Blob Hizmeti uç noktası, (GET ile çağrıldığında) hizmeti özelliklerini alma veya (KÜMESİYLE çağrıldığında) hizmet özelliklerini ayarlama parametrelere sahip. |
| Hizmetler |`ss=bf` |Merhaba SAS toohello Blob ve Dosya Hizmetleri için geçerlidir |
| Kaynak türleri |`srt=s` |Merhaba SAS tooservice düzeyindeki işlemleri uygular. |
| İzinler |`sp=rw` |Merhaba izinler erişim tooread vermek ve yazma işlemleri. |

İzinler sınırlı olduğuna toohello hizmet düzeyi, bu SAS erişilebilir işlemleriyle olan **Blob hizmeti özellik alma** (okuma) ve **Blob hizmeti özelliklerini ayarla** (yazma). Bununla birlikte, farklı olan bir kaynak URI, hello aynı SAS belirteci de etkilenebilir toodelegate erişimi çok kullanılan**Blob hizmeti istatistikleri almak** (okuma).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Bir SAS depolanmış erişim ilkesi ile denetleme
Paylaşılan erişim imzası iki biçimlerden birini gerçekleştirebilirsiniz:

* **Geçici SAS:** oluştururken bir geçici SAS hello başlangıç zamanı, bitiş saati ve hello SAS izinlerini tüm belirtilir SAS URI'sini hello (veya kapsanan, başlangıç saati burada atlanırsa hello durumda). Bu tür bir SAS hesap SAS veya hizmet SAS olarak oluşturulabilir.
* **Saklı erişim ilkesi ile SAS:** depolanmış erişim ilkesi bir kaynak kapsayıcı--bir blob kapsayıcısını tanımlanır, tablo, kuyruk, veya dosya paylaşımı--ve bir veya daha fazla paylaşılan erişim imzalar için kullanılan toomanage kısıtlamaları olabilir. Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, hello SAS hello kısıtlamaları--hello başlangıç saati, sona erme saati ve depolanan hello erişim ilkesi için tanımlanan izinleri--devralır.

> [!NOTE]
> Şu anda hesap SAS geçici bir SAS olmalıdır. Depolanmış. erişim ilkeleri SA hesabı için henüz desteklenmiyor.

Merhaba fark hello iki formlar arasında önemli bir senaryo için önemlidir: iptal. Bir SAS URI'si bir URL olduğundan hello alacağı herhangi bir kişi SAS, kimin ilk oluşturulduğu bağımsız olarak kullanabilirsiniz. Bir SAS yayımlandığını, hello world herkes tarafından kullanılabilir. Dört özelliklerinden biri işlem yapılana kadar işlediği bir SAS verir erişim tooresources tooanyone:

1. SAS ulaşıldığında hello üzerinde belirtilen hello bitiş saati.
2. SAS (depolanmış erişim ilkesi başvurulduğunda ve bir süre sonu zamanı belirtiyorsa) ulaşıldığında hello tarafından başvurulan depolanan hello erişim ilkesinde belirtilen hello bitiş saati. Bu, başlangıç aralığı sona erdiğinde olduğundan veya tek yönlü toorevoke hello SAS olan depolanan hello erişim ilkesi hello geçmiş, içinde bir sona erme saati ile değiştirdiğinden ortaya çıkabilir.
3. Merhaba, başka bir şekilde toorevoke hello SAS SAS silinir, hello tarafından başvurulan erişim ilkesi depolanır. Depolanan hello erişim ilkesi ile tam olarak yeniden aynı adı, tüm mevcut SAS hello açtıysanız belirteçler yeniden geçerli according toohello izinleri ile ilişkili olabilir (Bu SAS değil geçtikten hello hello bitiş zamanında varsayılarak) Bu saklı erişim ilkesi. Toorevoke hello SAS amaçlanıyorsa hello erişim ilkesi hello gelecekteki içinde bir sona erme saati ile yeniden farklı bir ad emin toouse olması.
4. kullanılan toocreate hello SAS olduğu hello hesap anahtarını yeniden oluşturur. Hesap anahtarı yeniden oluşturuluyor edilirse, bu anahtar toofail tooauthenticate kullanarak tüm uygulama bileşenleri güncelleştirilmiş kadar toouse ya da hello diğer geçerli hesap anahtarı veya hello yeni yeniden hesap anahtarı.

> [!IMPORTANT]
> Paylaşılan erişim imzası URI hello hesabı anahtar kullanılan toocreate hello imza ile ilişkili ve hello depolanmış erişim ilkesi (varsa) ilişkili. Hiçbir depolanmış erişim ilkesi belirtilirse, hello yalnızca yolu toorevoke paylaşılan erişim imzası toochange hello hesap anahtardır.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Bir istemci uygulamadan bir SAS ile kimlik doğrulaması
Bir SAS elinde olan bir istemci hello SAS tooauthenticate bir isteği hello hesabı anahtarları sahip olmayan bir depolama hesabı kullanabilirsiniz. Bir SAS bağlantı dizesi ile birlikte veya doğrudan hello uygun oluşturucunun ya da yöntemi kullanılır.

### <a name="using-a-sas-in-a-connection-string"></a>Bir SAS bağlantı dizesiyle
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>SAS Oluşturucusu veya yöntemi kullanarak
İstek toohello hizmet SAS ile doğrulanabilmesi birkaç Azure Storage istemci kitaplığı oluşturucular ve yöntemi aşırı bir SAS parametre sunar.

Örneğin, burada bir SAS URI'sini kullanılan toocreate başvuru tooa blok blobu verilmiştir. Merhaba SAS hello istek için gereken hello yalnızca kimlik bilgileri sağlar. Merhaba blok blob başvurusu daha sonra bir yazma işlemi için kullanılır:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>SAS kullanırken en iyi uygulamalar
Paylaşılan erişim imzaları uygulamalarınızda kullandığınızda, toobe iki olası riskleri farkında gerekir:

* Bir SAS sızmasını varsa, depolama hesabınız tehlikeye atabilir aldığı herkes tarafından kullanılabilir.
* Bir SAS tooa istemci uygulamanın süresi dolduktan ve hello uygulamanın oluşturulamıyor tooretrieve hizmetinizden yeni bir SAS verdiyse, hello uygulamanın işlevselliğini engelliyordu.

Merhaba paylaşılan erişim imzaları kullanma aşağıdaki öneriler bu riskleri azaltmaya yardımcı:

1. **Her zaman HTTPS kullanmak** toocreate veya bir SAS dağıtabilirsiniz. Bir SAS ise ve HTTP üzerinden geçirilen ele man-in--middle saldırısı gerçekleştiren bir saldırgan mümkün tooread hello SAS olduğu ve yalnızca olası hassas verileri tehlikeye veya veri bozulması hello tarafından izin vererek kullanıcı olabilir hello tasarlandığı gibi kullanın kötü amaçlı kullanıcı.
2. **Başvuru erişim ilkeleri, mümkün olduğunda depolanır.** Erişim ilkeleri verin tooregenerate hello depolama hesabı anahtarlarını gerek kalmadan seçeneği toorevoke izinleri hello depolanır. Merhaba sona erme süresini ayarlamanıza bu kadar çok hello üzerinde gelecekteki (veya sonsuz) ve emin toomove düzenli olarak güncelleştirdi uzağa hello gelecekteki içine.
3. **Zaman aşımı değeri yakın dönemde üzerinde geçici bir SAS kullanın.** Bir SAS tehlikede olsa bile bu şekilde, onu yalnızca kısa bir süre için geçerli değil. Bu yöntem, depolanmış erişim ilkesi başvuramaz, özellikle önemlidir. Yakın dönemde zaman aşımı değeri de hello tooa blob hello zaman kullanılabilir tooupload tooit sınırlayarak yazılabilir veri miktarını sınırlayın.
4. **İstemcilerin otomatik olarak hello SAS gerekirse yenileme yoktur.** İstemcileri hello SAS iyi hello geçerliliği sona ermeden önce sipariş tooallow zamanında hello SAS sağlayan hello hizmet kullanılamıyorsa, yeniden deneme yenilemeniz. Az sayıda hemen için kullanılan toobe, SAS istediyseniz, kısa süreli işlemleri hello sona erme süresi içinde tamamlandı toobe beklenen sonra bu SAS değil hello yenilendi toobe beklendiği gibi gereksiz olabilir. Ancak, düzenli olarak SAS aracılığıyla istek yapıyor istemciniz varsa, sona erme hello olasılığını oyuna gelir. (daha önce belirtildiği gibi) hello SAS toobe kısa süreli istemci hello hello gerek tooensure ile yenileme erken isteyen için hello anahtar toobalance hello gerek husustur yeterli (tooavoid kesintisi) toohello SAS süresi dolan önceki toosuccessful yenileme son.
5. **SAS başlangıç tarihine sahip dikkatli olun.** Hello başlangıç zamanı için bir SAS çok ayarlarsanız**şimdi**, sonra da tooclock eğme (toodifferent makineler göre geçerli saat farklılıkları) hataları aralıklı hello için ilk birkaç dakika gözlenecek. Genel olarak, hello başlangıç saati toobe en az 15 dakika hello geçmiş ayarlayın. Ya da hiç, bunu hemen tüm durumlarda geçerli yapacak ayarlamanız gerekmez. aynı genellikle de--tooexpiry zaman geçerlidir hello unutmayın saatinin too15 dakikada herhangi bir istek üzerinde herhangi bir yönde eğme gözlemlemek. Bir REST sürüm önceki too2012-02-12 kullanan istemciler için bir saklı erişim ilkesi başvurmayan bir SAS için en uzun süre hello 1 saat, başarısız olur daha uzun vadeli belirterek tüm ilkeleri ise.
6. **Merhaba kaynak toobe erişilen özgün olmalıdır.** En iyi güvenlik uygulaması tooprovide hello minimum gerekli ayrıcalıklara sahip bir kullanıcı değil. Bir kullanıcının yalnızca okuma erişimi tooa tek bir varlık gerekirse, daha sonra bunları okuma erişimi toothat tek bir varlık ve değil okuma/yazma/silme erişim tooall varlıkları verin. Bu, aynı zamanda hello SAS saldırgan hello elinizde daha az güç olduğundan SAS aşılıp aşılmadığını hello hasar azaltmak yardımcı olur.
7. **Hesabınız ile SAS yapılan dahil olmak üzere tüm kullanım için Fatura edilecek anlayın.** Yazma erişimi tooa blob sağlarsanız, bir kullanıcı 200 GB blob tooupload seçebilirsiniz. Okuma erişimi verdiniz, toodownload seçebilir, 10 kez 2 TB çıkış yansıtılmasını maliyetleri sizin için. Yeniden sınırlı izinleri sağlayan toohelp kötü amaçlı kullanıcılar olası eylemleri hello etkisini azaltır. Bu tehdit kısa süreli SAS tooreduce kullanın (ancak saatinin hello son saat eğriltme oluşturduğunu).
8. **SAS kullanarak yazılan veriler doğrulayın.** Bir istemci uygulaması veri tooyour depolama hesabı yazarken, verileri sorunları olabilir aklınızda bulundurun. Uygulamanız, veri doğrulanması gereken ya hazır toouse önce yetkili gerektiriyorsa, bu doğrulama hello veri yazıldıktan sonra ve uygulamanız tarafından kullanılan önce gerçekleştirmeniz gerekir. Bu yöntem aynı zamanda tooyour hesabı düzgün bir şekilde hello SAS alınan bir kullanıcı tarafından veya bir sızan SAS yararlanmasını bir kullanıcı tarafından yazılan bozuk veya kötü amaçlı veriler korur.
9. **Her zaman SAS kullanmayın.** Bazen, depolama hesabınız karşı belirli bir işlemle ilişkili hello riskleri SAS hello avantajlarından daha ağır basar. Bu tür işlemler için iş gerçekleştirildikten sonra tooyour depolama hesabı Yazar bir orta katman hizmet oluşturma kuralı doğrulama, kimlik doğrulaması ve denetim. Ayrıca, bazen onu diğer yollarla daha basit toomanage erişimi vardır. Bir kapsayıcıdaki tüm blob'lara toomake herkes tarafından okunabilir istiyorsanız örneğin, kapsayıcı Ortak, hello yapabileceğiniz bir SAS tooevery istemci erişimi için sağlama yerine.
10. **Storage Analytics toomonitor uygulamanızın kullanın.** Günlüğe kaydetme ve herhangi bir kimlik doğrulama hatalarına tooan kesinti, SAS sağlayıcısı hizmeti toohello yanlışlıkla kaldırma veya depolanmış erişim ilkesi, son çıkmasına ölçümleri tooobserve kullanabilirsiniz. Merhaba bkz [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) ek bilgi için.

## <a name="sas-examples"></a>SAS örnekleri
Aşağıda bazı örnekler her iki tür paylaşılan erişim imzalar, hesap SAS ve SAS hizmet.

toorun bu C# örnekleri, projenizdeki NuGet paketlerini aşağıdaki tooreference hello gerekir:

* [.NET için Azure Storage istemci Kitaplığı](http://www.nuget.org/packages/WindowsAzure.Storage), sürüm 6.x veya üzeri (toouse hesap SAS).
* [Azure Configuration Manager](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Toocreate ve test bir SAS nasıl görürüm gösteren ek örnekler için [depolama için Azure Kod örnekleri](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Örnek: Oluşturma ve hesap SAS kullanma
Merhaba aşağıdaki kod örneği oluşturur hesap hello Blob ve Dosya Hizmetleri için geçerli olan SAS ve istemci izinleri okuma, yazma ve listeleme izinleri verir hello tooaccess hizmet düzeyi API'leri. Merhaba istek HTTPS ile yapılmalıdır şekilde hello hesap SAS hello Protokolü tooHTTPS kısıtlar.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse hello hesap SAS tooaccess hello Blob hizmeti için API hizmet düzeyi, hello SAS kullanarak bir Blob istemci nesnesi oluşturun ve depolama hesabınız için Blob storage uç hello.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Örnek: bir saklı erişim ilkesi oluşturma
Merhaba aşağıdaki kod bir saklı erişim ilkesi bir kapsayıcıda oluşturur. Hizmet SAS hello kapsayıcısı üzerinde veya bloblarını hello erişim ilkesi toospecify kısıtlamalarını kullanabilirsiniz.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Örnek: bir kapsayıcıda hizmet SAS oluşturma
koddan hello SAS bir kapsayıcıda oluşturur. Varolan bir depolanmış erişim ilkesinin Hello adı sağlanmazsa, bu ilkeyi hello SAS ile ilişkilidir. Hiçbir depolanmış erişim ilkesi sağlanırsa, hello kod geçici SAS hello kapsayıcısını oluşturur.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Örnek: bir blob üzerindeki hizmet SAS oluşturma
koddan hello üzerinde bir blob SAS oluşturur. Varolan bir depolanmış erişim ilkesinin Hello adı sağlanmazsa, bu ilkeyi hello SAS ile ilişkilidir. Hiçbir depolanmış erişim ilkesi sağlanırsa, hello kod hello blob üzerindeki bir geçici SAS oluşturur.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Sonuç
Paylaşılan erişim imzalar, sınırlı izinlere hello hesap anahtarı olmamalıdır tooyour depolama hesabı tooclients sağlamak için yararlıdır. Bu nedenle, Azure Storage kullanarak herhangi bir uygulama için hello güvenlik modelinin önemli bir parçası olan. Burada listelenen hello en iyi uygulamaları izlerseniz, uygulamanızın hello güvenliği tehlikeye atmadan SAS tooprovide esneklik erişim tooresources, depolama hesabınızı kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
* [Anonim okuma erişimini toocontainers ve BLOB'ları yönetme](../blobs/storage-manage-access-to-resources.md)
* [Paylaşılan Erişim İmzası ile Erişim için Temsilci Seçme](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Tablo ve kuyruk SAS Tanıtımı](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
