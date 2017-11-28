<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="4c0d5-101">Bu yordamda şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="4c0d5-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="4c0d5-102">[Bakımcı yürütülebilir dosyayı çalıştırmak için hazırlık](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="4c0d5-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="4c0d5-103">[Geri Dönüşüm Kutusu ve içerik veritabanını yalnız bırakılmış BLOB'lar anında silme işlemi için hazırlama](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="4c0d5-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="4c0d5-104">[Maintainer.exe Çalıştır](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="4c0d5-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="4c0d5-105">[Geri Dönüşüm Kutusu ayarlarını ve içerik veritabanını geri](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="4c0d5-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="4c0d5-106">Bakımcı çalıştırmak hazırlamak için</span><span class="sxs-lookup"><span data-stu-id="4c0d5-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="4c0d5-107">Web ön uç sunucusunda, SharePoint 2013 Yönetim Kabuğu'nu bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="4c0d5-108">Klasöre gidin *önyükleme sürücüsü*: \Program SQL Uzak Blob Depolama 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="4c0d5-109">Yeniden Adlandır **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** için **web.config**.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="4c0d5-110">Kullanım `aspnet_regiis -pdf connectionStrings` web.config dosyasının şifresini çözmek için.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="4c0d5-111">Şifresi çözülmüş web.config dosyasında altında `connectionStrings` düğümü, SQL server örneğinizi ve içerik veritabanı adı için bağlantı dizesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="4c0d5-112">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="4c0d5-113">Kullanım `aspnet_regiis –pef connectionStrings` web.config dosyasını yeniden şifrelemek için.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="4c0d5-114">Web.config Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config için yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="4c0d5-115">İçerik Hazırlama için veritabanı ve hemen silmek için Geri Dönüşüm Kutusu'nu BLOB'lar yalnız bırakılmış</span><span class="sxs-lookup"><span data-stu-id="4c0d5-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="4c0d5-116">SQL Server'da aşağıdaki güncelleştirme sorguları hedef içerik veritabanı için SQL Management Studio'da çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4c0d5-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="4c0d5-117">Web ön uç sunucusunda altında **Merkezi Yönetim**, düzenleme **Web uygulaması genel ayarları** istenen içerik veritabanı geçici olarak geri dönüşüm kutusu devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="4c0d5-118">Tüm ilgili site koleksiyonları için bu eylem ayrıca geri dönüşüm kutusu boş.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="4c0d5-119">Bunu yapmak için tıklatın **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="4c0d5-120">Ayarlama **Geri Dönüşüm Kutusu'nu durumu** için **OFF**.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Web uygulaması genel ayarları](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="4c0d5-122">Bakımcı çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="4c0d5-122">To run the Maintainer</span></span>
* <span data-ttu-id="4c0d5-123">Web ön uç sunucusunda, SharePoint 2013 Yönetim Kabuğu'nda aşağıdaki gibi Bakımcı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4c0d5-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="4c0d5-124">Yalnızca `GarbageCollection` işlemi şu anda StorSimple için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="4c0d5-125">Ayrıca Microsoft.Data.SqlRemoteBlobs.Maintainer.exe için verilen parametreleri büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="4c0d5-126">Geri Dönüşüm Kutusu ayarlarını ve içerik veritabanını geri almak için</span><span class="sxs-lookup"><span data-stu-id="4c0d5-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="4c0d5-127">SQL Server'da aşağıdaki güncelleştirme sorguları hedef içerik veritabanı için SQL Management Studio'da çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4c0d5-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="4c0d5-128">Web ön uç sunucusunda, **Merkezi Yönetim**, düzenleme **Web uygulaması genel ayarları** Geri Dönüşüm Kutusu'nu yeniden etkinleştirmek istediğiniz içerik veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="4c0d5-129">Bunu yapmak için tıklatın **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="4c0d5-130">Geri Dönüşüm Kutusu'nu durum kümesine **ON**.</span><span class="sxs-lookup"><span data-stu-id="4c0d5-130">Set the Recycle Bin Status to **ON**.</span></span>

