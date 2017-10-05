---
title: "Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama | Microsoft Docs"
description: "Visual Studio bağlantılı hizmetler kullanarak bir depolama hesabı bağlandıktan sonra Visual Studio'da ASP.NET projesinde Azure kuyruk depolama kullanarak nereden başlayacaksınız"
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
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="89e0a-103">Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="89e0a-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="89e0a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="89e0a-104">Overview</span></span>

<span data-ttu-id="89e0a-105">Azure kuyruk depolama uygulama bileşenleri arasında Mesajlaşma bulut sağlar.</span><span class="sxs-lookup"><span data-stu-id="89e0a-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="89e0a-106">Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır.</span><span class="sxs-lookup"><span data-stu-id="89e0a-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="89e0a-107">Kuyruk depolama bulutta, masaüstünde, şirket içi sunucuda veya mobil bir cihazda çalışan uygulama bileşenleri arasındaki iletişim için zaman uyumsuz mesajlaşma sunar.</span><span class="sxs-lookup"><span data-stu-id="89e0a-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="89e0a-108">Kuyruk depolama ayrıca zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="89e0a-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="89e0a-109">Bu öğretici Azure kuyruk depolama varlıkları kullanarak bazı genel senaryolar için ASP.NET kodunun nasıl yazılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="89e0a-110">Bu senaryolar, bir Azure kuyruk oluşturma ve ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi genel görevleri içerir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="89e0a-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89e0a-111">Prerequisites</span></span>

* [<span data-ttu-id="89e0a-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89e0a-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="89e0a-113">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="89e0a-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="89e0a-114">Bir MVC denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89e0a-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="89e0a-115">İçinde **Çözüm Gezgini**, sağ **denetleyicileri**ve bağlam menüsünden seçin **Ekle -> denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Bir ASP.NET MVC uygulamasına denetleyici ekleme](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="89e0a-117">Üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="89e0a-119">Üzerinde **denetleyici Ekle** iletişim kutusunda, denetleyici adı *QueuesController*seçip **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![MVC Denetleyici adı](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="89e0a-121">Aşağıdakileri ekleyin *kullanarak* yönergeleri `QueuesController.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="89e0a-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="89e0a-122">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="89e0a-122">Create a queue</span></span>

<span data-ttu-id="89e0a-123">Aşağıdaki adımlar bir sıranın nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="89e0a-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="89e0a-124">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-125">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="89e0a-126">Adlı bir yöntem ekleyin **CreateQueue** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="89e0a-127">İçinde **CreateQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-128">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="89e0a-129">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="89e0a-130">Alma bir **CloudQueue** istenen sıra adı için bir başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="89e0a-131">**CloudQueueClient.GetQueueReference** yöntemi kuyruk depolama doğrulamasını yapmaz.</span><span class="sxs-lookup"><span data-stu-id="89e0a-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="89e0a-132">Sıranın var olup olmadığına bakılmaksızın başvuru döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89e0a-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-133">Çağrı **CloudQueue.CreateIfNotExists** henüz yoksa, kuyruk oluşturmak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="89e0a-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="89e0a-134">**CloudQueue.CreateIfNotExists** yöntemi döndürür **true** sıranın var olmadığından ve başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="89e0a-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="89e0a-135">Aksi takdirde, **false** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="89e0a-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="89e0a-136">Güncelleştirme **ViewBag** sıra adı.</span><span class="sxs-lookup"><span data-stu-id="89e0a-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="89e0a-137">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-138">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateQueue** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-139">Açık `CreateQueue.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="89e0a-140">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-141">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-142">Uygulamayı çalıştırmak ve seçmek **Oluşturma sırası** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Kuyruk oluşturma](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="89e0a-144">Daha önce belirtildiği gibi **CloudQueue.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca sıranın yok ve oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="89e0a-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="89e0a-145">Bu nedenle, sıranın mevcut olduğunda uygulama çalıştırırsanız, yöntem döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="89e0a-146">Birden çok kez uygulamayı çalıştırmak için uygulamayı yeniden çalıştırmadan önce sıranın silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="89e0a-147">Aracılığıyla sıra silme yapılabilir **CloudQueue.Delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="89e0a-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="89e0a-148">Kuyruğu kullanarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="89e0a-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="89e0a-149">Kuyruğa bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="89e0a-149">Add a message to a queue</span></span>

<span data-ttu-id="89e0a-150">Seçtiğiniz sonra [bir kuyruk oluşturan](#create-a-queue), bu kuyruğa iletileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89e0a-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="89e0a-151">Bu bölümde, bir sıraya bir ileti eklerken size yol gösterir *sınama sırası*.</span><span class="sxs-lookup"><span data-stu-id="89e0a-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="89e0a-152">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-153">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="89e0a-154">Adlı bir yöntem ekleyin **AddMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="89e0a-155">İçinde **AddMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-156">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="89e0a-157">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="89e0a-158">Alma bir **CloudQueueContainer** sıranın başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-159">Oluşturma **CloudQueueMessage** sıraya eklemek istediğiniz iletiyi temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="89e0a-160">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="89e0a-161">Çağrı **CloudQueue.AddMessage** messaged sıraya eklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="89e0a-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="89e0a-162">Birkaç oluşturup **ViewBag** görünümü görüntülemek özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="89e0a-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="89e0a-163">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-164">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddMessage** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-165">Açık `AddMessage.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="89e0a-166">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-167">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-168">Uygulamayı çalıştırmak ve seçmek **Ekle ileti** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Mesaj ekleyin.](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="89e0a-170">İki bölüm - [kaldırmadan bir sıradan ileti okumak](#read-a-message-from-a-queue-without-removing-it) ve [ekleme ve kaldırma bir iletiyi bir kuyruktan okunur](#read-and-remove-a-message-from-a-queue) -kuyruktan iletileri okumak nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="89e0a-171">Bir ileti kuyruktan kaldırmadan okuma</span><span class="sxs-lookup"><span data-stu-id="89e0a-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="89e0a-172">Bu bölümde, (ilk iletiyi kaldırmadan okuma) kuyruğa alınan iletinin peek göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="89e0a-173">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-174">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="89e0a-175">Adlı bir yöntem ekleyin **PeekMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="89e0a-176">İçinde **PeekMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-177">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="89e0a-178">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="89e0a-179">Alma bir **CloudQueueContainer** sıranın başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-180">Çağrı **CloudQueue.PeekMessage** sıradaki ilk iletiyi sıradan kaldırarak olmadan okumak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="89e0a-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="89e0a-181">Güncelleştirme **ViewBag** iki değerlerle: kuyruk adı ve okundu ileti.</span><span class="sxs-lookup"><span data-stu-id="89e0a-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="89e0a-182">**CloudQueueMessage** nesne nesnenin değeri almak için iki özellik sunar: **CloudQueueMessage.AsBytes** ve **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="89e0a-183">**AsString** (Bu örnekte kullanılan) bir dize döndürür sırada **AsBytes** bir bayt dizisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="89e0a-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="89e0a-184">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-185">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **PeekMessage** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-186">Açık `PeekMessage.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="89e0a-187">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-188">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-189">Uygulamayı çalıştırmak ve seçmek **gözlem ileti** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![İletiye Gözat](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="89e0a-191">Okuma ve bir ileti kuyruktan kaldırma</span><span class="sxs-lookup"><span data-stu-id="89e0a-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="89e0a-192">Bu bölümde, okuma ve bir ileti kuyruktan kaldırma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89e0a-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="89e0a-193">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-194">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="89e0a-195">Adlı bir yöntem ekleyin **ReadMessage** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="89e0a-196">İçinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-197">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="89e0a-198">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="89e0a-199">Alma bir **CloudQueueContainer** sıranın başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-200">Çağrı **CloudQueue.GetMessage** sıradaki ilk iletiyi okumak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="89e0a-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="89e0a-201">**CloudQueue.GetMessage** yöntemi yapar ileti görünmez başka bir kod değiştirmek veya ileti, onu işlenirken silmek böylece iletileri okuyan herhangi bir kod için 30 saniye (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="89e0a-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="89e0a-202">İleti görünmez süre miktarını değiştirmek için değiştirmek **visibilityTimeout** için geçirilen parametre **CloudQueue.GetMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="89e0a-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="89e0a-203">Çağrı **CloudQueueMessage.Delete** iletiyi sıradan silmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="89e0a-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="89e0a-204">Güncelleştirme **ViewBag** silinmiş ileti ve sıra adı.</span><span class="sxs-lookup"><span data-stu-id="89e0a-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="89e0a-205">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-206">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ReadMessage** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-207">Açık `ReadMessage.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="89e0a-208">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-209">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-210">Uygulamayı çalıştırmak ve seçmek **okuma/silme iletisi** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Okuma ve silme iletisi](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="89e0a-212">Kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="89e0a-212">Get the queue length</span></span>

<span data-ttu-id="89e0a-213">Bu bölümde, kuyruk uzunluğu (iletilerinin sayısı) alma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="89e0a-214">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-215">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="89e0a-216">Adlı bir yöntem ekleyin **GetQueueLength** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="89e0a-217">İçinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-218">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="89e0a-219">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="89e0a-220">Alma bir **CloudQueueContainer** sıranın başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-221">Çağrı **CloudQueue.FetchAttributes** (uzunluğu dahil) kuyruğun öznitelikleri alma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="89e0a-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="89e0a-222">Erişim **CloudQueue.ApproximateMessageCount** sıra uzunluğu alınacağı özellik.</span><span class="sxs-lookup"><span data-stu-id="89e0a-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="89e0a-223">Güncelleştirme **ViewBag** sırası uzunluğu ve ada sahip.</span><span class="sxs-lookup"><span data-stu-id="89e0a-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="89e0a-224">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-225">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetQueueLength** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-226">Açık `GetQueueLengthMessage.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="89e0a-227">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-228">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-229">Uygulamayı çalıştırmak ve seçmek **alma sırası uzunluğu** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Kuyruk uzunluğu alma](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="89e0a-231">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="89e0a-231">Delete a queue</span></span>
<span data-ttu-id="89e0a-232">Bu bölümde, bir kuyruk silme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="89e0a-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="89e0a-233">Bu bölümdeki adımları tamamladığınızdan varsayar [geliştirme ortamını ayarlama](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="89e0a-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="89e0a-234">`QueuesController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="89e0a-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="89e0a-235">Adlı bir yöntem ekleyin **DeleteQueue** döndüren bir **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="89e0a-236">İçinde **DeleteQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="89e0a-237">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın: (değişiklik  *&lt;depolama hesabı adı >* Azure depolama hesabı adını eriştiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="89e0a-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="89e0a-238">Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="89e0a-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="89e0a-239">Alma bir **CloudQueueContainer** sıranın başvuru temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="89e0a-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="89e0a-240">Çağrı **CloudQueue.Delete** yöntemi tarafından temsil edilen sıra silmek için **CloudQueue** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="89e0a-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="89e0a-241">Güncelleştirme **ViewBag** sırası uzunluğu ve ada sahip.</span><span class="sxs-lookup"><span data-stu-id="89e0a-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="89e0a-242">İçinde **Çözüm Gezgini**, genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve bağlam menüsünden seçin **Ekle -> Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="89e0a-243">Üzerinde **Görünüm Ekle** iletişim kutusunda, girin **DeleteQueue** Görünüm adı ' nı seçip için **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89e0a-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="89e0a-244">Açık `DeleteQueue.cshtml`ve aşağıdaki kod parçacığını gibi görünüyor şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="89e0a-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="89e0a-245">İçinde **Çözüm Gezgini**, genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="89e0a-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="89e0a-246">Son sonra **Html.ActionLink**, aşağıdakileri ekleyin **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="89e0a-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="89e0a-247">Uygulamayı çalıştırmak ve seçmek **alma sırası uzunluğu** aşağıdaki ekran görüntüsüne benzer sonuçlar görmek için:</span><span class="sxs-lookup"><span data-stu-id="89e0a-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Kuyruğu silin](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="89e0a-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89e0a-249">Next steps</span></span>
<span data-ttu-id="89e0a-250">Azure’da veri depolama ile ilgili ek seçenekler hakkında daha fazla bilgi edinmek için daha fazla özellik kılavuzu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="89e0a-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="89e0a-251">Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="89e0a-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="89e0a-252">Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="89e0a-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
