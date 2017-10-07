---
title: SQL Data Warehouse verilerini aaaLoad terabayt | Microsoft Docs
description: "Azure Data Factory ile altında 15 dakika nasıl 1 TB'lık veriyi Azure SQL Data Warehouse'a yüklenebilir gösterir"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>1 TB altında 15 dakika Data Factory ile Azure SQL Data Warehouse'a veri yükleme
[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) bir bulut tabanlı genişleme büyük miktarda veriyi, ilişkisel ve ilişkisel olmayan işleyebilen veritabanıdır.  SQL Data Warehouse, yüksek düzeyde paralel işleme (MPP) mimarisi üzerine kurulu, kurumsal veri ambarı iş yükleri için optimize edilmiştir.  Bulut esneklik hello esneklik tooscale depolama ile ve bağımsız olarak işlem sunar.

Azure SQL Data Warehouse ile çalışmaya başlama artık her zamankinden kullanmaktan daha kolay **Azure Data Factory**.  Azure Data Factory kullanılan toopopulate hello verileri var olan sisteminizden ve SQL Data Warehouse değerlendirmek ve analizlerinizi oluşturma, değerli zamandan kaydetme ile SQL Data Warehouse olabilen bir bulut tabanlı tam olarak yönetilen bir veri tümleştirme hizmetidir çözümleri. Azure SQL Data Azure Data Factory kullanarak Warehouse'a veri yükleme hello avantajları şunlardır:

* **Yukarı kolay tooset**: 5-adım sezgisel Sihirbazı ile gerekli komut dosyası yok.
* **Zengin veri depolamak Destek**: zengin bir şirket içi ve bulut tabanlı veri depoları için yerleşik destek.
* **Güvenli ve uyumlu**: veriler HTTPS veya ExpressRoute üzerinden aktarılır ve küresel hizmet varlığı sağlar, verilerinizin hiçbir zaman hello coğrafi sınır bırakır
* **PolyBase kullanarak benzersiz performansı** – Polybase kullanarak hello en verimli şekilde toomove verilerin Azure SQL veri ambarında eder. BLOB özelliği hazırlama hello kullanarak yüksek yük hızları, varsayılan olarak Polybase destekler hello veri depolarına Azure Blob Depolama yanı sıra tüm türlerinden elde edebilirsiniz.

Bu makale size nasıl gösterir toouse Itanium tabanlı sistemler için Data Factory Kopyalama Sihirbazı tooload 1 TB veri Azure SQL veri ambarında Azure Blob Depolama'dan üzerinde 1,2 GB/sn üretilen işi en altında 15 dakika içinde.

Bu makalede hello Kopyalama Sihirbazı'nı kullanarak Azure SQL Data Warehouse'a veri taşımak için adım adım yönergeler sağlar.

> [!NOTE]
>  Veri taşımada/Azure SQL Data Warehouse genel veri fabrikasının özellikleri hakkında bilgi için bkz: [Azure SQL veri Azure Data Factory kullanarak ambarından veri tooand taşıma](data-factory-azure-sql-data-warehouse-connector.md) makalesi.
>
> Ayrıca, Azure portalı, Visual Studio, PowerShell kullanılarak işlem hatlarını oluşturabilirsiniz vs. Bkz: [Öğreticisi: Azure Blob tooAzure SQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hızlı bir kılavuz hello kopya etkinliği Azure Data Factory kullanarak için adım adım yönergeler için.  
>
>

## <a name="prerequisites"></a>Ön koşullar
* Azure Blob Storage: TPC-H sınama veri kümesi depolamak için bu denemeyi Azure Blob Depolama (GRS) kullanır.  Azure depolama hesabınız yoksa, bilgi [nasıl toocreate bir depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) veri: biz toouse TPC-H sınama veri kümesi hello gibi yapacaksınız.  toouse gerekir, toodo `dbgen` TPC-H araç setinin yardımcı olan, hello veri kümesi oluşturur.  Kaynak kodu ya da indirebilirsiniz `dbgen` gelen [TPC Araçları](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) ve kendinize veya indirme derlenmiş hello ikiliden derleme [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Merhaba aşağıdaki ile çalışma dbgen.exe komutları toogenerate 1 TB düz dosya için `lineitem` yayılan 10 dosyalardaki tablosu:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Şimdi dosyaları tooAzure Blob kopyalama hello oluşturulur.  Çok başvuran[taşıma veri tooand bir şirket içi dosya sisteminden Azure Data Factory kullanarak](data-factory-onprem-file-system-connector.md) nasıl toodo, ADF kopyalama kullanarak.    
* Azure SQL Data Warehouse: Azure SQL Data Warehouse 6,000 Dwu ile oluşturulan veri bu deneme yükler

    Çok başvuran[bir Azure SQL Data Warehouse oluşturma](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) veritabanı nasıl toocreate SQL veri ambarı hakkında ayrıntılı yönergeler için.  tooget hello en iyi olası yük performans Polybase kullanarak SQL Data Warehouse, veri ambarı birimlerini (Dwu'lar) 6,000 Dwu olan hello performans ayarında, izin verilen en fazla sayısını seçin.

  > [!NOTE]
  > Azure Blob'tan yüklenirken hello veri performans yükleme orantılı toohello hello SQL veri ambarı hakkında yapılandırma Dwu sayısıdır:
  >
  > 1 TB 1.000 yüklenirken DWU SQL Data Warehouse 87 dakika (~ 200 MB/sn verim) yükleme 1 TB 14 dakika (~1.2 GB/sn verim) alır 46 dakika (~ 380 MB/sn verim) yükleme 1 TB 6,000 DWU SQL veri ambarında sürer 2.000 DWU SQL Data Warehouse'a alır
  >
  >

    toocreate SQL Data Warehouse 6,000 dwu'larla Taşı hello performans kaydırıcı tüm hello yolu toohello sağ:

    ![Performans kaydırıcı](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    6000 Dwu ile yapılandırılmamış bir var olan veritabanı için bunu Azure portal kullanarak ölçeklendirebilirsiniz.  Azure portalında toohello veritabanı gidin ve var olan bir **ölçek** hello düğmesini **genel bakış** görüntü aşağıdaki hello gösterilen paneli:

    ![Ölçek düğmesi](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Hello tıklatın **ölçek** düğmesini tooopen hello aşağıdaki panel, hello kaydırıcı toohello en büyük değer taşıyın ve tıklatın **kaydetmek** düğmesi.

    ![Ölçek iletişim](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Azure SQL Data Warehouse kullanarak verileri bu deneme yükler `xlargerc` kaynak sınıfı.

    tooachieve en iyi olası verimlilik, kopyalama gereken çok ait olan bir SQL Data Warehouse kullanıcı kullanılarak gerçekleştirilen toobe`xlargerc` kaynak sınıfı.  Bilgi nasıl toodo, izleyerek [kullanıcı kaynak sınıfı örneğini değiştirmek](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Hedef Tablo şemasını Azure SQL veri ambarı veritabanında DDL deyimi aşağıdaki hello çalıştırarak oluşturun:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Tamamlanan hello önkoşul adımları ile artık hazır tooconfigure hello kopyalama etkinliği hello Kopyalama Sihirbazı'nı kullanarak duyuyoruz.

## <a name="launch-copy-wizard"></a>Kopyalama Sihirbazı'nı başlatma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **+ yeni** hello sol üst köşeden tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.
3. Merhaba, **yeni data factory** dikey penceresinde:

   1. Girin **LoadIntoSQLDWDataFactory** hello için **adı**.
       Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: **veri fabrikası adı "LoadIntoSQLDWDataFactory" kullanılabilir değil**hello veri fabrikası (örneğin, yournameLoadIntoSQLDWDataFactory) hello adını değiştirin ve oluşturmayı yeniden deneyin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.  
   2. Azure **aboneliğinizi** seçin.
   3. Kaynak grubu için aşağıdaki adımları hello birini yapın:
      1. Seçin **var olanı kullan** tooselect varolan bir kaynak grubu.
      2. Seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.
   4. Seçin bir **konumu** hello veri fabrikası için.
   5. Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.  
   6. **Oluştur**'a tıklayın.
4. Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** dikey penceresini hello görüntü aşağıdaki gösterildiği gibi:

   ![Data factory giriş sayfası](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Merhaba Hello Data Factory giriş sayfasında, tıklatın **veri kopyalama** toolaunch döşeme **Kopyalama Sihirbazı'nı**.

   > [!NOTE]
   > Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini kaldırın **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** ayarlama (veya) etkin ve oluşturmak için bir özel durum **login.microsoftonline.com**ve hello Sihirbazı yeniden başlatmayı deneyin.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>1. adım: veri zamanlama yükleme yapılandırma
Merhaba ilk adımı Zamanlama yüklenirken tooconfigure hello verilerdir.  

Merhaba, **özellikleri** sayfa:

1. Girin **CopyFromBlobToAzureSqlDataWarehouse** için **görev adı**
2. Seçin **kez Şimdi Çalıştır** seçeneği.   
3. **İleri**’ye tıklayın.  

    ![Kopyalama Sihirbazı - Özellikler sayfası](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>2. adım: kaynak yapılandırma
Adımları tooconfigure hello kaynak hello bu bölümü gösterir: Azure Blob içeren hello 1 TB TPC-H satır öğesi dosyaları.

1. Select hello **Azure Blob Storage** hello veri depolamak ve tıklatın **sonraki**.

    ![Kopyalama Sihirbazı - Kaynak Seç sayfası](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Hello Azure Blob Depolama hesabı hello bağlantı bilgileri girin ve tıklayın **sonraki**.

    ![Kopyalama Sihirbazı - kaynağı bağlantı bilgileri](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Merhaba seçin **klasörü** hello TPC-H satırını içeren öğe dosyaları ve tıklayın **sonraki**.

    ![Kopyalama Sihirbazı - giriş klasörü seçin](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Tıklatarak bağlı **sonraki**, hello dosya biçimi ayarları otomatik olarak algılanır.  Bu sütun sınırlayıcı emin toomake denetleyin ' | 'yerine hello varsayılan virgül','.  Tıklatın **sonraki** hello veri önizlemesi sonra.

    ![Kopyalama Sihirbazı - dosya biçimi ayarları](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>3. adım: hedef yapılandırma
Bu bölümde, nasıl tooconfigure hello hedef gösterir: `lineitem` hello Azure SQL Data Warehouse veritabanı tablosunda.

1. Seçin **Azure SQL Data Warehouse** hello hedef olarak depolamak ve tıklatın **sonraki**.

    ![Kopyalama Sihirbazı - select hedef veri deposu](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Azure SQL Data Warehouse hello bağlantı bilgileri girin.  Hello rolünün bir üyesi olan hello kullanıcının belirttiğinizden emin olun `xlargerc` (Merhaba bkz **önkoşulları** ayrıntılı yönergeler için bölüm), tıklatıp **sonraki**.

    ![Kopyalama Sihirbazı - hedef bağlantı bilgileri](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Merhaba hedef tablo seçin ve tıklatın **sonraki**.

    ![Kopyalama Sihirbazı - Tablo eşleme sayfası](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. Şema Eşleme sayfasında "Sütun eşlemesi uygulama" seçeneği işaretsiz bırakın ve tıklatın **sonraki**.

## <a name="step-4-performance-settings"></a>4. adım: Performans ayarları

**Polybase izin** varsayılan olarak işaretli.  **İleri**’ye tıklayın.

![Kopyalama Sihirbazı - şema eşleme sayfası](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>5. adım: Dağıtma ve yükleme sonuçları izleme
1. Tıklatın **son** düğmesini toodeploy.

    ![Kopyalama Sihirbazı - Özet sayfası](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Merhaba dağıtım tamamlandıktan sonra tıklayın `Click here toomonitor copy pipeline` toomonitor hello kopyalama ilerleme çalıştırın. Select hello kopyalama işlem hattını hello oluşturduğunuz **etkinlik Windows** listesi.

    ![Kopyalama Sihirbazı - Özet sayfası](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Ayrıntı hello çalıştırın hello kopyalama görüntüleyebilirsiniz **etkinlik penceresini Explorer** panelinde kaynaktan okunan ve hedef, süre ve hello ortalama verimi hello çalıştırmak için yazılan hello veri birimi içeren hello doğru.

    Aşağıdaki ekran görüntüsü, 1 TB Azure Blob depolama alanından SQL Data Warehouse'a veri kopyalama hello gelen gördüğünüz etkili bir şekilde 1.22 GBps verimlilik elde 14 dakika sürdü!

    ![Kopyalama Sihirbazı - başarılı oldu, iletişim kutusu](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>En iyi uygulamalar
Azure SQL Data Warehouse veritabanınızı çalıştırmak için birkaç en iyi uygulamalar şunlardır:

* Daha büyük bir kaynak sınıfı, bir kümelenmiş COLUMNSTORE DİZİNİNE yüklerken kullanın.
* Daha verimli birleştirmeler için hepsini bir kez deneme dağıtımı varsayılan yerine select bir sütuna göre karma dağıtım kullanmayı düşünün.
* İçin daha hızlı yük hızları, geçici verileri öbek kullanmayı düşünün.
* Azure SQL Data Warehouse yüklemeyi bitirdikten sonra İstatistikler oluşturun.

Bkz: [en iyi uygulamalar Azure SQL Data Warehouse için](../sql-data-warehouse/sql-data-warehouse-best-practices.md) Ayrıntılar için.

## <a name="next-steps"></a>Sonraki adımlar
* [Data Factory Kopyalama Sihirbazı](data-factory-copy-wizard.md) -bu makalede hello Kopyalama Sihirbazı hakkında ayrıntılar sağlar.
* [Etkinlik performans ve ayarlama Kılavuzu kopyalama](data-factory-copy-activity-performance.md) -bu makalede hello başvuru performans ölçümleri ve ayarlama kılavuzu içerir.
