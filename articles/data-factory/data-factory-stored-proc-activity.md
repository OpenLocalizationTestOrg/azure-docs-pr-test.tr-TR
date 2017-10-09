---
title: "aaaSQL sunucu saklı yordam etkinliği"
description: "Merhaba SQL Server saklı yordam etkinliği tooinvoke bir saklı yordam bir Azure SQL Database veya Azure SQL veri ambarı Data Factory işlem hattı nasıl kullanabileceğinizi öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>SQL Server saklı yordam etkinliği
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md) 
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

## <a name="overview"></a>Genel Bakış
Veri fabrikasında veri dönüştürme etkinlikleri kullanma [ardışık düzen](data-factory-create-pipelines.md) Öngörüler ve öngörü içine tootransform ve işlem ham verileri. Merhaba saklı yordam etkinliği, veri fabrikası destekleyen hello dönüştürme etkinlikleri biridir. Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve veri fabrikası'nda desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.

Kuruluşunuzdaki veya bir Azure sanal makinesini (VM) bir saklı yordam veri aşağıdaki hello birinde depolar hello saklı yordam etkinliği tooinvoke kullanabilirsiniz: 

- Azure SQL Database
- Azure SQL Veri Ambarı
- SQL Server veritabanı.  SQL Server kullanıyorsanız, veri yönetimi ağ geçidi üzerinde aynı ana veritabanı hello veya ayrı bir makineye erişim toohello veritabanı olan makine hello yükleyin. Veri Yönetimi ağ geçidi, veri bağlayan bir bileşen şirket içi/açma Azure VM bulut Hizmetleri ile güvenli ve yönetilen bir şekilde kaynakları ' dir. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) Ayrıntılar için makale.

> [!IMPORTANT]
> Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke hello kullanarak bir saklı yordam içinde **sqlWriterStoredProcedureName** özelliği. Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md). Bağlayıcı makaleler hello özelliği hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Kopyalama etkinliği kullanarak bir Azure SQL Data Warehouse'a veri kopyalama sırasında bir saklı yordam çağırma desteklenmiyor. Ancak SQL Data Warehouse hello saklı yordam etkinliği tooinvoke bir saklı yordam kullanabilirsiniz. 
>  
> Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kopyalama etkinliği tooinvoke bir saklı yordam tooread veri hello kullanarak hello kaynak veritabanından içinde  **sqlReaderStoredProcedureName** özelliği. Bağlayıcı makaleler hello daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


izlenecek yol kullandığı aşağıdaki hello ardışık düzen tooinvoke bir Azure SQL veritabanındaki bir saklı yordam içinde saklı yordam etkinliği hello. 

## <a name="walkthrough"></a>Kılavuz
### <a name="sample-table-and-stored-procedure"></a>Örnek tablo ve saklı yordam
1. Merhaba aşağıdaki oluşturma **tablo** SQL Server Management Studio veya tanımanız başka bir araç kullanarak, Azure SQL veritabanındaki. Merhaba datetimestamp hello tarih ve saat hello karşılık gelen kimliği oluşturulduğunda bir sütundur.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    Kimliği tanımlanan hello benzersiz ve hello datetimestamp sütun hello tarih ve saat hello karşılık gelen kimliği ne zaman oluşturulur.
    
    ![Örnek veriler](./media/data-factory-stored-proc-activity/sample-data.png)

    Bu örnekte, depolanan hello bir Azure SQL veritabanı'nda bir yordamdır. Merhaba yaklaşım Hello saklı yordamı bir Azure SQL Data Warehouse hem de SQL Server veritabanı varsa, benzer. SQL Server veritabanı için yüklemeniz gereken bir [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).
2. Merhaba aşağıdaki oluşturma **saklı yordamı** toohello içinde veri ekleyen **sampletable**.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Ad** ve **büyük/küçük harf** Merhaba parametre (Bu örnekte DateTime) hello ardışık düzen/JSON etkinliğinde belirtilen parametresi eşleşmelidir. İçinde saklı yordamı tanımı Merhaba, emin  **@**  hello parametresi için bir önek olarak kullanılır.

### <a name="create-a-data-factory"></a>Veri fabrikası oluşturma
1. Çok oturum[Azure portal](https://portal.azure.com/).
2. Tıklatın **yeni** hello sol menüsünde **Intelligence + analiz**, tıklatıp **Data Factory**.

    ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. Merhaba, **yeni data factory** dikey penceresinde girin **SProcDF** hello adı için. Azure Data Factory adları **genel benzersiz**. Sizin adınızla tooenable hello başarılı oluşturulmasını hello Fabrika hello veri fabrikasının tooprefix hello adı gerekir.

   ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Seçin, **Azure aboneliği**.
5. İçin **kaynak grubu**, aşağıdaki adımları hello birini yapın:
   1. Tıklatın **Yeni Oluştur** ve hello kaynak grubu için bir ad girin.
   2. Tıklatın **var olanı kullan** ve varolan bir kaynak grubu seçin.  
6. Select hello **konumu** hello veri fabrikası için.
7. Seçin **PIN toodashboard** böylece hello panosunda oturum sonraki açışınızda hello veri fabrikası görebilirsiniz.
8. Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.
9. Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal. Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.

   ![Data Factory giriş sayfası](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Bir Azure SQL bağlı hizmeti oluşturma
Merhaba veri fabrikası oluşturduktan sonra içeren hello sampletable tablo ve sp_sample depolanan yordamı, tooyour veri fabrikası Azure SQL veritabanınızı bağlanan Azure SQL bağlı hizmeti oluşturun.

1. Tıklatın **yazar ve dağıtma** hello üzerinde **Data Factory** dikey **SProcDF** toolaunch hello Data Factory Düzenleyici.
2. Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure SQL veritabanı**. Hizmeti hello Düzenleyicisi'nde hello Azure SQL oluşturmak için JSON betiği bağlı görmeniz gerekir.

   ![Yeni veri deposu](media/data-factory-stored-proc-activity/new-data-store.png)
3. Hello JSON betiği, aşağıdaki değişiklikler hello olun:

   1. Değiştir `<servername>` Azure SQL veritabanı sunucunuzun hello ada sahip.
   2. Değiştir `<databasename>` içinde oluşturduğunuz hello tablo ve hello hello veritabanıyla saklı yordamı.
   3. Değiştir `<username@servername>` hello kullanıcı erişimi toohello veritabanı olan bir hesap ile.
   4. Değiştir `<password>` hello hello kullanıcı hesabının parolasını ile.

      ![Yeni veri deposu](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda. Merhaba solda görüntülemek hello AzureSqlLinkedService hello ağacında gördüğünüzü onaylayın.

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Çıktı veri kümesi oluşturma
Merhaba saklı yordamı olsa bile bir çıkış veri kümesi için bir saklı yordam etkinliği herhangi bir veri üretmez belirtmeniz gerekir. Buna ait hello hello zamanlama hello etkinlik (ne sıklıkta hello etkinlik - saatlik çalıştırılır, günlük, vb.) sürücüleri veri kümesi çıkışını olmasıdır. Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor. Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello ardışık düzeninde. Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz. Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur. Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset** (gerçekten hello çıktısını tutmaz tooa tablo işaret eden bir veri kümesi saklı yordamı). Hello çalıştırmak için toospecify hello zamanlama depolanan yordam etkinliği yalnızca kukla bu veri kümesi kullanılır. 

1. Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello araç çubuğundan, **yeni veri kümesi**, tıklatıp **Azure SQL**. **Yeni veri kümesi** hello komut çubuğu ve select **Azure SQL**.

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/new-dataset.png)
2. JSON betiği toohello JSON Düzenleyicisi'nde aşağıdaki hello kopyalayıp yapıştırın.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy dataset Merhaba, tıklatın **dağıtma** hello komut çubuğunda. Merhaba dataset hello ağaç görünümünde gördüğünüzü onaylayın.

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>SqlServerStoredProcedure etkinliği ile işlem hattı oluşturma
Şimdi, saklı yordam etkinliği ile işlem hattı oluşturalım. 

Merhaba aşağıdaki özelliklere dikkat edin: 

- Merhaba **türü** özelliği çok ayarlanmış**SqlServerStoredProcedure**. 
- Merhaba **storedProcedureName** türü özellikleri ayarlanmış çok**sp_sample** (Merhaba adını saklı yordamı).
- Merhaba **storedProcedureParameters** bölüm adlı bir parametre içeren **saniyeyi tarih /**. Ad ve büyük/küçük harf hello parametresinin json'da hello adını ve büyük/küçük harf hello saklı yordamı tanımında hello parametresinin eşleşmelidir. Bir parametre için null başarılı olursa hello sözdizimini kullanın: `"param1": null` (tüm küçük harf).
 
1. Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello komut çubuğu ve tıklatın **yeni işlem hattı**.
2. JSON parçacığı aşağıdaki hello kopyalayıp yapıştırın:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello ardışık tıklatın **dağıtma** hello araç çubuğunda.  

### <a name="monitor-hello-pipeline"></a>Merhaba işlem hattını izleme
1. Tıklatın **X** tooclose Data Factory Düzenleyici dikey toonavigate toohello Data Factory dikey penceresine geri tıklatın ve **diyagramı**.

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. Merhaba, **diyagram görünümü**hello ardışık düzen özetini görmek ve kullanılan veri kümelerine Bu öğretici.

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. Merhaba dataset Hello diyagram görünümü, çift `sprocsampleout`. Merhaba dilimi hazır durumda bakın. Merhaba başlangıç zamanı ve bitiş saati başlangıç JSON öğesinden arasındaki her bir saat dilimi oluşturduğundan beş dilimler olmalıdır.

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. Bir dilim olduğunda **hazır** Çalıştır durumunda, bir `select * from sampletable` veri hello hello Azure SQL veritabanı tooverify sorgusu toohello tabloda hello saklı yordamı tarafından eklenir.

   ![Çıktı verileri](./media/data-factory-stored-proc-activity/output.png)

   Bkz: [hello işlem hattını izleme](data-factory-monitor-manage-pipelines.md) Azure Data Factory işlem hatlarını izleme hakkında ayrıntılı bilgi.  


## <a name="specify-an-input-dataset"></a>Bir giriş veri kümesi belirtin
Merhaba kılavuzda saklı yordam etkinliği herhangi bir giriş veri kümesi yok. Bir giriş veri kümesi belirtirseniz, girdi veri kümesi hello dilimin (hazır durumda) kullanılabilir hale gelene kadar hello saklı yordam etkinliği çalışmaz. Merhaba veri kümesi, dış bir veri kümesini olabilir (değil üretilen hello başka bir etkinliğin tarafından aynı ardışık düzen) ya da bir Yukarı Akış etkinliği (Bu etkinlik önce çalışır hello etkinliği) tarafından üretilen bir iç veri kümesi. Merhaba saklı yordam etkinliği için birden çok giriş veri kümesi belirtebilirsiniz. Bunu yaparsanız, yalnızca tüm hello girdi veri kümesi dilimleri (hazır durumda) kullanılabilir hello saklı yordam etkinliği çalıştırılır. Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz. Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır.

## <a name="chaining-with-other-activities"></a>Diğer etkinliklerle zincirleme
Toochain bu etkinliği olmayan bir Yukarı Akış etkinliği istiyorsanız, bu etkinliğin bir giriş olarak hello Yukarı Akış etkinliği hello çıktısını belirtin. Bunu yaptığınızda hello saklı yordam etkinliği hello Yukarı Akış etkinliği tamamlar ve hello çıkış veri kümesi hello Yukarı Akış etkinliği (hazır durumunda) kullanılabilir kadar çalışmaz. Birden çok Yukarı Akış etkinliği çıkış kümelerini hello saklı yordam etkinliği giriş veri kümeleri belirtebilirsiniz. Yalnızca tüm hello girdi veri kümesi dilimler kullanılabilir hello saklı yordam etkinliği bunu yaptığınızda çalıştırılır.  

Aşağıdaki örneğine hello hello hello Kopyala etkinliğinin çıkışıdır: hello girişidir OutputDataset saklı yordam etkinliği. Bu nedenle, hello saklı yordam etkinliği hello kopyalama etkinliği tamamlar ve hello OutputDataset dilim (hazır durumda) kullanılabilir oluncaya kadar çalışmaz. Birden çok giriş veri kümeleri belirtirseniz, tüm hello girdi veri kümesi dilimleri (hazır durumda) kullanılabilir oluncaya kadar hello saklı yordam etkinliği çalışmaz. Merhaba giriş veri kümeleri doğrudan parametreleri toohello saklı yordam etkinliği kullanılamaz. 

Etkinlikler zincirleme daha fazla bilgi için bkz: [bir ardışık düzende birden çok etkinlik](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

Benzer şekilde, toolink hello deposu yordam etkinliği ile **aşağı akış etkinlikleri** (Merhaba saklı yordam etkinliği tamamlandıktan sonra çalıştırılan hello etkinlikleri) belirtin hello çıkış veri kümesi hello saklı yordam etkinliği bir Merhaba ardışık düzen hello aşağı akış etkinliğinde giriş.

> [!IMPORTANT]
> Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke hello kullanarak bir saklı yordam içinde **sqlWriterStoredProcedureName** özelliği. Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md). Bağlayıcı makaleler hello hello özelliği hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kopyalama etkinliği tooinvoke bir saklı yordam tooread veri hello kullanarak hello kaynak veritabanından içinde  **sqlReaderStoredProcedureName** özelliği. Bağlayıcı makaleler hello daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>JSON biçimi
Bir saklı yordam etkinliği tanımlamak için hello JSON biçimi şöyledir:

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

Aşağıdaki tablonun hello bu JSON özelliklerini açıklamaktadır:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad | Merhaba etkinlik adı |Evet |
| açıklama |Hangi hello etkinliği için kullanılan açıklayan metin |Hayır |
| type | Ayarlanmalıdır: **SqlServerStoredProcedure** | Evet |
| Girişleri | İsteğe bağlı. Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır Merhaba depolanan yordam etkinliği toorun. Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz. Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır. |Hayır |
| Çıkışları | Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir. Çıktı veri kümesi belirtir hello **zamanlama** hello için saklı yordam etkinliği (saatlik, haftalık, aylık, vb.). <br/><br/>Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor. <br/><br/>Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello ardışık düzeninde. Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz. Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur. <br/><br/>Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset**, toospecify hello zamanlama hello çalıştırmak için depolanan yordam etkinliği yalnızca kullanılır. |Evet |
| storedProcedureName |Hello Azure SQL veritabanı veya çıktı tablosu kullanır hello hello bağlantılı hizmeti tarafından temsil edilen Azure SQL Data Warehouse veya SQL Server veritabanında depolanan hello yordamı Hello adını belirtin. |Evet |
| storedProcedureParameters |Saklı yordam parametreleri için değerleri belirtin. Toopass parametresi için null ihtiyacınız varsa, hello sözdizimini kullanın: "param1": null (tüm küçük harf). Bu özellik kullanma hakkında örnek toolearn aşağıdaki hello bakın. |Hayır |

## <a name="passing-a-static-value"></a>Statik değer geçirme
Şimdi, şimdi 'örnek belge' adlı bir statik değeri içeren hello tabloda 'Senaryo' adlı başka bir sütun eklemeyi göz önünde bulundurun.

![Örnek veri 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**Tablo:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**Saklı yordam:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Şimdi, hello geçirmek **senaryo** hello parametre ve hello değerinden saklı yordam etkinliği. Merhaba **typeProperties** hello parçacığını aşağıdaki hello örnek görülüyor önceki bölümde:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Data Factory veri kümesi:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Data Factory işlem hattı**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```