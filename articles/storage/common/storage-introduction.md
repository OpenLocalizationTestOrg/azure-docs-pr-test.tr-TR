---
title: aaaIntroduction tooAzure depolama | Microsoft Docs
description: "Giriş tooAzure depolama, Microsoft'un veri depolama hello bulutta."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Giriş tooMicrosoft Azure depolama

Microsoft Azure Depolama, yüksek oranda kullanılabilir, güvenli, dayanıklı, ölçeklenebilir ve yedekli depolama sağlayan, Microsoft tarafından yönetilen bir bulut hizmetidir. Microsoft bakımı üstlenir ve kritik sorunları sizin yerinize çözer. 

Azure Depolama üç veri hizmetinden oluşur: Blob depolama, Dosya depolama ve Kuyruk depolama. BLOB Depolama hello hızlı performans olası için yalnızca SSD kullanarak premium depolama ile standart ve premium depolama destekler. Seyrek erişimli depolama seyrek erişilen verileri daha düşük maliyetli bir için büyük miktarlarda toostorage izin vererek, başka bir özelliktir.

Bu makalede, hello aşağıdaki hakkında bilgi edinin:
* Hello Azure depolama hizmetleri
* Merhaba türlerde depolama hesapları
* Bloblara, kuyruklara ve dosyalara erişme
* şifreleme
* çoğaltma 
* Depolama içine veya dışına veri aktarma
* çok sayıda depolama istemcisi kitaplıklarını kullanılabilir hello. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Hello Azure Storage hizmetlerine giriş

hello hizmetlerinden herhangi birini Azure Storage--Blob storage, dosya depolama ve kuyruk Depolama--tarafından sağladığınız toouse ilk bir depolama hesabı oluşturun ve verileri bu depolama hesabı alanındaki belirli bir hizmet/gruptan sonra aktarabilirsiniz. 

## <a name="blob-storage"></a>Blob depolama

Bloblar, temelde bilgisayarda (veya tablet, mobil cihaz ve benzeri) depoladığınız dosyalara benzer dosyalardır. Bu dosyalar resimler, Microsoft Excel dosyaları, HTML dosyaları, sanal sabit diskler (VHD) olabileceği gibi, günlükler, veritabanı yedeklemeleri gibi büyük veriler de dahil olmak üzere neredeyse her şey olabilir. BLOB'ları benzer toofolders olan kapsayıcılara depolanır. 

Blob storage'da dosyaları depolamak sonra her yerden erişebilmeleri REST arabirimini veya hello Azure SDK'sı depolama istemci kitaplıklarından birini URL'leri kullanarak hello world hello. Depolama istemcisi kitaplıkları, Node.js, Java, PHP, Ruby, Python ve .NET dahil olmak üzere birden çok dil için kullanılabilir. 

Blok bloblar, ekleme blobları ve sayfa blobları (VHD dosyaları için kullanılır) olmak üzere üç tür blob vardır.

* Blok blobları dosyalarıdır kullanılan toohold sıradan tooabout yukarı 4.7 TB. 
* Sayfa bloblarını kullanılan toohold rasgele erişim too8 TB boyutunda yukarı dosyalarıdır. Bu sanal makineleri yedekleme hello VHD dosyaları için kullanılır.
* Ekleme BLOB'ları gibi hello blok blobları blok yapılan ancak için iyileştirilmiş ekleme işlemleri. Bunlar, birden çok VM'lerin aynı blob bilgi toohello günlüğü gibi şeyler için kullanılır.

Karşıya yükleme veya veri tooBlob depolama belirtmeyi gerçekçi hello kablo üzerinden indirme ağ kısıtlamaları burada olun çok büyük veri kümeleri için bir dizi sabit sürücüler tooMicrosoft tooimport sevk veya verileri doğrudan hello veri merkezinden dışa aktarın. Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanmak](../storage-import-export-service.md).

## <a name="file-storage"></a>Dosya depolama

Hello Azure dosya hizmeti hello standart sunucu ileti bloğu (SMB) protokolünü kullanarak erişilebilir yüksek oranda kullanılabilir ağ dosya paylaşımları yukarı tooset sağlar. Birden çok VM paylaşabileceğiniz anlamına gelir aynı hello okuma ve yazma erişimi dosyaları. Ayrıca, hello dosyaları hello REST arabirimini veya hello depolama istemcisi kitaplıklarını kullanarak okuyabilirsiniz. 

Azure File storage Kurumsal dosya paylaşımında dosyalarından ayıran bir şeydir yerden hello dosyalara erişebilirsiniz toohello dosyasını işaret eder ve bir paylaşılan erişim imzası (SAS) belirteci içeren bir URL kullanarak Merhaba Dünya içinde. SAS belirteçleri üretebilir; belirli bir süre boyunca belirli erişim tooa özel varlık sağlarlar. 

Dosya paylaşımları için birçok yaygın senaryoda kullanılabilir: 

* Birçok şirket içi uygulama, dosya paylaşımlarını kullanır. Bu özellik daha kolay toomigrate kılar veri tooAzure paylaşmak uygulamalar. Bağlama hello aynı sürücü hello harfi dosya paylaşımı toohello uygulamanız tarafından kullanılan şirket içi, uygulamanızın hello dosya paylaşımına erişen hello bölümü ile küçük, varsa, değişiklikler çalışması gerekir.

* Yapılandırma dosyaları bir dosya paylaşımında depolanabilir ve birden çok VM tarafından bu dosyalara erişilebilir. Araçlar ve yardımcı programlar bir grup içindeki birden çok geliştiriciler tarafından kullanılan herkes bunları bulabilirsiniz sağlayarak bir dosya paylaşımında depolanabilir ve bunlar kullandığınız aynı sürüm hello.

* Tanılama günlükleri, Ölçümler ve kilitlenme bilgi dökümleri yalnızca üç tooa dosya paylaşımı yazılmış ve işlenen ya da daha sonra analiz veriler gösterilebilir.

Bu süre, Active Directory tabanlı kimlik doğrulaması ve erişim denetim listeleri (ACL'ler) desteklenmez, ancak bazı zaman hello gelecekteki olacaktır. erişim toohello dosya paylaşımı için kullanılan tooprovide kimlik doğrulaması Hello depolama hesabı kimlik bilgileridir. Bu bağlı hello paylaşımı herkesle tam okuma/yazma erişimi toohello paylaşımı olacağı anlamına gelir.

## <a name="queue-storage"></a>Kuyruk depolama

Hello Azure Queue hizmeti kullanılan toostore ve alma iletileri ' dir. İletileri kuyruğa too64 KB boyutunda yukarı olabilir ve bir sıraya milyonlarca ileti içerebilir. Kuyruklar genellikle kullanılan toostore zaman uyumsuz olarak işlenen iletiler toobe listeleridir. 

Örneğin, müşteriler toobe mümkün tooupload resimlerinizi istediğiniz ve toocreate küçük resimleri için her resim istediğiniz söyleyin. Müşterinizin sizin için toocreate hello küçük resimleri hello resimleri karşıya yüklenirken bekleyin olabilir. Alternatif bir kuyruk toouse olacaktır. Merhaba müşteri kendi karşıya yükleme tamamlandığında, bir ileti toohello sırası yazma. Ardından Azure hello sıradan hello ileti almak ve hello küçük resimler oluşturma işlevi vardır. Her hello parçalarının bu işlem, kullanımınız için ayarlama sonra daha fazla denetim vermiş ayrı ayrı ölçeklendirilebilir.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Table Storage
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
Standart Azure Tablo Depolama artık Cosmos DB’nin bir parçasıdır. Ayrıca Azure Tablo depolama için aktarım hızı iyileştirilmiş tablolar, global dağıtım ve otomatik ikincil dizinler sunan Premium Tablolar seçeneği vardır. Lütfen daha fazla toolearn ve hello yeni premium deneyimi deneme kullanıma [Azure Cosmos DB: Tablo API](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Disk depolama

Hello Azure depolama ekibi ayrıca tüm yönetilen hello içerir ve yönetilmeyen disk özellikleri sanal makineler tarafından kullanılan diskler, sahip olur. Bu özellikler hakkında daha fazla bilgi için lütfen hello bakın [işlem hizmeti belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Depolama hesabı türleri 

Bu tabloda, çeşitli türlerde depolama hesapları ve hangi nesnelerin her biri kullanılabilir hello gösterilmektedir.

|**Depolama hesabı türü**|**Genel amaçlı Standart**|**Genel amaçlı Premium**|**Blob depolama, sık erişimli ve seyrek erişimli erişim katmanları**|
|-----|-----|-----|-----|
|**Desteklenen hizmetler**| Blob, Dosya, Kuyruk Hizmetleri | Blob Hizmeti | Blob Hizmeti|
|**Desteklenen blob türleri**|Blok blobları, sayfa blobları ve ek bloblar | Sayfa blobları | Blok blobları ve ek blobları|

### <a name="general-purpose-storage-accounts"></a>Genel amaçlı depolama hesapları

Genel amaçlı depolama hesaplarının iki türü vardır. 

#### <a name="standard-storage"></a>Standart depolama 

en yaygın olarak kullanılan hello depolama hesapları tüm veri türleri için kullanılabilir standart depolama hesaplarıdır. Standart depolama hesapları, manyetik ortam toostore verileri kullanın.

#### <a name="premium-storage"></a>Premium depolama

Premium depolama hesapları öncelikle VHD dosyaları için kullanılan sayfa blobları için yüksek performanslı depolama sağlar. Premium depolama hesapları SSD toostore verileri kullanın. Microsoft, tüm VM'leriniz için Premium depolama kullanmanızı önerir.

### <a name="blob-storage-accounts"></a>Blob Depolama Hesapları

Merhaba Blob Depolama hesabının özel depolama hesabı kullanılan toostore blok blobları ve ilave bloblarının ' dir. Sayfa bloblarını bu hesaplarda depolayacağınızdan, VHD dosyalarını da depolayamazsınız. Bu hesaplar, tooset bir erişim katmanı tooHot veya Cool sağlar; Merhaba katmanı herhangi bir zamanda değiştirilebilir. 

Merhaba etkin erişim katmanını sık erişilen dosyalar için kullanılır--depolama için daha yüksek bir maliyet ödeme ancak hello BLOB'lar erişme hello maliyet çok düşüktür. Merhaba seyrek erişimli erişim katmanında depolanan BLOB'lar için hello BLOB'lar erişmek için daha yüksek bir maliyet ödeme, ancak depolama maliyetini hello çok düşüktür.

## <a name="accessing-your-blobs-files-and-queues"></a>Bloblara, kuyruklara ve dosyalara erişme

Her depolama hesabı herhangi bir işlem için kullanılabilen iki kimlik doğrulama anahtarına sahiptir. Merhaba toplamak için iki anahtarları bazen tooenhance güvenlik vardır. Merhaba hesap adı, yanı sıra kendi mülkü hello depolama hesabında sınırsız erişimi tooall veri sağladığından Bu anahtarları korunması önemlidir. 

Bu bölümde, iki yolu toosecure hello depolama hesabı ve verileri arar. Depolama hesabınız ve verilerinizin güvenliğini sağlama hakkında ayrıntılı bilgi için bkz: Merhaba [Azure Storage Güvenlik Kılavuzu'nu](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Azure AD kullanarak toostorage hesaplarını erişimi güvenli hale getirme

Tek yönlü toosecure erişim tooyour depolama veri erişim toohello depolama hesabı anahtarlarını denetlenmesidir. Resource Manager'da rol tabanlı erişim denetimi (RBAC) rolleri toousers, grupları veya uygulamaların atayabilirsiniz. Bu rolleri bağlıdır tooa belirli izin verilen veya izin verilmeyen eylem kümesidir. RBAC kullanarak toogrant erişim tooa depolama hesabı yalnızca hello yönetim işlemlerini hello erişim katmanını değiştirme gibi bu depolama hesabı için işler. RBAC toogrant erişim toodata nesneleri belirli bir kapsayıcı veya dosya paylaşımı gibi kullanamazsınız. Ancak, kullanılan tooread hello veri nesneleri sonra olabilen RBAC toogrant erişim toohello depolama hesabı anahtarları, kullanabilirsiniz. 

### <a name="securing-access-using-shared-access-signatures"></a>Paylaşılan erişim imzalarını kullanarak erişim güvenliğini sağlama 

Erişim ilkeleri toosecure veri nesnelerinizi depolanan ve paylaşılan erişim imzaları kullanabilirsiniz. Paylaşılan erişim imzası (SAS) olabilir bir güvenlik belirteci içeren bir dize toodelegate erişim toospecific depolama nesneleri ve izinler ve erişim hello tarih aralığı gibi toospecify kısıtlamaları izin veren bir varlık için URI toohello bağlı olur. Bu özellik kapsamlı olanaklar sağlar. Ayrıntılı bilgi için çok başvurun[kullanarak paylaşılan erişim imzaları (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Genel erişim tooblobs

Merhaba Blob hizmeti tooprovide genel erişim tooa kapsayıcı ve bloblarını veya belirli bir blobu sağlar. Bir kapsayıcı veya bir blobun genel erişime açıldığını belirttiğinizde herkes anonim olarak okuyabilir, herhangi bir kimlik doğrulama gerekli değildir. Görüntü, video veya Blob depolama biriminden belgeleri kullanarak bir Web sitesi varsa, ne zaman toodo istediğiniz örneği budur. Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetme](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Şifreleme

Merhaba depolama hizmetleri için birkaç şifreleme temel tür yok. 

### <a name="encryption-at-rest"></a>Bekleme sırasında şifreleme 

Blob hizmeti bir Azure depolama hesabı için hello ya da depolama hizmeti şifreleme (SSE) ya da hello dosyaları hizmetini (Önizleme) etkinleştirin. Etkinleştirilirse, toohello belirli hizmet yazılan tüm veriler şifrelenir yazılmış önce. Merhaba verileri okurken şifresi döndürmeden önce. 

### <a name="client-side-encryption"></a>İstemci Tarafında Şifreleme

Merhaba depolama istemcisi kitaplıklarını sahip çağırabilirsiniz yöntemleri tooprogrammatically hello kablo hello istemci tooAzure göndermeden önce verileri şifreleyin. Şifreli olarak depolandığından, bekleme sırasında da şifrelenmiş olacaktır. Merhaba veri okunurken alındıktan sonra hello bilgilerini şifresini. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Azure Dosya Paylaşımları ile aktarım sırasında şifreleme

Paylaşılan erişim imzaları ile ilgili daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](../storage-dotnet-shared-access-signature-part-1.md). Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md) ve [hello Azure Storage Hizmetleri için kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dd179428.aspx) güvenli erişim tooyour depolama hesabı hakkında daha fazla bilgi için.

Depolama hesabı ve şifreleme güvenliğini sağlama hakkında daha fazla ayrıntı için bkz: hello [Azure Storage Güvenlik Kılavuzu'nu](storage-security-guide.md).

## <a name="replication"></a>Çoğaltma

Verilerinizi dayanıklı sipariş tooensure Azure depolama hello özelliği tookeep sahip (ve yönetme) verilerinizin birden çok kopyasını. Buna çoğaltma veya yedekleme denir. Depolama hesabınızı ayarladığınızda, çoğaltma türünü seçersiniz. Merhaba depolama hesabı ayarladıktan sonra çoğu durumda, bu ayar değiştirilebilir. 

Tüm depolama hesaplarında **yerel olarak yedekli depolama (LRS)** vardır. Verilerinizin üç kopyasını hello veri merkezinde Azure Storage tarafından yönetilen Bunun anlamı hello depolama hesap zaman ayarlanan belirtilmiş. Değişiklikleri kabul edilen tooone olduğunda kopyalayın, hello diğer iki kopya başarı döndürmeden önce güncelleştirilir. Bu, hello üç çoğaltmaların her zaman eşitlenmiş anlamına gelir. Ayrıca, hello üç kopyaları ayrı hata etki alanlarında bulunan ve etki alanlarını, yükseltme, verilerinizi bulunduran bir depolama düğüm başarısız veya çekildiği çevrimdışı toobe güncelleştirildiğinde olsa bile verilerinizi kullanılabilir olduğu anlamına gelir. 

**Yerel olarak yedekli depolama (LRS)**

Yukarıda da açıklandığı şekilde, LRS ile tek bir veri merkezinde verilerinizin üç kopyasına sahip olursunuz. Bu veri depolama düğümü başarısız veya güncelleştirilmiş çevrimdışı toobe alınır ancak kullanılamaz hale bir veri merkezinin tamamı durumunun hello değil kullanılamaz hale hello sorun işler.

**Bölgesel olarak yedekli depolama (ZRS)**

Bölge olarak yedekli depolama (ZRS) hello üç yerel kopyasını verilerinizi ve aynı zamanda başka bir dizi verilerinizin üç kopyasını tutar. Merhaba üç kopyaları ikinci kümesini zaman uyumsuz olarak bir veya iki bölgeleri içindeki veri merkezleri arasında çoğaltılır. ZRS’nin yalnızca genel amaçlı depolama hesaplarındaki blok bloblar için kullanılabilir olduğunu unutmayın. Depolama hesabınızı oluşturup zrs'yi sonra Ayrıca, bu diğer toouse tooany dönüştüremezsiniz çoğaltma veya tersi yazın.

ZRS hesapları LRS’ye göre daha fazla dayanıklılık sağlar, ancak ZRS hesaplarının ölçüm ve günlüğe kaydetme özelliği yoktur. 

**Coğrafi olarak yedekli depolama (GRS)**

Coğrafi olarak yedekli depolama (GRS) hello üç yerel kopyasını verilerinizi bir birincil bölge içinde artı başka bir dizi bir ikincil bölgede yüzlerce mil hello birincil bölge yöntemi bir kenara bırakarak verilerinizin üç kopyasını tutar. Merhaba birincil bölge sırasında bir hata Hello olayda Azure Storage toohello ikincil bölge başarısız olur. 

**Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)** 

Merhaba ikincil konumda okuma erişimi toohello Veri Al okuma erişimli coğrafi olarak yedekli depolama tam olarak GRS gibi olmasıdır. Merhaba birincil veri merkezi geçici olarak kullanılamaz duruma gelirse, hello ikincil konumdan tooread hello veri devam edebilirsiniz. Bu çok yararlı olabilir. Örneğin, salt okunur moduna değiştirir ve toohello ikincil kopya gösteren bir web uygulaması güncelleştirmeleri kullanılabilir olmasa da bazı erişimine sahip olabilir. 

> [!IMPORTANT]
> Depolama hesabınız oluşturulduktan sonra hello hesabınızı oluştururken zrs seçmediyseniz verilerinizin çoğaltılma değiştirebilirsiniz. Ancak, LRS tooGRS veya RA-GRS'ye geçiş yaparsanız tek seferlik veri aktarımı ücreti ödemeniz gerekebileceğini unutmayın.
>

Çoğaltma hakkında daha fazla bilgi için bkz. [Azure Depolama çoğaltma](storage-redundancy.md).

Olağanüstü durum kurtarma için bilgi [bir Azure Storage kesinti oluşursa hangi toodo](storage-disaster-recovery-guidance.md).

Bir örnek için nasıl tooleverage RA-GRS depolama tooensure yüksek kullanılabilirlik, bkz: [tasarlama yüksek oranda kullanılabilir RA-GRS kullanarak uygulamaları](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Azure depolama biriminden veri tooand aktarma

Depolama hesabınızda veya depolama hesaplarınız arasında hello AzCopy komut satırı yardımcı programını toocopy blob ve dosya verilerini kullanabilirsiniz. Yardım makaleleri hello aşağıdakilerden birini bakın:

* [Windows için AzCopy ile veri aktarma](storage-use-azcopy.md)
* [Linux için AzCopy ile veri aktarma](storage-use-azcopy-linux.md)

AzCopy üstünde hello yerleşik [Azure veri hareketi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), şu anda önizlemede kullanılabilen.

Hello Azure içeri/dışarı aktarma hizmeti kullanılan tooimport veya dışarı aktarma büyük miktarda depolama hesabınızdaki blob veri tooor olabilir. Merhaba veri öğesine/öğesinden hello sabit sürücüleri burada aktaracak birden çok sabit sürücüler tooan Azure veri merkezine posta hazırlamak ve hello sabit sürücüler tooyou geri gönderebilirsiniz. Merhaba içeri/dışarı aktarma hizmeti hakkında daha fazla bilgi için bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanmak](../storage-import-export-service.md).

## <a name="pricing"></a>Fiyatlandırma

Azure Storage için fiyatlandırma hakkında ayrıntılı bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>Depolama API'leri, kitaplıklar ve araçlar
Azure Storage kaynakları HTTP/HTTPS isteği yapabilen her dil ile erişilebilir. Ayrıca, Azure Storage birkaç popüler dilde programlama kitaplıkları sunar. Bu kitaplıklar zaman uyumlu ve zaman uyumsuz çağrılar, işlemleri gruplama, özel durum yönetimi, otomatik yeniden denemeler, işlemsel davranışlar vb. ayrıntıları ele alarak Azure Storage ile çalışmanın çoğu yönünü basitleştirir. Kitaplıklar dilleri aşağıdaki hello için şu anda kullanılabilir ve ardışık düzen başkalarıyla platformları hello:

### <a name="azure-storage-data-services"></a>Azure Depolama veri hizmetleri
* [Depolama Hizmetleri REST API'si](/rest/api/storageservices/)
* [.NET için Depolama İstemcisi Kitaplığı](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [C++ için Depolama İstemcisi Kitaplığı](https://github.com/Azure/azure-storage-cpp)
* [Java/Android için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/java/)
* [Node.js için Depolama İstemcisi Kitaplığı](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [PHP için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/php/)
* [Python için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/python/)
* [Ruby için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/ruby/)
* [PowerShell için Depolama Cmdlet'leri](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [CLI 2.0 için Depolama Komutları](/cli/azure/storage)

## <a name="next-steps"></a>Sonraki adımlar

* [Blob depolama hakkında daha fazla bilgi](../blobs/storage-blobs-introduction.md)
* [Dosya depolama hakkında daha fazla bilgi](../storage-files-introduction.md)
* [Kuyruk depolama hakkında daha fazla bilgi](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Yöneticiler için
* [Azure Depolama ile Azure PowerShell’i kullanma](storage-powershell-guide-full.md)
* [Azure Depolama ile Azure CLI'sini kullanma](../storage-azure-cli.md)

### <a name="for-net-developers"></a>.NET geliştiricileri için
* [.NET kullanarak Azure Blob Depolama ile çalışmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md)
* [.NET kullanarak Azure Tablo Depolama ile çalışmaya başlama](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [.NET kullanarak Azure Kuyruk Depolama ile çalışmaya başlama](../storage-dotnet-how-to-use-queues.md)
* [Windows'da Azure Dosya Depolama ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Java/Android geliştiricileri için
* [Nasıl toouse Java'dan Blob storage](../blobs/storage-java-how-to-use-blob-storage.md)
* [Nasıl toouse Java'dan Table storage](../../cosmos-db/table-storage-how-to-use-java.md)
* [Nasıl toouse Java'dan kuyruk depolama](../storage-java-how-to-use-queue-storage.md)
* [Nasıl toouse Java'dan File storage](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Node.js geliştiricileri için
* [Nasıl toouse node.js'den Blob storage](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Nasıl toouse node.js'den Table storage](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Nasıl toouse node.js'den kuyruk depolama](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>PHP geliştiricileri için
* [Nasıl toouse php'den Blob storage](../blobs/storage-php-how-to-use-blobs.md)
* [Nasıl toouse php'den Table storage](../../cosmos-db/table-storage-how-to-use-php.md)
* [Nasıl toouse php'den kuyruk depolama](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Ruby geliştiricileri için
* [Nasıl toouse ruby'den Blob storage](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Nasıl toouse ruby'den Table storage](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Nasıl toouse ruby'den kuyruk depolama](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Python geliştiricileri için
* [Nasıl toouse python'dan Blob storage](../blobs/storage-python-how-to-use-blob-storage.md)
* [Nasıl toouse python'dan Table storage](../../cosmos-db/table-storage-how-to-use-python.md)
* [Nasıl toouse python'dan kuyruk depolama](../storage-python-how-to-use-queue-storage.md)   
* [Nasıl toouse python'dan File storage](../storage-python-how-to-use-file-storage.md) 
-->