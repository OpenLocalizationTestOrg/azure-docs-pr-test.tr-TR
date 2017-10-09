<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="d1cc4-101">Bu yordamda şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="d1cc4-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="d1cc4-102">[Toorun hello Bakımcı yürütülebilir hazırlama](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="d1cc4-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="d1cc4-103">[Merhaba içerik veritabanını ve geri dönüşüm kutusu yalnız bırakılmış BLOB'lar anında silme işlemi için hazırlama](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="d1cc4-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="d1cc4-104">[Maintainer.exe Çalıştır](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="d1cc4-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="d1cc4-105">[Merhaba içerik veritabanı ve geri dönüşüm kutusu ayarlarını geri](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="d1cc4-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="d1cc4-106">tooprepare toorun hello Bakımcı</span><span class="sxs-lookup"><span data-stu-id="d1cc4-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="d1cc4-107">Merhaba Web ön uç sunucusunda, yönetici olarak hello SharePoint 2013 Yönetim Kabuğu'nu açın.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="d1cc4-108">Toohello klasörüne gidin *önyükleme sürücüsü*: \Program SQL Uzak Blob Depolama 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="d1cc4-109">Yeniden Adlandır **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** çok**web.config**.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="d1cc4-110">Kullanım `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config dosyası.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="d1cc4-111">Merhaba altında hello şifresi çözülmüş web.config dosyasında `connectionStrings` düğümü, SQL server örneği için başlangıç bağlantı dizesi eklemek ve hello içerik veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="d1cc4-112">Merhaba aşağıdaki örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="d1cc4-113">Kullanım `aspnet_regiis –pef connectionStrings` toore-hello web.config dosyasını şifrelemek.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="d1cc4-114">Web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="d1cc4-115">tooprepare hello içerik veritabanı ve geri dönüşüm kutusu tooimmediately yalnız bırakılmış BLOB'ları silme</span><span class="sxs-lookup"><span data-stu-id="d1cc4-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="d1cc4-116">Merhaba SQL Management Studio'da, SQL Server üzerinde güncelleştirme sorguları hello hedef içerik veritabanı için aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d1cc4-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="d1cc4-117">Merhaba üzerinde web ön uç sunucusu altında **Merkezi Yönetim**, hello Düzenle **Web uygulaması genel ayarları** hello istenen içerik veritabanını tootemporarily devre dışı bırak hello geri dönüşüm kutusu için.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="d1cc4-118">Bu eylem boş hello geri dönüşüm kutusu tüm ilgili site koleksiyonları için de olur.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="d1cc4-119">toodo bunu, **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="d1cc4-120">Set hello **Geri Dönüşüm Kutusu'nu durumu** çok**OFF**.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Web uygulaması genel ayarları](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="d1cc4-122">toorun hello Bakımcı</span><span class="sxs-lookup"><span data-stu-id="d1cc4-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="d1cc4-123">Merhaba web ön uç sunucusunda, hello SharePoint 2013 Yönetim Kabuğu hello Bakımcı aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d1cc4-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="d1cc4-124">Yalnızca hello `GarbageCollection` işlemi şu anda StorSimple için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="d1cc4-125">Ayrıca Microsoft.Data.SqlRemoteBlobs.Maintainer.exe için verilen hello parametreleri büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="d1cc4-126">toorevert hello içerik veritabanını ve Geri Dönüşüm Kutusu ayarları</span><span class="sxs-lookup"><span data-stu-id="d1cc4-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="d1cc4-127">Merhaba SQL Management Studio'da, SQL Server üzerinde güncelleştirme sorguları hello hedef içerik veritabanı için aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d1cc4-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="d1cc4-128">Ön uç web sunucusuna Merhaba, içinde **Merkezi Yönetim**, hello Düzenle **Web uygulaması genel ayarları** hello istenen içerik veritabanını toore etkinleştir hello geri dönüşüm kutusu için.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="d1cc4-129">toodo bunu, **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="d1cc4-130">Merhaba Geri Dönüşüm Kutusu'nu durumu çok ayarlamak**ON**.</span><span class="sxs-lookup"><span data-stu-id="d1cc4-130">Set hello Recycle Bin Status too**ON**.</span></span>

