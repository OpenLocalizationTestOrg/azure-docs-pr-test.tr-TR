---
title: "Uygulamanızı Azure yedekleme aaaBack"
description: "Bilgi nasıl uygulamalarınızın Azure uygulama hizmetinde toocreate yedekler."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="4cb54-103">Uygulamanızı Azure’a yedekleme</span><span class="sxs-lookup"><span data-stu-id="4cb54-103">Back up your app in Azure</span></span>
<span data-ttu-id="4cb54-104">Yedekleme hello ve geri yükleme özelliği [Azure App Service](../app-service/app-service-value-prop-what-is.md) el ile veya bir zamanlamaya göre uygulama yedeklemeleri kolayca oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cb54-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="4cb54-105">Üzerine yazma hello varolan uygulaması veya geri yükleme tooanother uygulama tarafından hello uygulama tooa anlık görüntüsünü önceki bir duruma geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="4cb54-106">Bir uygulama yedekten geri yükleme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada geri](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4cb54-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="4cb54-107">Ne yedeklenir</span><span class="sxs-lookup"><span data-stu-id="4cb54-107">What gets backed up</span></span>
<span data-ttu-id="4cb54-108">Uygulama hizmeti hello aşağıdaki yedekleme bilgi tooan Azure depolama hesabı ve kapsayıcı uygulama toouse yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="4cb54-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="4cb54-109">Uygulama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="4cb54-109">App configuration</span></span>
* <span data-ttu-id="4cb54-110">Dosya içeriği</span><span class="sxs-lookup"><span data-stu-id="4cb54-110">File content</span></span>
* <span data-ttu-id="4cb54-111">Veritabanı bağlı tooyour uygulama</span><span class="sxs-lookup"><span data-stu-id="4cb54-111">Database connected tooyour app</span></span>

<span data-ttu-id="4cb54-112">veritabanı çözümleri aşağıdaki hello ile yedekleme özelliği desteklenir:</span><span class="sxs-lookup"><span data-stu-id="4cb54-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="4cb54-113">SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="4cb54-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="4cb54-114">Azure veritabanı için MySQL (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="4cb54-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="4cb54-115">Azure veritabanı için PostgreSQL (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="4cb54-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="4cb54-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="4cb54-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="4cb54-117">Uygulama MySQL</span><span class="sxs-lookup"><span data-stu-id="4cb54-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="4cb54-118">Her yedekleme bir değil Artımlı güncelleştirme, uygulamanızın çevrimdışı tam kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4cb54-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="4cb54-119">Gereksinimleri ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="4cb54-119">Requirements and restrictions</span></span>
* <span data-ttu-id="4cb54-120">Yedekleme hello ve geri yükleme özelliğini gerektirir hello uygulama hizmeti planı toobe hello içinde **standart** katmanı veya **Premium** katmanı.</span><span class="sxs-lookup"><span data-stu-id="4cb54-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="4cb54-121">Uygulama hizmeti planı toouse daha yüksek bir katmanı ölçeklendirme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4cb54-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="4cb54-122">**Premium** katmanı sağlayan daha fazla sayıda günlük geri ups daha **standart** katmanı.</span><span class="sxs-lookup"><span data-stu-id="4cb54-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="4cb54-123">Bir Azure depolama hesabı ve kapsayıcı hello içinde gereksinim toobackup istediğiniz hello uygulama aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="4cb54-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="4cb54-124">Azure depolama hesapları hakkında daha fazla bilgi için bkz: Merhaba [bağlantılar](#moreaboutstorage) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="4cb54-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="4cb54-125">Yedeklemeler, uygulama ve veritabanı içeriğinin too10 GB olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="4cb54-126">Merhaba yedekleme boyutu bu sınırı aşarsa, bir hata alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="4cb54-127">El ile yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="4cb54-127">Create a manual backup</span></span>
1. <span data-ttu-id="4cb54-128">Merhaba, [Azure Portal](https://portal.azure.com), tooyour uygulamanın dikey gidin, seçin **yedeklemeleri**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="4cb54-129">Merhaba **yedeklemeleri** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Yedeklemeleri sayfası][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="4cb54-131">Aşağıdaki hello iletisini görürseniz, yedeklemeler sayesinde, önce uygulama hizmeti planınızı geçebilmeniz tooupgrade tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4cb54-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="4cb54-132">Bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4cb54-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="4cb54-133">![Depolama hesabı seçin](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="4cb54-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="4cb54-134">Merhaba, **yedekleme** dikey penceresinde, tıklatın **yapılandırma**
![tıklatın yapılandırın](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="4cb54-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="4cb54-135">Merhaba, **yedekleme yapılandırması** dikey penceresinde tıklatın **Depolama: yapılandırılmamış** tooconfigure bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4cb54-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Depolama hesabı seçin][ChooseStorageAccount]
4. <span data-ttu-id="4cb54-137">Yedekleme Hedefinizi seçerek bir **depolama hesabı** ve **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="4cb54-138">Merhaba depolama hesabı toohello ait olmalıdır tooback yukarı hello uygulamanın aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="4cb54-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="4cb54-139">İsterseniz, yeni bir depolama hesabı veya yeni bir kapsayıcı hello ilgili dikey oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="4cb54-140">İşiniz bittiğinde tıklatın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-140">When you're done, click **Select**.</span></span>
   
    ![Depolama hesabı seçin](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="4cb54-142">Merhaba, **yedekleme yapılandırması** yapılandırabileceğiniz hala açık kaldığını dikey penceresinde, **Backup Database**, hello yedekleri (SQL veritabanı veya MySQL) tooinclude istediğiniz, ardından tıklatın hello veritabanlarını seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Depolama hesabı seçin](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="4cb54-144">Bu listedeki bir veritabanı tooappear için bağlantı dizesi hello bulunmalıdır **bağlantı dizeleri** hello bölümünü **uygulama ayarları** dikey penceresinde uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="4cb54-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="4cb54-145">Merhaba, **yedekleme yapılandırması** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="4cb54-146">Merhaba, **yedeklemeleri** dikey penceresinde tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![BackUpNow düğmesi][BackUpNow]
   
    <span data-ttu-id="4cb54-148">Merhaba yedekleme işlemi sırasında bir ilerleme iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="4cb54-149">Merhaba depolama hesabı ve kapsayıcı yapılandırılmış sonra istediğiniz zaman el ile yedekleme başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="4cb54-150">Otomatik yedeklemeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4cb54-150">Configure automated backups</span></span>
1. <span data-ttu-id="4cb54-151">Merhaba, **yedekleme yapılandırması** dikey penceresinde ayarlamak **zamanlanmış yedekleme** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Depolama hesabı seçin](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="4cb54-153">Seçenekleri gösterir, yedekleme zamanlamasını ayarlamak **zamanlanmış yedekleme** çok**üzerinde**, ardından hello yedekleme zamanlamasını istediğiniz gibi yapılandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4cb54-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Otomatik yedeklemeler etkinleştir][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="4cb54-155">Kısmi yedeklemeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4cb54-155">Configure Partial Backups</span></span>
<span data-ttu-id="4cb54-156">Bazen, toobackup her şeyi uygulamanıza istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="4cb54-157">İşte birkaç örnek:</span><span class="sxs-lookup"><span data-stu-id="4cb54-157">Here are a few examples:</span></span>

* <span data-ttu-id="4cb54-158">[Haftalık yedeklemeler kurabilir](web-sites-backup.md#configure-automated-backups) uygulamanızın hiçbir zaman, eski blog gönderileri veya görüntüleri gibi değişiklikler statik içerik içerir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="4cb54-159">Uygulamanızın üzerinde 10 GB (aynı anda yedekleme hello maks tutar) içerik var.</span><span class="sxs-lookup"><span data-stu-id="4cb54-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="4cb54-160">Toobackup hello günlük dosyalarını istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="4cb54-161">Kısmi yedekleri sağlayan tam olarak hangi dosyaları seçtiğiniz toobackup istiyor.</span><span class="sxs-lookup"><span data-stu-id="4cb54-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="4cb54-162">Yedekleme dosyaları dışarıda bırak</span><span class="sxs-lookup"><span data-stu-id="4cb54-162">Exclude files from your backup</span></span>
<span data-ttu-id="4cb54-163">Günlük dosyaları ve bir kez yedekleme atanmış olması ve toochange yapmayacağınız statik görüntüleri içeren bir uygulama olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4cb54-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="4cb54-164">Böyle durumlarda, gelecekteki yedeklemeler depolanan bu klasörleri ve dosyaları dışlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="4cb54-165">tooexclude dosya ve klasörler, yedeklerden oluşturabilir bir `_backup.filter` hello dosyasında `D:\home\site\wwwroot` , uygulamanızın klasör.</span><span class="sxs-lookup"><span data-stu-id="4cb54-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="4cb54-166">Merhaba listesini dosyaları ve bu dosyadaki tooexclude istediğiniz klasörleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="4cb54-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="4cb54-167">Dosyalarınızı toouse Kudu olan bir kolay bir yolu tooaccess.</span><span class="sxs-lookup"><span data-stu-id="4cb54-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="4cb54-168">Tıklatın **Gelişmiş Araçlar -> Git** web uygulama tooaccess Kudu için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="4cb54-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Portal kullanarak kudu][kudu-portal]

<span data-ttu-id="4cb54-170">Hello klasörleri yedeklemelerinizi tooexclude istediğinizi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4cb54-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="4cb54-171">Örneğin, toofilter hello vurgulanan klasör ve dosyaları istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4cb54-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Görüntüler klasörüne][ImagesFolder]

<span data-ttu-id="4cb54-173">Adlı bir dosya oluşturun `_backup.filter` ve yukarıdaki hello listede hello dosyaya yerleştirin, ancak kaldırma `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="4cb54-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="4cb54-174">Bir dizin veya dosya her satırda listeleyin.</span><span class="sxs-lookup"><span data-stu-id="4cb54-174">List one directory or file per line.</span></span> <span data-ttu-id="4cb54-175">Bu nedenle hello dosyanın Merhaba içeriğine olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="4cb54-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="4cb54-176">Karşıya yükleme `_backup.filter` toohello dosya `D:\home\site\wwwroot\` kullanarak site dizininde [ftp](web-sites-deploy.md#ftp) veya başka bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="4cb54-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="4cb54-177">İsterseniz, Kudu kullanarak doğrudan hello dosyası oluşturabilirsiniz `DebugConsole` ve hello içeriği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4cb54-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="4cb54-178">Çalışma yedeklemeleri hello aynı şekilde aşağıdakini normalde yapın, [el ile](#create-a-manual-backup) veya [otomatik olarak](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="4cb54-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="4cb54-179">Şimdi, tüm dosya ve klasörlerin içinde belirtilen `_backup.filter` zamanlanmış veya el ile başlatma hello gelecekteki yedeklemelerden dışlandı.</span><span class="sxs-lookup"><span data-stu-id="4cb54-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="4cb54-180">Site hello kısmi yedekleri geri yükleme yaptığınız şekilde [normal bir yedeklemeyi geri](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4cb54-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="4cb54-181">Merhaba geri yükleme işlemi doğru şeyi hello.</span><span class="sxs-lookup"><span data-stu-id="4cb54-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="4cb54-182">Tam bir yedekleme geri yüklendiğinde hello sitedeki tüm içeriğin hello yedeklemeye ne olursa olsun ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="4cb54-183">Bir dosya hello sitesinde, ancak hello yedekleme ise silinir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="4cb54-184">Ancak, kısmi yedekleme geri yüklendiğinde kara listede hello dizinlerden biri veya herhangi bir kara listede dosyanın içinde bulunan herhangi bir içerik olduğu gibi bırakılır.</span><span class="sxs-lookup"><span data-stu-id="4cb54-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="4cb54-185">Yedeklemeler nasıl depolanır</span><span class="sxs-lookup"><span data-stu-id="4cb54-185">How backups are stored</span></span>
<span data-ttu-id="4cb54-186">Uygulamanız için bir veya daha fazla yedekleme yaptıktan sonra hello yedeklemeleri hello üzerinde görünürdür **kapsayıcıları** depolama hesabınız ve uygulamanızın dikey.</span><span class="sxs-lookup"><span data-stu-id="4cb54-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="4cb54-187">Her yedekleme oluşan Hello depolama hesabında bir`.zip` hello yedekleme verilerini içeren dosyası ve bir `.xml` hello bildirimi içeren dosya `.zip` dosya içeriği.</span><span class="sxs-lookup"><span data-stu-id="4cb54-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="4cb54-188">Sıkıştırmasını açın ve bir uygulama geri yükleme işlemini gerçekleştirmeden Yedeklemelerinizin tooaccess istiyorsanız, bu dosyalara gözatın.</span><span class="sxs-lookup"><span data-stu-id="4cb54-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="4cb54-189">Merhaba uygulama için Hello veritabanı yedeklemesi the.zip dosya hello kök dizininde depolanır.</span><span class="sxs-lookup"><span data-stu-id="4cb54-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="4cb54-190">Bir SQL veritabanı için bu bir BACPAC dosyası (dosya uzantısı yok) ve içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="4cb54-191">bkz, toocreate bir SQL veritabanı temel BACPAC verme hello üzerinde [BACPAC dosya tooCreate yeni bir kullanıcı veritabanı alma](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cb54-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="4cb54-192">Merhaba dosyalardan birini değiştirme, **websitebackups** kapsayıcı hello yedekleme toobecome geçersiz ve bu nedenle olmayan-geri yüklenebilen neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cb54-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="4cb54-193">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4cb54-193">Next Steps</span></span>
<span data-ttu-id="4cb54-194">Bir uygulama bir yedekten geri yükleme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada geri](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4cb54-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="4cb54-195">Ayrıca Yedekleme ve geri yükleme REST API kullanarak App Service uygulamalarının (bkz [kullanım REST toobackup ve geri yükleme App Service uygulamalarının](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="4cb54-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

