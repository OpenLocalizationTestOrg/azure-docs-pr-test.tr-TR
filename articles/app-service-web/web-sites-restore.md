---
title: aaaRestore azure'da uygulama
description: "Bilgi nasıl toorestore bir yedekleme uygulamanızdan."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="f8e3f-103">Uygulamanızı Azure’a geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f8e3f-103">Restore an app in Azure</span></span>
<span data-ttu-id="f8e3f-104">Bu makale size nasıl gösterir uygulamada bir toorestore [Azure App Service](../app-service/app-service-value-prop-what-is.md) önceden yedeklediğiniz (bkz [uygulamanızı Azure yedekleme](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="f8e3f-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="f8e3f-105">Uygulamanızı bağlantılı veritabanı isteğe bağlı tooa önceki durumuna geri yüklemek veya özgün uygulamanızın yedekleme birini temel alan yeni bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="f8e3f-106">Azure uygulama hizmeti veritabanlarını yedekleme ve geri yükleme için aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="f8e3f-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="f8e3f-107">SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="f8e3f-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="f8e3f-108">Azure veritabanı için MySQL (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="f8e3f-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="f8e3f-109">Azure veritabanı için PostgreSQL (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="f8e3f-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="f8e3f-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="f8e3f-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="f8e3f-111">Uygulama MySQL</span><span class="sxs-lookup"><span data-stu-id="f8e3f-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="f8e3f-112">Kullanılabilir tooapps çalışır durumda olduğunu yedeklerden geri yükleme **standart** ve **Premium** katmanı.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="f8e3f-113">Uygulamanızı ölçeklendirme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="f8e3f-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="f8e3f-114">**Premium** katmanı sağlayan daha gerçekleştirilen günlük yedekleri toobe daha fazla sayıda **standart** katmanı.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="f8e3f-115">Bir uygulama olan bir yedekten geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f8e3f-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="f8e3f-116">Merhaba üzerinde **ayarları** uygulamanızın hello Azure Portal dikey tıklayın **yedeklemeleri** toodisplay hello **yedeklemeleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="f8e3f-117">Ardından **geri**.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-117">Then click **Restore**.</span></span>
   
    ![Şimdi Geri Yükle'yi seçin][ChooseRestoreNow]
2. <span data-ttu-id="f8e3f-119">Merhaba, **geri** dikey penceresinde, ilk select hello yedekleme kaynak.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="f8e3f-120">Merhaba **uygulama yedekleme** seçeneği gösterir, size, tüm hello geçerli uygulamanın var olan yedekleri hello ve kolayca birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="f8e3f-121">Merhaba **depolama** seçeneği mevcut Azure depolama hesabı ve kapsayıcı aboneliğinizde tüm yedekleme ZIP dosyası seçin olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="f8e3f-122">Toorestore başka bir uygulama yedeğini çalışıyorsanız, hello kullan **depolama** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="f8e3f-123">Ardından, hello uygulama geri yükleme için hello hedef belirtin **geri yükleme hedefini**.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="f8e3f-124">Seçerseniz **üzerine yaz**, tüm geçerli uygulamanızda mevcut verileri silinir ve üzerine.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="f8e3f-125">Tıklamadan önce **Tamam**, onu tam olarak istediğinizi olduğundan emin olun toodo.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="f8e3f-126">Seçebileceğiniz **var olan bir uygulamayı** toorestore hello uygulama yedekleme tooanother hello uygulamada aynı kaynak kaydının grubu.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="f8e3f-127">Bu seçenek kullanmadan önce zaten başka bir uygulama veritabanı yapılandırması toohello hello uygulama yedeklemeye tanımlı tek yansıtma ile kaynak grubu oluşturmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="f8e3f-128">Ayrıca bir **yeni** uygulama toorestore içeriğinize.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="f8e3f-129">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="f8e3f-130">İndirme veya depolama hesabından bir yedek Sil</span><span class="sxs-lookup"><span data-stu-id="f8e3f-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="f8e3f-131">Merhaba ana gelen **Gözat** hello Azure portal, select dikey **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="f8e3f-132">Varolan depolama hesaplarınızı listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="f8e3f-133">Merhaba depolama hesabı için toodownload veya delete.hello dikey penceresinde görüntülenmesini istediğiniz hello yedeklemeyi içeren hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="f8e3f-134">Merhaba depolama hesabı dikey penceresinde istediğiniz hello kapsayıcısı seçin</span><span class="sxs-lookup"><span data-stu-id="f8e3f-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Görünüm kapsayıcıları][ViewContainers]
4. <span data-ttu-id="f8e3f-136">Toodownload istediğiniz ya da silme yedekleme dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="f8e3f-138">Tıklatın **karşıdan** veya **silmek** ne bağlı olarak toodo istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="f8e3f-139">İzleyici bir geri yükleme işlemi</span><span class="sxs-lookup"><span data-stu-id="f8e3f-139">Monitor a restore operation</span></span>
<span data-ttu-id="f8e3f-140">Merhaba başarı veya başarısızlık hello uygulama geri yükleme işleminin toosee ayrıntılarını gidin toohello **etkinlik günlüğü** dikey penceresinde hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="f8e3f-141">Toofind istenen hello geri yükleme işlemi ve tıklatın tooselect kaydırma.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="f8e3f-142">Merhaba ayrıntıları dikey penceresinde hello kullanılabilir bilgileri görüntüler toohello geri yükleme işlemi ilgili.</span><span class="sxs-lookup"><span data-stu-id="f8e3f-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8e3f-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f8e3f-143">Next Steps</span></span>
<span data-ttu-id="f8e3f-144">Yedekleme ve REST API kullanarak App Service uygulamalarının geri yükleme (bkz [kullanım REST tooback ayarlama ve App Service uygulamalarının geri](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="f8e3f-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
