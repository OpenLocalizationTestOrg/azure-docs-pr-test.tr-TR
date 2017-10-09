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
# <a name="back-up-your-app-in-azure"></a>Uygulamanızı Azure’a yedekleme
Yedekleme hello ve geri yükleme özelliği [Azure App Service](../app-service/app-service-value-prop-what-is.md) el ile veya bir zamanlamaya göre uygulama yedeklemeleri kolayca oluşturmanıza olanak sağlar. Üzerine yazma hello varolan uygulaması veya geri yükleme tooanother uygulama tarafından hello uygulama tooa anlık görüntüsünü önceki bir duruma geri yükleyebilirsiniz. 

Bir uygulama yedekten geri yükleme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada geri](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Ne yedeklenir
Uygulama hizmeti hello aşağıdaki yedekleme bilgi tooan Azure depolama hesabı ve kapsayıcı uygulama toouse yapılandırdınız. 

* Uygulama yapılandırması
* Dosya içeriği
* Veritabanı bağlı tooyour uygulama

veritabanı çözümleri aşağıdaki hello ile yedekleme özelliği desteklenir: 
   - [SQL Veritabanı](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Azure veritabanı için MySQL (Önizleme)](https://azure.microsoft.com/en-us/services/mysql)
   - [Azure veritabanı için PostgreSQL (Önizleme)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [Uygulama MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Her yedekleme bir değil Artımlı güncelleştirme, uygulamanızın çevrimdışı tam kopyasıdır.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Gereksinimleri ve kısıtlamaları
* Yedekleme hello ve geri yükleme özelliğini gerektirir hello uygulama hizmeti planı toobe hello içinde **standart** katmanı veya **Premium** katmanı. Uygulama hizmeti planı toouse daha yüksek bir katmanı ölçeklendirme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md).  
  **Premium** katmanı sağlayan daha fazla sayıda günlük geri ups daha **standart** katmanı.
* Bir Azure depolama hesabı ve kapsayıcı hello içinde gereksinim toobackup istediğiniz hello uygulama aynı abonelik. Azure depolama hesapları hakkında daha fazla bilgi için bkz: Merhaba [bağlantılar](#moreaboutstorage) hello bu makalenin sonunda.
* Yedeklemeler, uygulama ve veritabanı içeriğinin too10 GB olabilir. Merhaba yedekleme boyutu bu sınırı aşarsa, bir hata alıyorsunuz.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>El ile yedekleme oluşturun
1. Merhaba, [Azure Portal](https://portal.azure.com), tooyour uygulamanın dikey gidin, seçin **yedeklemeleri**. Merhaba **yedeklemeleri** dikey penceresinde görüntülenir.
   
    ![Yedeklemeleri sayfası][ChooseBackupsPage]
   
   > [!NOTE]
   > Aşağıdaki hello iletisini görürseniz, yedeklemeler sayesinde, önce uygulama hizmeti planınızı geçebilmeniz tooupgrade tıklayın.
   > Bkz: [Azure bir uygulamada ölçeklendirin](web-sites-scale.md) daha fazla bilgi için.  
   > ![Depolama hesabı seçin](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Merhaba, **yedekleme** dikey penceresinde, tıklatın **yapılandırma**
![tıklatın yapılandırın](./media/web-sites-backup/ClickConfigure1.png)
3. Merhaba, **yedekleme yapılandırması** dikey penceresinde tıklatın **Depolama: yapılandırılmamış** tooconfigure bir depolama hesabı.
   
    ![Depolama hesabı seçin][ChooseStorageAccount]
4. Yedekleme Hedefinizi seçerek bir **depolama hesabı** ve **kapsayıcı**. Merhaba depolama hesabı toohello ait olmalıdır tooback yukarı hello uygulamanın aynı abonelik. İsterseniz, yeni bir depolama hesabı veya yeni bir kapsayıcı hello ilgili dikey oluşturabilirsiniz. İşiniz bittiğinde tıklatın **seçin**.
   
    ![Depolama hesabı seçin](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Merhaba, **yedekleme yapılandırması** yapılandırabileceğiniz hala açık kaldığını dikey penceresinde, **Backup Database**, hello yedekleri (SQL veritabanı veya MySQL) tooinclude istediğiniz, ardından tıklatın hello veritabanlarını seçin **Tamam**.  
   
    ![Depolama hesabı seçin](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Bu listedeki bir veritabanı tooappear için bağlantı dizesi hello bulunmalıdır **bağlantı dizeleri** hello bölümünü **uygulama ayarları** dikey penceresinde uygulamanız için.
   > 
   > 
6. Merhaba, **yedekleme yapılandırması** dikey penceresinde tıklatın **kaydetmek**.    
7. Merhaba, **yedeklemeleri** dikey penceresinde tıklatın **yedekleme**.
   
    ![BackUpNow düğmesi][BackUpNow]
   
    Merhaba yedekleme işlemi sırasında bir ilerleme iletisini görürsünüz.

Merhaba depolama hesabı ve kapsayıcı yapılandırılmış sonra istediğiniz zaman el ile yedekleme başlatabilir.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Otomatik yedeklemeleri yapılandırma
1. Merhaba, **yedekleme yapılandırması** dikey penceresinde ayarlamak **zamanlanmış yedekleme** çok**üzerinde**. 
   
    ![Depolama hesabı seçin](./media/web-sites-backup/05ScheduleBackup1.png)
2. Seçenekleri gösterir, yedekleme zamanlamasını ayarlamak **zamanlanmış yedekleme** çok**üzerinde**, ardından hello yedekleme zamanlamasını istediğiniz gibi yapılandırın ve tıklayın **Tamam**.
   
    ![Otomatik yedeklemeler etkinleştir][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Kısmi yedeklemeleri yapılandırma
Bazen, toobackup her şeyi uygulamanıza istemezsiniz. İşte birkaç örnek:

* [Haftalık yedeklemeler kurabilir](web-sites-backup.md#configure-automated-backups) uygulamanızın hiçbir zaman, eski blog gönderileri veya görüntüleri gibi değişiklikler statik içerik içerir.
* Uygulamanızın üzerinde 10 GB (aynı anda yedekleme hello maks tutar) içerik var.
* Toobackup hello günlük dosyalarını istemezsiniz.

Kısmi yedekleri sağlayan tam olarak hangi dosyaları seçtiğiniz toobackup istiyor.

### <a name="exclude-files-from-your-backup"></a>Yedekleme dosyaları dışarıda bırak
Günlük dosyaları ve bir kez yedekleme atanmış olması ve toochange yapmayacağınız statik görüntüleri içeren bir uygulama olduğunu varsayalım. Böyle durumlarda, gelecekteki yedeklemeler depolanan bu klasörleri ve dosyaları dışlayabilirsiniz. tooexclude dosya ve klasörler, yedeklerden oluşturabilir bir `_backup.filter` hello dosyasında `D:\home\site\wwwroot` , uygulamanızın klasör. Merhaba listesini dosyaları ve bu dosyadaki tooexclude istediğiniz klasörleri belirtin. 

Dosyalarınızı toouse Kudu olan bir kolay bir yolu tooaccess. Tıklatın **Gelişmiş Araçlar -> Git** web uygulama tooaccess Kudu için ayarlama.

![Portal kullanarak kudu][kudu-portal]

Hello klasörleri yedeklemelerinizi tooexclude istediğinizi belirleyin.  Örneğin, toofilter hello vurgulanan klasör ve dosyaları istiyorsunuz.

![Görüntüler klasörüne][ImagesFolder]

Adlı bir dosya oluşturun `_backup.filter` ve yukarıdaki hello listede hello dosyaya yerleştirin, ancak kaldırma `D:\home`. Bir dizin veya dosya her satırda listeleyin. Bu nedenle hello dosyanın Merhaba içeriğine olmalıdır:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Karşıya yükleme `_backup.filter` toohello dosya `D:\home\site\wwwroot\` kullanarak site dizininde [ftp](web-sites-deploy.md#ftp) veya başka bir yöntem. İsterseniz, Kudu kullanarak doğrudan hello dosyası oluşturabilirsiniz `DebugConsole` ve hello içeriği ekleyin.

Çalışma yedeklemeleri hello aynı şekilde aşağıdakini normalde yapın, [el ile](#create-a-manual-backup) veya [otomatik olarak](#configure-automated-backups). Şimdi, tüm dosya ve klasörlerin içinde belirtilen `_backup.filter` zamanlanmış veya el ile başlatma hello gelecekteki yedeklemelerden dışlandı. 

> [!NOTE]
> Site hello kısmi yedekleri geri yükleme yaptığınız şekilde [normal bir yedeklemeyi geri](web-sites-restore.md). Merhaba geri yükleme işlemi doğru şeyi hello.
> 
> Tam bir yedekleme geri yüklendiğinde hello sitedeki tüm içeriğin hello yedeklemeye ne olursa olsun ile değiştirilir. Bir dosya hello sitesinde, ancak hello yedekleme ise silinir. Ancak, kısmi yedekleme geri yüklendiğinde kara listede hello dizinlerden biri veya herhangi bir kara listede dosyanın içinde bulunan herhangi bir içerik olduğu gibi bırakılır.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Yedeklemeler nasıl depolanır
Uygulamanız için bir veya daha fazla yedekleme yaptıktan sonra hello yedeklemeleri hello üzerinde görünürdür **kapsayıcıları** depolama hesabınız ve uygulamanızın dikey. Her yedekleme oluşan Hello depolama hesabında bir`.zip` hello yedekleme verilerini içeren dosyası ve bir `.xml` hello bildirimi içeren dosya `.zip` dosya içeriği. Sıkıştırmasını açın ve bir uygulama geri yükleme işlemini gerçekleştirmeden Yedeklemelerinizin tooaccess istiyorsanız, bu dosyalara gözatın.

Merhaba uygulama için Hello veritabanı yedeklemesi the.zip dosya hello kök dizininde depolanır. Bir SQL veritabanı için bu bir BACPAC dosyası (dosya uzantısı yok) ve içeri aktarılabilir. bkz, toocreate bir SQL veritabanı temel BACPAC verme hello üzerinde [BACPAC dosya tooCreate yeni bir kullanıcı veritabanı alma](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Merhaba dosyalardan birini değiştirme, **websitebackups** kapsayıcı hello yedekleme toobecome geçersiz ve bu nedenle olmayan-geri yüklenebilen neden olabilir.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
Bir uygulama bir yedekten geri yükleme hakkında daha fazla bilgi için bkz: [Azure bir uygulamada geri](web-sites-restore.md). Ayrıca Yedekleme ve geri yükleme REST API kullanarak App Service uygulamalarının (bkz [kullanım REST toobackup ve geri yükleme App Service uygulamalarının](websites-csm-backup.md)).


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

