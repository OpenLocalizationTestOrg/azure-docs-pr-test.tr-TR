---
title: "aaaGet başlatılan Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak tooa depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="97da0-103">Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="97da0-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="97da0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="97da0-104">Overview</span></span>

<span data-ttu-id="97da0-105">Azure kuyruk depolama uygulama bileşenleri arasında Mesajlaşma bulut sağlar.</span><span class="sxs-lookup"><span data-stu-id="97da0-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="97da0-106">Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır.</span><span class="sxs-lookup"><span data-stu-id="97da0-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="97da0-107">Merhaba bulutta, hello Masaüstü, bir şirket içi sunucu veya bir mobil cihaz çalıştırıp çalıştırmadığınızı uygulama bileşenleri arasında iletişim için zaman uyumsuz Mesajlaşma kuyruk depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="97da0-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="97da0-108">Kuyruk depolama ayrıca zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="97da0-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="97da0-109">Bu öğretici, nasıl Azure kuyruk depolama varlıklar kullanarak bazı genel senaryolar için toowrite ASP.NET kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="97da0-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="97da0-110">Bu senaryolar, bir Azure kuyruk oluşturma ve ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi genel görevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="97da0-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="97da0-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="97da0-111">Prerequisites</span></span>

* [<span data-ttu-id="97da0-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97da0-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="97da0-113">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="97da0-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="97da0-114">Bir MVC denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97da0-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="97da0-115">Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="97da0-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="97da0-117">Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="97da0-119">Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *QueuesController*seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="97da0-121">Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `QueuesController.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="97da0-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="97da0-122">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="97da0-122">Create a queue</span></span>

<span data-ttu-id="97da0-123">Merhaba aşağıdaki adımları göstermek nasıl toocreate bir sıra:</span><span class="sxs-lookup"><span data-stu-id="97da0-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="97da0-124">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-125">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="97da0-126">Adlı bir yöntem ekleyin **CreateQueue** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="97da0-127">Merhaba içinde **CreateQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-128">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="97da0-129">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="97da0-130">Alma bir **CloudQueue** başvuru toohello istenen sıra adını temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="97da0-131">Merhaba **CloudQueueClient.GetQueueReference** yöntemi kuyruk depolama doğrulamasını yapmaz.</span><span class="sxs-lookup"><span data-stu-id="97da0-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="97da0-132">Merhaba sıra var olup olmadığına bakılmaksızın hello başvuru döndürülür.</span><span class="sxs-lookup"><span data-stu-id="97da0-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-133">Merhaba çağrısı **CloudQueue.CreateIfNotExists** henüz yoksa, yöntem toocreate hello sırası.</span><span class="sxs-lookup"><span data-stu-id="97da0-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="97da0-134">Merhaba **CloudQueue.CreateIfNotExists** yöntemi döndürür **true** hello sıra yok ve başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="97da0-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="97da0-135">Aksi takdirde, **false** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="97da0-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="97da0-136">Güncelleştirme hello **ViewBag** hello sırasının hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="97da0-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="97da0-137">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-138">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateQueue** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-139">Açık `CreateQueue.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="97da0-140">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-141">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-142">Merhaba uygulamayı çalıştırın ve seçin **Oluşturma sırası** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Kuyruk oluşturma](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="97da0-144">Daha önce belirtildiği gibi hello **CloudQueue.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello sıra yok ve oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="97da0-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="97da0-145">Bu nedenle, hello sırası mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="97da0-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="97da0-146">toorun hello uygulama birden çok kez, hello sıra hello uygulama yeniden çalıştırmadan önce silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="97da0-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="97da0-147">Silme hello sıra hello yapılabilir **CloudQueue.Delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97da0-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="97da0-148">Merhaba sıra hello kullanarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="97da0-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="97da0-149">Bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="97da0-149">Add a message tooa queue</span></span>

<span data-ttu-id="97da0-150">Seçtiğiniz sonra [bir kuyruk oluşturan](#create-a-queue), iletileri toothat sırası ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97da0-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="97da0-151">Bu bölümde, bir ileti tooa sırası eklerken size yol gösterir *sınama sırası*.</span><span class="sxs-lookup"><span data-stu-id="97da0-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="97da0-152">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-153">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="97da0-154">Adlı bir yöntem ekleyin **AddMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97da0-155">Merhaba içinde **AddMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-156">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97da0-157">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="97da0-158">Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-159">Merhaba oluşturma **CloudQueueMessage** tooadd toohello sıra istediğiniz selamlama iletisine temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="97da0-160">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="97da0-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="97da0-161">Merhaba çağrısı **CloudQueue.AddMessage** yöntemi tooadd hello messaged toohello sırası.</span><span class="sxs-lookup"><span data-stu-id="97da0-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="97da0-162">Birkaç oluşturup **ViewBag** hello görünümünde görüntülenmesi için özellikler.</span><span class="sxs-lookup"><span data-stu-id="97da0-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="97da0-163">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-164">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddMessage** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-165">Açık `AddMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="97da0-166">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-167">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-168">Merhaba uygulamayı çalıştırın ve seçin **Ekle ileti** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Mesaj ekleyin.](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="97da0-170">iki bölüm - hello [kaldırmadan bir sıradan ileti okumak](#read-a-message-from-a-queue-without-removing-it) ve [ekleme ve kaldırma bir iletiyi bir kuyruktan okunur](#read-and-remove-a-message-from-a-queue) -nasıl tooread kuyruktan iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="97da0-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="97da0-171">Bir ileti kuyruktan kaldırmadan okuma</span><span class="sxs-lookup"><span data-stu-id="97da0-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="97da0-172">Bu bölümde anlatılacaktır nasıl toopeek sıraya alınmış bir iletiye (kaldırarak olmadan okuma hello ilk iletiyi).</span><span class="sxs-lookup"><span data-stu-id="97da0-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="97da0-173">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-174">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="97da0-175">Adlı bir yöntem ekleyin **PeekMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97da0-176">Merhaba içinde **PeekMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-177">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97da0-178">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="97da0-179">Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-180">Merhaba çağrısı **CloudQueue.PeekMessage** yöntemi tooread hello hello sıradan kaldırarak olmadan hello sıradaki ilk iletiyi.</span><span class="sxs-lookup"><span data-stu-id="97da0-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="97da0-181">Güncelleştirme hello **ViewBag** iki değerlerle: hello kuyruk adı ve okundu hello ileti.</span><span class="sxs-lookup"><span data-stu-id="97da0-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="97da0-182">Merhaba **CloudQueueMessage** nesne hello nesnenin değeri almak için iki özellik sunar: **CloudQueueMessage.AsBytes** ve **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="97da0-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="97da0-183">**AsString** (Bu örnekte kullanılan) bir dize döndürür sırada **AsBytes** bir bayt dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="97da0-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="97da0-184">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-185">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **PeekMessage** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-186">Açık `PeekMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="97da0-187">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-188">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-189">Merhaba uygulamayı çalıştırın ve seçin **gözlem ileti** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![İletiye Gözat](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="97da0-191">Okuma ve bir ileti kuyruktan kaldırma</span><span class="sxs-lookup"><span data-stu-id="97da0-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="97da0-192">Bu bölümde, bilgi nasıl tooread ve kuyruktan bir ileti kaldırın.</span><span class="sxs-lookup"><span data-stu-id="97da0-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="97da0-193">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-194">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="97da0-195">Adlı bir yöntem ekleyin **ReadMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97da0-196">Merhaba içinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-197">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97da0-198">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="97da0-199">Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-200">Merhaba çağrısı **CloudQueue.GetMessage** yöntemi tooread hello hello sıradaki ilk iletiyi.</span><span class="sxs-lookup"><span data-stu-id="97da0-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="97da0-201">Merhaba **CloudQueue.GetMessage** yöntemi yapar (varsayılan) 30 saniye tooany ileti görünmez başka bir kod değiştirmek veya selamlama iletisine, onu işlenirken silmek böylece iletileri okumak başka bir kod hello.</span><span class="sxs-lookup"><span data-stu-id="97da0-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="97da0-202">toochange hello zaman selamlama iletisine miktarıdır görünmez, hello Değiştir **visibilityTimeout** toohello geçirilen parametre **CloudQueue.GetMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97da0-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="97da0-203">Merhaba çağrısı **CloudQueueMessage.Delete** hello kuyruğundan yöntemi toodelete hello ileti.</span><span class="sxs-lookup"><span data-stu-id="97da0-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="97da0-204">Güncelleştirme hello **ViewBag** hello ileti silinmiş ile Merhaba hello sırasının adı.</span><span class="sxs-lookup"><span data-stu-id="97da0-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="97da0-205">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-206">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ReadMessage** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-207">Açık `ReadMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="97da0-208">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-209">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-210">Merhaba uygulamayı çalıştırın ve seçin **okuma/silme iletisi** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Okuma ve silme iletisi](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="97da0-212">Merhaba kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="97da0-212">Get hello queue length</span></span>

<span data-ttu-id="97da0-213">Bu bölümde, nasıl tooget hello sırası uzunluğu (ileti sayısını) gösterir.</span><span class="sxs-lookup"><span data-stu-id="97da0-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="97da0-214">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-215">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="97da0-216">Adlı bir yöntem ekleyin **GetQueueLength** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97da0-217">Merhaba içinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-218">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97da0-219">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="97da0-220">Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-221">Merhaba çağrısı **CloudQueue.FetchAttributes** yöntemi tooretrieve hello sıranın öznitelikleri (uzunluğu dahil).</span><span class="sxs-lookup"><span data-stu-id="97da0-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="97da0-222">Erişim hello **CloudQueue.ApproximateMessageCount** özelliği tooget hello sırasının uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="97da0-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="97da0-223">Güncelleştirme hello **ViewBag** hello kuyruk ve uzunluğu hello adı.</span><span class="sxs-lookup"><span data-stu-id="97da0-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="97da0-224">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-225">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetQueueLength** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-226">Açık `GetQueueLengthMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="97da0-227">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-228">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-229">Merhaba uygulamayı çalıştırın ve seçin **alma sırası uzunluğu** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Kuyruk uzunluğu alma](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="97da0-231">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="97da0-231">Delete a queue</span></span>
<span data-ttu-id="97da0-232">Bu bölümde anlatılacaktır nasıl toodelete bir sıra.</span><span class="sxs-lookup"><span data-stu-id="97da0-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="97da0-233">Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="97da0-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="97da0-234">Açık hello `QueuesController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="97da0-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="97da0-235">Adlı bir yöntem ekleyin **DeleteQueue** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="97da0-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="97da0-236">Merhaba içinde **DeleteQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97da0-237">Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)</span><span class="sxs-lookup"><span data-stu-id="97da0-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="97da0-238">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="97da0-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="97da0-239">Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97da0-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="97da0-240">Merhaba çağrısı **CloudQueue.Delete** hello tarafından temsil edilen yöntem toodelete hello sıra **CloudQueue** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="97da0-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="97da0-241">Güncelleştirme hello **ViewBag** hello kuyruk ve uzunluğu hello adı.</span><span class="sxs-lookup"><span data-stu-id="97da0-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="97da0-242">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="97da0-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="97da0-243">Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **DeleteQueue** hello Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="97da0-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="97da0-244">Açık `DeleteQueue.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97da0-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="97da0-245">Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="97da0-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="97da0-246">Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="97da0-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="97da0-247">Merhaba uygulamayı çalıştırın ve seçin **alma sırası uzunluğu** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:</span><span class="sxs-lookup"><span data-stu-id="97da0-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Kuyruğu silin](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="97da0-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97da0-249">Next steps</span></span>
<span data-ttu-id="97da0-250">Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="97da0-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="97da0-251">Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="97da0-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="97da0-252">Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="97da0-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
