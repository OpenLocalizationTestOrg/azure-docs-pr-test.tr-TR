---
title: ".NET Framework hello aaaSend olayları tooAzure olay hub'ları kullanarak | Microsoft Docs"
description: "Merhaba .NET Framework kullanarak tooEvent hub olayların gönderilmesi kullanmaya başlama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="df081-103">Olayları tooAzure olay hub'ın hello .NET Framework kullanarak Gönder</span><span class="sxs-lookup"><span data-stu-id="df081-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="df081-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="df081-104">Introduction</span></span>

<span data-ttu-id="df081-105">Event Hubs bağlı cihaz ve uygulamalardan büyük miktarlarda olay verileri (telemetri) işleyen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="df081-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="df081-106">Verileri Event Hubs'a topladıktan sonra bir depolama kümesi kullanarak hello veri depolamak veya gerçek zamanlı analiz sağlayıcısı kullanarak dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="df081-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="df081-107">Bu büyük ölçekli olay toplama ve işleme özelliği hello nesnelerin interneti (IOT) dahil modern uygulama mimarilerinin temel bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="df081-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="df081-108">Bu öğreticide gösterilmiştir nasıl toouse hello [Azure portal](https://portal.azure.com) toocreate bir event hub.</span><span class="sxs-lookup"><span data-stu-id="df081-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="df081-109">C# kullanarak yazılmış bir konsol uygulaması kullanarak toosend olayları tooan olay hub'ı hello .NET Framework nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="df081-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="df081-110">Merhaba, .NET Framework kullanarak tooreceive olaylara bakın hello [hello .NET Framework kullanarak olayları alma](event-hubs-dotnet-framework-getstarted-receive-eph.md) makale ya da uygun alıcı dili hello sol İçindekiler hello tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df081-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="df081-111">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="df081-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="df081-112">[Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="df081-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="df081-113">Bu öğreticide Hello ekran görüntüleri, Visual Studio 2017 kullanın.</span><span class="sxs-lookup"><span data-stu-id="df081-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="df081-114">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="df081-114">An active Azure account.</span></span> <span data-ttu-id="df081-115">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df081-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="df081-116">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="df081-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="df081-117">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="df081-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="df081-118">Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate ad alanı bir olay hub'ları yazın ve hello uygulamanız gereken toocommunicate hello olay hub'ı ile yönetim kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="df081-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="df081-119">toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md), sonra Bu öğreticide adımları izleyerek hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="df081-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="df081-120">Gönderen konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="df081-120">Create a sender console application</span></span>

<span data-ttu-id="df081-121">Bu bölümde, tooyour olay hub'ı olaylar gönderir bir Windows konsol uygulamasını yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="df081-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="df081-122">Visual Studio'da hello kullanarak yeni bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="df081-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="df081-123">Ad hello proje **gönderen**.</span><span class="sxs-lookup"><span data-stu-id="df081-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="df081-124">Çözüm Gezgini'nde hello sağ **gönderen** proje ve ardından **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="df081-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="df081-125">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="df081-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="df081-126">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="df081-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="df081-127">Visual Studio indirir, yükler ve başvuru toohello ekler [Azure Service Bus kitaplığı NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="df081-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="df081-128">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="df081-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="df081-129">Aşağıdaki alanları toohello hello eklemek **Program** hello yer tutucu değerlerini hello event hub'ı hello önceki bölümde oluşturduğunuz ve daha önce kaydettiğiniz hello ad alanı düzeyinde bağlantı dizesi hello adıyla değiştirerek sınıfı.</span><span class="sxs-lookup"><span data-stu-id="df081-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="df081-130">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="df081-130">Add hello following method toohello **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="df081-131">Bu yöntem, olayları tooyour olay hub'ı 200 ms gecikmeyle sürekli olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="df081-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="df081-132">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="df081-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="df081-133">Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="df081-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="df081-134">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="df081-134">Congratulations!</span></span> <span data-ttu-id="df081-135">İletileri tooan olay hub'ı şimdi gönderdiniz.</span><span class="sxs-lookup"><span data-stu-id="df081-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df081-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df081-136">Next steps</span></span>
<span data-ttu-id="df081-137">Bir olay hub'ı oluşturur ve veri gönderir çalışan bir uygulama oluşturduğunuza göre aşağıdaki senaryoları toohello üzerinde hareket edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df081-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="df081-138">Merhaba olay işleyicisi konağı kullanarak olayları alma</span><span class="sxs-lookup"><span data-stu-id="df081-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="df081-139">Olay İşlemcisi Konağı başvurusu</span><span class="sxs-lookup"><span data-stu-id="df081-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="df081-140">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="df081-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

