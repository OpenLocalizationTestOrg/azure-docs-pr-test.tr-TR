---
title: "Öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, bir Azure Data Factory işlem hattı kopyalama etkinliği ile Merhaba Data Factory ile desteklenen Kopyalama Sihirbazı'nı kullanarak oluşturduğunuz"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Öğretici: Data Factory Kopyalama Sihirbazı kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Bu öğretici şunların nasıl yapıldığını gösterir toouse hello **Kopyalama Sihirbazı'nı** bir Azure blob depolama tooan Azure SQL veritabanından toocopy veri. 

Hello Azure Data Factory **Kopyalama Sihirbazı'nı** sağlar tooquickly bir desteklenen kaynak veri deposu desteklenen tooa hedef veri deposundan verileri kopyalayan bir veri işlem hattı oluşturun. Bu nedenle, veri taşıma senaryonuz için ilk adım toocreate örnek bir işlem hattı hello Sihirbazı'nı kullanmanızı öneririz. Kaynak ve hedef olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Bu öğretici nasıl toocreate başlatma hello Kopyalama Sihirbazı, bir Azure data factory geçtikleri bir dizi adımları tooprovide veri alım/taşıma senaryonuz ayrıntılarını gösterir. Hello sihirbazındaki adımları tamamladığınızda, Başlangıç Sihirbazı'nı bir ardışık düzen kopyalama etkinliği toocopy verilerle Azure blob depolama tooan Azure SQL veritabanını otomatik olarak oluşturur. Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Ön koşullar
Hello listelenen önkoşulları tamamlamanız [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Bu öğreticiyi gerçekleştirmeden önce makalesi.

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda, kullandığınız hello Azure portal toocreate adlı bir Azure data factory **ADFTutorialDataFactory**.

1. Çok oturum[Azure portal](https://portal.azure.com).
2. Tıklatın **+ yeni** hello sol üst köşeden tıklatın **veri + analiz**, tıklatıp **Data Factory**. 
   
   ![Yeni->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. Merhaba, **yeni data factory** dikey penceresinde:
   
   1. Girin **ADFTutorialDataFactory** hello için **adı**.
       Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: `Data factory name “ADFTutorialDataFactory” is not available`, hello veri fabrikası (örneğin, yournameADFTutorialDataFactoryYYYYMMDD) hello adını değiştirin ve oluşturmayı yeniden deneyin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.  
      
       ![Data Factory adı yok](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Azure **aboneliğinizi** seçin.
   3. Kaynak grubu için aşağıdaki adımları hello birini yapın: 
      
      - Seçin **var olanı kullan** tooselect varolan bir kaynak grubu.
      - Seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.
          
        Bu öğreticideki hello adımlardan bazıları hello adı kullandığınızı varsayar: **ADFTutorialResourceGroup** hello kaynak grubu için. Kaynak grupları hakkında toolearn bkz [Azure kaynaklarınızı grupları toomanage kaynağı kullanan](../azure-resource-manager/resource-group-overview.md).
   4. Seçin bir **konumu** hello veri fabrikası için.
   5. Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.  
   6. **Oluştur**'a tıklayın.
      
       ![Yeni veri fabrikası dikey penceresi](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** dikey penceresini hello görüntü aşağıdaki gösterildiği gibi:
   
   ![Data factory giriş sayfası](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Kopyalama Sihirbazı'nı başlatma
1. Merhaba Data Factory dikey penceresinde **kopyalama [Önizleme] verileri** toolaunch hello **Kopyalama Sihirbazı'nı**. 
   
   > [!NOTE]
   > Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** hello tarayıcı ayarlarını (veya) etkin tutma ayarlama ve oluşturmak için bir özel durum  **Login.microsoftonline.com** ve hello Sihirbazı yeniden başlatmayı deneyin.
2. Merhaba, **özellikleri** sayfa:
   
   1. **Görev adı** için **CopyFromBlobToAzureSql** girin
   2. **Açıklama** girin (isteğe bağlı).
   3. Değişiklik hello **başlangıç tarihi ve saati** ve hello **bitiş tarihi ve saati** hello bitiş tarihi ayarla tootoday ve tarih toofive gün önce başla olmasını sağlayın.  
   4. **İleri**’ye tıklayın.  
      
      ![Kopyalama Aracı - Özellikler sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Merhaba üzerinde **kaynak veri deposu** sayfasında, **Azure Blob Storage** döşeme. Bu sayfa toospecify hello kaynak veri deposu hello kopyalama görevi için kullanın. 
   
    ![Kopyalama Aracı - Kaynak veri deposu sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Merhaba üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:
   
   1. **Bağlı hizmet adı** için **AzureStorageLinkedService** girin.
   2. **Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.
   3. Azure **aboneliğinizi** seçin.  
   4. Seçin bir **Azure depolama hesabı** hello hesaplarına Azure depolama listesi hello seçili abonelikte kullanılabilir. Ayrıca tooenter depolama hesabı ayarlarını el ile seçerek seçebilirsiniz **el ile girmeniz** hello seçeneği **hesap seçme yöntemi**ve ardından **sonraki**. 
      
      ![Kopyalama aracı - hello Azure Blob Depolama hesabı belirtin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:
   
   1. **adftutorial** seçeneğine (klasör) çift tıklayın.
   2. **emp.txt** dosyasını seçip **Seç** öğesine tıklayın
      
      ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Merhaba üzerinde **Seç hello girdi dosyası veya klasörü** sayfasında, **sonraki**. **İkili kopya**’yı seçmeyin. 
   
    ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Merhaba üzerinde **dosya biçimi ayarları** sayfasında, gördüğünüz hello sınırlayıcıları ve hello dosyası ayrıştırılırken hello Sihirbazı tarafından otomatik olarak algılanır hello şema. Da hello sınırlayıcıları el ile Merhaba Kopyalama Sihirbazı'nı toostop otomatik-algılama veya toooverride girebilirsiniz. Tıklatın **sonraki** hello sınırlayıcıları gözden geçirin ve Önizleme veri sonra. 
   
    ![Kopyalama Aracı - Dosya biçimi ayarları](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Merhaba hedef veri deposu sayfasında, seçin **Azure SQL veritabanı**, tıklatıp **sonraki**.
   
    ![Kopyalama Aracı - Hedef depo seçme](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Üzerinde **belirt hello Azure SQL veritabanı** sayfa:
   
   1. Girin **AzureSqlLinkedService** hello için **bağlantı adı** alan.
   2. **Sunucu / veritabanı seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.
   3. Azure **aboneliğinizi** seçin.  
   4. **Sunucu adı** ve **Veritabanı** öğelerini seçin.
   5. **Kullanıcı Adı** ve **Parola** girin.
   6. **İleri**’ye tıklayın.  
      
      ![Kopyalama Aracı - Azure SQL veritabanı belirtme](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Merhaba üzerinde **tablo eşlemesi** sayfasında, **emp** hello için **hedef** alan hello aşağı açılan listeden, tıklatın **aşağı ok** (isteğe bağlı) toosee hello şema ve toopreview hello verileri.
    
     ![Kopyalama Aracı - Tablo eşleme](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Merhaba üzerinde **şema eşleme** sayfasında, **sonraki**.
    
    ![Kopyalama Aracı - düzen eşlemesi](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Merhaba üzerinde **performans ayarlarını** sayfasında, **sonraki**. 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Merhaba bilgileri gözden **Özet** sayfasında ve tıklayın **son**. Başlangıç Sihirbazı'nı (Başlangıç burada hello Kopyalama Sihirbazı'nı başlatılan) hello veri fabrikasında iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur. 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Uygulama İzleme ve Yönetmeyi başlatma
1. Merhaba üzerinde **dağıtım** sayfasında, hello bağlantıyı tıklatın: `Click here toomonitor copy pipeline`.
   
   ![Kopyalama Aracı - Dağıtım başarılı](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. Uygulama izleme hello web tarayıcınızda ayrı bir sekmede başlatılır.   
   
   ![İzleme Uygulaması](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. toosee hello son durumunu saat dilimleri tıklatın **yenileme** hello düğmesini **etkinlik WINDOWS** hello altındaki listesi. Beş etkinlik windows hello ardışık düzeni için başlangıç ve bitiş zamanları arasında beş gün boyunca bakın. Merhaba listesi otomatik olarak yenilenmez, açabilmeniz için tooclick birkaç tüm hello etkinlik windows hello hazır durumda görmeden önce kaç kez yenilemeniz. 
4. Bir etkinlik penceresinde hello listesinde seçin. Merhaba hakkındaki Hello ayrıntıları görmek **etkinlik penceresini Explorer** hello sağ üzerinde.

    ![Etkinlik penceresi ayrıntıları](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Merhaba tarihleri 11, 12, 13, 14 ve 15 hello günlük çıktısı dilimler bu tarihler için zaten oluşturulmuş olduğunu anlamına gelir, yeşil renkte olduğuna dikkat edin. Ayrıca bu renk hello ardışık kodlama bakın ve çıktı veri kümesi hello diyagram görünümünde hello. Hello önceki adımda (Merhaba renk kodlama göre) iki dilimlerinin zaten oluşturulmuş olduğunu, bir dilim işlenmekte olan ve hello diğer iki işlenen toobe bekleyen dikkat edin. 

    Bu uygulamayı kullanma hakkında daha fazla bilgi için [İzleme Uygulamasını kullanarak işlem hattını izleme ve yönetme](data-factory-monitor-manage-app.md) makalesine bakın.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Bir veri deposu hello Kopyalama Sihirbazı'nda bkz alanları/özellikleri hakkında daha fazla ayrıntı için hello tablo veri deposunda hello hello bağlantısına tıklayın. 
