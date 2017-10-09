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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="a92ac-103">Azure işlevleri tooconnect tooan Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="a92ac-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="a92ac-104">Bu konu, nasıl toouse Azure işlevleri toocreate zamanlanmış bir işi, gösterir. bir Azure SQL veritabanı tablosunda satır temizler.</span><span class="sxs-lookup"><span data-stu-id="a92ac-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="a92ac-105">Merhaba yeni C# işlevi hello Azure portalı önceden tanımlanmış Zamanlayıcı tetikleyicisi şablonda temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a92ac-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="a92ac-106">toosupport bu senaryo ayrıca bir veritabanı bağlantı dizesi hello işlevi uygulama ayarı olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a92ac-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="a92ac-107">Bu senaryo, bir toplu işlemin hello veritabanında kullanır.</span><span class="sxs-lookup"><span data-stu-id="a92ac-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="a92ac-108">toohave, işlev işlem tek tek CRUD işlemleri Mobile Apps tablodaki, bunun yerine kullanmanız gerekir [Mobile Apps bağlamaları](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a92ac-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a92ac-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a92ac-109">Prerequisites</span></span>

+ <span data-ttu-id="a92ac-110">Bu konuda bir zamanlayıcı tetiklenen işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a92ac-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="a92ac-111">Tam hello hello konudaki adımları [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md) bu işlev toocreate C# sürümü.</span><span class="sxs-lookup"><span data-stu-id="a92ac-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="a92ac-112">Bu konuda hello toplu temizleme işlemi yürüten bir Transact-SQL komutu gösterilir **SalesOrderHeader** hello AdventureWorksLT örnek veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="a92ac-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="a92ac-113">toocreate hello AdventureWorksLT örnek veritabanı tam hello hello konudaki adımları [hello Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a92ac-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="a92ac-114">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="a92ac-114">Get connection information</span></span>

<span data-ttu-id="a92ac-115">Tamamlandığında, oluşturulan hello veritabanı için tooget hello bağlantı dizesi gerekiyor [hello Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a92ac-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="a92ac-116">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a92ac-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="a92ac-117">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello seçip **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a92ac-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="a92ac-118">Seçin **veritabanı bağlantı dizelerini Göster** ve kopyalama hello tam **ADO.NET** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="a92ac-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Merhaba ADO.NET bağlantı dizesini kopyalayın.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="a92ac-120">Merhaba bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a92ac-120">Set hello connection string</span></span> 

<span data-ttu-id="a92ac-121">Merhaba azure'da işlevlerinizin yürütülmesini bir işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="a92ac-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="a92ac-122">Bu en iyi yöntem toostore bağlantı dizeleri ve diğer parolaları işlevi uygulama ayarlarınızda olur.</span><span class="sxs-lookup"><span data-stu-id="a92ac-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="a92ac-123">Uygulama ayarları kullanarak kodunuzu hello bağlantı dizesiyle yanlışlıkla açıklanması engeller.</span><span class="sxs-lookup"><span data-stu-id="a92ac-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="a92ac-124">Oluşturduğunuz tooyour işlevi uygulamasına gidin [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="a92ac-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="a92ac-125">Seçin **Platform özellikleri** > **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a92ac-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Merhaba işlev uygulaması için uygulama ayarları.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="a92ac-127">Çok ilerleyin**bağlantı dizeleri** ve hello tabloda belirtildiği gibi hello ayarları kullanarak bir bağlantı dizesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a92ac-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Bir bağlantı dizesi toohello işlevi uygulama ayarları ekleyin.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="a92ac-129">Ayar</span><span class="sxs-lookup"><span data-stu-id="a92ac-129">Setting</span></span>       | <span data-ttu-id="a92ac-130">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="a92ac-130">Suggested value</span></span> | <span data-ttu-id="a92ac-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a92ac-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="a92ac-132">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a92ac-132">**Name**</span></span>  |  <span data-ttu-id="a92ac-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="a92ac-133">sqldb_connection</span></span>  | <span data-ttu-id="a92ac-134">Kullanılan tooaccess hello işlevi kodunuzdaki bağlantı dizesi depolanır.</span><span class="sxs-lookup"><span data-stu-id="a92ac-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="a92ac-135">**Değer**</span><span class="sxs-lookup"><span data-stu-id="a92ac-135">**Value**</span></span> | <span data-ttu-id="a92ac-136">Kopyalanan dize</span><span class="sxs-lookup"><span data-stu-id="a92ac-136">Copied string</span></span>  | <span data-ttu-id="a92ac-137">Merhaba bağlantı dizesi hello önceki bölümde kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="a92ac-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="a92ac-138">**Tür**</span><span class="sxs-lookup"><span data-stu-id="a92ac-138">**Type**</span></span> | <span data-ttu-id="a92ac-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a92ac-139">SQL Database</span></span> | <span data-ttu-id="a92ac-140">Merhaba varsayılan SQL veritabanı bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a92ac-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="a92ac-141">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a92ac-141">Click **Save**.</span></span>

<span data-ttu-id="a92ac-142">Şimdi, tooyour SQL veritabanına bağlanan hello C# kod işlevi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a92ac-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="a92ac-143">İşlev kodunuzu güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="a92ac-143">Update your function code</span></span>

1. <span data-ttu-id="a92ac-144">İşlev uygulamanızda hello Zamanlayıcı tetiklenen işlevi seçin.</span><span class="sxs-lookup"><span data-stu-id="a92ac-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="a92ac-145">Derleme başvurularını hello varolan işlev kodu hello üstündeki aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a92ac-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="a92ac-146">Merhaba aşağıdakileri ekleyin `using` deyimleri toohello işlevi:</span><span class="sxs-lookup"><span data-stu-id="a92ac-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="a92ac-147">Merhaba varolan **çalıştırmak** koddan hello işleviyle:</span><span class="sxs-lookup"><span data-stu-id="a92ac-147">Replace hello existing **Run** function with hello following code:</span></span>
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

    <span data-ttu-id="a92ac-148">Bu örnek komut hello güncelleştirir **durum** sütun temel hello sevk tarihi.</span><span class="sxs-lookup"><span data-stu-id="a92ac-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="a92ac-149">Veri 32 satırı güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a92ac-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="a92ac-150">Tıklatın **kaydetmek**, izleme hello **günlükleri** windows hello için sonraki işlev yürütme sonra Not hello hello güncelleştirilen satır sayısı **SalesOrderHeader** tablo.</span><span class="sxs-lookup"><span data-stu-id="a92ac-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Merhaba işlevi günlüklerine bakın.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="a92ac-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a92ac-152">Next steps</span></span>

<span data-ttu-id="a92ac-153">Ardından, bilgi toouse nasıl çalıştığını Logic Apps toointegrate diğer hizmetlerle birlikte.</span><span class="sxs-lookup"><span data-stu-id="a92ac-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a92ac-154">Logic Apps ile tümleşen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="a92ac-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="a92ac-155">Aşağıdaki konularda hello işlevleri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a92ac-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="a92ac-156">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="a92ac-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="a92ac-157">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="a92ac-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="a92ac-158">Azure İşlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="a92ac-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="a92ac-159">İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="a92ac-159">Describes various tools and techniques for testing your functions.</span></span>  
