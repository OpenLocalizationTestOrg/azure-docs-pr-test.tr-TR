---
title: "Azure hizmetlerine bağlanan işlev oluşturma | Microsoft Docs"
description: "Diğer Azure hizmetlerine bağlanan sunucusuz bir uygulama oluşturmak için Azure İşlevleri’ni kullanın."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="2fcce-104">Diğer Azure hizmetlerine bağlanan bir işlev oluşturmak için Azure İşlevleri’ni kullanma</span><span class="sxs-lookup"><span data-stu-id="2fcce-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="2fcce-105">Bu konu başlığında, bir Azure Depolama Kuyruğundaki iletileri dinleyen ve iletileri bir Azure Depolama tablosundaki satırlara kopyalayan Azure İşlevleri içinde işlev oluşturma hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="2fcce-106">İletilerin kuyruğa yüklenmesi için zamanlayıcı ile tetiklenen bir işlev kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2fcce-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="2fcce-107">İkinci bir işlev ise iletileri kuyruktan okuyarak tabloya yazar.</span><span class="sxs-lookup"><span data-stu-id="2fcce-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="2fcce-108">Hem kuyruk hem de tablo, bağlama tanımları temel alınarak Azure İşlevleri tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2fcce-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="2fcce-109">İşleri daha ilginç hale getirmek için, bir işlev JavaScript dilinde yazılırken diğer işlev C# kodunda yazılır.</span><span class="sxs-lookup"><span data-stu-id="2fcce-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="2fcce-110">Bu durum bir işlev uygulamasının nasıl çeşitli dillerde işlevleri olabileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="2fcce-111">Bu senaryoyu [Kanal 9’daki bir videoda](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="2fcce-112">Kuyruğa yazan bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fcce-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="2fcce-113">Bir depolama kuyruğuna bağlanabilmeniz için ileti kuyruğunu yükleyen bir işlev oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="2fcce-114">Bu JavaScript işlevi, 10 saniyede bir kuyruğa ileti yazan zamanlama tetikleyicisini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2fcce-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="2fcce-115">Azure hesabınız yoksa [Azure İşlevleri Deneme](https://functions.azure.com/try) deneyimini inceleyin veya [ücretsiz Azure hesabınızı oluşturun](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2fcce-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="2fcce-116">Azure portalına gidin ve işlev uygulamanızı bulun.</span><span class="sxs-lookup"><span data-stu-id="2fcce-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="2fcce-117">**Yeni İşlev** > **TimerTrigger-JavaScript** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="2fcce-118">İşlevi **FunctionsBindingsDemo1** olarak adlandırın, **Zamanlama** için cron değeri olarak `0/10 * * * * *` girin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Zamanlayıcı ile tetiklenen işlev ekleme](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="2fcce-120">10 saniyede bir çalışan zamanlayıcı tetiklemeli bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="2fcce-121">**Geliştir** sekmesinde **Günlükler**’e tıklayın ve günlükteki etkinliği görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="2fcce-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="2fcce-122">10 saniyede bir yazılmış bir günlük girişi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-122">You see a log entry written every 10 seconds.</span></span>
   
    ![İşlevin çalıştığını doğrulamak için günlüğü görüntüleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="2fcce-124">İleti kuyruğu çıktı bağlaması ekleme</span><span class="sxs-lookup"><span data-stu-id="2fcce-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="2fcce-125">**Tümleştir** sekmesinde **Yeni Çıktı** > **Azure Kuyruk Depolama** > **Seç** seçeneğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="2fcce-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Tetikleyici zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="2fcce-127">**İleti parametre adı** için `myQueueItem`, **Kuyruk adı** için `functions-bindings` girin, var olan bir **Depolama hesabı bağlantısı** seçin veya **yeni** seçeneğine tıklayarak bir depolama hesabı bağlantısı oluşturup **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Depolama kuyruğu için çıktı bağlama oluşturma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="2fcce-129">**Geliştir** sekmesine geri dönerek aşağıdaki kodu işleve ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2fcce-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="2fcce-130">İşlevin 9. satırına yakın bir yerde bulunan *if* deyimini bulun ve bu deyimin sonuna aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2fcce-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="2fcce-131">Bu kod bir **myQueueItem** oluşturur ve bu öğenin **zaman** özelliğini geçerli timeStamp olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2fcce-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="2fcce-132">Daha sonra yeni kuyruk, öğesini bağlamın **myQueueItem** bağlamasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="2fcce-133">**Kaydet ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="2fcce-134">Depolama Gezgini'ni kullanarak depolama güncelleştirmelerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="2fcce-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="2fcce-135">Oluşturduğunuz kuyruktaki iletileri görüntüleyerek, işlevinizin çalışıp çalışmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="2fcce-136">Visual Studio'daki Bulut Gezgini'ni kullanarak depolama kuyruğunuza bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="2fcce-137">Ancak, portal Microsoft Azure Depolama Gezgini’ni kullanarak depolama hesabınıza bağlanmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2fcce-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="2fcce-138">**Tümleştir** sekmesinde kuyruk çıktı bağlaması > **Belgeler**’e tıklayın, ardından depolama hesabınıza ait Bağlantı Dizesini gösterin ve değeri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="2fcce-139">Depolama hesabınıza bağlanmak için bu değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-139">You use this value to connect to your storage account.</span></span>

    ![Azure Depolama Gezgini’ni İndir](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="2fcce-141">Henüz yapmadıysanız [Microsoft Azure Depolama Gezgini](http://storageexplorer.com)’ni indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2fcce-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="2fcce-142">Depolama Gezgini'nde, Azure Depolama’ya bağlan simgesine tıklayın, bağlantı dizesini alana yapıştırın ve sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Depolama Gezgini ile bağlantı ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="2fcce-144">**Yerel ve bağlı** altındaki **Depolama Hesapları** > depolama hesabınız > **Kuyruklar** > **functions-bindings** öğesini genişletin ve iletilerin kuyruğa yazıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Kuyruktaki iletilerin görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="2fcce-146">Kuyruk yoksa veya boşsa, işlev bağlamanız veya kodunuz ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="2fcce-147">Kuyruktan okuyan bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fcce-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="2fcce-148">İletileriniz artık kuyruğa eklendiğine göre, kuyruktan iletileri okuyan ve bir Azure Depolama tablosuna kalıcı olarak yazan başka bir işlev oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="2fcce-149">**Yeni İşlev** > **QueueTrigger-CSharp** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="2fcce-150">İşlevi `FunctionsBindingsDemo2` olarak adlandırın, **Kuyruk adı** alanına **functions-bindings** girin, var olan bir depolama hesabı seçin ya da bir tane oluşturun ve sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Çıkış kuyruğu zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="2fcce-152">(İsteğe bağlı) Depolama Gezgini’nde önceki gibi yeni kuyruğu görüntüleyerek yeni işlevin çalıştığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="2fcce-153">Ayrıca Visual Studio’daki Bulut Gezgini’ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="2fcce-154">(İsteğe bağlı) **functions-bindings** kuyruğunu yenileyin ve öğelerin kuyruktan kaldırıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2fcce-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="2fcce-155">İşlev **functions-bindings** kuyruğuna bir giriş tetikleyicisi olarak bağlı olduğundan ve işlev kuyruğu okuduğundan kaldırma gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="2fcce-156">Tablo çıktı bağlaması ekleme</span><span class="sxs-lookup"><span data-stu-id="2fcce-156">Add a table output binding</span></span>

1. <span data-ttu-id="2fcce-157">FunctionsBindingsDemo2 içinde **Tümleştir** > **Yeni Çıkış** > **Azure Tablo Depolama** > **Seç** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Bir Azure Depolama tablosuna bağlama ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="2fcce-159">**Tablo adı** için `functionbindings` ve **Tablo parametre adı** için `myTable` girin, bir **Depolama hesabı bağlantısı** seçin ya da yeni bir tane oluşturun ve ardından **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Depolama tablo bağlamasını yapılandırma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="2fcce-161">**Geliştir** sekmesinde var olan işlev kodunu aşağıdakiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2fcce-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="2fcce-162">**TableItem** sınıfı, depolama sınıfındaki bir satırı temsil eder ve öğeyi **TableItem** nesnelerinin `myTable` koleksiyonuna eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="2fcce-163">**PartitionKey** ve **RowKey** özelliklerini tabloya eklemek için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="2fcce-164">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-164">Click **Save**.</span></span>  <span data-ttu-id="2fcce-165">Son olarak, Depolama gezginindeki tabloyu veya Visual Studio Bulut Gezgini'ni görüntüleyerek işlevin çalıştığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="2fcce-166">(İsteğe bağlı) Depolama Gezgini'ndeki depolama hesabınızda **Tablolar** > **functionsbindings** öğesini genişletin ve satırların tabloya eklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2fcce-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="2fcce-167">Aynı işlemi Visual Studio’daki Bulut Gezgini’nde de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fcce-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Tablodaki satırların görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="2fcce-169">Tablo yoksa veya boşsa, işlev bağlamanız veya kodunuz ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="2fcce-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="2fcce-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2fcce-170">Next steps</span></span>
<span data-ttu-id="2fcce-171">Azure İşlevleri hakkında daha fazla bilgi edinmek için, aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="2fcce-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="2fcce-172">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="2fcce-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="2fcce-173">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="2fcce-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="2fcce-174">Azure İşlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="2fcce-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="2fcce-175">İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fcce-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="2fcce-176">Azure İşlevlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2fcce-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="2fcce-177">Tüketim barındırma planı dahil olmak üzere, Azure İşlevlerinde kullanılabilen hizmet planlarını ve doğru planın nasıl seçileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fcce-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

