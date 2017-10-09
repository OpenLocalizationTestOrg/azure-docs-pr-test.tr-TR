<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="d5a90-101">SharePoint KKY yapılandırma değişiklikleri toohello StorSimple bağdaştırıcısı yaparken toohello Domain Admins grubuna üye olduğu bir kullanıcı hesabıyla oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="d5a90-102">Ayrıca, merkezi yönetim aynı ana bilgisayar hello üzerinde çalışan bir tarayıcıdan hello yapılandırma sayfası erişmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="d5a90-103">tooconfigure KKY</span><span class="sxs-lookup"><span data-stu-id="d5a90-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="d5a90-104">Merhaba SharePoint Yönetim Merkezi sayfasını açın ve çok gözatın**sistem ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="d5a90-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="d5a90-105">Merhaba, **Azure StorSimple** 'yi tıklatın **StorSimple bağdaştırıcısı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="d5a90-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Merhaba StorSimple bağdaştırıcısını yapılandırın](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="d5a90-107">Merhaba üzerinde **StorSimple bağdaştırıcısını yapılandırın** sayfa:</span><span class="sxs-lookup"><span data-stu-id="d5a90-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="d5a90-108">Bu hello emin olun **düzenleme yolu etkinleştir** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="d5a90-109">Merhaba metin kutusuna hello BLOB deposu hello Evrensel Adlandırma Kuralı (UNC) yolunu yazın.</span><span class="sxs-lookup"><span data-stu-id="d5a90-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="d5a90-110">Merhaba BLOB Depolama Birimi hello StorSimple cihazında yapılandırılmış bir iSCSI birim üzerinde barındırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="d5a90-111">Merhaba tıklatın **etkinleştirmek** her bir uzak depolama için tooconfigure istediğiniz hello içerik veritabanı aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="d5a90-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="d5a90-112">Merhaba BLOB deposu tüm web ön uç (WFE) sunucuları tarafından paylaşılan ve erişilebilir olması gerekir ve erişim toohello paylaşımı hello SharePoint sunucu grubu için yapılandırılmış hello kullanıcı hesabı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5a90-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Merhaba KKY sağlayıcısını etkinleştirin](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="d5a90-114">Etkinleştirmek ya da KKY devre dışı iletiden hello ayrıca görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d5a90-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![StorSimple bağdaştırıcısı etkinleştirme devre dışı bırakma yapılandırın](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="d5a90-116">Merhaba tıklatın **güncelleştirme** düğme tooapply hello yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="d5a90-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="d5a90-117">Merhaba tıkladığınızda **güncelleştirme** düğmesi tüm WFE sunucularında hello KKY yapılandırma durumu güncelleştirilir ve hello tüm Grup KKY etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d5a90-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="d5a90-118">iletiden hello görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-118">hello following message appears.</span></span>
      
      ![Bağdaştırıcı yapılandırma iletisi](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="d5a90-120">Bir çok sayıda (200'den büyük) veritabanları bir SharePoint çiftliği için KKY yapılandırıyorsanız, zaman aşımı hello SharePoint Yönetim Merkezi web sayfası olabilir. Bu gerçekleşirse, hello sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="d5a90-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="d5a90-121">Bu hello yapılandırma işlemi etkilemez.</span><span class="sxs-lookup"><span data-stu-id="d5a90-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="d5a90-122">Merhaba yapılandırmasını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="d5a90-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="d5a90-123">Toohello SharePoint Yönetim Merkezi Web sitesinde oturum ve toohello Gözat **StorSimple bağdaştırıcısını yapılandırın** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d5a90-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="d5a90-124">Merhaba yapılandırma ayrıntıları toomake girdiğiniz hello ayarları eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5a90-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="d5a90-125">KKY düzgün çalıştığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="d5a90-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="d5a90-126">Bir belge tooSharePoint karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d5a90-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="d5a90-127">Yapılandırdığınız toohello UNC yoluna göz atın.</span><span class="sxs-lookup"><span data-stu-id="d5a90-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="d5a90-128">Merhaba KKY dizin yapısını oluşturulduğunu ve karşıya hello nesne içerir emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5a90-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="d5a90-129">(İsteğe bağlı) Merhaba Microsoft RBS kullanabileceğiniz `Migrate()` SharePoint toomigrate mevcut BLOB içerik toohello StorSimple cihazı ile dahil PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d5a90-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="d5a90-130">Daha fazla bilgi için bkz: [içine veya SharePoint 2013'te KKY dışında İçerik Geçişi] [ 6] veya [içine veya dışına KKY (SharePoint Foundation 2010) İçerik Geçişi] [7].</span><span class="sxs-lookup"><span data-stu-id="d5a90-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="d5a90-131">(İsteğe bağlı) Test yüklemelerinde hello BLOB'ları gibi hello içerik veritabanı dışında taşındı doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5a90-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="d5a90-132">SQL Management Studio'yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="d5a90-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="d5a90-133">Merhaba Listblobsındb_2010.SQL veya Listblobsındb_2013.SQL sorgu aşağıdaki gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d5a90-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="d5a90-134">KKY doğru şekilde yapılandırıldıysa, bir NULL değer karşıya ve başarıyla KKY ile externalized herhangi bir nesnenin hello SizeOfContentInDB Sütun görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="d5a90-135">(İsteğe bağlı) KKY yapılandırın ve sonra tüm BLOB içerik toohello StorSimple cihazı taşıma hello içerik veritabanını toohello aygıt taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5a90-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="d5a90-136">Toomove hello içerik veritabanını seçerseniz, birincil bir birim olarak hello aygıtta hello içerik veritabanı depolama yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d5a90-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="d5a90-137">Ardından, kullanım toomigrate hello içerik veritabanını toohello StorSimple cihazı SQL Server en iyi yöntemler kurdu.</span><span class="sxs-lookup"><span data-stu-id="d5a90-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d5a90-138">Taşıma hello içerik veritabanını toohello cihaz yalnızca hello StorSimple 8000 serisi (bunu hello 5000 veya 7000 Serisi için desteklenmiyor) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d5a90-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="d5a90-139">Merhaba StorSimple cihazı ayrı birimlerde içinde BLOB'ları ve hello içerik veritabanını depoluyorsanız bunları hello yapılandırmanızı öneririz aynı birim kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d5a90-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="d5a90-140">Bu, bunlar birlikte yedeklenecek olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5a90-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="d5a90-141">KKY etkinleştirmediyseniz hello içerik veritabanını toohello StorSimple cihazı taşıma önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="d5a90-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="d5a90-142">Bu sınanmamış bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="d5a90-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="d5a90-143">Sonraki adıma gidin toohello: [çöp toplama yapılandırma](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="d5a90-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
