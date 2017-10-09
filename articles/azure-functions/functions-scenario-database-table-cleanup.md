---
title: "aaaUse Azure işlevleri tooperform bir veritabanı temizleme görevi | Microsoft Docs"
description: "Kullanım Azure işlevleri tooschedule tooAzure SQL veritabanı tooperiodically bağlayan görev satırları temizleyin."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Azure işlevleri tooconnect tooan Azure SQL veritabanını kullan
Bu konu, nasıl toouse Azure işlevleri toocreate zamanlanmış bir işi, gösterir. bir Azure SQL veritabanı tablosunda satır temizler. Merhaba yeni C# işlevi hello Azure portalı önceden tanımlanmış Zamanlayıcı tetikleyicisi şablonda temel alınarak oluşturulur. toosupport bu senaryo ayrıca bir veritabanı bağlantı dizesi hello işlevi uygulama ayarı olarak ayarlamanız gerekir. Bu senaryo, bir toplu işlemin hello veritabanında kullanır. toohave, işlev işlem tek tek CRUD işlemleri Mobile Apps tablodaki, bunun yerine kullanmanız gerekir [Mobile Apps bağlamaları](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Ön koşullar

+ Bu konuda bir zamanlayıcı tetiklenen işlevini kullanır. Tam hello hello konudaki adımları [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md) bu işlev toocreate C# sürümü.   

+ Bu konuda hello toplu temizleme işlemi yürüten bir Transact-SQL komutu gösterilir **SalesOrderHeader** hello AdventureWorksLT örnek veritabanı tablosunda. toocreate hello AdventureWorksLT örnek veritabanı tam hello hello konudaki adımları [hello Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma

Tamamlandığında, oluşturulan hello veritabanı için tooget hello bağlantı dizesi gerekiyor [hello Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
 
3. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello seçip **SQL veritabanları** sayfası.

4. Seçin **veritabanı bağlantı dizelerini Göster** ve kopyalama hello tam **ADO.NET** bağlantı dizesi.

    ![Merhaba ADO.NET bağlantı dizesini kopyalayın.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Merhaba bağlantı dizesini ayarlayın 

Merhaba azure'da işlevlerinizin yürütülmesini bir işlev uygulaması barındırır. Bu en iyi yöntem toostore bağlantı dizeleri ve diğer parolaları işlevi uygulama ayarlarınızda olur. Uygulama ayarları kullanarak kodunuzu hello bağlantı dizesiyle yanlışlıkla açıklanması engeller. 

1. Oluşturduğunuz tooyour işlevi uygulamasına gidin [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md).

2. Seçin **Platform özellikleri** > **uygulama ayarları**.
   
    ![Merhaba işlev uygulaması için uygulama ayarları.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Çok ilerleyin**bağlantı dizeleri** ve hello tabloda belirtildiği gibi hello ayarları kullanarak bir bağlantı dizesi ekleyin.
   
    ![Bir bağlantı dizesi toohello işlevi uygulama ayarları ekleyin.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Ayar       | Önerilen değer | Açıklama             | 
    | ------------ | ------------------ | --------------------- | 
    | **Ad**  |  sqldb_connection  | Kullanılan tooaccess hello işlevi kodunuzdaki bağlantı dizesi depolanır.    |
    | **Değer** | Kopyalanan dize  | Merhaba bağlantı dizesi hello önceki bölümde kopyalanır. |
    | **Tür** | SQL Database | Merhaba varsayılan SQL veritabanı bağlantısı kullanın. |   

3. **Kaydet** düğmesine tıklayın.

Şimdi, tooyour SQL veritabanına bağlanan hello C# kod işlevi ekleyebilirsiniz.

## <a name="update-your-function-code"></a>İşlev kodunuzu güncelleştirin

1. İşlev uygulamanızda hello Zamanlayıcı tetiklenen işlevi seçin.
 
3. Derleme başvurularını hello varolan işlev kodu hello üstündeki aşağıdaki hello ekleyin:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Merhaba aşağıdakileri ekleyin `using` deyimleri toohello işlevi:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Merhaba varolan **çalıştırmak** koddan hello işleviyle:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Bu örnek komut hello güncelleştirir **durum** sütun temel hello sevk tarihi. Veri 32 satırı güncelleştirmeniz gerekir.

5. Tıklatın **kaydetmek**, izleme hello **günlükleri** windows hello için sonraki işlev yürütme sonra Not hello hello güncelleştirilen satır sayısı **SalesOrderHeader** tablo.

    ![Merhaba işlevi günlüklerine bakın.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Sonraki adımlar

Ardından, bilgi toouse nasıl çalıştığını Logic Apps toointegrate diğer hizmetlerle birlikte.

> [!div class="nextstepaction"] 
> [Logic Apps ile tümleşen bir işlev oluşturun](functions-twitter-email.md)

Aşağıdaki konularda hello işlevleri hakkında daha fazla bilgi için bkz:

* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)  
  İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu
* [Azure İşlevlerini test etme](functions-test-a-function.md)  
  İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.  
