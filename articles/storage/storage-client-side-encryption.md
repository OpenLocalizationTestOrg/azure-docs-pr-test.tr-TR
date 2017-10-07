---
title: "Microsoft Azure Storage için .NET ile aaaClient tarafı şifreleme | Microsoft Docs"
description: "Merhaba .NET için Azure Storage istemci kitaplığı, Azure Storage uygulamalarınız için en yüksek güvenlik için istemci tarafı şifreleme ve Azure anahtar kasası ile tümleştirmeyi destekler."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: e99551925069d5e05bc283039b252cffe8df5383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Microsoft Azure depolama için istemci tarafı şifreleme ve Azure anahtar kasası
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Genel Bakış
Merhaba [.NET Nuget paketi için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) tooAzure depolama karşıya yükleme ve toohello istemci indirilirken verilerin şifresini çözmek önce istemci uygulamalar içinde verilerin şifrelenmesi destekler. Merhaba kitaplığı ile tümleştirme de destekler [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) depolama hesabı anahtarı yönetimi için.

İstemci tarafı şifreleme ve Azure anahtar kasası kullanarak blob'lara şifreleme hello işleminde size yol gösterir bir adım adım öğretici için bkz: [Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları şifreleme ve şifre çözme](storage-encrypt-decrypt-blobs-key-vault.md).

Java ile istemci tarafı şifreleme için bkz: [Java için Microsoft Azure Storage istemci tarafı şifreleme](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Şifreleme ve şifre çözme hello Zarf teknik aracılığıyla
şifreleme ve şifre çözme Hello işlemleri hello Zarf teknik izleyin.

### <a name="encryption-via-hello-envelope-technique"></a>Merhaba Zarf teknik aracılığıyla şifreleme
Şifreleme hello Zarf teknik aracılığıyla hello aşağıdaki şekilde çalışır:

1. Hello Azure storage istemci kitaplığı simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) oluşturur.
2. Kullanıcı verileri bu CEK kullanılarak şifrelenir.
3. Merhaba CEK sonra (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir. Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya Azure anahtar kasası depolanan.
   
    Merhaba depolama istemci kitaplığı kendisini hiçbir zaman erişim tooKEK sahiptir. Merhaba kitaplığı anahtar kasası tarafından sağlanan hello anahtar kaydırma algoritması çağırır. Kullanıcıların toouse anahtar kaydırma/isterseniz açmak için özel sağlayıcılar seçebilirsiniz.

4. Merhaba şifrelenmiş verileri ise toohello Azure depolama hizmeti karşıya yüklendi. Bazı ek şifreleme meta verilerle birlikte Hello Sarmalanan anahtarın meta veriler (hakkında bir blob) olarak depolanır veya (iletileri kuyruğa ve tablo varlıkları) ile şifrelenmiş hello veri Ara değerli.

### <a name="decryption-via-hello-envelope-technique"></a>Merhaba Zarf teknik aracılığıyla şifre çözme
Şifre çözme hello Zarf teknik aracılığıyla hello aşağıdaki şekilde çalışır:

1. Merhaba istemci kitaplığı hello kullanıcının yerel olarak veya Azure anahtar kasası hello anahtar şifreleme anahtarı (KEK) yönetiyor varsayar. Merhaba kullanıcı şifreleme için kullanılan tooknow hello özel anahtarı gerektirmez. Bunun yerine, farklı anahtar tanımlayıcıları tookeys çözümlenen bir anahtar çözümleyici ayarlayabilir ve kullanılır.
2. Hello istemci kitaplığı hello şifrelenmiş veriler hello hizmette depolanan tüm şifreleme malzeme birlikte yükler.
3. sarmalanmamış (şifresi çözülmüş) kullanarak hello sonra anahtar şifreleme anahtarı (KEK) hello Sarmalanan içerik şifreleme anahtarı (CEK) olabilir. Burada yeniden hello istemci kitaplığı erişimi tooKEK sahip değil. Yalnızca özel hello veya anahtar kasası sağlayıcının açma algoritmasını çağırır.
4. şifreleme anahtarı (CEK) ise içerik Hello toodecrypt şifrelenmiş hello kullanıcı verilerini kullanılır.

## <a name="encryption-mechanism"></a>Şifreleme mekanizması
Merhaba depolama istemci kitaplığı kullanıp [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) sipariş tooencrypt kullanıcı verileri. Özellikle, [Şifre blok zincirleme (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) AES moduyla. Her bir hizmet works biraz farklı şekilde Burada bunların her birini aşağıdakiler ele alınacaktır.

### <a name="blobs"></a>Bloblar
Merhaba istemci kitaplığı şu anda yalnızca tüm blobları şifreleme desteklemektedir. Kullanıcıların hello kullandığınızda Şifreleme özellikle, desteklenen **UploadFrom*** yöntemleri ya da hello **OpenWrite** yöntemi. Yüklemeleri, hem tam hem aralık yüklemeleri desteklenen için.

Şifreleme sırasında hello istemci kitaplığı rastgele başlatma vektörü (IV), 32 bayt rasgele bir içerik şifreleme anahtarı (CEK) ile birlikte 16 bayt oluşturmak ve bu bilgileri kullanarak hello blob verisi Zarf şifreleme gerçekleştirin. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra şifrelenmiş bir blobu hello hello hizmetinin yanı sıra meta verileri blob olarak depolanır.

> [!WARNING]
> Düzenleme veya kendi hello blob meta verilerini karşıya yükleme, bu meta veriler korunur tooensure gerekir. Bu meta veriler olmadan yeni meta veriler karşıya yükleme, hello Sarmalanan CEK, IV ve diğer meta veriler kaybolur ve hello blob içeriğinin hiçbir zaman tekrar alınabilir.
> 
> 

Şifrelenmiş bir blobu indirme içerir hello tüm blob hello kullanarak Merhaba içeriğine alma **DownloadTo***/**BlobReadStream** kolaylığı yöntemleri. Sarmalanan CEK sarılmamış ve hello IV ile birlikte kullanılan hello (blob meta verileri bu durumda tooreturn şifresi hello veri toohello kullanıcıları depolanır).

Rastgele bir aralığı indirme (**DownloadRange*** yöntemleri) sipariş tooget bulunan kullanıcılar tarafından kullanılan toosuccessfully olabilecek ek veri az miktarda şifresi sağlanan hello hello aralık ayarlamak şifrelenmiş bir blobu hello içerir İstenen aralık.

Tüm türleri blob (blok blobları, sayfa blobları ve ilave bloblarını) şifrelenmiş/bu şeması kullanarak şifresi.

### <a name="queues"></a>Kuyruklar
İletileri kuyruğa herhangi biçimi olamayacağından hello istemci kitaplığı hello başlatma vektörü (IV) ve hello şifrelenmiş içerik şifreleme anahtarı (CEK) hello metinde içeren özel bir biçim tanımlar.

Şifreleme sırasında hello istemci kitaplığı 16 bayt rastgele CEK 32 bayt yanı sıra rasgele bir IV oluşturur ve bu bilgileri kullanarak hello sıraya ileti metninin Zarf şifreleme gerçekleştirir. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra toohello şifrelenmiş kuyruk iletisi eklenir. (Aşağıda gösterilen) bu değiştirilmiş ileti hello hizmetinde depolanır.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

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
3. Merhaba CEK Sarmalanan ve bazı ek şifreleme meta verileri sonra iki ek ayrılmış özellikleri olarak depolanır. Merhaba ilk ayrılmış özelliği (_ClientEncryptionMetadata1) hello bilgilerini IV, sürüm ve Sarmalanan anahtarı tutan bir dize özelliğidir. Merhaba ikinci ayrılmış özelliği (_ClientEncryptionMetadata2) hello özellikleri hakkında bilgi şifrelenmiş hello tutan bir ikili özelliğidir. Merhaba bu ikinci özelliğinde (_ClientEncryptionMetadata2) kendisi şifrelenmiş bilgilerdir.
4. Şifreleme için gereken toothese ek ayrılmış özellikleri, kullanıcılar artık 252 yerine yalnızca 250 özel özelliklere sahip olabilir. Merhaba varlık Hello toplam boyutu 1 MB'tan az olması gerekir.

Yalnızca dize özellikleri şifrelenmiş olduğunu unutmayın. Diğer türdeki özellikleri şifrelenmiş toobe varsa, bunların dönüştürülmüş toostrings olması gerekir. şifrelenmiş hello dizeleri hello hizmette ikili özellikleri olarak depolanır ve şifre çözme sonra geri toostrings dönüştürülür.

Tablolar için ayrıca toohello şifreleme ilkesi, kullanıcıların şifrelenmiş hello özellikleri toobe belirtmeniz gerekir. Bu, ya da bir [EncryptProperty] özniteliği (için TableEntity türetilen POCO varlıklar) veya bir şifreleme çözümleyici isteği seçenekleri belirterek yapılabilir. Bir şifreleme çözümleyici bölüm anahtarı, satır anahtarını ve özellik adını alır ve bu özellik şifrelenmesi gerekip gerekmediğini belirten bir Boole değeri döndüren bir temsilci ' dir. Bir özellik toohello kablo yazılırken şifrelenmesi gerekip gerekmediğini şifreleme sırasında bu bilgileri toodecide hello istemci kitaplığını kullanın. Merhaba temsilci özellikler nasıl şifrelenir geçici mantığı hello olasılığı için de sağlar. (Örneğin, X ise ardından özelliği A şifrelemek; Aksi takdirde özellikleri A ve b şifreleme) Bu BT Not gerekli tooprovide okurken veya varlıklar sorgulama bu bilgilerdir.

### <a name="batch-operations"></a>Toplu işlemleri
Merhaba istemci kitaplığı yalnızca bir seçenekleri nesnesi (ve bu nedenle bir ilke/KEK) izin verdiği için toplu işlemlerde hello aynı KEK bu toplu işlemdeki tüm hello satırları boyunca toplu işlem kullanılır. Ancak, hello istemci kitaplığı dahili olarak yeni rastgele IV ve satır başına rastgele CEK hello toplu işlemde oluşturur. Kullanıcılar ayrıca tooencrypt her işlem için farklı özellikleri hello toplu işlemde Bu davranış hello şifreleme Çözümleyicisi tanımlayarak seçebilirsiniz.

### <a name="queries"></a>Sorgular
tooperform sorgu işlemleri yapabilir tooresolve olan anahtar çözümleyici belirtmelisiniz tüm anahtarları hello sonuç kümesinde hello. Merhaba sorgu sonucunda bulunan bir varlık çözümlenmiş tooa sağlayıcı olamazsa hello istemci kitaplığı bir hata durum oluşturur. Sunucu tarafı tahminleri gerçekleştirir herhangi bir sorgu için varsayılan seçili toohello sütunlara göre hello özel şifreleme meta veri özellikleri (_ClientEncryptionMetadata1 ve _ClientEncryptionMetadata2) hello istemci kitaplığı ekleyin.

## <a name="azure-key-vault"></a>Azure Key Vault
Azure Anahtar Kasası, bulut uygulamaları ve hizmetleri tarafından kullanılan şifreleme anahtarlarının ve gizli anahtarların korunmasına yardımcı olur. Azure anahtar kasası kullanarak, kullanıcılar anahtarları ve gizli anahtarları (örneğin, kimlik doğrulaması anahtarları, depolama hesabı anahtarları, veri şifreleme anahtarları,. şifreleyebilirsiniz PFX dosyaları ve parolalar), donanım güvenlik modülleri (HSM'ler) tarafından korunan anahtarları kullanarak. Daha fazla bilgi için bkz: [Azure anahtar kasası nedir?](../key-vault/key-vault-whatis.md).

Merhaba depolama istemci kitaplığı hello anahtar kasası çekirdek Kitaplığı'nda sipariş tooprovide ortak bir çerçeve Azure anahtarları yönetmek için kullanır. Kullanıcılar ayrıca hello anahtar kasası uzantıları kitaplığı kullanarak hello ek bir avantaja alır. Merhaba uzantıları kitaplığı basit ve sorunsuz simetrik/RSA yerel ve bulut anahtar sağlayıcıları ve aynı zamanda toplama ve önbelleğe alma ile yararlı işlevsellik sağlar.

### <a name="interface-and-dependencies"></a>Arabirim ve bağımlılıkları
Üç anahtar kasası paketi vardır:

* Microsoft.Azure.KeyVault.Core hello IKey ve IKeyResolver içerir. Hiçbir bağımlılıkları olan küçük bir pakettir. .NET için depolama istemci kitaplığı Hello bağımlılık olarak tanımlar.
* Microsoft.Azure.KeyVault hello anahtar kasası REST istemcisi içerir.
* Microsoft.Azure.KeyVault.Extensions şifreleme algoritmalarının ve bir RSAKey ve bir SymmetricKey uygulamaları içeren uzantı kodu içerir. Merhaba çekirdek ve KeyVault ad alanında bulunan bağlıdır ve bir toplama Çözümleyicisi (kullanıcılar birden çok anahtar sağlayıcısı toouse istediğiniz zaman) ve önbelleğe alma anahtar çözümleyici işlevselliği toodefine sağlar. Kullanıcılar kendi anahtarları veya toouse hello anahtar kasası uzantıları tooconsume hello toouse Azure anahtar kasası toostore yerel istiyor ve şifreleme sağlayıcıları bulut hello depolama istemci kitaplığı doğrudan bu pakete, olmasa da, bunlar bu paketi gerekir.

Anahtar kasası yüksek değerli ana anahtarları için tasarlanmıştır ve azaltma sınırları anahtar kasası başına bunu göz önünde tasarlanmıştır. İstemci tarafı şifreleme anahtar kasası ile gerçekleştirirken hello tercih edilen toouse simetrik ana anahtar kasasına gizli olarak depolanır ve yerel önbelleğe alınan anahtarlar modelidir. Kullanıcıların gerçekleştirmelisiniz hello aşağıdaki:

1. Çevrimdışı bir gizli anahtar oluşturma ve tooKey kasası yükleyin.
2. Bir parametre tooresolve hello gizli şifreleme için geçerli sürümü hello ve bu bilgileri yerel olarak önbelleğe gibi hello parolanın temel tanımlayıcı kullanın. CachingKeyResolver önbelleğe almak için kullanın. Kullanıcılar kendi önbelleğe alma mantığını değil beklenen tooimplement şunlardır.
3. Merhaba önbellek Çözümleyicisi hello şifreleme ilkesi oluşturulurken bir giriş olarak kullanın.

Anahtar kasası kullanımıyla ilgili daha fazla bilgi hello bulunabilir [şifreleme kod örnekleri](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>En iyi uygulamalar
Şifreleme desteği, yalnızca .NET hello depolama istemci Kitaplığı'nda kullanılabilir. Şu anda Windows Phone ve Windows çalışma zamanı şifreleme desteklemez.

> [!IMPORTANT]
> İstemci tarafı şifreleme kullanırken bu önemli noktalara dikkat edin:
> 
> * Ne zaman okunurken veya yazılırken tooan blob, tüm blob karşıya yükleme komutları kullanın ve aralığı/bütün blob yükleme komutları şifrelenir. Yerleştirme blok, Put engelleme listesi, yazma sayfaları, Temizle sayfaları veya blok ekleme gibi işlemleri protokolü kullanarak tooan şifrelenmiş bir blobu yazma kaçının; Aksi takdirde hello şifreli blob bozuk ve okunamaz olun.
> * Tablolar için benzer bir kısıtlama var. Merhaba şifreleme meta verilerini güncelleştirme olmadan dikkatli toonot şifrelenmiş güncelleştirme özellikleri olabilir.
> * Meta veri hello şifreli blob üzerindeki ayarlarsanız, hello şifrelemeyle ilgili meta verileri meta verileri ayarlama eklenebilir olmadığından şifre çözme için gerekli üzerine yazabilir. Bu da anlık görüntüler için geçerlidir; meta veri anlık görüntüsünü şifrelenmiş bir blobu oluşturulurken belirtmekten kaçının. Meta veriler ayarlanmalıdır emin toocall hello olması **FetchAttributes** yöntemi ilk tooget geçerli şifreleme meta verilerin hello ve meta veri ayarlanırken eşzamanlı yazma kaçının.
> * Merhaba etkinleştirmek **RequireEncryption** hello varsayılan istek seçenekleri yalnızca ile çalışması kullanıcılar için özellik şifrelenmiş veriler. Aşağıda daha fazla bilgi için bkz.
> 
> 

## <a name="client-api--interface"></a>İstemci API / arabirim
Bir EncryptionPolicy nesnesi oluşturulurken, kullanıcılara (IKey uygulama) yalnızca bir anahtar sağlayabilir Çözümleyicisi (IKeyResolver uygulama) ya da her ikisini de. IKey anahtar tanımlayıcısını kullanarak tanımlanır ve kaydırma/açmak için hello mantık sağlayan hello temel anahtar türüdür. IKeyResolver hello şifre çözme işlemi sırasında kullanılan tooresolve bir anahtar değil. Anahtar tanımlayıcısını verilen IKey döndüren bir ResolveKey yöntemi tanımlar. Bu, kullanıcıların hello özelliği toochoose birden fazla konumda yönetilen birden çok anahtar arasındaki sağlar.

* Şifreleme için bir anahtarın hello olmaması bir hataya neden olur ve başlangıç anahtarı her zaman kullanılır.
* Şifre çözme için:
  * Merhaba anahtar çözümleyici tooget hello anahtarı belirtilmişse çağrılır. Merhaba çözümleyici belirtildi ancak hello anahtarı tanımlayıcısı için bir eşleme yok, bir hata oluşturulur.
  * Tanıtıcısını gerekli hello anahtarı tanımlayıcısı eşleşirse çözümleyici belirtilmedi, ancak belirtilen bir anahtar hello anahtar kullanılır. Merhaba tanımlayıcı eşleşmiyorsa, bir hata oluşturulur.

Merhaba [şifreleme örnekleri](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) daha ayrıntılı bir uçtan uca senaryoyu BLOB, kuyruklar ve tablolar, bunların ile anahtar kasası tümleştirme göstermektedir.

### <a name="requireencryption-mode"></a>RequireEncryption modu
Kullanıcıların isteğe bağlı olarak bir çalışma modu, burada tüm ve indirmelere şifrelenmelidir sağlayabilirsiniz. Bu modda, deneme tooupload veri hello hizmette şifrelenmez bir şifreleme ilkesi veya indirme verileri olmadan hello istemcide başarısız olur. Merhaba **RequireEncryption** hello isteği seçenekleri nesnesinin özelliği, bu davranışı denetler. Uygulamanızı Azure depolama alanında depolanan tüm nesnelere şifreler sonra hello ayarlayabilirsiniz **RequireEncryption** hello varsayılan istek seçenekleri hello hizmeti istemci nesnesi özelliği. Örneğin, **CloudBlobClient.DefaultRequestOptions.RequireEncryption** çok**true** toorequire şifreleme tüm blob işlemleri için bu istemci nesnesi gerçekleştirilir.

### <a name="blob-service-encryption"></a>BLOB hizmeti şifreleme
Oluşturma bir **BlobEncryptionPolicy** nesne ve hello isteği seçeneklerinde ayarlayın (API başına veya kullanarak bir istemci düzeyinde **DefaultRequestOptions**). Şey hello istemci kitaplığı tarafından dahili olarak ele alınacaktır.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Kuyruk hizmeti şifreleme
Oluşturma bir **QueueEncryptionPolicy** nesne ve hello isteği seçeneklerinde ayarlayın (API başına veya kullanarak bir istemci düzeyinde **DefaultRequestOptions**). Şey hello istemci kitaplığı tarafından dahili olarak ele alınacaktır.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Tablo hizmeti şifreleme
Ayrıca toocreating bir şifreleme ilkesi ve istek seçeneklerini ayarlama, ya da belirtmeniz gerekir bir **EncryptionResolver** içinde **TableRequestOptions**, veya kümesi hello [EncryptProperty] özniteliği Merhaba varlık.

#### <a name="using-hello-resolver"></a>Merhaba Çözücü kullanma

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Öznitelikleri kullanma
Merhaba varlık TableEntity uyguluyorsa, yukarıda belirtildiği gibi ardından hello özellikleri hello belirtme yerine hello [EncryptProperty] özniteliğiyle tasarlanabilir **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Şifreleme ve performans
Depolama veri sonuçlarınızda ek performans yükü şifreleme unutmayın. başlangıç anahtarı ve IV oluşturulması gerektiğini hello içeriğin kendisini şifrelenmelidir ve ek meta veri biçimlendirilmiş karşıya ve içerik. Bu ek yükü hello Şifrelenmekte veri miktarını bağlı olarak değişir. Müşterilerin kendi uygulamalarında geliştirme sırasında performansı için her zaman sınamanızı öneririz.

## <a name="next-steps"></a>Sonraki adımlar
* [Öğretici: Şifrelemek ve şifresini Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları](storage-encrypt-decrypt-blobs-key-vault.md)
* Merhaba karşıdan [.NET NuGet paketi için Azure Storage istemci kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage)
* Hello Azure anahtar kasası NuGet karşıdan [çekirdek](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [istemci](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), ve [uzantıları](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) paketleri  
* Merhaba ziyaret [Azure anahtar kasası belgeleri](../key-vault/key-vault-whatis.md)
