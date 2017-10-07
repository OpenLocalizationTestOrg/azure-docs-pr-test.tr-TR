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
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Azure kuyruk depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış

Azure kuyruk depolama uygulama bileşenleri arasında Mesajlaşma bulut sağlar. Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır. Merhaba bulutta, hello Masaüstü, bir şirket içi sunucu veya bir mobil cihaz çalıştırıp çalıştırmadığınızı uygulama bileşenleri arasında iletişim için zaman uyumsuz Mesajlaşma kuyruk depolama sunar. Kuyruk depolama ayrıca zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını destekler.

Bu öğretici, nasıl Azure kuyruk depolama varlıklar kullanarak bazı genel senaryolar için toowrite ASP.NET kodu gösterir. Bu senaryolar, bir Azure kuyruk oluşturma ve ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi genel görevleri içerir.

##<a name="prerequisites"></a>Ön koşullar

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Bir MVC denetleyicisi oluşturun. 

1. Merhaba, **Çözüm Gezgini**, sağ **denetleyicileri**ve hello bağlam menüsünden seçin **Ekle -> denetleyicisi**.

    ![Bir ASP.NET MVC uygulama denetleyicisi tooan Ekle](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Merhaba üzerinde **İskele Ekle** iletişim kutusunda **MVC 5 denetleyici - boş**seçip **Ekle**.

    ![MVC denetleyicisi türünü belirtin](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Merhaba üzerinde **denetleyici Ekle** iletişim, ad hello denetleyicisi *QueuesController*seçip **Ekle**.

    ![Ad hello MVC denetleyicisi](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Merhaba aşağıdakileri ekleyin *kullanarak* yönergeleri toohello `QueuesController.cs` dosyası:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Bir kuyruk oluşturma

Merhaba aşağıdaki adımları göstermek nasıl toocreate bir sıra:

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya. 

1. Adlı bir yöntem ekleyin **CreateQueue** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Merhaba içinde **CreateQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Alma bir **CloudQueue** başvuru toohello istenen sıra adını temsil eden nesne. Merhaba **CloudQueueClient.GetQueueReference** yöntemi kuyruk depolama doğrulamasını yapmaz. Merhaba sıra var olup olmadığına bakılmaksızın hello başvuru döndürülür. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba çağrısı **CloudQueue.CreateIfNotExists** henüz yoksa, yöntem toocreate hello sırası. Merhaba **CloudQueue.CreateIfNotExists** yöntemi döndürür **true** hello sıra yok ve başarıyla oluşturuldu. Aksi takdirde, **false** döndürülür.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Güncelleştirme hello **ViewBag** hello sırasının hello ada sahip.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **CreateQueue** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `CreateQueue.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **Oluşturma sırası** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Kuyruk oluşturma](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Daha önce belirtildiği gibi hello **CloudQueue.CreateIfNotExists** yöntemi döndürür **doğru** yalnızca hello sıra yok ve oluşturulur. Bu nedenle, hello sırası mevcut olduğunda hello uygulama çalıştırırsanız, hello yöntemi döndürür **false**. toorun hello uygulama birden çok kez, hello sıra hello uygulama yeniden çalıştırmadan önce silmeniz gerekir. Silme hello sıra hello yapılabilir **CloudQueue.Delete** yöntemi. Merhaba sıra hello kullanarak silebilirsiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) veya hello [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Bir ileti tooa sırası Ekle

Seçtiğiniz sonra [bir kuyruk oluşturan](#create-a-queue), iletileri toothat sırası ekleyebilirsiniz. Bu bölümde, bir ileti tooa sırası eklerken size yol gösterir *sınama sırası*. 

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya.

1. Adlı bir yöntem ekleyin **AddMessage** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **AddMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba oluşturma **CloudQueueMessage** tooadd toohello sıra istediğiniz selamlama iletisine temsil eden nesne. A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Merhaba çağrısı **CloudQueue.AddMessage** yöntemi tooadd hello messaged toohello sırası.

    ```csharp
    queue.AddMessage(message);
    ```

1. Birkaç oluşturup **ViewBag** hello görünümünde görüntülenmesi için özellikler.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **AddMessage** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `AddMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **Ekle ileti** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Mesaj ekleyin.](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

iki bölüm - hello [kaldırmadan bir sıradan ileti okumak](#read-a-message-from-a-queue-without-removing-it) ve [ekleme ve kaldırma bir iletiyi bir kuyruktan okunur](#read-and-remove-a-message-from-a-queue) -nasıl tooread kuyruktan iletileri gösterir.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Bir ileti kuyruktan kaldırmadan okuma

Bu bölümde anlatılacaktır nasıl toopeek sıraya alınmış bir iletiye (kaldırarak olmadan okuma hello ilk iletiyi).  

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya.

1. Adlı bir yöntem ekleyin **PeekMessage** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **PeekMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba çağrısı **CloudQueue.PeekMessage** yöntemi tooread hello hello sıradan kaldırarak olmadan hello sıradaki ilk iletiyi. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Güncelleştirme hello **ViewBag** iki değerlerle: hello kuyruk adı ve okundu hello ileti. Merhaba **CloudQueueMessage** nesne hello nesnenin değeri almak için iki özellik sunar: **CloudQueueMessage.AsBytes** ve **CloudQueueMessage.AsString**. **AsString** (Bu örnekte kullanılan) bir dize döndürür sırada **AsBytes** bir bayt dizisi döndürür.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **PeekMessage** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `PeekMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **gözlem ileti** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![İletiye Gözat](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Okuma ve bir ileti kuyruktan kaldırma

Bu bölümde, bilgi nasıl tooread ve kuyruktan bir ileti kaldırın.   

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya.

1. Adlı bir yöntem ekleyin **ReadMessage** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba çağrısı **CloudQueue.GetMessage** yöntemi tooread hello hello sıradaki ilk iletiyi. Merhaba **CloudQueue.GetMessage** yöntemi yapar (varsayılan) 30 saniye tooany ileti görünmez başka bir kod değiştirmek veya selamlama iletisine, onu işlenirken silmek böylece iletileri okumak başka bir kod hello. toochange hello zaman selamlama iletisine miktarıdır görünmez, hello Değiştir **visibilityTimeout** toohello geçirilen parametre **CloudQueue.GetMessage** yöntemi.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Merhaba çağrısı **CloudQueueMessage.Delete** hello kuyruğundan yöntemi toodelete hello ileti.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Güncelleştirme hello **ViewBag** hello ileti silinmiş ile Merhaba hello sırasının adı.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **ReadMessage** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `ReadMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

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

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **okuma/silme iletisi** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Okuma ve silme iletisi](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Merhaba kuyruk uzunluğu alma

Bu bölümde, nasıl tooget hello sırası uzunluğu (ileti sayısını) gösterir. 

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya.

1. Adlı bir yöntem ekleyin **GetQueueLength** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **ReadMessage** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba çağrısı **CloudQueue.FetchAttributes** yöntemi tooretrieve hello sıranın öznitelikleri (uzunluğu dahil). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Erişim hello **CloudQueue.ApproximateMessageCount** özelliği tooget hello sırasının uzunluğu.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Güncelleştirme hello **ViewBag** hello kuyruk ve uzunluğu hello adı.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **GetQueueLength** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `GetQueueLengthMessage.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **alma sırası uzunluğu** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Kuyruk uzunluğu alma](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Bir kuyruk silme
Bu bölümde anlatılacaktır nasıl toodelete bir sıra. 

> [!NOTE]
> 
> Bu bölümde hello adımları tamamladığınızdan varsayılır [hello geliştirme ortamını ayarlama](#set-up-the-development-environment). 

1. Açık hello `QueuesController.cs` dosya.

1. Adlı bir yöntem ekleyin **DeleteQueue** döndüren bir **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Merhaba içinde **DeleteQueue** yöntemi, get bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kullanım hello aşağıdaki kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgileri hello Azure hizmet yapılandırması: (değişiklik  *&lt;depolama hesabı adı >* hello Azure depolama toohello adı hesabı. eriştiğiniz)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Alma bir **CloudQueueClient** nesnesi, bir kuyruk hizmeti istemcisi temsil eder.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Alma bir **CloudQueueContainer** başvuru toohello sırası temsil eden nesne. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Merhaba çağrısı **CloudQueue.Delete** hello tarafından temsil edilen yöntem toodelete hello sıra **CloudQueue** nesnesi.

    ```csharp
    queue.Delete();
    ```

1. Güncelleştirme hello **ViewBag** hello kuyruk ve uzunluğu hello adı.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü sağ tıklatın **sıraları**ve hello bağlam menüsünden seçin **Ekle -> Görünüm**.

1. Merhaba üzerinde **Görünüm Ekle** iletişim kutusunda, girin **DeleteQueue** hello Görünüm adı ' nı seçip için **Ekle**.

1. Açık `DeleteQueue.cshtml`ve kod parçacığını aşağıdaki hello gibi görünüyor şekilde değiştirin:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. Merhaba, **Çözüm Gezgini**, hello genişletin **görünümleri -> paylaşılan** klasörü ve açık `_Layout.cshtml`.

1. Merhaba sonra son **Html.ActionLink**, hello aşağıdakileri ekleyin **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Merhaba uygulamayı çalıştırın ve seçin **alma sırası uzunluğu** toosee benzer toohello ekran görüntüsü aşağıdaki sonuçları:
  
    ![Kuyruğu silin](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Sonraki adımlar
Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.

  * [Azure blob depolama ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Azure tablo depolaması ve Visual Studio bağlı Hizmetleri (ASP.NET) kullanmaya başlama](vs-storage-aspnet-getting-started-tables.md)
