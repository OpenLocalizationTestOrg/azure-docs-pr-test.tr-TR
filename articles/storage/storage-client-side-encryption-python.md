---
title: "Microsoft Azure Storage için Python aaaClient tarafı şifreleme | Microsoft Docs"
description: "Merhaba Python için Azure Storage istemci kitaplığı, Azure Storage uygulamalarınız için en yüksek güvenlik için istemci tarafı Şifreleme destekler."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: d2e943977322b97b777369508b957a1b2cbaa4e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Microsoft Azure depolama için istemci tarafı şifreleme Python ile
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Genel Bakış
Merhaba [Python için Azure Storage istemci Kitaplığı](https://pypi.python.org/pypi/azure-storage) tooAzure depolama karşıya yükleme ve toohello istemci indirilirken verilerin şifresini çözmek önce istemci uygulamalar içinde verilerin şifrelenmesi destekler.

> [!NOTE]
> Hello Azure depolama Python kitaplığı önizlemede değil.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Şifreleme ve şifre çözme hello Zarf teknik aracılığıyla
şifreleme ve şifre çözme Hello işlemleri hello Zarf teknik izleyin.

### <a name="encryption-via-hello-envelope-technique"></a>Merhaba Zarf teknik aracılığıyla şifreleme
Şifreleme hello Zarf teknik aracılığıyla hello aşağıdaki şekilde çalışır:

1. Hello Azure storage istemci kitaplığı simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) oluşturur.
2. Kullanıcı verileri bu CEK kullanılarak şifrelenir.
3. Merhaba CEK sonra (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir. Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da yerel olarak yönetilen bir simetrik anahtar olabilir.
   Merhaba depolama istemci kitaplığı kendisini hiçbir zaman erişim tooKEK sahiptir. Merhaba kitaplığı KEK hello tarafından sağlanan algoritması kaydırma hello anahtar çağırır. Kullanıcıların toouse anahtar kaydırma/isterseniz açmak için özel sağlayıcılar seçebilirsiniz.
4. Merhaba şifrelenmiş verileri ise toohello Azure depolama hizmeti karşıya yüklendi. Bazı ek şifreleme meta verilerle birlikte Hello Sarmalanan anahtarın meta veriler (hakkında bir blob) olarak depolanır veya (iletileri kuyruğa ve tablo varlıkları) ile şifrelenmiş hello veri Ara değerli.

### <a name="decryption-via-hello-envelope-technique"></a>Merhaba Zarf teknik aracılığıyla şifre çözme
Şifre çözme hello Zarf teknik aracılığıyla hello aşağıdaki şekilde çalışır:

1. Merhaba istemci kitaplığı hello kullanıcı hello anahtar şifreleme anahtarı (KEK) yerel olarak yönetme varsayar. Merhaba kullanıcı şifreleme için kullanılan tooknow hello özel anahtarı gerektirmez. Bunun yerine, farklı anahtar tanımlayıcıları tookeys çözümler, bir anahtar çözümleyici ayarlayabilir ve kullanılır.
2. Hello istemci kitaplığı hello şifrelenmiş veriler hello hizmette depolanan tüm şifreleme malzeme birlikte yükler.
3. sarmalanmamış (şifresi çözülmüş) kullanarak hello sonra anahtar şifreleme anahtarı (KEK) hello Sarmalanan içerik şifreleme anahtarı (CEK) olabilir. Burada yeniden hello istemci kitaplığı erişimi tooKEK sahip değil. Yalnızca, hello özel sağlayıcının açma algoritması çağırır.
4. şifreleme anahtarı (CEK) ise içerik Hello toodecrypt şifrelenmiş hello kullanıcı verilerini kullanılır.

## <a name="encryption-mechanism"></a>Şifreleme mekanizması
Merhaba depolama istemci kitaplığı kullanıp [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) sipariş tooencrypt kullanıcı verileri. Özellikle, [Şifre blok zincirleme (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) AES moduyla. Her bir hizmet works biraz farklı şekilde Burada bunların her birini aşağıdakiler ele alınacaktır.

### <a name="blobs"></a>Bloblar
Merhaba istemci kitaplığı şu anda yalnızca tüm blobları şifreleme desteklemektedir. Kullanıcıların hello kullandığınızda Şifreleme özellikle, desteklenen **oluşturma*** yöntemleri. Yüklemeleri, hem tam hem aralık yüklemeleri desteklenir ve her iki paralelleştirme karşıya yükleme ve indirme için kullanılabilir.

Şifreleme sırasında hello istemci kitaplığı rastgele başlatma vektörü (IV), 32 bayt rasgele bir içerik şifreleme anahtarı (CEK) ile birlikte 16 bayt oluşturmak ve bu bilgileri kullanarak hello blob verisi Zarf şifreleme gerçekleştirin. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra şifrelenmiş bir blobu hello hello hizmetinin yanı sıra meta verileri blob olarak depolanır.

> [!WARNING]
> Düzenleme veya kendi hello blob meta verilerini karşıya yükleme, bu meta veriler korunur tooensure gerekir. Bu meta veriler olmadan yeni meta veriler karşıya yükleme, Sarmalanan CEK Merhaba, IV ve diğer meta veriler kaybolur ve hello blob içeriğinin hiçbir zaman tekrar alınabilir.
> 
> 

Şifrelenmiş bir blobu indirme içerir hello tüm blob hello kullanarak Merhaba içeriğine alma **almak*** kullanışlı yöntemler. Sarmalanan CEK sarılmamış ve hello IV ile birlikte kullanılan hello (blob meta verileri bu durumda tooreturn şifresi hello veri toohello kullanıcıları depolanır).

Rastgele bir aralığı indirme (**almak*** aralığı parametreleri yöntemleriyle geçirilen) sipariş tooget kullanılabilir ek veri az miktarda bulunan kullanıcılar tarafından sağlanan hello aralığı ayarlama şifrelenmiş bir blobu hello içerir toosuccessfully şifresini çözme hello aralığı istedi.

Blok blobları ve sayfa BLOB'ları yalnızca şifrelenmiş şifresi/bu şeması kullanarak olabilir. Aynı zamanda şifreleme eklemek için BLOB'ları şu anda desteği yoktur.

### <a name="queues"></a>Kuyruklar
İletileri kuyruğa herhangi biçimi olamayacağından hello istemci kitaplığı hello başlatma vektörü (IV) ve hello şifrelenmiş içerik şifreleme anahtarı (CEK) hello metinde içeren özel bir biçim tanımlar.

Şifreleme sırasında hello istemci kitaplığı 16 bayt rastgele CEK 32 bayt yanı sıra rasgele bir IV oluşturur ve bu bilgileri kullanarak hello sıraya ileti metninin Zarf şifreleme gerçekleştirir. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra toohello şifrelenmiş kuyruk iletisi eklenir. (Aşağıda gösterilen) bu değiştirilmiş ileti hello hizmetinde depolanır.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Şifre çözme sırasında hello Sarmalanan anahtarı hello sıra iletiden ayıklanan ve sarılmamış. Merhaba IV ayrıca hello sıra iletiden ayıklanan ve sarılmamış hello anahtar toodecrypt hello kuyruk iletisi verilerle birlikte kullanılır. Bir kuyruk iletisi hello 64 KB sınırını doğru sayım sırasında hello etkisi yönetilebilir nedenle hello şifreleme meta verilerin (altında 500 bayt), küçük olduğunu unutmayın.

### <a name="tables"></a>Tablolar
İstemci Kitaplığı destekler şifreleme Ekle varlık özelliklerinin hello ve değiştirme işlemlerini.

> [!NOTE]
> Birleştirme şu anda desteklenmiyor. Bir alt özellikler kümesini daha önce farklı bir anahtar kullanılarak şifrelenmiş olabilecek olduğundan, sadece hello yeni özellikleri birleştirme ve hello meta verilerini güncelleştirme veri kaybına neden olur. Ya da birleştirme ek hizmet yapma tooread hello önceden var olan varlık hello hizmetinden çağıran veya yeni bir anahtar özellik başına kullanarak, her ikisi de performansı artırmak için uygun olmayan gerektirir.
> 
> 

Tablo verileri şifreleme gibi çalışır:

1. Kullanıcılar şifrelenmiş hello özellikleri toobe belirtin.
2. Merhaba istemci kitaplığı rastgele başlatma vektörü (IV) yanı sıra rasgele içerik bir şifreleme anahtarı (CEK) 32 bayt her varlık için 16 bayt oluşturur ve yeni bir IV başına türetme tarafından şifrelenmiş hello ayrı ayrı özellikler toobe Zarf şifreleme gerçekleştirir. özellik. şifrelenmiş hello özelliği ikili veri olarak depolanır.
3. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra iki ek ayrılmış özellikleri olarak depolanır. Merhaba, özelliği ilk ayrılmış (\_ClientEncryptionMetadata1) hello bilgilerini IV, sürüm ve Sarmalanan anahtarı tutan bir dize özelliğidir. Merhaba ikinci ayrılmış özelliği (\_ClientEncryptionMetadata2) hello özellikleri hakkında bilgi şifrelenmiş hello tutan ikili bir özelliktir. Bu ikinci özellik bilgileri Hello (\_ClientEncryptionMetadata2) kendisi şifrelenmiş olduğunu.
4. Şifreleme için gereken toothese ek ayrılmış özellikleri, kullanıcılar artık 252 yerine yalnızca 250 özel özelliklere sahip olabilir. Merhaba varlık Hello toplam boyutu 1 MB'tan az olması gerekir.
   
   Yalnızca dize özellikleri şifrelenmiş olduğunu unutmayın. Diğer türdeki özellikleri şifrelenmiş toobe varsa, bunların dönüştürülmüş toostrings olması gerekir. şifrelenmiş hello dizeleri hello hizmette ikili özellikleri olarak depolanır ve şifre çözme sonra geri toostrings (ham dizeleri, EntityProperties EdmType.STRING türüyle değil) dönüştürülür.
   
   Tablolar için ayrıca toohello şifreleme ilkesi, kullanıcıların şifrelenmiş hello özellikleri toobe belirtmeniz gerekir. Bu da bu özellikleri hello türü kümesi tooEdmType.STRING TableEntity nesneleriyle depolayarak yapılabilir ve kümesi tootrue veya ayar hello encryption_resolver_function hello tableservice nesnesinde şifreleyebilirsiniz. Bir şifreleme çözümleyici bölüm anahtarı, satır anahtarını ve özellik adını alır ve bu özellik şifrelenmesi gerekip gerekmediğini belirten bir Boole değeri döndüren bir işlevdir. Bir özellik toohello kablo yazılırken şifrelenmesi gerekip gerekmediğini şifreleme sırasında bu bilgileri toodecide hello istemci kitaplığını kullanın. Merhaba temsilci özellikler nasıl şifrelenir geçici mantığı hello olasılığı için de sağlar. (Örneğin, X ise ardından özelliği A şifrelemek; Aksi takdirde özellikleri A ve b şifreleme) Bu BT Not gerekli tooprovide okurken veya varlıklar sorgulama bu bilgilerdir.

### <a name="batch-operations"></a>Toplu işlemleri
Bir şifreleme ilkesi hello toplu tooall satır geçerlidir. Merhaba istemci kitaplığı dahili olarak yeni rastgele IV ve satır başına rastgele CEK hello toplu işlemde oluşturur. Kullanıcılar ayrıca tooencrypt her işlem için farklı özellikleri hello toplu işlemde Bu davranış hello şifreleme Çözümleyicisi tanımlayarak seçebilirsiniz.
Bir toplu hello tableservice batch() yöntemi ile bir bağlam Yöneticisi olarak oluşturduysanız hello tableservice'nın şifreleme ilkesi otomatik olarak uygulanan toohello toplu olacaktır. Bir toplu açıkça hello Oluşturucu çağırarak oluşturulursa hello şifreleme ilkesi parametre ve sol hello toplu hello ömrü boyunca değiştirilmemiş olarak geçirilmelidir.
Merhaba toplu iş şifreleme ilkesi (varlıklar hello tableservice'nın Şifreleme İlkesi'ni kullanarak hello toplu yürütülen hello zaman şifreli değildir) kullanarak hello toplu içine eklenen gibi varlıkları şifrelenmesini unutmayın.

### <a name="queries"></a>Sorgular
tooperform sorgu işlemleri yapabilir tooresolve olan anahtar çözümleyici belirtmelisiniz tüm anahtarları hello sonuç kümesinde hello. Merhaba sorgu sonucunda bulunan bir varlık çözümlenmiş tooa sağlayıcı olamazsa hello istemci kitaplığı bir hata durum oluşturur. Sunucu tarafı tahminleri gerçekleştirir herhangi bir sorgu için hello istemci kitaplığı hello özel şifreleme meta veri özelliklerini ekler (\_ClientEncryptionMetadata1 ve \_ClientEncryptionMetadata2) tarafından varsayılan toohello Seçili sütunları .

> [!IMPORTANT]
> İstemci tarafı şifreleme kullanırken bu önemli noktalara dikkat edin:
> 
> * Ne zaman okunurken veya yazılırken tooan blob, tüm blob karşıya yükleme komutları kullanın ve aralığı/bütün blob yükleme komutları şifrelenir. Put bloğu, Put engelleme listesi, yazma sayfaları veya Temizle sayfalar gibi Protokolü işlemleri kullanarak tooan şifrelenmiş bir blobu yazma kaçının; Aksi takdirde hello şifreli blob bozuk ve okunamaz olun.
> * Tablolar için benzer bir kısıtlama var. Merhaba şifreleme meta verilerini güncelleştirme olmadan dikkatli toonot şifrelenmiş güncelleştirme özellikleri olabilir.
> * Meta veri hello şifreli blob üzerindeki ayarlarsanız, hello şifrelemeyle ilgili meta verileri meta verileri ayarlama eklenebilir olmadığından şifre çözme için gerekli üzerine yazabilir. Bu da anlık görüntüler için geçerlidir; meta veri anlık görüntüsünü şifrelenmiş bir blobu oluşturulurken belirtmekten kaçının. Meta veriler ayarlanmalıdır emin toocall hello olması **get_blob_metadata** yöntemi ilk tooget geçerli şifreleme meta verilerin hello ve meta veri ayarlanırken eşzamanlı yazma kaçının.
> * Merhaba etkinleştirmek **require_encryption** hello hizmet nesnesi yalnızca şifrelenmiş verileri ile çalışması gereken kullanıcılar için bayrak. Aşağıda daha fazla bilgi için bkz.
> 
> 

Merhaba depolama istemci kitaplığı hello KEK ve anahtar Çözümleyicisi arabirimi aşağıdaki tooimplement hello sağlanan bekliyor. [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) Python KEK Yönetimi Beklemede ve tamamlandığında bu kitaplığa tümleşik desteği.

## <a name="client-api--interface"></a>İstemci API / arabirim
Depolama hizmet nesnesi (yani blockblobservice) oluşturulduktan sonra hello kullanıcı bir şifreleme ilkesi oluşturan toohello alanları değerleri atayabilirsiniz: key_encryption_key, key_resolver_function ve require_encryption. Kullanıcılar, yalnızca bir KEK sağlayabilir yalnızca Çözümleyici veya her ikisi de. key_encryption_key anahtar tanımlayıcısını kullanarak tanımlanır ve kaydırma/açmak için hello mantık sağlayan hello temel anahtar türüdür. key_resolver_function hello şifre çözme işlemi sırasında kullanılan tooresolve bir anahtar değil. Anahtar tanımlayıcısını verilen geçerli bir KEK döndürür. Bu, kullanıcıların hello özelliği toochoose birden fazla konumda yönetilen birden çok anahtar arasındaki sağlar.

Merhaba KEK hello aşağıdaki uygulanmalı yöntemleri toosuccessfully verileri şifreleme:

* wrap_key(cek): sarmalayan hello belirtilen hello kullanıcının tercih ettiğiniz bir algoritma kullanarak CEK (bayt). Döndürür hello anahtar sarılır.
* get_key_wrap_algorithm(): döndürür hello algoritması toowrap anahtarları kullanılır.
* get_kid(): Bu KEK için döndürür hello dize anahtarı kimliği.
  Merhaba KEK yöntemleri toosuccessfully şifre çözme veri aşağıdaki hello uygulamanız gerekir:
* unwrap_key (cek, algoritma): döndürür sarılmamış hello biçiminde hello belirtilen hello dize belirtilen algoritmasını kullanarak CEK.
* get_kid(): dize anahtar kimliği için bu KEK döndürür.

Merhaba anahtar çözümleyici en az, anahtar kimliği verilen hello karşılık gelen KEK uygulama hello arabirimi yukarıdaki döndüren bir yöntem uygulamalıdır. Bu yöntem yalnızca hello hizmet nesnesi üzerinde toohello key_resolver_function özelliğine atanan toobe kullanılır.

* Şifreleme için bir anahtarın hello olmaması bir hataya neden olur ve başlangıç anahtarı her zaman kullanılır.
* Şifre çözme için:
  
  * Merhaba anahtar çözümleyici tooget hello anahtarı belirtilmişse çağrılır. Merhaba çözümleyici belirtildi ancak hello anahtarı tanımlayıcısı için bir eşleme yok, bir hata oluşturulur.
  * Tanıtıcısını gerekli hello anahtarı tanımlayıcısı eşleşirse çözümleyici belirtilmedi, ancak belirtilen bir anahtar hello anahtar kullanılır. Merhaba tanımlayıcı eşleşmiyorsa, bir hata oluşturulur.
    
    azure.storage.samples şifreleme örnekleri hello <fix URL>BLOB, kuyruklar ve tablolar için daha ayrıntılı bir uçtan uca senaryoyu göstermektedir.
      Örnek uygulamaları hello KEK ve anahtar çözümleyici hello örnek dosyalarında sırasıyla KeyWrapper ve KeyResolver sağlanır.

### <a name="requireencryption-mode"></a>RequireEncryption modu
Kullanıcıların isteğe bağlı olarak bir çalışma modu, burada tüm ve indirmelere şifrelenmelidir sağlayabilirsiniz. Bu modda, deneme tooupload veri hello hizmette şifrelenmez bir şifreleme ilkesi veya indirme verileri olmadan hello istemcide başarısız olur. Merhaba **require_encryption** Bu davranış hello hizmet nesnesi denetimlere bayrak.

### <a name="blob-service-encryption"></a>BLOB hizmeti şifreleme
Merhaba şifreleme ilkesi alanlarında hello blockblobservice nesne üzerinde ayarlayın. Şey hello istemci kitaplığı tarafından dahili olarak ele alınacaktır.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Kuyruk hizmeti şifreleme
Merhaba şifreleme ilkesi alanlarında hello queueservice nesne üzerinde ayarlayın. Şey hello istemci kitaplığı tarafından dahili olarak ele alınacaktır.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Tablo hizmeti şifreleme
Ayrıca toocreating bir şifreleme ilkesi ve istek seçeneklerini ayarlama, ya da belirtmeniz gerekir bir **encryption_resolver_function** hello üzerinde **tableservice**, veya üzerinde özniteliği şifreleme kümesi hello Merhaba EntityProperty.

### <a name="using-hello-resolver"></a>Merhaba Çözücü kullanma

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Öznitelikleri kullanma
Yukarıda belirtildiği gibi bir özellik için şifreleme EntityProperty nesneyi depolayarak işaretlenmiş olabilir ve hello ayarı alan şifreleyebilirsiniz.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Şifreleme ve performans
Depolama veri sonuçlarınızda ek performans yükü şifreleme unutmayın. başlangıç anahtarı ve IV oluşturulması gerektiğini hello içeriğin kendisini şifrelenmelidir ve ek meta veri biçimlendirilmiş karşıya ve içerik. Bu ek yükü hello Şifrelenmekte veri miktarını bağlı olarak değişir. Müşterilerin kendi uygulamalarında geliştirme sırasında performansı için her zaman sınamanızı öneririz.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba karşıdan [Java Pypı paket için Azure Storage istemci kitaplığı](https://pypi.python.org/pypi/azure-storage)
* Merhaba karşıdan [Python kaynak kodu github'dan için Azure Storage istemci kitaplığı](https://github.com/Azure/azure-storage-python)
