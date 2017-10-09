
<span data-ttu-id="673f3-101">Azure Cosmos DB genel dağıtım bu Azure Cuma video Scott Hanselman ve sorumlu mühendislik Yöneticisi Karthik Raman hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673f3-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="673f3-102">Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Cosmos DB genel verilerle dağıtmak](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="673f3-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="673f3-103"><a id="addregion"></a>Genel veritabanı bölgeleri Hello Azure Portal kullanarak ekleyin</span><span class="sxs-lookup"><span data-stu-id="673f3-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="673f3-104">Azure Cosmos DB kullanılabilir tüm [Azure bölgeleri] [ azureregions] dünya çapında.</span><span class="sxs-lookup"><span data-stu-id="673f3-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="673f3-105">Merhaba varsayılan tutarlılık düzeyi, veritabanı hesabının seçtikten sonra bir veya daha fazla bölgeler (tercih ettiğiniz varsayılan tutarlılık düzeyi ve genel dağıtım gereksinimlerine bağlı olarak) ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673f3-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="673f3-106">Merhaba, [Azure portal](https://portal.azure.com/), buna hello sol çubuğu, tıklatın **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="673f3-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="673f3-107">Merhaba, **Azure Cosmos DB** dikey penceresinde, select hello veritabanı hesabı toomodify.</span><span class="sxs-lookup"><span data-stu-id="673f3-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="673f3-108">Merhaba hesabı dikey penceresinde tıklayın **genel veri çoğaltma** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="673f3-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="673f3-109">Merhaba, **genel veri çoğaltma** dikey penceresinde hello bölgeleri tooadd seçin veya hello harita bölgelerde tıklatarak kaldırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="673f3-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="673f3-110">Maliyet tooadding bölgeler, hello bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/) veya hello [DocumentDB genel verilerle dağıtmak](../articles/documentdb/documentdb-distribute-data-globally.md) daha fazla bilgi için makalenin.</span><span class="sxs-lookup"><span data-stu-id="673f3-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Merhaba harita tooadd Hello bölgelerde tıklatın veya onları kaldırın][1]
    
<span data-ttu-id="673f3-112">İkinci bir bölge ekledikten sonra hello **elle yük devretme** seçeneği hello üzerinde etkin **genel veri çoğaltma** dikey penceresinde hello portal.</span><span class="sxs-lookup"><span data-stu-id="673f3-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="673f3-113">Bu seçenek tootest hello yük devretme işlemini kullanın veya hello birincil yazma bölge değiştirin.</span><span class="sxs-lookup"><span data-stu-id="673f3-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="673f3-114">Üçüncü bir bölgeye eklediğinizde, hello **yük devretme öncelikleri** seçeneğini etkinleştirerek hello aynı dikey okuma hello yük devretme sırasını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673f3-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="673f3-115">Genel veritabanı bölgeler seçme</span><span class="sxs-lookup"><span data-stu-id="673f3-115">Selecting global database regions</span></span>
<span data-ttu-id="673f3-116">İki veya daha fazla bölge yapılandırma için iki yaygın senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="673f3-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="673f3-117">Merhaba Dünya nerede bulundukları olsun toodata tooend kullanıcılar düşük gecikmeli erişim gönderiliyor</span><span class="sxs-lookup"><span data-stu-id="673f3-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="673f3-118">İş devamlılığı ve olağanüstü durum kurtarma (BCDR) için bölgesel esnekliği ekleme</span><span class="sxs-lookup"><span data-stu-id="673f3-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="673f3-119">Teslim edilmesini sağlayan düşük gecikmeli tooend-kullanıcılar, hem uygulama hello hem de Azure Cosmos DB hello bölgelerdeki toowhere hello uygulamanın kullanıcılara karşılık gelen konumlandırıldığını eklemek toodeploy önerilir.</span><span class="sxs-lookup"><span data-stu-id="673f3-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="673f3-120">BCDR için hello açıklanan hello bölge çiftleri temel tooadd bölgeler önerilir [iş devamlılığı ve olağanüstü durum kurtarma (BCDR): Azure eşleştirilmiş bölgeleri] [ bcdr] makalesi.</span><span class="sxs-lookup"><span data-stu-id="673f3-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

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
