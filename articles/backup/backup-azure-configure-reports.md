---
title: "Azure Backup için aaaConfigure raporları"
description: "Bu makalede, Azure kurtarma Hizmetleri kasası kullanarak yedekleme için Power BI raporları yapılandırma hakkında alınmaktadır."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Azure Backup raporlarını yapılandırma
Bu makalede, Azure kurtarma Hizmetleri kasası ve tooaccess kullanarak yedekleme için Power BI'ı kullanarak bu raporları adımları tooconfigure raporları hakkında alınmaktadır. Bu adımları gerçekleştirdikten sonra doğrudan tooPower BI tooview tüm hello raporları gidin, özelleştirebilir ve raporlar oluşturun. 

## <a name="supported-scenarios"></a>Desteklenen senaryolar
1. Azure yedekleme raporları Azure kurtarma Hizmetleri aracısını kullanarak Azure sanal makine yedekleme ve dosya/klasör yedekleme toocloud için desteklenmiyor.
2. Azure SQL, DPM ve Azure yedekleme sunucusu için raporlar şu anda desteklenmiyor.
3. Aynı depolama hesabındaki her hello kasaları için yapılandırılmışsa, kasa ve abonelikler arasında raporları görüntüleyebilir. Seçilen depolama hesabı hello olmalıdır aynı bölgede kurtarma Hizmetleri kasası.
4. Merhaba hello rapor için zamanlanan yenileme sıklığını Power bı'da 24 saattir. Power BI, raporları işlemeye yönelik büyük/küçük harfe en son verileri müşteri depolama hesabındaki kullanıldığı hello raporlarını geçici yenilenmesini de gerçekleştirebilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar
1. Oluşturma bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure için raporlar. Bu depolama hesabını raporları ilgili verileri depolamak için kullanılır.
2. [Power BI hesabınızı oluşturmak](https://powerbi.microsoft.com/landing/signin/) tooview, özelleştirme ve Power BI portalını kullanarak kendi raporlarınızı oluşturun.
3. Merhaba kaynak sağlayıcısı kaydetme **Microsoft.ınsights** zaten kayıtlı değil, veri tooflow toohello raporlama tooenable hello abonelik depolama hesabı ile aynı zamanda hello abonelik kurtarma Hizmetleri kasası Depolama hesabı. toodo aynı Merhaba, tooAzure portal gidin > abonelik > kaynak sağlayıcıları ve bu sağlayıcı tooregister denetleyin. 

## <a name="configure-storage-account-for-reports"></a>Raporlar için depolama hesabı yapılandırma
Aşağıdaki adımları tooconfigure hello depolama hesabı için Azure portalını kullanarak kurtarma Hizmetleri kasası hello kullanın. Bu tek seferlik yapılandırma ve depolama hesabı yapılandırıldıktan sonra raporları tooview İçerik Paketi ve Dengeleme doğrudan tooPower BI gidebilirsiniz.
1. Açık bir kurtarma Hizmetleri kasası zaten varsa toonext adıma geçin. Açık kurtarma Hizmetleri kasanız yoksa ancak hello hello Hub menüsünde, Azure portalında bulunan tıklatmak **Gözat**.

   * Kaynakları Hello listesinde yazın **kurtarma Hizmetleri**.
   * Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Kurtarma Hizmetleri kasaları** seçeneğini gördüğünüzde buna tıklayın.

      ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir. Kurtarma Hizmetleri kasalarının Hello listesinden bir kasa seçin.

     Merhaba seçilen kasa panosu açılır.
2. Kasa altında görüntülenen hello listeden öğelerinin tıklatın **yedekleme raporları** raporlar ve izleme bölümü tooconfigure hello için depolama hesabı raporları altında.

      ![Select yedekleme raporları menü öğesi 2. adım](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Merhaba yedekleme raporları dikey penceresinde **yapılandırma** düğmesi. Bu veri toocustomer depolama hesabı gönderilmesi için kullanılan hello Azure Application Insights dikey pencere açılır.

      ![Depolama hesabı adım 3 yapılandırma](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Merhaba durumu iki durumlu düğme çok ayarlamak**üzerinde** seçip **tooa depolama hesabı arşiv** veri toohello depolama hesabında akan başlayabileceğini raporlama böylece onay kutusunu işaretleyin.

      ![Adım 4 tanılamayı etkinleştir](./media/backup-azure-configure-reports/set-status-on.png)
5. Depolama hesabı Seçici ve raporlama veri ve tıklatın depolamak için hello listesinden seçim hello depolama hesabı'ı **Tamam**.

      ![Depolama hesabı adım 5'i seçin](./media/backup-azure-configure-reports/select-storage-account.png)
6. Seçin **AzureBackupReport** onay kutusunu işaretleyin ve ayrıca raporlama verilerini hello kaydırıcı tooselect saklama dönemi bu taşıyın. Raporlama verilerini hello depolama hesabındaki bu kaydırıcı kullanılarak seçilen hello boyunca tutulur.

      ![Depolama hesabı adım 6 seçin](./media/backup-azure-configure-reports/save-configuration.png)
7. Tüm hello değişiklikleri gözden geçirin ve tıklatın **kaydetmek** hello yukarıda gösterildiği gibi en üstte, düğme. Bu eylem, yaptığınız tüm değişiklikler kaydedilir ve raporlama verilerini depolamak için depolama hesabı artık yapılandırılmıştır sağlar.

> [!NOTE]
> Depolama hesabı kaydederek raporları yapılandırdıktan sonra aşağıdakileri yapmalısınız **24 saat bekleyin** ilk veri gönderme toocomplete için. Bundan sonra yalnızca Power BI içerik paketi Azure Backup almanız gerekir. Başvuru [SSS bölümüne](#frequently-asked-questions) diğer ayrıntılar için. 
>
>

## <a name="view-reports-in-power-bi"></a>Power BI raporları görüntüleme 
Depolama hesabı için yapılandırma kurtarma Hizmetleri kasası kullanarak raporları sonra veri toostart içinde akan raporlama için yaklaşık 24 saat sürer. Depolama hesabı kurma 24 saat sonra Power BI tooview raporlarda kullanmak hello aşağıdaki adımları:
1. [Oturum](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Tıklatın **Veri Al** altında Get tıklatıp **Hizmetleri** içerik paketi Kitaplığı'nda. Belirtilen adımları kullanın [belgelerine tooaccess Power BI içerik paketi](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![İçerik paketini İçeri Aktar](./media/backup-azure-configure-reports/content-pack-import.png)
3. Tür **Azure Backup** arama çubuğunda ve tıklatın **Şimdi Al**.

      ![İçerik Paketi Al](./media/backup-azure-configure-reports/content-pack-get.png)
4. Yukarıdaki 5. adımda yapılandırılmış hello depolama hesabı adı girin ve tıklayın **sonraki** düğmesi.

    ![Depolama hesabı adı girin](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Bu depolama hesabının Hello depolama hesabı anahtarı girin. Yapabilecekleriniz [görüntülemek ve depolama erişim tuşlarını kopyalayın](../storage/common/storage-create-storage-account.md#manage-your-storage-account) tooyour depolama hesabı Azure portalında gezinme tarafından. 

     ![Depolama hesabı girin](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Tıklatın **oturum** düğmesi. Oturum açma başarılı olduktan sonra size **veri alma** bildirim.

    ![İçerik Paketi içe aktarma](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Bir süre sonra size **başarı** hello alma işlemi tamamlandıktan sonra bildirim. Çok miktarda veri hello depolama hesabındaki ise biraz daha uzun tooimport hello içerik paketi, sürebilir.
    
    ![İçeri aktarma başarılı İçerik Paketi](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Verileri başarıyla içeri aktarıldığında **Azure Backup** içerik paketi, görünür **uygulamaları** hello Gezinti bölmesindeki. Merhaba liste Azure Backup Pano, raporlar ve veri kümesi artık yeni içe aktarılan raporlar belirten için sarı bir yıldız gösterir. 

     ![Azure yedekleme İçerik Paketi](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Tıklatın **Azure Backup** panolar altında sabitlenmiş anahtar rapor kümesini gösterir.

      ![Azure yedekleme Panosu](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. tooview hello eksiksiz raporları, herhangi bir rapordaki hello panosunda'ı tıklatın.

      ![Azure yedekleme işi durumu](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Merhaba tooview raporların alanındaki her bir sekmede'ı tıklatın.

      ![Azure yedekleme raporları sekmeleri](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Sık sorulan sorular
1. **Raporlama verilerini toostorage hesabında akan başlatılmış olup olmadığını nasıl kontrol?**
    
    Toohello depolama gidebilirsiniz seçin ve yapılandırılmış kapsayıcılar hesap. Merhaba kapsayıcı Öngörüler günlükleri azurebackupreport için bir giriş varsa, veri raporlama akan başlatıldığını gösterir.

2. **Merhaba sıklığı veri gönderme toostorage hesabı ve Power BI içerik paketi Azure Backup nedir?**

   0. gün kullanıcılar için yaklaşık 24 saat toopush veri toostorage hesabı kalırsınız. Bu ilk anında compelete olduğunda, veriler hello aşağıdaki çizimde gösterilen sıklığı aşağıdaki hello ile yenilenir. 
      * İlgili verileri çok**işleri, uyarılar, yedekleme öğeleri, kasa, korumalı sunucular ve ilkeleri** toocustomer depolama hesabı olarak ve ne zaman günlüğe gönderilir.
      * İlgili verileri çok**depolama** toocustomer depolama hesabı 24 saatte gönderilir.
   
    ![Azure yedekleme raporları veri gönderme sıklığını](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI bir [zamanlanan yenileme günde bir kez](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). Power BI'da hello verileri el ile yenileme için içerik paketi hello gerçekleştirebilirsiniz.

3. **Merhaba raporları ne kadar süreyle koruyabilir miyim?** 

   Depolama hesabı yapılandırırken, raporlama veri saklama dönemi (yukarıdaki rapor bölümü için adım 6 yapılandırma depolama hesabındaki kullanarak) hello depolama hesabındaki seçebilirsiniz. Yanı sıra yapabilecekleriniz [Çözümle raporlarda excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) ve bunları gereksinimlerinize göre daha uzun bir bekletme dönemi için kaydedin. 

4. **Tüm verilerimi raporlarında hello depolama hesabı yapılandırdıktan sonra görüyor?**

   Tüm sonra oluşturulan veri hello **"depolama hesabı yapılandırma"** toohello depolama hesabı gönderilir ve raporlarda kullanılabilir olacaktır. Ancak, **içinde devam eden işler değil gönderilen** raporlama için. Merhaba iş tamamlanana veya başarısız sonra tooreports gönderilir.

5. **Merhaba depolama hesabı tooview raporları ı zaten yapılandırdıysanız, başka bir depolama hesabı hello yapılandırma toouse değiştirebilirim?** 

   Evet, hello yapılandırma toopoint tooa farklı depolama hesabı değiştirebilirsiniz. TooAzure yedekleme içerik paketi bağlanırken hello yeni yapılandırılan depolama hesabı kullanmanız gerekir. Ayrıca, farklı bir depolama hesabı yapılandırıldıktan sonra yeni verileri bu depolama hesabında akış. Ancak (önce hello yapılandırmasını değiştirme) daha eski verileri hello eski depolama hesabında kalır olur.

6. **Raporları ve abonelikleri kasalarını arasında görüntüleyebilir miyim?** 

   Evet, hello yapılandırabileceğiniz çeşitli arasında aynı depolama hesabındaki kasaları tooview arası kasası raporlar. Ayrıca, yapılandırabileceğiniz abonelikler arasında hello kasaları için aynı depolama hesabı. Power BI tooview hello raporlarında tooAzure yedekleme içerik paketi bağlanırken daha sonra bu depolama hesabını kullanabilirsiniz. Ancak, seçilen hello depolama hesabı hello olmalıdır aynı bölgede kurtarma Hizmetleri kasası.
   
## <a name="next-steps"></a>Sonraki adımlar
Yapılandırdığınız artık hello depolama hesabı ve içeri aktarılan Azure Backup içerik paketi, hello sonraki adıma toocustomize bu raporları ve raporlama veri modeli toocreate raporları kullanım olmamasıdır. Daha fazla ayrıntı için makaleler hello bakın.

* [Azure Backup veri modeli raporlama kullanma](backup-azure-reports-data-model.md)
* [Power BI raporları filtreleme](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Power BI raporları oluşturma](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

