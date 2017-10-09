---
title: aaaIntroduction tooAzure depolama | Microsoft Docs
description: "Azure Storage, Microsoft'un çevrimiçi veri depolama hello bulutta genel bakış. Toouse hello uygulamalarınızda en uygun bulut depolama çözümünü nasıl öğrenin."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Giriş tooMicrosoft Azure depolama

## <a name="overview"></a>Genel Bakış
Azure Storage hello bulut depolama dayanıklılık, kullanılabilirlik ve ölçeklenebilirlik toomeet hello müşterilerin ihtiyaçlarını kullanan modern uygulamalar için çözümüdür. Bu makaleyi okuyan geliştiriciler, BT Uzmanları ve kurumsal karar alıcılar şu konularda bilgi edinebilir:

* Azure Storage’ın içeriği ve bulut, mobil, sunucu ve masaüstü uygulamalarınızda Azure Storage’dan nasıl faydalanılabileceği
* Hangi veri türlerini hello Azure Storage Hizmetleri ile depolayabileceğiniz: blob (nesne) verileri, NoSQL tablo verileri, kuyruk mesajları ve dosya paylaşımları.
* Erişim tooyour veriler Azure depolama alanında nasıl yönetilir
* Azure Storage verilerinizin yedekleme ve çoğaltma ile nasıl dayanıklı hale getirildiği
* Burada toogo sonraki toobuild ilk Azure Storage uygulamanızı

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Azure Storage ile çalışma konusunda gerekli araçlar, kitaplıklar ve diğer kaynaklar için aşağıda yer alan [Sonraki Adımlar](#next-steps)’a göz atın.

## <a name="what-is-azure-storage"></a>Azure Storage nedir?
Bulut bilgi işlem; veriler için ölçeklenebilir, sağlam ve yüksek seviyede kullanılabilir depolama alanına ihtiyaç duyan uygulamalara yönelik yeni senaryolara olanak tanıyor. Microsoft’un Azure Storage’ı geliştirmesinin nedeni budur. Toplama toomaking içinde olası geliştiriciler toobuild büyük ölçekli uygulamalar toosupport yeni senaryolar için Azure Storage ayrıca hello depolama foundation Azure sanal makineler için daha güçlü bir kanıtı tooits sağlamlık sağlar.

Azure depolama depolamak ve yüzlerce terabaytlık veri toosupport hello büyük veri senaryolarını Bilimsel, finansal analiz ve medya uygulamalar tarafından gerekli işlem yüksek düzeyde ölçeklenebilir olduğundan. Veya hello küçük miktarda bir küçük işletmenin Web sitesi için gerekli veri depolayabilirsiniz. İhtiyaçlarınız ne olursa yalnızca, depoladığınız hello veri için ücret ödersiniz. Şu anda Azure Storage onlarca trilyon benzersiz müşteri nesnesi depolamaktadır ve saniyede ortalama olarak milyonlarca talebi ele alır.

Azure depolama geniş global kullanıcılara yönelik uygulamalar tasarlayabilir ve gerektiği gibi - her ikisi de hello depolanan veri miktarı bakımından bu uygulamaları ölçeklendirme ve karşı yapılan isteklerin sayısı hello esnek, olduğundan. Yalnızca kullandıklarınız için ve kullandığınız zaman ücret ödersiniz.

Azure Storage trafiğe bağlı olarak verilerinize otomatik olarak yük dengelemesi yapan bir otomatik bölümleme sistemi kullanır. Bu, uygulama Büyüt üzerinde hello taleplerini Azure Storage otomatik olarak hello uygun kaynaklara toomeet ayıracağı anlamına gelir bunları.

Azure depolama olup erişilebilen herhangi bir yerinde uygulama, her tür hello world hello bulutta, hello Masaüstü, bir şirket içi sunucu veya mobil çalıştıran veya tablet cihaza. Azure depolama burada hello uygulama verilerinin bir alt kümesini hello cihazda depoladığı ve hello bulutta depolanan veriler tam kümesi ile eşitler mobil senaryolarda kullanabilirsiniz.

Azure Storage, geliştirme sürecini kolaylaştırmak için farklı işletim sistemleri (Windows ve Linux dahil) kullanan istemcileri ve farklı programlama dillerini (.NET, Java, Node.js, Python, Ruby, PHP, C++ ve mobil programlama dilleri) destekler. Azure Storage kullanılabilir tooany istemci HTTP/HTTPS üzerinden veri gönderme ve alma özelliğine sahip olan basit REST API'leri aracılığıyla veri kaynaklarını da gösterir.

Azure Premium Storage, Azure Virtual Machines’de çalışan G/Ç açısından yoğun iş yükleri için yüksek performanslı ve düşük gecikmeli disk desteği sağlar. Azure Premium Storage ile birden çok kalıcı veri diskleri tooa sanal makine ekleyin ve bunları toomeet yapılandırmanız performans gereksinimlerinizi. Azure Premium Storage’da her veri diski maksimum G/Ç performansı için bir SSD disk ile desteklenir. Ayrıntılar için bkz. [Premium Storage: Azure Virtual Machines İş Yükleri İçin Yüksek Performanslı Depolama](storage-premium-storage.md).

## <a name="introducing-hello-azure-storage-services"></a>Hello Azure Storage hizmetlerine giriş
Azure depolama dört Hizmetleri aşağıdaki hello sunar: Blob Depolama, Table storage, kuyruk depolama ve dosya depolama.

* Blob Storage yapılandırılmamış nesne verilerini depolar. Blob; bir belge, ortam dosyası veya uygulama yükleyici gibi herhangi bir türde metin veya ikili veri olabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.
* Table Storage yapılandırılmış veri kümelerini depolar. Tablo depolama hızlı geliştirme ve hızlı erişim toolarge miktarda veri sağlayan bir NoSQL anahtar özniteliği veri deposudur.
* Kuyruk Depolama bulut hizmetlerinin bileşenleri arasında iş akışı işlemeye ve iletişime yönelik güvenilir mesajlaşma sağlar.
* File Storage hello standart SMB protokolünü kullanan eski uygulamalar için paylaşılan depolama alanı sağlar. Azure virtual machines ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara hello dosya hizmeti REST API'si üzerinden dosya verilerine erişebilir.

Size sağladığı güvenli bir hesap erişim tooservices Azure storage'da bir Azure depolama hesabıdır. Depolama hesabınız depolama kaynaklarınız için hello benzersiz ad alanı sağlar. Aşağıdaki Hello görüntü depolama hesabındaki hello Azure storage kaynakları arasındaki hello ilişkileri gösterir:

![Azure Storage Kaynakları](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob depolama
Büyük miktarda yapılandırılmamış nesne verilerini toostore hello bulutta kullanıcılar için Blob storage uygun maliyetli ve ölçeklenebilir bir çözüm sunar. Blob Depolama toostore içeriği gibi kullanabilirsiniz:

* Belgeler
* Fotoğraf, video, müzik ve blog gibi sosyal veriler
* Dosyaların, bilgisayarların, veritabanlarının ve cihazların yedekleri
* Web uygulamaları için görüntüler ve metinler
* Bulut uygulamaları için yapılandırma verileri
* Günlükler ve diğer büyük veri kümeleri gibi büyük veriler

Her blob bir kapsayıcı halinde düzenlenmiştir. Kapsayıcılar ayrıca kullanışlı bir yol tooassign güvenlik ilkeleri toogroups nesnelerin sağlar. Bir kapsayıcı herhangi bir sayıda hello depolama hesabının 500 TB kapasite sınırını toohello yukarı BLOB'ları içerebilir ve bir depolama hesabı kapsayıcıların herhangi bir sayı içerebilir.

Blob Storage blok blobları, ekleme blobları ve sayfa blobları (diskler) olmak üzere üç türde blob sunar.

* Blok blobları bulut nesnelerinin akış ve depolanması için en iyi duruma getirilmiştir ve belge, ortam dosyaları ve yedekler vb. öğelerin depolanması için uygun bir seçenektir.
* Ekleme blobları benzer tooblock BLOB'ları, ancak bunlar için iyileştirilmiş ekleme işlemleri. Bir ek blobu yalnızca yeni bir blok toohello uç eklenerek güncelleştirilebilir. Ekleme blobları olan, burada yeni verileri yalnızca toohello sonuna hello blob yazılmış toobe gereken günlüğe kaydetme gibi senaryolar için iyi bir seçimdir.
* Sayfa blobları Iaas disklerini temsil etmek için en iyi duruma getirilir ve rastgele destekleme yazar ve yukarı too1 TB boyutunda olabilir. IaaS diskine bağlı bir Azure Virtual Machine ağı, sayfa blobu olarak kaydedilen bir VHD’dir.

Karşıya yükleme veya veri tooBlob depolama belirtmeyi gerçekçi hello kablo üzerinden indirme ağ kısıtlamaları burada olun çok büyük veri kümeleri için bir sabit sürücü tooMicrosoft tooimport sevk ya da verileri doğrudan hello veri merkezinden verin. Bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanmak](storage-import-export-service.md).

## <a name="table-storage"></a>Table Storage

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Modern uygulamalar genellikle eski nesil yazılımların gerektirdiğinden daha fazla ölçeklenebilirlik ve esneklik özelliklerine sahip veri depoları gerektirir. Uygulamanızı otomatik olarak toomeet kullanıcı talebine ölçeklendirmek tablo depolama yüksek oranda kullanılabilir, yüksek düzeyde ölçeklenebilir depolama sunar. Tablo depolama, Microsoft’un NoSQL anahtar/öznitelik deposudur ve geleneksel ilişkisel veritabanlarından farklı olarak şemasız bir tasarıma sahiptir. Şemasız veri deposu sayesinde, uygulama geliştikçe verilerinizi hello olarak gereken kolay tooadapt olduğu. Tablo depolama kolay toouse olduğundan, geliştiriciler uygulamalarını hızla geliştirebilir. Hızlı ve uygun maliyetli türlü uygulama için erişim toodata.  Table Storage, benzer hacimdeki veriler için geleneksel SQL’e oranla çok daha düşük maliyetlidir.

Table Storage bir anahtar öznitelik deposudur; bu, bir tablodaki her değerin türü belirtilmiş bir özellik adıyla depolandığı anlamına gelir. Merhaba özellik adı filtreleme ve seçim kriterlerinin belirlenmesi için kullanılabilir. Özellik ve değerlerinin toplamı bir varlığı oluşturur. Table storage şemasız olduğu içinde iki varlık aynı hello tabloda farklı özellik koleksiyonları içerebilir ve bu özellikler farklı türde olabilir.

Tablo depolama toostore esnek veri kümelerini, web uygulamaları, adres defterleri, cihaz bilgilerini ve başka türde bir hizmetiniz için gerekli meta veriler için kullanıcı verileri gibi kullanabilirsiniz.  Bir tablodaki herhangi bir sayıda varlık depolayabilirsiniz ve bir depolama hesabı tabloları, hello depolama hesabının kapasite sınırını toohello herhangi bir sayıda içerebilir.

Bloblar ve kuyruklarda olduğu gibi geliştiricilerin yönetebilir ve standart REST protokollerini kullanarak Table storage erişim, ancak depolama da bir alt kümesini hello OData protokolü destekleyen gelişmiş özelliklerini basitleştiren ve hem JSON hem de AtomPub (XML tabanlı) etkinleştirme basitleştirme tablo biçimlendirir.

Bugünün Internet tabanlı uygulamaları için Table storage gibi NoSQL veritabanları ilişkisel veritabanları popüler bir alternatif tootraditional sunar.

## <a name="queue-storage"></a>Kuyruk depolama
Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır. Merhaba bulutta, hello Masaüstü, bir şirket içi sunucu veya bir mobil cihaz çalıştırıp çalıştırmadığınızı kuyruk depolama uygulama bileşenleri arasında zaman uyumsuz iletişim için güvenilir bir Mesajlaşma çözümü sağlar. Kuyruk depolama zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını da destekler.

Bir depolama hesabı herhangi sayıda kuyruk içerebilir. Bir kuyruk mesajlarını hello depolama hesabının kapasite sınırını toohello herhangi bir sayıda içerebilir. Tek bir ileti yukarı too64 KB boyutunda olabilir.

## <a name="file-storage"></a>Dosya depolama
Hello Azure dosya hizmeti hello standart sunucu ileti bloğu (SMB) protokolünü kullanarak erişilebilir yüksek oranda kullanılabilir ağ dosya paylaşımları yukarı tooset sağlar. Birden çok VM paylaşabileceğiniz anlamına gelir aynı hello okuma ve yazma erişimi dosyaları. Ayrıca, hello dosyaları hello REST arabirimini veya hello depolama istemcisi kitaplıklarını kullanarak okuyabilirsiniz.

Azure File storage Kurumsal dosya paylaşımında dosyalarından ayıran bir şeydir yerden hello dosyalara erişebilirsiniz toohello dosyasını işaret eder ve bir paylaşılan erişim imzası (SAS) belirteci içeren bir URL kullanarak Merhaba Dünya içinde. SAS belirteçleri üretebilir; belirli bir süre boyunca belirli erişim tooa özel varlık sağlarlar.

Dosya paylaşımları için birçok yaygın senaryoda kullanılabilir:

* Birçok şirket içi uygulama, dosya paylaşımlarını kullanır. Bu özellik daha kolay toomigrate kılar veri tooAzure paylaşmak uygulamalar. Bağlama hello aynı sürücü hello harfi dosya paylaşımı toohello uygulamanız tarafından kullanılan şirket içi, uygulamanızın hello dosya paylaşımına erişen hello bölümü ile küçük, varsa, değişiklikler çalışması gerekir.

* Yapılandırma dosyaları bir dosya paylaşımında depolanabilir ve birden çok VM tarafından bu dosyalara erişilebilir. Araçlar ve yardımcı programlar bir grup içindeki birden çok geliştiriciler tarafından kullanılan herkes bunları bulabilirsiniz sağlayarak bir dosya paylaşımında depolanabilir ve bunlar kullandığınız aynı sürüm hello.

* Tanılama günlükleri, Ölçümler ve kilitlenme bilgi dökümleri yalnızca üç tooa dosya paylaşımı yazılmış ve işlenen ya da daha sonra analiz veriler gösterilebilir.

Bu süre, Active Directory tabanlı kimlik doğrulaması ve erişim denetim listeleri (ACL'ler) desteklenmez, ancak bazı zaman hello gelecekteki olacaktır. erişim toohello dosya paylaşımı için kullanılan tooprovide kimlik doğrulaması Hello depolama hesabı kimlik bilgileridir. Bu bağlı hello paylaşımı herkesle tam okuma/yazma erişimi toohello paylaşımı olacağı anlamına gelir.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Erişim tooBlob, tablo, kuyruk ve dosya kaynakları
Varsayılan olarak, yalnızca hello depolama hesabı sahibi hello depolama hesabındaki kaynaklara erişebilir. Verilerinizin Hello güvenliği için hesabınızdaki kaynaklara karşı yapılan her isteği kimlik doğrulaması gerekir. Kimlik doğrulama bir Paylaşılan Anahtar modelini kullanır. BLOB'ları yapılandırılmış toosupport anonim kimlik doğrulamasını da olabilir.

Depolama hesabınız oluşturulduğunda, kimlik doğrulama için kullanılmak üzere hesabınıza iki özel erişim tuşu atanır. İki anahtarın kullanılması hello anahtarları genel güvenlik anahtar yönetimi uygulaması olarak düzenli olarak yenilediğinizde uygulamanızın kullanılabilir kalmasını sağlar.

Daha sonra tooallow denetlenen kullanıcıların erişim tooyour depolama kaynaklarını gerekiyorsa, paylaşılan erişim imzası oluşturabilirsiniz. Paylaşılan erişim imzası (SAS) etkinleştirir erişim tooa depolama kaynağı temsilci eklenmiş tooa URL olabilecek bir belirteçtir. Merhaba belirteci sahip olan herkes toowith hello izinleri belirtir işaret hello kaynağa erişebilir, onun hello süre için geçerlidir. Azure Storage, 2015-04-05 sürümüyle birlikte hizmet SAS ve hesap SAS olmak üzere iki tür paylaşılan erişim imzası destekler.

Merhaba hizmet SAS temsilciler erişim tooa kaynak yalnızca bir hello depolama hizmetleri: Blob, kuyruk, tablo veya dosya hizmeti hello.

Hesap SAS bir veya daha fazla hello depolama hizmet erişim tooresources atar. Hizmet SAS ile kullanılamayan erişim tooservice düzeyindeki işlemleri devredebilirsiniz. Ayrıca, erişim tooread, yazma ve silme işlemleri blob kapsayıcılar, tablolar, kuyruklar ve hizmet SAS ile izin verilmiyor dosya paylaşımları üzerinde devredebilirsiniz.

Son olarak bir kapsayıcı ve bloblarını veya belirli bir blobu genel erişime açabilirsiniz. Bir kapsayıcı veya bir blobun genel erişime açıldığını belirttiğinizde herkes anonim olarak okuyabilir, herhangi bir kimlik doğrulama gerekli değildir.  Genel kapsayıcılar ve bloblar web sitelerinde barındırılan ortam ve belgeler gibi kaynakların sunulması için kullanışlı bir seçenektir.  global çapta kullanıcılar toodecrease ağ gecikmesi, hello Azure CDN ile Web siteleri tarafından kullanılan blob verilerini önbelleğe alabilir.

Paylaşılan erişim imzaları ile ilgili daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md). Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md) ve [hello Azure Storage Hizmetleri için kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dd179428.aspx) güvenli erişim tooyour depolama hesabı hakkında daha fazla bilgi için.

## <a name="replication-for-durability-and-high-availability"></a>Dayanıklılık ve yüksek kullanılabilirlik için çoğaltma
Microsoft Azure depolama hesabı her zaman olduğu Hello verilerde tooensure dayanıklılık ve yüksek kullanılabilirlik çoğaltılan. Aynı veri merkezinde ya da çoğaltma seçeneğine bağlı olarak seçtiğiniz tooa ikinci veri merkezi, verilerinizi içinde ya da hello çoğaltma kopyalar. Çoğaltma, verilerinizi korur ve geçici donanım arızalarında hello olay, uygulama yukarı zamanında korur. Verilerinizi çoğaltılır tooa ikinci veri merkezi, bu da hello birincil konuma geri dönülemez bir hataya karşı verilerinizi korur.

Çoğaltma sağlar, depolama hesabınız hello karşıladığını [depolama için hizmet düzeyi sözleşmesi (SLA)](https://azure.microsoft.com/support/legal/sla/storage/) bile hello karşılaştığı hataların içinde. Bkz. Azure depolama hakkında bilgi için başlangıç SLA dayanıklılık ve kullanılabilirlik için güvence altına alır.

Bir depolama hesabı oluşturduğunuzda, çoğaltma seçenekleri aşağıdaki hello birini seçebilirsiniz:

* **Yerel olarak yedekli depolama (LRS).** Yerel olarak yedekli depolama verilerinizin üç kopyasını tutar. LRS, tek bir bölgedeki tek bir veri merkezinde üç kez çoğaltılır. LRS normal donanım arızalarına karşı değiştirebilir, ancak tek bir veri merkezi hello başarısızlığını verilerinizi korur.

    LRS indirimli fiyatla sunulur. En üst düzeyde dayanıklılık için aşağıda açıklanan coğrafi olarak yedekli depolamayı kullanmanızı öneririz.
* **Bölgesel olarak yedekli depolama (ZRS).** Bölgesel olarak yedekli depolama verilerinizin üç kopyasını tutar. ZRS, LRS daha fazla dayanıklılık sağlayan üç kez, tek bir bölge içinde veya iki bölgede, iki toothree tesis arasında çoğaltılır. ZRS, verilerinizin tek bir bölge içinde dayanıklı olmasını sağlar.

    ZRS, LRS'ye daha yüksek düzeyde dayanıklılık sağlar; Ancak, en üst düzeyde dayanıklılık için aşağıda açıklanan coğrafi olarak yedekli depolamayı kullanmanızı öneririz.

  > [!NOTE]
  > ZRS şu an yalnızca blok bloblar için kullanılabilir ve yalnızca 2014 02 14 ve daha yeni sürümleri destekler.
  >
  > Depolama hesabınızı oluşturup zrs'yi sonra diğer toouse tooany dönüştürülemiyor çoğaltma veya tersi yazın.
  >
  >
* **Coğrafi olarak yedekli depolama (GRS)**. GRS verilerinizin altı kopyasını tutar. GRS ile verileriniz hello birincil bölge içinde üç kez çoğaltılır ve ayrıca ikincil bir bölgede yüzlerce mil hello yüksek seviyede dayanıklılık sağlanır hello birincil bölge çıktığınızda, üç kez çoğaltılır. Azure Storage hello birincil bölge sırasında bir hata Hello olayda yük devretme toohello ikincil bölge olur. GRS, verilerinizin iki ayrı bölge içinde dayanıklı olmasını sağlar.

    Bölgeye göre birincil ve ikincil eşleştirmeler hakkında daha fazla bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/).
* **Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)**. Okuma erişimli coğrafi olarak yedekli depolama, veri tooa ikincil bir coğrafi konumda çoğaltır ve ayrıca hello ikincil konumda okuma erişimi tooyour verileri sağlar. Coğrafi olarak yedekli depolamaya okuma erişimi tooaccess hello birincil veya tek bir konumda kullanılamaz hale hello olay hello ikincil konum verilerinizden sağlar. Oluşturduğunuz okuma erişimli coğrafi olarak yedekli depolama hello varsayılan depolama hesabınızın varsayılan seçenektir.

  > [!IMPORTANT]
  > Depolama hesabınız oluşturulduktan sonra hello hesabınızı oluştururken zrs seçmediyseniz verilerinizin çoğaltılma değiştirebilirsiniz. Ancak, LRS tooGRS veya RA-GRS'ye geçiş yaparsanız tek seferlik veri aktarımı ücreti ödemeniz gerekebileceğini unutmayın.
  >
  >

Depolama çoğaltma seçenekleri ile ilgili ayrıntılar için bkz. [Azure Storage çoğaltma](storage-redundancy.md).

Depolama hesabı çoğaltma ile ilgili fiyat bilgileri için bkz. [Azure Storage Fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/). Bir bölgede hangi hizmetin sağlandığına dair daha fazla bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/#services).

Azure Storage ile dayanıklılık konusunda mimari ayrıntılar için bkz. [SOSP Belgesi - Azure Storage: Güçlü Tutarlılıkla Yüksek Seviyede Kullanılabilen Bulut Depolama Hizmeti](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).

## <a name="transferring-data-tooand-from-azure-storage"></a>Azure depolama biriminden veri tooand aktarma
Depolama hesabınızda veya depolama hesaplarınız arasında hello AzCopy komut satırı yardımcı programını toocopy blob, dosya ve tablo verileri kullanabilirsiniz. Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) daha fazla bilgi için.

AzCopy üstünde hello yerleşik [Azure veri hareketi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), şu anda önizlemede kullanılabilen.

Hello Azure içeri/dışarı aktarma hizmeti veya toohello Azure veri merkezine Postalanacak sabit sürücü üzerinden depolama hesabınızla blob verisi verilecek şekilde tooimport blob verisine sağlar. Merhaba içeri/dışarı aktarma hizmeti hakkında daha fazla bilgi için bkz: [hello Microsoft Azure içeri/dışarı aktarma hizmeti tooTransfer veri tooBlob depolama kullanmak](storage-import-export-service.md).

## <a name="pricing"></a>Fiyatlandırma
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Depolama API'leri, kitaplıklar ve araçlar
Azure Storage kaynakları HTTP/HTTPS isteği yapabilen her dil ile erişilebilir. Ayrıca, Azure Storage birkaç popüler dilde programlama kitaplıkları sunar. Bu kitaplıklar zaman uyumlu ve zaman uyumsuz çağrılar, işlemleri gruplama, özel durum yönetimi, otomatik yeniden denemeler, işlemsel davranışlar vb. ayrıntıları ele alarak Azure Storage ile çalışmanın çoğu yönünü basitleştirir. Kitaplıklar dilleri aşağıdaki hello için şu anda kullanılabilir ve ardışık düzen başkalarıyla platformları hello:

### <a name="azure-storage-data-services"></a>Azure Depolama veri hizmetleri
* [Depolama Hizmetleri REST API'si](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [.NET, Windows Phone, ve Windows Çalışma Zamanı için Depolama İstemcisi Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [C++ için Depolama İstemcisi Kitaplığı](https://github.com/Azure/azure-storage-cpp)
* [Java/Android için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/java/)
* [Node.js için Depolama İstemcisi Kitaplığı](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [PHP için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/php/)
* [Ruby için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/ruby/)
* [Python için Depolama İstemcisi Kitaplığı](https://azure.microsoft.com/develop/python/)
* [PowerShell 1.0 için Depolama Cmdlet'leri](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Azure Depolama yönetim hizmetleri
* [Depolama Kaynak Sağlayıcısı REST API Başvurusu](/rest/api/storagerp/)
* [.NET için Depolama Kaynak Sağlayıcısı İstemci Kitaplığı](/dotnet/api/microsoft.azure.management.storage)
* [PowerShell 1.0 için Depolama Kaynak Sağlayıcısı Cmdlet'leri](/powershell/module/azure.storage)
* [Depolama Hizmet Yönetimi REST API'si (Klasik)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Azure Depolama veri taşıma hizmetleri
* [Depolama İçeri/Dışarı Aktarma Hizmeti REST API'si](storage-import-export-service.md)
* [.NET için Depolama Veri Taşıma İstemcisi Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Araçlar ve Yardımcı Programlar
* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Azure Depolama İstemcisi Araçları](storage-explorers.md)
* [Azure SDK'ları ve Araçları](https://azure.microsoft.com/tools/)
* [Azure Depolama Öykünücüsü](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Komut Satırı Yardımcı Programı](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Sonraki adımlar
Azure Storage hakkında daha fazla toolearn bu kaynakları araştırın:

### <a name="documentation"></a>Belgeler
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)
* [Depolama hesabı oluşturma](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Yöneticiler için
* [Azure Depolama ile Azure PowerShell’i kullanma](storage-powershell-guide-full.md)
* [Azure Depolama ile Azure CLI'sini kullanma](storage-azure-cli.md)

### <a name="for-net-developers"></a>.NET geliştiricileri için
* [.NET kullanarak Azure Blob Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-blobs.md)
* [.NET kullanarak Azure Tablo Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-tables.md)
* [.NET kullanarak Azure Kuyruk Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-queues.md)
* [Windows'da Azure Dosya Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Java/Android geliştiricileri için
* [Nasıl toouse Java'dan Blob storage](storage-java-how-to-use-blob-storage.md)
* [Nasıl toouse Java'dan Table storage](storage-java-how-to-use-table-storage.md)
* [Nasıl toouse Java'dan kuyruk depolama](storage-java-how-to-use-queue-storage.md)
* [Nasıl toouse Java'dan File storage](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Node.js geliştiricileri için
* [Nasıl toouse node.js'den Blob storage](storage-nodejs-how-to-use-blob-storage.md)
* [Nasıl toouse node.js'den Table storage](storage-nodejs-how-to-use-table-storage.md)
* [Nasıl toouse node.js'den kuyruk depolama](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>PHP geliştiricileri için
* [Nasıl toouse php'den Blob storage](storage-php-how-to-use-blobs.md)
* [Nasıl toouse php'den Table storage](storage-php-how-to-use-table-storage.md)
* [Nasıl toouse php'den kuyruk depolama](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Ruby geliştiricileri için
* [Nasıl toouse ruby'den Blob storage](storage-ruby-how-to-use-blob-storage.md)
* [Nasıl toouse ruby'den Table storage](storage-ruby-how-to-use-table-storage.md)
* [Nasıl toouse ruby'den kuyruk depolama](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Python geliştiricileri için
* [Nasıl toouse python'dan Blob storage](storage-python-how-to-use-blob-storage.md)
* [Nasıl toouse python'dan Table storage](storage-python-how-to-use-table-storage.md)
* [Nasıl toouse python'dan kuyruk depolama](storage-python-how-to-use-queue-storage.md)
* [Nasıl toouse python'dan File storage](storage-python-how-to-use-file-storage.md)
