---
title: "aaaCreate tooAzure Hizmetleri bağlanan bir işlev | Microsoft Docs"
description: "Azure işlevleri toocreate tooother Azure bağlayan sunucusuz bir uygulama kullanın Hizmetleri."
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
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="703ec-104">Azure işlevleri toocreate tooother Azure bağlanan bir işlev kullanan hizmetler</span><span class="sxs-lookup"><span data-stu-id="703ec-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="703ec-105">Bu konu, nasıl Azure Storage bir tabloda toorows toocreate toomessages bir Azure depolama kuyruğu ve kopya hello üzerinde dinler Azure işlevleri işlevinde iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="703ec-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="703ec-106">Kullanılan tooload iletileri hello kuyruğuna tetiklenen Zamanlayıcı işlevdir.</span><span class="sxs-lookup"><span data-stu-id="703ec-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="703ec-107">İkinci bir işlev hello kuyruktaki iletileri okur ve iletileri toohello tablo yazar.</span><span class="sxs-lookup"><span data-stu-id="703ec-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="703ec-108">Merhaba kuyruk ve hello tablo sizin için Azure hello bağlama tanımları tabanlı işlevleri tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="703ec-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="703ec-109">toomake şeyleri daha ilginç, bir işlev JavaScript'te yazılmış ve hello diğer C# kodda yazılır.</span><span class="sxs-lookup"><span data-stu-id="703ec-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="703ec-110">Bu durum bir işlev uygulamasının nasıl çeşitli dillerde işlevleri olabileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="703ec-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="703ec-111">Bu senaryoyu [Kanal 9’daki bir videoda](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="703ec-112">Toohello sıra Yazar bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="703ec-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="703ec-113">Tooa depolama kuyruğu bağlanmadan önce toocreate hello ileti sırası yükleyen işlevi gerekir.</span><span class="sxs-lookup"><span data-stu-id="703ec-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="703ec-114">Bu JavaScript işlevi 10 saniyede bir ileti toohello sırası yazan Zamanlayıcı tetikleyicisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="703ec-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="703ec-115">Zaten bir Azure hesabınız yoksa, hello denetleyin [deneyin Azure işlevleri](https://functions.azure.com/try) deneyimi veya [ücretsiz Azure hesabınızı oluşturmak](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="703ec-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="703ec-116">Toohello Azure portalına gidin ve işlev uygulamanızı bulun.</span><span class="sxs-lookup"><span data-stu-id="703ec-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="703ec-117">**Yeni İşlev** > **TimerTrigger-JavaScript** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="703ec-118">Ad hello işlevi **FunctionsBindingsDemo1**, cron ifade değeri girin `0/10 * * * * *` için **zamanlama**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="703ec-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Zamanlayıcı ile tetiklenen işlev ekleme](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="703ec-120">10 saniyede bir çalışan zamanlayıcı tetiklemeli bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="703ec-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="703ec-121">Merhaba üzerinde **geliştirme** sekmesini tıklatın, **günlükleri** ve hello günlüğü'nde hello etkinlik görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="703ec-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="703ec-122">10 saniyede bir yazılmış bir günlük girişi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Görünüm hello günlük tooverify hello işlevi çalışır](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="703ec-124">İleti kuyruğu çıktı bağlaması ekleme</span><span class="sxs-lookup"><span data-stu-id="703ec-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="703ec-125">Merhaba üzerinde **tümleştir** sekmesinde, seçin **yeni çıktı** > **Azure kuyruk depolama** > **seçin**.</span><span class="sxs-lookup"><span data-stu-id="703ec-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Tetikleyici zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="703ec-127">Girin `myQueueItem` için **ileti parametre adı** ve `functions-bindings` için **sıra adı**, var olan seçin **depolama hesabı bağlantısı** veya tıklatın**yeni** bir depolama hesabı bağlantı ve ardından toocreate **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="703ec-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Merhaba çıkış bağlama toohello depolama kuyruğu oluşturma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="703ec-129">Merhaba edilene **geliştirme** sekmesinde, aşağıdaki kod toohello işlevi hello Ekle:</span><span class="sxs-lookup"><span data-stu-id="703ec-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="703ec-130">Merhaba bulun *varsa* deyimi yaklaşık hello işlevinin 9 satır ve INSERT hello aşağıdaki kod bu deyim sonra.</span><span class="sxs-lookup"><span data-stu-id="703ec-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="703ec-131">Bu kod oluşturur bir **myQueueItem** ve ayarlar kendi **zaman** özelliği toohello geçerli zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="703ec-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="703ec-132">Ardından hello yeni kuyruk öğesi toohello bağlamın ekler **myQueueItem** bağlama.</span><span class="sxs-lookup"><span data-stu-id="703ec-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="703ec-133">**Kaydet ve Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="703ec-134">Depolama Gezgini'ni kullanarak depolama güncelleştirmelerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="703ec-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="703ec-135">İşlevinizi oluşturduğunuz hello kuyrukta iletileri görüntüleyerek çalışıp çalışmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="703ec-136">Visual Studio'da bulut Gezgini'ni kullanarak tooyour depolama kuyruğu bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="703ec-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="703ec-137">Ancak, hello portal kolay tooconnect tooyour depolama hesabı Microsoft Azure Storage Gezgini kullanarak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="703ec-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="703ec-138">Merhaba, **tümleştir** sekmesini ve ardından sıranız bağlama çıktı > **belgelerine**, ardından depolama hesabınız için bağlantı dizesi hello Göster ve kopyalama hello değeri.</span><span class="sxs-lookup"><span data-stu-id="703ec-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="703ec-139">Bu değer tooconnect tooyour depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="703ec-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Azure Depolama Gezgini’ni İndir](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="703ec-141">Henüz yapmadıysanız [Microsoft Azure Depolama Gezgini](http://storageexplorer.com)’ni indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="703ec-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="703ec-142">Depolama Gezgini'nde hello tıklayın Bağlan tooAzure depolama simgesi, hello alanında hello bağlantı dizesini yapıştırın ve hello Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Depolama Gezgini ile bağlantı ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="703ec-144">Altında **yerel ve bağlı**, genişletin **depolama hesapları** > depolama hesabınız > **sıraları** > **işlevleri bağlamaları**ve iletileri toohello sıraya yazılan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Merhaba sıradaki iletiler görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="703ec-146">Merhaba sıra yok veya boş bırakılırsa, da büyük olasılıkla işlev bağlama veya kod ile ilgili bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="703ec-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="703ec-147">Merhaba kuyruktaki iletileri okur bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="703ec-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="703ec-148">Toohello sıraya eklenen iletileri sahip olduğunuza göre yazma hello kalıcı olarak tooan Azure depolama tablosu iletileri ve hello kuyruktaki iletileri okur başka bir işlev oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="703ec-149">**Yeni İşlev** > **QueueTrigger-CSharp** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="703ec-150">Ad hello işlevi `FunctionsBindingsDemo2`, girin **işlevleri bağlamaları** hello içinde **sıra adı** alan, mevcut bir depolama hesabını seçin veya oluşturun ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="703ec-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Çıkış kuyruğu zamanlayıcı işlevi ekleme](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="703ec-152">(İsteğe bağlı) Merhaba yeni işlev önce Depolama Gezgini hello yeni kuyruk görüntüleyerek çalıştığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="703ec-153">Ayrıca Visual Studio’daki Bulut Gezgini’ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="703ec-154">(İsteğe bağlı) Merhaba yenileme **işlevleri bağlamaları** sıraya ve öğeler hello sıradan kaldırıldı dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="703ec-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="703ec-155">Merhaba işlevi ilişkili toohello hello kaldırma oluşur **işlevleri bağlamaları** sıraya giriş tetikleyici ve hello işlevi hello sıra okuduğu.</span><span class="sxs-lookup"><span data-stu-id="703ec-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="703ec-156">Tablo çıktı bağlaması ekleme</span><span class="sxs-lookup"><span data-stu-id="703ec-156">Add a table output binding</span></span>

1. <span data-ttu-id="703ec-157">FunctionsBindingsDemo2 içinde **Tümleştir** > **Yeni Çıkış** > **Azure Tablo Depolama** > **Seç** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Bağlama tooan Azure Storage tablo ekleme](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="703ec-159">**Tablo adı** için `functionbindings` ve **Tablo parametre adı** için `myTable` girin, bir **Depolama hesabı bağlantısı** seçin ya da yeni bir tane oluşturun ve ardından **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Merhaba depolama tablo bağlaması yapılandırma](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="703ec-161">Merhaba, **geliştirme** sekmesinde, hello varolan işlev kodu hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="703ec-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
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
        
        // Add hello item toohello table binding collection.
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
    <span data-ttu-id="703ec-162">Merhaba **Tableıtem** sınıfı hello depolama tablosunda bir satırı temsil eder ve hello öğesi toohello ekleyin `myTable` koleksiyonu **Tableıtem** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="703ec-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="703ec-163">Merhaba ayarlamalısınız **PartitionKey** ve **RowKey** özellikleri toobe mümkün tooinsert hello tabloya.</span><span class="sxs-lookup"><span data-stu-id="703ec-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="703ec-164">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-164">Click **Save**.</span></span>  <span data-ttu-id="703ec-165">Son olarak, Depolama Gezgini veya Visual Studio Cloud Explorer hello tablo görüntüleyerek hello işlevi works doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="703ec-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="703ec-166">(İsteğe bağlı) Depolama Gezgini'nde, depolama hesabınızı içinde **tabloları** > **functionsbindings** ve satır toohello tablo eklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="703ec-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="703ec-167">Yapabileceğiniz aynı Visual Studio Cloud Explorer'da hello.</span><span class="sxs-lookup"><span data-stu-id="703ec-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Merhaba tablosundaki satırları görünümü](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="703ec-169">Merhaba tablo yok veya boş bırakılırsa, da büyük olasılıkla işlev bağlama veya kod ile ilgili bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="703ec-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="703ec-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="703ec-170">Next steps</span></span>
<span data-ttu-id="703ec-171">Azure işlevleri hakkında daha fazla bilgi için aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="703ec-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="703ec-172">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="703ec-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="703ec-173">İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için programcı başvurusu</span><span class="sxs-lookup"><span data-stu-id="703ec-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="703ec-174">Azure İşlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="703ec-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="703ec-175">İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="703ec-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="703ec-176">Nasıl tooscale Azure işlevleri</span><span class="sxs-lookup"><span data-stu-id="703ec-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="703ec-177">Merhaba tüketim barındırma planı ve nasıl toochoose hello doğru planın dahil olmak üzere Azure işlevlerinde kullanılabilen hizmet planlarını açıklanır.</span><span class="sxs-lookup"><span data-stu-id="703ec-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

