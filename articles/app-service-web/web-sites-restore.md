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
# <a name="restore-an-app-in-azure"></a>Uygulamanızı Azure’a geri yükleme
Bu makale size nasıl gösterir uygulamada bir toorestore [Azure App Service](../app-service/app-service-value-prop-what-is.md) önceden yedeklediğiniz (bkz [uygulamanızı Azure yedekleme](web-sites-backup.md)). Uygulamanızı bağlantılı veritabanı isteğe bağlı tooa önceki durumuna geri yüklemek veya özgün uygulamanızın yedekleme birini temel alan yeni bir uygulama oluşturun. Azure uygulama hizmeti veritabanlarını yedekleme ve geri yükleme için aşağıdaki hello destekler:
- [SQL Veritabanı](https://azure.microsoft.com/en-us/services/sql-database/)
- [Azure veritabanı için MySQL (Önizleme)](https://azure.microsoft.com/en-us/services/mysql)
- [Azure veritabanı için PostgreSQL (Önizleme)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [Uygulama MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Kullanılabilir tooapps çalışır durumda olduğunu yedeklerden geri yükleme **standart** ve **Premium** katmanı. Uygulamanızı ölçeklendirme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md). **Premium** katmanı sağlayan daha gerçekleştirilen günlük yedekleri toobe daha fazla sayıda **standart** katmanı.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Bir uygulama olan bir yedekten geri yükleme
1. Merhaba üzerinde **ayarları** uygulamanızın hello Azure Portal dikey tıklayın **yedeklemeleri** toodisplay hello **yedeklemeleri** dikey. Ardından **geri**.
   
    ![Şimdi Geri Yükle'yi seçin][ChooseRestoreNow]
2. Merhaba, **geri** dikey penceresinde, ilk select hello yedekleme kaynak.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Merhaba **uygulama yedekleme** seçeneği gösterir, size, tüm hello geçerli uygulamanın var olan yedekleri hello ve kolayca birini seçebilirsiniz.
    Merhaba **depolama** seçeneği mevcut Azure depolama hesabı ve kapsayıcı aboneliğinizde tüm yedekleme ZIP dosyası seçin olanak sağlar.
    Toorestore başka bir uygulama yedeğini çalışıyorsanız, hello kullan **depolama** seçeneği.
3. Ardından, hello uygulama geri yükleme için hello hedef belirtin **geri yükleme hedefini**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Seçerseniz **üzerine yaz**, tüm geçerli uygulamanızda mevcut verileri silinir ve üzerine. Tıklamadan önce **Tamam**, onu tam olarak istediğinizi olduğundan emin olun toodo.
   > 
   > 
   
    Seçebileceğiniz **var olan bir uygulamayı** toorestore hello uygulama yedekleme tooanother hello uygulamada aynı kaynak kaydının grubu. Bu seçenek kullanmadan önce zaten başka bir uygulama veritabanı yapılandırması toohello hello uygulama yedeklemeye tanımlı tek yansıtma ile kaynak grubu oluşturmuş olmalıdır. Ayrıca bir **yeni** uygulama toorestore içeriğinize.

4. **Tamam** düğmesine tıklayın.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>İndirme veya depolama hesabından bir yedek Sil
1. Merhaba ana gelen **Gözat** hello Azure portal, select dikey **depolama hesapları**. Varolan depolama hesaplarınızı listesi görüntülenir.
2. Merhaba depolama hesabı için toodownload veya delete.hello dikey penceresinde görüntülenmesini istediğiniz hello yedeklemeyi içeren hello depolama hesabı seçin.
3. Merhaba depolama hesabı dikey penceresinde istediğiniz hello kapsayıcısı seçin
   
    ![Görünüm kapsayıcıları][ViewContainers]
4. Toodownload istediğiniz ya da silme yedekleme dosyasını seçin.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Tıklatın **karşıdan** veya **silmek** ne bağlı olarak toodo istediğiniz.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>İzleyici bir geri yükleme işlemi
Merhaba başarı veya başarısızlık hello uygulama geri yükleme işleminin toosee ayrıntılarını gidin toohello **etkinlik günlüğü** dikey penceresinde hello Azure portalı.  
 

Toofind istenen hello geri yükleme işlemi ve tıklatın tooselect kaydırma.

Merhaba ayrıntıları dikey penceresinde hello kullanılabilir bilgileri görüntüler toohello geri yükleme işlemi ilgili.

## <a name="next-steps"></a>Sonraki Adımlar
Yedekleme ve REST API kullanarak App Service uygulamalarının geri yükleme (bkz [kullanım REST tooback ayarlama ve App Service uygulamalarının geri](websites-csm-backup.md)).


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
