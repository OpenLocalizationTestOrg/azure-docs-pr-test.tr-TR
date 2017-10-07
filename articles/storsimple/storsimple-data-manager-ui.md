---
title: "Azure StorSimple veri Yöneticisi kullanıcı Arabirimi aaaMicrosoft | Microsoft Docs"
description: "Açıklar nasıl toouse StorSimple veri Yöneticisi hizmetini UI (özel olarak incelenmektedir)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Merhaba StorSimple veri Yöneticisi hizmeti kullanıcı Arabirimi (özel olarak incelenmektedir) kullanarak yönetme

Bu makalede hello StorSimple 8000 serisi cihazlar üzerinde bulunan verileri hello StorSimple veri Yöneticisi kullanıcı Arabirimi tooperform veri dönüştürme nasıl kullanabileceğiniz açıklanır. Merhaba dönüştürülen veriler sonra Azure Media Services, Azure Hdınsight, Azure Machine Learning ve Azure Search gibi Azure diğer hizmetler tarafından kullanılabilecek. 


## <a name="use-storsimple-data-transformation"></a>StorSimple veri dönüşümü kullanın

Merhaba StorSimple Data Manager içinde veri dönüştürme oluşturulabilir hello kaynaktır. Merhaba veri dönüştürme hizmeti, StorSimple şirket içi cihaz tooblobs Azure storage'da veri taşıma olanak sağlar. Bu nedenle, iş akışında, toospecify hello ayrıntıları StorSimple cihaz ve hello verilerinizi toomove toohello depolama hesabı istediğiniz ilgi hakkında gerekir.

### <a name="create-a-storsimple-data-manager-service"></a>Bir StorSimple veri Yöneticisi hizmet oluşturma

Aşağıdaki adımları toocreate bir StorSimple veri Yöneticisi hizmeti hello gerçekleştirin.

1. toocreate bir StorSimple veri Yöneticisi hizmeti Git çok[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Merhaba tıklatın ** + ** simgesi ve StorSimple veri Yöneticisi arama. StorSimple veri Yöneticisi hizmetinize tıklayın ve ardından **oluşturma**.

3. Bu hizmet oluşturmak için aboneliğinizi etkinse, dikey penceresinde aşağıdaki hello bakın.

    ![StorSimple veri yöneticilerini kaynak oluşturma](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Merhaba girişleri girin ve tıklayın **oluşturma**. konum, depolama hesaplarınızı ve StorSimple Yöneticisi hizmetiniz barındıran bir hello olmalıdır Hello belirtildi. Şu anda yalnızca Batı ABD ve Batı Avrupa bölgeleri desteklenir. Bu nedenle, StorSimple Yöneticisi hizmeti, veri Yöneticisi hizmeti ve hello depolama hesabı tüm desteklenen hello önceki bölgelerde olmalıdır ilişkilendirilmiş. Bir dakika toocreate hello hizmeti hakkında alır.

### <a name="create-a-data-transformation-job-definition"></a>Veri dönüştürme iş tanımı oluştur

Bir StorSimple Data Manager Hizmeti'nde toocreate veri dönüştürme iş tanımı gerekir. Bir iş tanımı hello yerel biçiminde bir depolama hesabı taşınmasını ilgilendiğiniz hello veri ayrıntılarını belirtir. 

Aşağıdaki adımları toocreate yeni bir veri dönüştürme işi tanımı hello gerçekleştirin.

1.  Oluşturduğunuz toohello hizmete gidin. Tıklatın **+ iş tanımı**.

    ![Tıklatın + iş tanımı](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. Merhaba yeni iş tanımı bir dikey pencere açılır. İş tanımı bir ad verin ve tıklatın **kaynak**. Merhaba, **yapılandırma veri kaynağı** dikey penceresinde, StorSimple Cihazınızı hello ayrıntılarını belirtin ve hello verileri.

    ![İş tanımı oluştur](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Bu yeni bir veri Yöneticisi hizmeti olduğundan, hiçbir veri depoları yapılandırılır. tooadd, bir veri deposu olarak StorSimple Yöneticisi **yeni Ekle** hello veri deposu açılır ve ardından **eklemek veri deposu**.

4. Seçin **StorSimple 8000 serisi Yöneticisi** hello deposu olarak yazın ve hello özelliklerini girin, **StorSimple Yöneticisi**. Hello için **kaynak kimliği** alan, hello önce tooenter hello numarasını ihtiyacınız **:** hello kayıt anahtarı, StorSimple Yöneticisi.

    ![Veri kaynağı oluşturun](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Tıklatın **Tamam** bittiğinde. Bu veri deponuz kaydeder ve bu StorSimple Yöneticisi diğer iş tanımları bu parametreler tekrar girmeden yeniden kullanılabilir. Tıklattıktan sonra birkaç saniye sürer **Tamam** hello hello açılır listesinde, StorSimple Yöneticisi tooshow yedeklemek için.

6.  Merhaba, **yapılandırma veri kaynağı** dikey penceresinde hello aygıt adı girin ve hello verilerinizi ilgi birim adı.

7.  Merhaba, **filtre** alt bölüm, verilerinizi ilgi içeren hello kök dizini girin (Bu alan ile başlaması gereken bir `\`). Dosya filtreleri burada da ekleyebilirsiniz.

8.  Merhaba veri dönüştürme hizmeti Azure toohello anlık görüntüleri gönderilen hello veri çalışır. Bu iş çalışırken, bu işi (en son verileri toowork) çalıştırın veya toouse hello hello bulutta son varolan yedekleme (bazı arşivlenmiş veriler üzerinde çalışıyorsanız) her zaman tootake bir yedekleme seçebilirsiniz.

    ![Yeni veri kaynağı ayrıntıları](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Ardından, hello hedef ayarları yapılandırılmış toobe gerekir. Desteklenen hedefleri – Azure Storage ve Azure Media Services hesapları 2 tür vardır. Depolama hesapları, bu hesaptaki BLOB'lar içine tooput dosyaları seçin. Media services hesabı tooput dosyaları bu hesaptaki varlıklar'ı seçin. Yeniden tooadd depo gerekir. Merhaba açılır menüde seçin **yeni Ekle** ve ardından **ayarlarını yapılandırma**.

    ![Veri havuzu oluşturma](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. Burada, hello deposuyla ilişkili diğer parametreleri tooadd ve hello istediğiniz havuz hello türü seçebilirsiniz. Merhaba işi çalıştığında, her iki durumda da, bir depolama kuyruğu oluşturulur. Bu kuyruk, hazır olduğunda dönüştürülen bloblar hakkında iletilerle doldurulur. Bu sıranın Hello adı olduğu hello hello iş tanımı hello adı ile aynı. Seçerseniz **Media Services** hello depo türü, sonra da depolama hesabının kimlik bilgilerini hello Sıranın oluşturulduğu girebilirsiniz.

    ![Yeni veri havuzu ayrıntıları](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. (Bu, birkaç saniye sürer) hello veri deposu ekledikten sonra hello hello açılır, hello depodaki bulabilirsiniz **hedef hesap adı**.  Gereksinim duyduğunuz hello hedef seçin.

12. Tıklatın **Tamam** toocreate hello iş tanımı. İş tanımı şimdi ayarlanır. Bu iş tanımı birden çok kez aracılığıyla hello kullanıcı Arabirimi kullanabilirsiniz.

    ![Yeni iş tanımı Ekle](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Merhaba iş tanımı çalıştırın

StorSimple toohello depolama hesabından hello iş tanımında belirtilen toomove veri ihtiyaç duyduğunuzda tooinvoke gerekir. Merhaba parametrelerinin değiştirilmesi hello iş çağırma her zaman biraz esneklik vardır. Merhaba adımlar aşağıdaki gibidir:

1. StorSimple Data Manager hizmetinizi seçin ve çok Git**izleme**. Tıklatın **Şimdi Çalıştır**.

    ![Tetikleyici iş tanımı](./media/storsimple-data-manager-ui/run-now.png)

2. Merhaba iş tanımı seçin toorun istiyor. Tıklatın **çalışma ayarları** toomodify bu işi çalıştırmak için toochange isteyebilirsiniz herhangi bir ayarı.

    ![Çalışma proje ayarları](./media/storsimple-data-manager-ui/run-settings.png)

3. Tıklatın **Tamam** ve ardından **çalıştırmak** toolaunch işinizi. toomonitor bu iş, Git toohello **işleri** sayfası, StorSimple veri Yöneticisi'nde.

    ![İşlerini listesi ve durumu](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. Merhaba içinde toplama toomonitoring içinde **işleri** dikey penceresinde, ayrıca dinlemesi hello depolama kuyruğu burada bir ileti eklenen her zaman bir dosya StorSimple toohello depolama hesabından taşınır.


## <a name="next-steps"></a>Sonraki adımlar

[.NET SDK'sı toolaunch StorSimple Data Manager işleri](storsimple-data-manager-dotnet-jobs.md).
