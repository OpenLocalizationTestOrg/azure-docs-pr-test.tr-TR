---
title: "Bir veritabanı temizleme görevini gerçekleştirmek için Azure işlevleri kullanın | Microsoft Docs"
description: "Azure işlevleri, düzenli aralıklarla satırları temizlemek için Azure SQL veritabanına bağlanan bir görev zamanlamak için kullanın."
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="5254c-103">Bir Azure SQL veritabanına bağlanmak için Azure işlevleri kullanın</span><span class="sxs-lookup"><span data-stu-id="5254c-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="5254c-104">Bu konu Azure işlevleri, bir Azure SQL veritabanındaki bir tablodaki satırların temizler zamanlanmış bir işi oluşturmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5254c-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="5254c-105">Yeni C# işlevi önceden tanımlanmış Zamanlayıcı tetikleyicisi şablonu Azure portalında temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5254c-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="5254c-106">Bu senaryoyu desteklemek için de bir işlev uygulaması ayarında olarak bir veritabanı bağlantı dizesi ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5254c-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="5254c-107">Bu senaryo, bir toplu işlemin veritabanında kullanır.</span><span class="sxs-lookup"><span data-stu-id="5254c-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="5254c-108">Mobile Apps tablodaki tek tek CRUD işlemlerini işlevinizi sağlamak için kullanmanız [Mobile Apps bağlamaları](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5254c-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5254c-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5254c-109">Prerequisites</span></span>

+ <span data-ttu-id="5254c-110">Bu konuda bir zamanlayıcı tetiklenen işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5254c-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="5254c-111">Konusundaki adımları tamamlamak [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md) bu işlev, C# sürümünü oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5254c-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="5254c-112">Bu konuda bir toplu temizleme işlemi yürüten bir Transact-SQL komutu gösterilir **SalesOrderHeader** AdventureWorksLT örnek veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="5254c-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="5254c-113">AdventureWorksLT örnek veritabanı oluşturmak için konusundaki adımları [Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5254c-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="5254c-114">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="5254c-114">Get connection information</span></span>

<span data-ttu-id="5254c-115">Tamamlandığında, oluşturulan veritabanı için bağlantı dizesini almak gereken [Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5254c-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="5254c-116">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5254c-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="5254c-117">Seçin **SQL veritabanları** sol taraftaki menüden ve veritabanınızı seçin **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5254c-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="5254c-118">Seçin **veritabanı bağlantı dizelerini Göster** ve tam kopyalayın **ADO.NET** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="5254c-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesini kopyalayın.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="5254c-120">Bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="5254c-120">Set the connection string</span></span> 

<span data-ttu-id="5254c-121">Azure'da işlevlerinizin yürütülmesini bir işlev uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="5254c-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="5254c-122">Bağlantı dizeleri ve diğer parolaları işlevi uygulama ayarlarınızı depolamak için en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="5254c-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="5254c-123">Uygulama ayarları kullanarak kodunuzu bağlantı dizesiyle yanlışlıkla açıklanması engeller.</span><span class="sxs-lookup"><span data-stu-id="5254c-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="5254c-124">Oluşturduğunuz işlevi uygulamanıza gidin [zamanlayıcısı tarafından tetiklenen Azure işlevi oluşturma](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="5254c-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="5254c-125">Seçin **Platform özellikleri** > **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5254c-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![İşlev uygulaması için uygulama ayarları.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="5254c-127">Ekranı aşağı kaydırarak **bağlantı dizeleri** ve tabloda belirtildiği gibi ayarları kullanarak bir bağlantı dizesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5254c-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Bir bağlantı dizesi işlevi uygulama ayarlarına ekleyin.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="5254c-129">Ayar</span><span class="sxs-lookup"><span data-stu-id="5254c-129">Setting</span></span>       | <span data-ttu-id="5254c-130">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="5254c-130">Suggested value</span></span> | <span data-ttu-id="5254c-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5254c-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="5254c-132">**Ad**</span><span class="sxs-lookup"><span data-stu-id="5254c-132">**Name**</span></span>  |  <span data-ttu-id="5254c-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="5254c-133">sqldb_connection</span></span>  | <span data-ttu-id="5254c-134">İşlev kodunuzu depolanan bağlantı dizesinde erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5254c-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="5254c-135">**Değer**</span><span class="sxs-lookup"><span data-stu-id="5254c-135">**Value**</span></span> | <span data-ttu-id="5254c-136">Kopyalanan dize</span><span class="sxs-lookup"><span data-stu-id="5254c-136">Copied string</span></span>  | <span data-ttu-id="5254c-137">Bağlantı dizesi önceki bölümde kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5254c-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="5254c-138">**Tür**</span><span class="sxs-lookup"><span data-stu-id="5254c-138">**Type**</span></span> | <span data-ttu-id="5254c-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="5254c-139">SQL Database</span></span> | <span data-ttu-id="5254c-140">Varsayılan SQL veritabanı bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5254c-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="5254c-141">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5254c-141">Click **Save**.</span></span>

<span data-ttu-id="5254c-142">Şimdi, SQL veritabanına bağlanan C# işlev kodu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5254c-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="5254c-143">İşlev kodunuzu güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="5254c-143">Update your function code</span></span>

1. <span data-ttu-id="5254c-144">İşlev uygulamanızda Zamanlayıcı tetiklenen işlevi seçin.</span><span class="sxs-lookup"><span data-stu-id="5254c-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="5254c-145">Varolan işlev kodu en üstte aşağıdaki derleme başvurularını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5254c-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="5254c-146">Aşağıdakileri ekleyin `using` deyimleri işlevi için:</span><span class="sxs-lookup"><span data-stu-id="5254c-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="5254c-147">Varolan **çalıştırmak** işlevi aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="5254c-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="5254c-148">Bu örnek komut güncelleştirir **durum** sütun temel sevk tarih.</span><span class="sxs-lookup"><span data-stu-id="5254c-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="5254c-149">Veri 32 satırı güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5254c-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="5254c-150">Tıklatın **kaydetmek**, izleme **günlükleri** sonraki windows işlev yürütme ve ardından güncelleştirilir satır sayısını Not **SalesOrderHeader** tablo.</span><span class="sxs-lookup"><span data-stu-id="5254c-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![İşlev günlüklerine bakın.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="5254c-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5254c-152">Next steps</span></span>

<span data-ttu-id="5254c-153">Ardından, işlevleri Logic Apps ile diğer hizmetleri ile tümleştirme için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5254c-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="5254c-154">Logic Apps ile tümleşen bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="5254c-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="5254c-155">İşlevler hakkında daha fazla bilgi için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="5254c-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="5254c-156">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="5254c-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="5254c-157">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="5254c-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="5254c-158">Azure İşlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="5254c-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="5254c-159">İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="5254c-159">Describes various tools and techniques for testing your functions.</span></span>  
