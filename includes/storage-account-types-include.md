İki tür depolama hesabı vardır:

### <a name="general-purpose-storage-accounts"></a>Genel Amaçlı Depolama Hesapları
Tabloları, kuyrukları, dosyaları, Blobları ve Azure gibi tooAzure depolama hizmetlere erişim genel amaçlı depolama hesabı verir sanal makine disklerini tek bir hesap altında. Bu tür depolama hesabında iki performans katmanı bulunur:

* Toostore tabloları, kuyrukları, dosyaları, Blobları ve Azure sağlayan standart depolama performans katmanı sanal makine disklerini.
* Şu anda yalnızca Azure Sanal Makinesi disklerini destekleyen Premium Storage performans katmanı. Premium Storage’a yönelik ayrıntılı genel bakış için bkz. [Premium Storage: Azure Virtual Machine İş Yükleri için Yüksek Performanslı Depolama](../articles/storage/common/storage-premium-storage.md).

### <a name="blob-storage-accounts"></a>Blob Storage Hesapları
Blob Storage hesabı, yapılandırılmamış verilerinizi bloblar (nesneler) olarak Azure Storage’da depolamanıza yönelik özel depolama hesabıdır. BLOB storage hesapları benzer tooyour mevcut genel amaçlı depolama hesapları ve % 100 API tutarlığı dahil günümüzde blok bloblar için kullanılır ve ilave blobları tüm hello harika dayanıklılık, kullanılabilirlik, ölçeklenebilirlik ve performans özelliklerini paylaşır. Yalnızca blok veya engelleme blobunun gerektiği uygulamalar için Blob Storage hesaplarının kullanılmasını öneririz.

> [!NOTE]
> Blob Storage hesapları yalnızca blok ve ilave bloblarını destekler, sayfa bloblarını desteklemez.
> 
> 

BLOB storage hesapları kullanıma hello **erişim katmanı** hesabı oluşturma sırasında belirtilen ve gerektiğinde daha sonra değiştirilebilir özniteliği. Erişim deseniniz temelinde belirtilebilecek iki tür erişim katmanı vardır:

* A **etkin** erişim katmanı hello depolama hesabındaki nesnelere hello daha sık erişilen olduğunu belirtir. Bu, toostore veri düşük bir erişim maliyetiyle sağlar.
* A **Cool** erişim katmanı hello depolama hesabındaki nesnelere hello daha az sıklıkta erişilen olduğunu belirtir. Bu, toostore veri düşük bir veri depolama maliyetiyle sağlar.

Merhaba, verilerinizin kullanım düzeninde bir değişiklik varsa, aynı zamanda herhangi bir zamanda bu erişim katmanları arasında geçiş yapabilirsiniz. Değişen hello erişim katmanı ek ücretlere neden olabilir. Daha fazla ayrıntı için lütfen bkz. [Blob Storage hesapları için fiyatlandırma ve faturalama](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing).

Blob Storage hesapları hakkında daha fazla ayrıntı için bkz. [Azure Blob Storage: Seyrek Erişimli ve Sık Erişimli katmanlar](../articles/storage/blobs/storage-blob-storage-tiers.md).

Bir depolama hesabı oluşturabilmeniz için önce sunan bir plan olan bir Azure aboneliğine sahip olmalıdır tooa çeşitli Azure hizmetlerine erişim. [Ücretsiz hesapla](https://azure.microsoft.com/pricing/free-trial/) Azure’a başlayabilirsiniz. Bir abonelik planı toopurchase karar verdiğinizde, çeşitli arasından seçim yapabilirsiniz [satın alma seçeneği](https://azure.microsoft.com/pricing/purchase-options/). [MSDN abonesiyseniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure Storage da dahil, Azure hizmetlerinde kullanabileceğiniz aylık ücretsiz krediler alırsınız. Birim fiyatlandırma hakkında bilgi için bkz. [Azure Storage Fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).

toocreate bir depolama hesabı nasıl görürüm toolearn [depolama hesabı oluşturma](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) daha fazla ayrıntı için. Depolama hesapları tek bir abonelik ile benzersiz olarak adlandırılmış too200 oluşturabilirsiniz. Depolama hesabı limitleri hakkında ayrıntılı bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../articles/storage/common/storage-scalability-targets.md).

