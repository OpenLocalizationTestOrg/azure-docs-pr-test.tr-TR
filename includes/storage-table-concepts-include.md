## <a name="what-is-table-storage"></a>Tablo depolama nedir
Azure Tablo depolama, büyük miktarlarda yapısal veriyi depolar. Merhaba içinden ve dışından hello Azure bulut gelen çağrıları kabul eden bir NoSQL veri deposu kimlik doğrulaması hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir. Tablo depolamanın yaygın kullanımları şunlardır:

* Web ölçekli uygulamalara hizmet verebilen yapılandırılmış verilerin TB depolaması
* Karmaşık katılımların, yabancı anahtarların veya depolanan yordamların gerekmediği ve hızlı erişim için normal olmayabilen veri kümelerinin depolanması
* Kümelenmiş dizin kullanarak hızlı veri sorgulaması
* WCF veri hizmeti .NET kitaplıklarıyla Hello OData protokolü ve LINQ sorgularını kullanarak verilere erişme

Tablo depolama toostore ve sorgu büyük kümelerini yapılandırılmış ve ilişkisel olmayan verilerin kullanabilirsiniz ve; tablolara talep arttıkça ölçeklendirir.

## <a name="table-storage-concepts"></a>Tablo depolama kavramları
Tablo depolama hello aşağıdaki bileşenleri içerir:

![Tablo depolama bileşen diyagramı][Table1]

* **URL biçimi:** Kod, buradaki adres biçimini kullanarak hesaptaki tabloları işaret eder:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  Bu adres hello ile OData protokolü kullanarak doğrudan Azure tablolarını işaret edebilirsiniz. Daha fazla bilgi için bkz. [OData.org][OData.org].
* **Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../articles/storage/common/storage-scalability-targets.md).
* **Tablo**: Tablo, bir varlıklar koleksiyonudur. Tablolar varlıklardaki şemayı zorlamaz; bu da, tek tabloda farklı özellik kümelerine sahip varlıklar olabileceği anlamına gelir. bir depolama hesabı içerebilir tabloları Hello sayısı yalnızca hello depolama hesabının kapasite sınırıyla sınırlıdır.
* **Varlık**: özellikler, benzer tooa veritabanı satır kümesi bir varlıktır. Bir varlık boyutu too1MB yukarı olabilir.
* **Özellikler**: Özellik bir ad-değer çiftidir. Her varlığın too252 özellikleri toostore verileri içerebilir. Her varlıkta ayrıca, bölüm anahtarını, satır anahtarını ve zaman damgasını belirten üç sistem özelliği bulunur. Aynı bölüm anahtarı daha hızlı sorgulanabilir ve atomik işlemlere eklenir/güncelleştirilir hello olan varlık. Varlığın satır anahtarı bölüm içinde kendine ait benzersiz tanımlayıcıdır.

Tabloları ve özellikleri adlandırma hakkında daha fazla bilgi için bkz [anlama hello tablo hizmeti veri modelini](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
