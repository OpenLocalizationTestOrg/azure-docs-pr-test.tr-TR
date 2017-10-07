---
title: "Blob Storage tooSQL veritabanı - Azure aaaCopy verilerden | Microsoft Docs"
description: "Bu öğretici nasıl toouse bir Azure Data Factory kopyalama etkinliği kanal Blob Depolama tooSQL veritabanındaki toocopy verileri gösterir."
keywords: BLOB sql, blob depolama, veri kopyalama
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Öğretici: Data Factory kullanarak veritabanı Blob Storage tooSQL veri kopyalama
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Bu öğreticide, Blob Depolama tooSQL veritabanından bir ardışık düzen toocopy verilerle bir veri fabrikası oluşturun.

Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir. Bu etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir. Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.  

> [!NOTE]
> Merhaba hello Data Factory hizmetinin ayrıntılı bir genel bakış için bkz [giriş tooAzure Data Factory](data-factory-introduction.md) makalesi.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Başlangıç öğreticisi için Önkoşullar
Bu öğreticiye başlamadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:

* **Azure aboneliği**.  Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Merhaba bkz [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) Ayrıntılar için makale.
* **Azure depolama hesabı**. Merhaba blob depolama alanı olarak kullandığınız bir **kaynak** verileri depolamak Bu öğreticide. bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.
* **Azure SQL veritabanı**. Bir Azure SQL veritabanı olarak kullandığınız bir **hedef** verileri depolamak Bu öğreticide. Merhaba öğretici, bkz: kullanabileceğiniz bir Azure SQL veritabanı yoksa [nasıl toocreate ve bir Azure SQL veritabanı yapılandırma](../sql-database/sql-database-get-started.md) toocreate biri.
* **SQL Server 2012/2014 veya Visual Studio 2013**. Merhaba veritabanında SQL Server Management Studio veya Visual Studio toocreate bir örnek veritabanı ve tooview hello sonuç verileri kullanın.  

## <a name="collect-blob-storage-account-name-and-key"></a>BLOB Depolama hesabı adı ve anahtar Topla
Merhaba hesap adını ve hesap anahtarını, Azure depolama hesabı toodo Bu öğretici gerekir. Aşağı Not **hesap adı** ve **hesap anahtarı** Azure depolama hesabınız için.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **daha fazla hizmet** sol menü ve select hello üzerinde **depolama hesapları**.

    ![Gözat - depolama hesapları](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. Merhaba, **depolama hesapları** dikey penceresinde, select hello **Azure depolama hesabı** Bu öğreticide toouse istiyor.
4. Seçin **erişim anahtarları** altında bağlantı **ayarları**.
5. Tıklatın **kopya** (görüntü) sonraki çok düğmesini**depolama hesabı adı** metin kutusuna ve kaydetme/bunu herhangi bir yerde Yapıştır (örneğin: bir metin dosyasındaki).
6. Merhaba önceki adım toocopy veya hello Not yineleyin **key1**.

    ![Depolama erişim tuşu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Tüm hello dikey tıklayarak kapatın **X**.

## <a name="collect-sql-server-database-user-names"></a>SQL server, veritabanı, kullanıcı adları Topla
Bu öğreticide Azure SQL server, veritabanı ve kullanıcı toodo hello adlarını gerekir. Adlarını Not **server**, **veritabanı**, ve **kullanıcı** Azure SQL veritabanı.

1. Merhaba, **Azure portal**, tıklatın **daha fazla hizmet** hello seçin ve sol üzerinde **SQL veritabanları**.
2. Merhaba, **SQL veritabanları dikey**seçin hello **veritabanı** Bu öğreticide toouse istiyor. Merhaba Not **veritabanı adı**.  
3. Merhaba, **SQL veritabanı** dikey penceresinde tıklatın **özellikleri** altında **ayarları**.
4. Merhaba değerlerini Not **sunucu adı** ve **Sunucu Yöneticisi oturum açma**.
5. Tüm hello dikey tıklayarak kapatın **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Azure Hizmetleri tooaccess SQL server izin ver
Emin **tooAzure Hizmetleri erişimine izin** açık ayarı **ON** bu hello Data Factory hizmeti Azure SQL sunucunuza erişebilmesi için Azure SQL sunucunuzun. tooverify ve bu ayarı etkinleştirin adımları izleyerek hello:

1. Tıklatın **daha fazla hizmet** hello solda ve tıklatın hub **SQL sunucuları**.
2. Sunucunuzu seçin ve tıklayın **Güvenlik Duvarı** altında **ayarları**.
3. Merhaba, **Güvenlik Duvarı ayarları** dikey penceresinde tıklatın **ON** için **tooAzure Hizmetleri erişimine izin**.
4. Tüm hello dikey tıklayarak kapatın **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>BLOB Storage ve SQL veritabanı hazırlayın
Şimdi, Azure blob depolama ve Azure SQL veritabanı için başlangıç Öğreticisi hello aşağıdaki adımları gerçekleştirerek hazırlayın:  

1. Not Defteri'ni başlatın. Metin aşağıdaki hello kopyalayın ve olarak kaydedin **emp.txt** çok**C:\ADFGetStarted** sabit diskinizde klasör.

    ```
    John, Doe
    Jane, Doe
    ```
2. Gibi araçlar kullanın [Azure Storage Gezgini](http://storageexplorer.com/) toocreate hello **adftutorial** kapsayıcı ve tooupload hello **emp.txt** dosya toohello kapsayıcısı.

    ![Azure Storage Gezgini. Blob Depolama tooSQL veritabanından veri kopyalama](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Aşağıdaki SQL komut dosyası toocreate hello kullan hello **emp** Azure SQL veritabanı tablosunda.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **SQL Server 2012/2014 bilgisayarınızda yüklü olup olmadığını:** makalesindeki yönergeleri izleyin [Azure SQL SQL Server Management Studio'yu kullanarak veritabanı yönetme](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server ve Çalıştır hello SQL komut dosyası. Bu makalede hello kullanan [Klasik Azure portalı](http://manage.windowsazure.com), değil hello [yeni Azure portalına](https://portal.azure.com), bir Azure SQL server için Güvenlik Duvarı'nı tooconfigure.

    İstemci tooaccess hello Azure SQL server izin verilmiyorsa tooconfigure Güvenlik Duvarı'nı makinenizden (IP adresi), Azure SQL sunucusu tooallow erişimi için gerekir. Bkz: [bu makalede](../sql-database/sql-database-configure-firewall-settings.md) adımları tooconfigure hello Azure SQL server için Güvenlik Duvarı için.

## <a name="create-a-data-factory"></a>Veri fabrikası oluşturma
Merhaba Önkoşullar tamamladınız. Aşağıdaki şekilde hello birini kullanarak bir veri fabrikası oluşturabilirsiniz. Merhaba üst veya bağlantılar tooperform hello öğreticiyi izleyerek hello hello aşağı açılan listesinde hello seçeneklerden birini tıklatın.     

* [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
* [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Giriş verisi tooproduce çıktı verilerini dönüştürmez. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tootransform verilerinizi yapı](data-factory-build-your-first-pipeline.md).
> 
> Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md). 
