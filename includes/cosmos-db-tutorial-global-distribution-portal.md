
Azure Cosmos DB genel dağıtım bu Azure Cuma video Scott Hanselman ve sorumlu mühendislik Yöneticisi Karthik Raman hakkında bilgi edinebilirsiniz.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Cosmos DB genel verilerle dağıtmak](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Genel veritabanı bölgeleri Hello Azure Portal kullanarak ekleyin
Azure Cosmos DB kullanılabilir tüm [Azure bölgeleri] [ azureregions] dünya çapında. Merhaba varsayılan tutarlılık düzeyi, veritabanı hesabının seçtikten sonra bir veya daha fazla bölgeler (tercih ettiğiniz varsayılan tutarlılık düzeyi ve genel dağıtım gereksinimlerine bağlı olarak) ilişkilendirebilirsiniz.

1. Merhaba, [Azure portal](https://portal.azure.com/), buna hello sol çubuğu, tıklatın **Azure Cosmos DB**.
2. Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello veritabanı hesabı toomodify.
3. Merhaba hesabı dikey penceresinde tıklayın **genel veri çoğaltma** hello menüsünde.
4. Merhaba, **genel veri çoğaltma** dikey penceresinde hello bölgeleri tooadd seçin veya hello harita bölgelerde tıklatarak kaldırın ve ardından **kaydetmek**. Maliyet tooadding bölgeler, hello bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/) veya hello [DocumentDB genel verilerle dağıtmak](../articles/documentdb/documentdb-distribute-data-globally.md) daha fazla bilgi için makalenin.
   
    ![Merhaba harita tooadd Hello bölgelerde tıklatın veya onları kaldırın][1]
    
İkinci bir bölge ekledikten sonra hello **elle yük devretme** seçeneği hello üzerinde etkin **genel veri çoğaltma** dikey penceresinde hello portal. Bu seçenek tootest hello yük devretme işlemini kullanın veya hello birincil yazma bölge değiştirin. Üçüncü bir bölgeye eklediğinizde, hello **yük devretme öncelikleri** seçeneğini etkinleştirerek hello aynı dikey okuma hello yük devretme sırasını değiştirebilirsiniz.  

### <a name="selecting-global-database-regions"></a>Genel veritabanı bölgeler seçme
İki veya daha fazla bölge yapılandırma için iki yaygın senaryolar şunlardır:

1. Merhaba Dünya nerede bulundukları olsun toodata tooend kullanıcılar düşük gecikmeli erişim gönderiliyor
2. İş devamlılığı ve olağanüstü durum kurtarma (BCDR) için bölgesel esnekliği ekleme

Teslim edilmesini sağlayan düşük gecikmeli tooend-kullanıcılar, hem uygulama hello hem de Azure Cosmos DB hello bölgelerdeki toowhere hello uygulamanın kullanıcılara karşılık gelen konumlandırıldığını eklemek toodeploy önerilir.

BCDR için hello açıklanan hello bölge çiftleri temel tooadd bölgeler önerilir [iş devamlılığı ve olağanüstü durum kurtarma (BCDR): Azure eşleştirilmiş bölgeleri] [ bcdr] makalesi.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
