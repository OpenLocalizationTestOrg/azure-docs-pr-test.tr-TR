---
title: "aaaMove data - veri yönetimi ağ geçidi | Microsoft Docs"
description: "Şirket içi ve hello arasında veri ağ geçidi toomove veri ayarlama bulut. Veri Yönetimi ağ geçidi, verilerinizi Azure Data Factory toomove kullanın."
keywords: "Veri ağ geçidi, veri tümleştirme, veri, Ağ Geçidi kimlik taşıma"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma
Bu makalede, şirket içi veri depoları ve veri fabrikası kullanarak bulut veri depoları arasında veri tümleştirme genel bir bakış sağlar. Merhaba üzerinde derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale ve diğer veri fabrikası temel kavramları makaleler: [veri kümeleri](data-factory-create-datasets.md) ve [ardışık düzen](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Veri Yönetimi Ağ Geçidi
Bir şirket içi veri deposu denetleyicisinden verilerin taşınması, şirket içi makineyi tooenable veri yönetimi ağ geçidi yüklemeniz gerekir. Merhaba ağ geçidi hello hello ağ geçidi toohello veri deposu bağlanabileceği sürece hello veri deposu olarak veya farklı bir makinede aynı makine üzerinde yüklenebilir.

> [!IMPORTANT]
> Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için. 

Merhaba aşağıdaki örneklerde, nasıl gösterir toocreate data factory bir şirket içi veri taşır ardışık ile **SQL Server** veritabanı tooan Azure blob depolama. Merhaba izlenecek bir parçası olarak yükleyin ve makinenizde hello veri yönetimi ağ geçidi yapılandırın.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>İzlenecek yol: şirket içi veri toocloud kopyalama
Bu izlenecek adımları izleyerek hello: 

1. Veri Fabrikası oluşturun.
2. Veri Yönetimi ağ geçidi oluşturun. 
3. Kaynak ve havuz veri depoları için bağlantılı Hizmetleri oluşturun.
4. Veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.
5. Bir kopyalama etkinliği toomove hello verilerle bir işlem hattı oluşturun.

## <a name="prerequisites-for-hello-tutorial"></a>Başlangıç öğreticisi için Önkoşullar
Bu kılavuzda başlamadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:

* **Azure aboneliği**.  Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Merhaba bkz [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) Ayrıntılar için makale.
* **Azure depolama hesabı**. Merhaba blob depolama alanı olarak kullandığınız bir **hedef/havuz** verileri depolamak Bu öğreticide. bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.
* **SQL Server**. Bir şirket içi SQL Server veritabanı olarak kullandığınız bir **kaynak** verileri depolamak Bu öğreticide. 

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
Bu adımda, kullandığınız hello Azure Data Factory örneğini adlı Azure portal toocreate **ADFTutorialOnPremDF**.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **+ yeni**, tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.

   ![Yeni->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. Merhaba, **yeni data factory** want **ADFTutorialOnPremDF** hello adı için.

    ![TooStartboard Ekle](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: **veri fabrikası adı "ADFTutorialOnPremDF" kullanılabilir değil**hello veri fabrikası (örneğin, yournameADFTutorialOnPremDF) hello adını değiştirin ve oluşturmayı yeniden deneyin. Bu öğreticide adımları uygularken ADFTutorialOnPremDF yerine bu adı kullanın.
   >
   > Merhaba veri fabrikasının Hello adı olarak kaydedilmesi bir **DNS** hello gelecekte olarak adlandırın ve bu nedenle herkese görünür hale gelmiştir.
   >
   >
4. Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.
5. Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun. Merhaba öğretici için adlı bir kaynak grubu oluşturun: **ADFTutorialResourceGroup**.
6. Tıklatın **oluşturma** hello üzerinde **yeni data factory** sayfası.

   > [!IMPORTANT]
   > toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.
   >
   >
7. Oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** sayfasında hello görüntü aşağıdaki gösterildiği gibi:

   ![Data Factory giriş sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Ağ geçidi oluşturma
1. Merhaba, **Data Factory** sayfasında, **yazar ve dağıtma** döşeme toolaunch hello **Düzenleyicisi** hello veri fabrikası için.

    ![Geliştir ve Dağıt Kutucuğu](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla** hello araç ve ardından **yeni veri ağ geçidi**. Alternatif olarak, sağ tıklayarak **Data Gateways** hello ağaç görünümü ve tıklatın **yeni veri ağ geçidi**.

   ![Araç çubuğundaki yeni veri ağ geçidi](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. Merhaba, **oluşturma** want **adftutorialgateway** hello için **adı**, tıklatıp **Tamam**.     

    ![Ağ geçidi sayfası oluşturma](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > Bu kılavuzda, yalnızca bir düğümle (şirket içi Windows makine) hello mantıksal ağ geçidi oluşturun. Veri Yönetimi ağ geçidi hello ağ geçidi ile birden çok şirket içi makineler ilişkilendirerek ölçeklendirebilirsiniz. Ölçeklendirmek yukarı bir düğümde aynı anda çalıştırabilirsiniz veri taşıma işlerinin sayısını artırarak. Bu özellik, tek bir düğüme sahip mantıksal bir ağ geçidi için de kullanılabilir. Bkz: [ölçeklendirme veri yönetimi ağ geçidi Azure veri fabrikası'nda](data-factory-data-management-gateway-high-availability-scalability.md) Ayrıntılar için makale.  
4. Merhaba, **yapılandırma** sayfasında, **doğrudan bu bilgisayar Yükle**. Bu eylem hello ağ geçidi için hello yükleme paketi indirir, yükler, yapılandırır ve hello bilgisayarda hello ağ geçidi kaydeder.  

   > [!NOTE]
   > Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı kullanın.
   >
   > Chrome kullanıyorsanız, toohello Git [Chrome web mağazası](https://chrome.google.com/webstore/), arama "ClickOnce" sözcüğünü, hello ClickOnce uzantıları birini seçin ve yükleyin.
   >
   > Firefox (yükleme eklenti) aynı hello. Tıklatın **menü Aç** hello araç çubuğunda (**üç yatay çizgi** hello sağ üst köşesinde), tıklatın **eklentileri**, arama "ClickOnce" sözcüğünü, hello birini seçin ClickOnce uzantıları ve yükleyin.    
   >
   >

    ![Ağ geçidi - yapılandırma sayfası](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    Bu, en kolay yolu (tek tıklatmayla) toodownload Merhaba, yüklemek, yapılandırmak ve tek tek adımda hello ağ geçidini kaydetmek yoludur. Merhaba görebilirsiniz **Microsoft Veri Yönetimi ağ geçidi Yapılandırma Yöneticisi** uygulaması bilgisayarınızda yüklü. Merhaba yürütülebilir bulabileceğiniz **ConfigManager.exe** hello klasöründeki: **C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared**.

    Ayrıca indirebilir ve bu sayfada hello bağlantıları kullanarak ağ geçidini el ile yükleyin ve hello gösterilen hello anahtarı kullanarak kaydetmek **yeni anahtar** metin kutusu.

    Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) tüm hello ağ geçidi ayrıntılarını hello için makalesi.

   > [!NOTE]
   > Merhaba yerel bilgisayar tooinstall yönetici olmanız ve hello veri yönetimi ağ geçidi başarılı bir şekilde yapılandırmanız gerekir. Ek kullanıcılar toohello ekleyebilirsiniz **veri yönetimi ağ geçidi kullanıcıları** yerel Windows grubu. Bu grubun üyeleri Hello hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi Aracı tooconfigure hello ağ geçidi kullanabilirsiniz.
   >
   >
5. Birkaç dakika bekleyin ya da bildirim iletisi aşağıdaki hello görene kadar bekleyin:

    ![Ağ geçidi yükleme başarılı](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** bilgisayarınızdaki uygulama. Merhaba, **arama** penceresinde, türü **veri yönetimi ağ geçidi** tooaccess bu yardımcı programı. Merhaba yürütülebilir bulabileceğiniz **ConfigManager.exe** hello klasöründeki: **C:\Program Files\Microsoft veri yönetim Gateway\2.0\Shared**

    ![Ağ geçidi Yapılandırma Yöneticisi](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Gördüğünüzü onaylayın `adftutorialgateway is connected toohello cloud service` ileti. Durum çubuğu hello alt görüntüler Hello **bağlı toohello bulut hizmeti** ile birlikte bir **yeşil onay işareti**.

    Merhaba üzerinde **giriş** sekmesinde de yapabilirsiniz hello işlemleri:

   * **Kayıt** bir ağ geçidi bir anahtarla hello hello kayıt düğmesini kullanarak Azure portalı.
   * **Durdur** veri yönetimi ağ geçidi ana bilgisayar hizmeti, ağ geçidi makine üzerinde çalışan hello.
   * **Zamanlama güncelleştirmeleri** toobe hello günün belirli bir zamanda yüklü.
   * Merhaba ağ geçidi olduğu zaman görüntülemek **son güncelleştirme**.
   * Bir güncelleştirme toohello ağ geçidi yüklenebilmesi için süreyi belirtin.
8. Geçiş toohello **ayarları** hello belirtilen sekmesini hello sertifikası **sertifika** hello portalında belirttiğiniz hello şirket içi veri deposu için kullanılan tooencrypt/şifre çözme kimlik bilgilerini bir bölümdür. (isteğe bağlı) Tıklatın **değişiklik** toouse kullanarak kendi sertifikanızı yerine. Varsayılan olarak, hello ağ geçidi hello Data Factory hizmeti tarafından otomatik olarak oluşturulan hello sertifika kullanır.

    ![Ağ geçidi sertifika yapılandırma](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    Ayrıca yapabilirsiniz hello hello eylemleri aşağıdaki **ayarları** sekmesi:

   * Görüntülemek veya hello ağ geçidi tarafından kullanılan hello sertifikayı dışa aktarın.
   * Merhaba HTTPS uç noktası Hello ağ geçidi tarafından kullanılan değiştirin.    
   * Merhaba ağ geçidi tarafından kullanılan bir HTTP proxy toobe ayarlayın.     
9. (isteğe bağlı) Geçiş toohello **tanılama** sekmesinde, hello denetleyin **ayrıntılı günlük kaydını etkinleştir** tooenable ayrıntılı tootroubleshoot hello ağ geçidi ile ilgili sorunları kullanabilirsiniz günlüğü istiyorsanız seçeneği. Merhaba günlük bilgileri bulunabilir **Olay Görüntüleyicisi'ni** altında **uygulama ve hizmet günlükleri** -> **veri yönetimi ağ geçidi** düğümü.

    ![Tanılama sekmesi](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Merhaba eylemleri aşağıdaki hello de gerçekleştirebilirsiniz **tanılama** sekmesi:

   * Kullanım **Bağlantıyı Sına** bölüm tooan şirket içi veri kaynağı hello ağ geçidini kullanma.
   * Tıklatın **günlüklerini görüntüle** toosee hello veri yönetimi ağ geçidi bir Olay Görüntüleyici'de oturum açın.
   * Tıklatın **günlükleri Gönder** tooupload son yedi gün tooMicrosoft toofacilitate sorunları, sorun giderme günlük içeren bir zip dosyası.
10. Merhaba üzerinde **tanılama** sekmede hello **Bağlantıyı Sına** bölümünde, select **SqlServer** hello veri hello türü için depolamak, hello ad hello veritabanı sunucusunun adını girin Merhaba veritabanı, kimlik doğrulama türünü belirtin, kullanıcı adı ve parola girin ve tıklatın **Test** tootest hello ağ geçidi toohello veritabanı olup bağlanabilir.
11. Anahtar toohello web tarayıcısı ve hello **Azure portal**, tıklatın **Tamam** hello üzerinde **yapılandırma** sayfa ve ardından hello **yeni veri ağ geçidi** Sayfa.
12. Görmeniz gerekir **adftutorialgateway** altında **Data Gateways** hello hello soldaki ağaç görünümünde.  Tıklarsanız, JSON hello ilişkili görmeniz gerekir.

## <a name="create-linked-services"></a>Bağlı hizmetler oluşturma
Bu adımda, iki bağlı hizmet oluşturma: **AzureStorageLinkedService** ve **SqlServerLinkedService**. Merhaba **SqlServerLinkedService** bir şirket içi SQL Server veritabanı ve hello bağlantılar **AzureStorageLinkedService** bağlantılı hizmeti bir Azure blob depolama toohello data factory bağlar. Merhaba şirket içi SQL Server veritabanı toohello Azure blob depolama alanından verileri kopyalayan daha sonra bu kılavuzda bir işlem hattı oluşturun.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Bağlantılı hizmet tooan şirket içi SQL Server veritabanı ekleyin
1. Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri deposu** hello araç ve seçim **SQL Server**.

   ![Yeni SQL Server bağlantılı hizmeti](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. Merhaba, **JSON Düzenleyicisi** sağ hello üzerinde adımları hello:

   1. Hello için **gatewayName**, belirtin **adftutorialgateway**.    
   2. Merhaba, **connectionString**, adımları hello:    

      1. İçin **servername**, hello hello SQL Server veritabanını barındıran hello sunucusunun adını girin.
      2. İçin **databasename**, hello hello veritabanının adını girin.
      3. Tıklatın **şifrele** hello araç çubuğunda. Merhaba kimlik bilgileri Yöneticisi uygulaması bakın.

         ![Kimlik bilgileri Yöneticisi uygulaması](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. Merhaba, **kimlik bilgilerini ayarlama** iletişim kutusunda, kimlik doğrulama türü, kullanıcı adı ve parola belirtin ve tıklatın **Tamam**. Merhaba bağlantı başarılı olursa, hello JSON depolanan hello şifrelenmiş kimlik bilgileri ve hello iletişim kutusunu kapatır.
      5. Merhaba iletişim kutusu otomatik olarak kapalı, başlatılan ve hello Azure portal ile toohello sekmesine geri dönmek hello boş tarayıcı sekmesinde kapatın.

         Merhaba ağ geçidi makinesinde, bu kimlik bilgileri olan **şifrelenmiş** Data Factory hello bir sertifika kullanarak hizmetin sahibi. Bunun yerine hello veri yönetimi ağ geçidi ile ilişkili toouse hello sertifikası istiyorsanız, bkz: [kimlik bilgilerini güvenli bir şekilde ayarlamak](#set-credentials-and-security).    
   3. Tıklatın **dağıtma** toodeploy hello SQL Server bağlantılı hizmet çubuğu hello komutu. Merhaba bağlantılı hizmet hello ağaç görünümünde görmeniz gerekir.

      ![SQL Server bağlantılı hizmet hello ağaç görünümünde](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Bir Azure depolama hesabı için bağlı hizmet ekleme
1. Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri deposu** hello komut çubuğu ve tıklatın **Azure depolama**.
2. Merhaba, Azure depolama hesabınızın hello adı **hesap adı**.
3. Merhaba, Azure depolama hesabınız için Hello anahtarını girin **hesap anahtarı**.
4. Tıklatın **dağıtma** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu adımda, girdi oluşturun ve çıkış hello kopyalama işlemi için girdi ve çıktı verilerini temsil eden veri kümeleri (şirket içi SQL Server veritabanı = > Azure blob depolama). Veri kümeleri oluşturmadan önce aşağıdaki adımları (ayrıntılı adımları izler hello listesi) hello:

* Adlı bir tablo oluşturmak **emp** SQL Server veritabanı bağlantılı hizmet toohello veri fabrikası eklediğiniz hello ve birkaç örnek girdileri hello tabloya ekleyin.
* Adlı bir blob kapsayıcı oluşturun **adftutorial** hello Azure blob depolama hesabı bir bağlantılı hizmet toohello veri fabrikası eklendi.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Şirket içi SQL Server hello öğretici için hazırlama
1. Merhaba içi SQL Server için belirttiğiniz hello veritabanında bağlantılı hizmetinin (**SqlServerLinkedService**), aşağıdaki SQL komut dosyası toocreate hello hello kullan **emp** hello veritabanındaki tablo.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Bazı örnek hello tabloya ekleyin:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Girdi veri kümesi oluşturma

1. Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla**, tıklatın **yeni veri kümesi** hello komut çubuğunda ve'ı tıklatın **SQL Server tablosuna**.
2. Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Hello aşağıdaki noktaları göz önünde bulundurun:

   * **tür** çok ayarlanır**SqlServerTable**.
   * **tableName** çok ayarlanır**emp**.
   * **linkedServiceName** çok ayarlanır**SqlServerLinkedService** (Bu kılavuzda daha önce bu bağlı hizmetin oluşturmuştunuz.).
   * Azure Data Factory başka bir ardışık düzen tarafından üretilen olmayan bir giriş veri kümesi için ayarlamalısınız **dış** çok**doğru**. Bu, üretilen dış toohello Azure Data Factory hizmetine hello giriş verisi olduğu gösterir. İsteğe bağlı olarak hello kullanarak tüm dış veri ilkeleri belirtebilirsiniz **externalData** hello öğesinde **İlkesi** bölümü.    

   Bkz: [/SQL Server'dan veri taşıma](data-factory-sqlserver-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.
3. Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutu.  

### <a name="create-output-dataset"></a>Çıktı veri kümesi oluşturma

1. Merhaba, **Data Factory düzenleyici**, tıklatın **yeni veri kümesi** hello komut çubuğunda ve'ı tıklatın **Azure Blob Depolama**.
2. Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Hello aşağıdaki noktaları göz önünde bulundurun:

   * **tür** çok ayarlanır**AzureBlob**.
   * **linkedServiceName** çok ayarlanır**AzureStorageLinkedService** (Bu bağlı hizmeti 2. adımda oluşturmuştunuz).
   * **folderPath** çok ayarlanır**adftutorial/outfromonpremdf** outfromonpremdf hello adftutorial kapsayıcı hello klasöründe olduğu. Merhaba oluşturma **adftutorial** zaten yoksa, kapsayıcı.
   * Merhaba **kullanılabilirlik** çok ayarlanır**saatlik** (**sıklığı** çok ayarlamak**saat** ve **aralığı** çok ayarlama **1**).  Merhaba Data Factory hizmetinin her saat bir çıktı veri dilimi hello oluşturur **emp** hello Azure SQL veritabanı tablosunda.

   Belirtmezseniz, bir **fileName** için bir **çıktı tablosu**, hello oluşturulan hello dosyalarında **folderPath** biçimini izleyen hello adlı: veri.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** ve **fileName** hello göre dinamik olarak **SliceStart** zaman, hello partitionedBy özelliğini kullanın. Hello, aşağıdaki örnekte, folderPath yıl, ay ve gün hello SliceStart (başlangıç saati hello dilimin işlenmekte olan) ve fileName saat SliceStart hello kullanır. Örneğin, dilim 2014 için üretilen-10-20T08:00:00, hello KlasörAdı toowikidatagateway/wikisampledataout/2014/10/20 ayarlanır ve hello fileName too08.csv ayarlayın.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Bkz: [/Azure Blob storage'da veri taşıma](data-factory-azure-blob-connector.md) JSON özellikleri hakkında ayrıntılı bilgi için.
3. Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutu. Her iki hello veri kümeleri hello ağaç görünümünde gördüğünüzü onaylayın.  

## <a name="create-pipeline"></a>İşlem hattı oluşturma
Bu adımda, oluşturduğunuz bir **ardışık düzen** biriyle **kopyalama etkinliği** kullanan **EmpOnPremSQLTable** giriş olarak ve **OutputBlobTable** olarak çıktı.

1. Veri Fabrikası Düzenleyicisi'nde tıklatın **... Daha fazla** ve **Yeni işlem hattı** öğelerine tıklayın.
2. Merhaba sağ bölmedeki JSON Hello metin aşağıdaki hello ile değiştirin:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri.
   >
   >

   Hello aşağıdaki noktaları göz önünde bulundurun:

   * Merhaba etkinlikler bölümünde, yalnızca etkinliği yoktur, **türü** çok ayarlanır**kopya**.
   * **Giriş** hello etkinlik çok ayarlamak için**EmpOnPremSQLTable** ve **çıkış** hello etkinlik çok ayarlamak için**OutputBlobTable**.
   * Merhaba, **typeProperties** bölümünde **SqlSource** hello belirtilen **kaynak türünü** ve ** BlobSink ** hello belirtilen **Havuz türü**.
   * SQL sorgusu `select * from emp` Merhaba belirtilen **sqlReaderQuery** özelliği **SqlSource**.

   Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır. Örneğin: 2014-10-14T16:32:41Z. Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın.

   Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**". toorun hello ardışık kalıcı olarak belirtmek **9/9/9999** hello hello değeri olarak **son** özelliği.

   Merhaba üzerinde göre hangi hello veri dilimleri işlenir süre hello tanımlama **kullanılabilirlik** her Azure Data Factory veri kümesi için tanımlanan özellikler.

   Merhaba örnekte vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.        
3. Tıklatın **dağıtma** toodeploy hello dataset çubuğu hello komutunda (tablo dikdörtgen bir veri kümesi olur). Altında hello ağaç görünümünde bu hello ardışık düzen görüntülenir onaylayın **ardışık düzen** düğümü.  
4. Şimdi, **X** iki kez tooclose hello sayfa tooget geri toohello **Data Factory** hello için sayfa **ADFTutorialOnPremDF**.

**Tebrikler!** Bir Azure data factory, bağlı hizmetler, veri kümeleri ve ardışık düzen ve zamanlanmış hello ardışık düzen başarıyla oluşturdunuz.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Görünüm hello data factory'de bir diyagram görünümü
1. Merhaba, **Azure portal**, tıklatın **diyagramı** döşeme hello hello giriş sayfasında **ADFTutorialOnPremDF** veri fabrikası. :

    ![Diyagram bağlantı](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Merhaba diyagramı benzer toohello görüntü aşağıdaki görmeniz gerekir:

    ![Diyagram Görünümü](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Yakınlaştırma, yakınlaştırma too100% yakınlaştırma toofit, otomatik olarak konumu ardışık düzen ve veri kümeleri, yakınlaştırma ve çizgileri gösterebilirsiniz (Seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini vurgular).  Bir nesne (giriş/çıkış veri kümesi veya işlem hattı) toosee özellikleri için çift tıklayabilirsiniz.

## <a name="monitor-pipeline"></a>İşlem hattını izleme
Bu adımda, bir Azure data factory'de neler olduğunu Azure portal toomonitor hello kullanın. PowerShell cmdlet'leri toomonitor veri kümeleri ve işlem hatlarını de kullanabilirsiniz. İzleme hakkında daha fazla bilgi için bkz [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md).

1. Merhaba şemada çift **EmpOnPremSQLTable**.  

    ![EmpOnPremSQLTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Tüm hello veri dilimi yukarı bildirimi olan **hazır** hello ardışık düzen süresi (başlangıç zamanı tooend süresi) hello geçmiş olduğundan belirtin. Hello SQL Server veritabanında hello veri ekledikten ve tüm hello zaman yoktur çünkü de olabilir. Hiç dilim hello gösterilmediğini onaylayın **sorunu dilimleri** hello alt kısmına. Tüm hello dilimler tooview tıklatın **daha görmek** hello altındaki dilimler hello listesi.
3. Merhaba, şimdi **veri kümeleri** sayfasında, **OutputBlobTable**.

    ![OputputBlobTable dilimleri](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Merhaba listeden herhangi bir veri dilimine tıklayın ve hello görmelisiniz **veri dilimi** sayfası. Merhaba dilimle ilgili etkinlik çalışır bakın. Yalnızca bir etkinlik genellikle bakın.  

    ![Veri dilimi dikey penceresi](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Merhaba dilim hello değilse **hazır** durumu, hazır olmayan ve geçerli dilimin yürütülmesini hello hello engelleme hello Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi.
5. Merhaba tıklatın **etkinlik** hello alt toosee hello listesinden **etkinlik çalışma ayrıntıları**.

   ![Etkinlik çalışma Ayrıntıları sayfası](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Verimlilik, süre ve hello ağ geçidi tootransfer hello veri kullanılan gibi bilgileri görür.
6. Tıklatın **X** tooclose tüm sayfaları dek hello
7. Merhaba toohello giriş sayfasına geri dönmek **ADFTutorialOnPremDF**.
8. (isteğe bağlı) ' I tıklatın **ardışık düzen**, tıklatın **ADFTutorialOnPremDF**ve detaya girdi tablolarında (**tüketilen**) veya çıkış veri kümeleri (**üretilen**).
9. Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) tooverify her saat için bir blob/dosyası oluşturulur.

   ![Azure Depolama Gezgini](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) tüm hello veri yönetimi ağ geçidi ayrıntılarını hello için makalesi.
* Bkz: [SQL Azure Blob tooAzure veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) nasıl toouse kopyalama etkinliği toomove veri kaynağına veri tooa havuz veri deposunu hakkında toolearn.
