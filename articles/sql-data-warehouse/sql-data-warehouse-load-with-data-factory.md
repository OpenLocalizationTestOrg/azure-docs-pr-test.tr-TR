---
title: "Azure SQL veri ambarı – Data Factory aaaLoad verisine | Microsoft Docs"
description: "Bu öğreticide Azure Data Factory kullanarak Azure SQL Data Warehouse'a veri yükler ve hello veri kaynağı olarak bir SQL Server veritabanını kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Data Factory ile SQL veri ambarına veri yükleme

Azure SQL veri ambarında herhangi birinden hello Azure Data Factory tooload verileri kullanabilirsiniz [desteklenen kaynak veri depoları](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Örneğin, verileri Azure SQL veritabanına veya bir Oracle veritabanından bir SQL data warehouse'a veri fabrikası kullanarak yükleyebilirsiniz. Bu makalede öğreticide SQL data warehouse'a nasıl tooload verilerden bir şirket içi SQL Server veritabanı gösterir.

**Zaman tahmin**: hello Önkoşullar sağlandığında, Bu öğretici hakkında 10-15 dakika toocomplete gösterir.

## <a name="prerequisites"></a>Ön koşullar

- Gereksinim duyduğunuz bir **SQL Server veritabanı** hello verileri içeren tablolarla toobe toohello SQL veri ambarı kopyalanır.  

- Çevrimiçi ihtiyacınız **SQL Data Warehouse**. Veri ambarı zaten yoksa, nasıl çok öğrenin[bir Azure SQL Data Warehouse oluşturma](sql-data-warehouse-get-started-provision.md).

- Gereksinim duyduğunuz bir **Azure depolama hesabı**. Bir depolama hesabı zaten yoksa, nasıl çok öğrenin[depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md). En iyi performans için hello depolama hesabını bulun ve hello veri ambarı hello aynı Azure bölgesi.

## <a name="configure-a-data-factory"></a>Data factory Yapılandır
1. İçinde toohello oturum [Azure portal][].
2. Veri ambarınız bulun ve tooopen tıklatın.
3. Merhaba ana dikey penceresinde tıklayın **veri yükleme** > **Azure Data Factory**.

    ![Veri Yükleme Sihirbazını Başlat](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Azure aboneliğinizde bir veri fabrikası yoksa gördüğünüz bir **yeni Data Factory** hello tarayıcısının ayrı bir sekmede iletişim kutusu. Merhaba doldurun istenen bilgilerin öğesini tıklatıp **oluşturma**. Merhaba veri fabrikası oluşturulduktan sonra hello **yeni Data Factory** iletişim kutusunu kapatır ve hello bkz **seçin Data Factory** iletişim kutusu.

    Bir veya daha fazla data factory'leri zaten hello Azure aboneliği varsa hello bkz **seçin Data Factory** iletişim kutusu. Bu iletişim kutusunda, mevcut bir veri fabrikasını seçin veya tıklatın **oluştur yeni data factory** toocreate yeni bir tane.

    ![Veri Fabrikası yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. Merhaba, **seçin Data Factory** iletişim kutusu, hello **veri yükleme** seçeneği, varsayılan olarak seçilidir. Tıklatın **sonraki** toostart veri görev yükleme oluşturma.

## <a name="configure-hello-data-factory-properties"></a>Merhaba veri fabrikası özelliklerini yapılandırın
Veri Fabrikası oluşturduğunuza göre hello sonraki adıma Zamanlama yüklenirken tooconfigure hello verilerdir.

1. İçin **görev adı**, girin **DWLoadData fromSQLServer**.
2. Merhaba varsayılan kullanmak **kez Şimdi Çalıştır** seçeneği, tıklatın **sonraki**.

    ![Yükleme zamanlamasını yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Merhaba kaynak veri deposu ve ağ geçidi yapılandırma
Şimdi veri fabrikası hello şirket içi SQL Server veritabanı tooload veri istediğiniz hakkında söyleyin.

1. Seçin **SQL Server** desteklenen hello kaynak verilerinden katalog depolamak ve tıklatın **sonraki**.

    ![SQL Server kaynak seçin](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **belirt hello şirket içi SQL Server veritabanı** iletişim kutusu görüntülenir. ilk hello **bağlantı adı** doldurulmuş otomatik bir alandır. Merhaba ikinci alan ister hello hello adını **ağ geçidi**. Bir ağ geçidi zaten mevcut bir veri fabrikasını kullanıyorsanız, hello aşağı açılan listeden seçerek hello ağ geçidi yeniden kullanabilirsiniz. Merhaba tıklatın **ağ geçidi Oluştur** toocreate veri yönetimi ağ geçidi bağlantı.  

    > [!NOTE]
    > Merhaba kaynak veri deposu, şirket içi veya bir Azure Iaas sanal makinesi veri yönetimi ağ geçidi gereklidir. Bir ağ geçidi, veri fabrikası bir 1-1 ilişkisi yok. Başka bir veri fabrikası'ndan kullanılamaz, ancak birden çok veri hello görevlerle yükleme tarafından kullanılabilir aynı veri fabrikası. Bir ağ geçidi, veri görevleri yükleme çalıştırırken kullanılan tooconnect toomultiple veri depolarına olabilir.
    >
    > Merhaba ağ geçidi hakkında ayrıntılı bilgi için bkz: [veri yönetimi ağ geçidi](../data-factory/data-factory-data-management-gateway.md) makalesi.

3. A **ağ geçidi Oluştur** iletişim kutusu görüntülenir. Adı **GatewayForDWLoading**, tıklatıp **oluşturma**.

4. A **yapılandırma ağ geçidi** iletişim kutusu görüntülenir. Tıklatın **başlatma hızlı kurulum bu bilgisayarda** tooautomatically indirme, yükleme ve veri yönetimi ağ geçidi geçerli makinenize kaydedin. Merhaba ilerleme açılır pencerede gösterilir. Merhaba makine toohello veri deposuna bağlanamazsa, el ile denetleyebilirsiniz [hello ağ geçidi yükleyip](https://www.microsoft.com/download/details.aspx?id=39717) toohello veri bağlanabilir bir makinede depolayın ve sonra hello anahtar tooregister kullanın.
    > [!NOTE]
    > Merhaba hızlı kurulumu, Microsoft Edge ve Internet Explorer ile yerel olarak çalışır. İlk Google Chrome kullanıyorsanız, hello ClickOnce uzantı Chrome web Mağazası'ndan yükleyin.

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Merhaba ağ geçidi Kurulum toocomplete bekleyin. Merhaba ağ geçidi başarıyla kaydedildi ve çevrimiçi sonra hello açılır penceresi kapanır ve hello yeni ağ geçidi hello ağ geçidi alanında görünür. Ardından hello rest doldurun gibi gerekli alanları, ardından **sonraki**.
    - **Sunucu adı**: hello adını şirket içi SQL Server.
    - **Veritabanı adı**: SQL Server veritabanı.
    - **Kimlik bilgisi şifreleme**: "web tarayıcısı tarafından" Merhaba varsayılan kullanın.
    - **Kimlik doğrulama türü**: hello kullanmakta olduğunuz kimlik doğrulama türünü seçin.
    - **Kullanıcı adı** ve **parola**: izni toocopy hello veri sahip bir kullanıcı için hello kullanıcı adını ve parolasını girin.

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Merhaba sonraki toochoose hello toocopy hello veri tablolarından adımdır. Anahtar sözcükler kullanarak hello tabloları filtre uygulayabilirsiniz. Ve hello veri ve tablo şeması hello alt panelinde önizleyebilirsiniz. Seçiminiz tamamladıktan sonra tıklatın **sonraki**.

    ![Tabloları seçme](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Merhaba hedef, SQL veri ambarı yapılandırma

Şimdi veri fabrikası hello hedef bilgilerini söyleyin.

1. SQL veri ambarı bağlantı bilgilerini otomatik olarak doldurulur. Merhaba parola hello kullanıcı adını girin. tıklatıp **sonraki**.

    ![Hedef yapılandırma](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Bir akıllı tablo eşlemesi kaynak toodestination tabloları Tablo adlarına göre eşleştiren görüntülenir. Merhaba tablo hello hedef mevcut değilse, varsayılan olarak ADF hello biriyle oluşturur (bu geçerlidir tooSQL sunucu ya da kaynak olarak Azure SQL veritabanı) aynı adı. Toomap tooan var olan tablo de seçebilirsiniz. Gözden geçirin ve tıklatın **sonraki**.

    ![Eşleme tabloları](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Merhaba şema eşleme gözden geçirin ve hata veya uyarı iletilerini arayın. Akıllı Eşleme sütun adını temel alır. Desteklenmeyen veri türü dönüştürme hello kaynak ve hedef sütun arasında ise hello ilgili tablo yanında bir hata iletisine bakın. Toolet Data Factory otomatik seçerseniz hello tabloları oluşturmak, kaynak ve hedef depoları arasında toofix hello uyumsuzluk gerekirse uygun veri türü dönüşümü oluşabilir.

    ![Şema eşleme](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. **İleri**’ye tıklayın.

## <a name="configure-hello-performance-settings"></a>Merhaba performans ayarlarını yapılandırma
SQL Data Warehouse performantly kullanarak içine yüklenmeden önce hello verileri hazırlamak için kullanılan bir Azure depolama hesabı yapılandırma Hello performans yapılandırmalarında [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Başlangıç kopyası yapıldıktan sonra depolama birimindeki hello geçici verileri otomatik olarak temizlenecek.

Mevcut bir Azure depolama hesabını seçin ve tıklayın **sonraki**.

![Hazırlama blob yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Özet bilgileri gözden geçirin ve hello ardışık düzen dağıtın

Merhaba yapılandırmasını gözden geçirin ve tıklatın **son** düğmesini toodeploy hello ardışık düzen.

![Veri Fabrikası dağıtma](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Yükleme ilerlemesini izleme verileri

Merhaba dağıtımının ilerleme durumunu ve hello sonuçlarında görebilirsiniz **dağıtım** sayfası.

1. Merhaba dağıtımı yapıldıktan sonra diyor hello bağlantısına tıklayın **toomonitor kopyalama işlem hattını burayı** toomonitor veri yükleme ilerleme durumu.

    ![İşlem hattını izleme](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Yeni oluşturulan hello **DWLoadData fromSQLServer** veri yükleme ardışık olan hello sol seçili otomatik **kaynak Gezgini**.

    ![Görünüm ardışık düzen](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Merhaba ortasında hello ardışık düzen'yi tıklatın paneli toosee hello için ayrıntılı durum tooan etkinlik eşlemeleri her bir tablo.

    ![Tablo etkinliği görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Daha fazla etkinliğin içinde tıklatın ve hello veri hello sağ panelde veri boyutu, satır, işleme, vb. dahil olmak üzere ayrıntıları yükleme bakın.

    ![Tablo Etkinlik ayrıntıları görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. Bu izleme görünümü daha sonra Git tooyour SQL Data Warehouse, toolaunch tıklatın **veri yükleme > Azure Data Factory**, fabrikanızı seçin ve **izleme görevleri yüklenirken varolan**.

## <a name="next-steps"></a>Sonraki adımlar

Veri ambarı, veritabanı tooSQL toomigrate bkz [geçişine genel bakış](sql-data-warehouse-overview-migrate.md).

Azure Data Factory ve kendi veri taşıma özellikleri hakkında daha fazla toolearn makaleler hello bakın:

- [Giriş tooAzure veri fabrikası](../data-factory/data-factory-introduction.md)
- [Kopyalama etkinliği kullanarak veri taşıma](../data-factory/data-factory-data-movement-activities.md)
- [Azure Data Factory kullanarak Azure SQL veri ambarından veri tooand taşıma](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

SQL Data Warehouse verilerinizi tooexplore bkz hello makaleler:

- [Visual Studio ve SSDT ile tooSQL veri ambarına bağlanma](sql-data-warehouse-query-visual-studio.md)
- [Görsel verilerinizi Power BI ile](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[Azure portal]: https://portal.azure.com
