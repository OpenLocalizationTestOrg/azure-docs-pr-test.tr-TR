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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Olayları tooAzure olay hub'ın hello .NET Framework kullanarak Gönder

## <a name="introduction"></a>Giriş

Event Hubs bağlı cihaz ve uygulamalardan büyük miktarlarda olay verileri (telemetri) işleyen bir hizmettir. Verileri Event Hubs'a topladıktan sonra bir depolama kümesi kullanarak hello veri depolamak veya gerçek zamanlı analiz sağlayıcısı kullanarak dönüştürme. Bu büyük ölçekli olay toplama ve işleme özelliği hello nesnelerin interneti (IOT) dahil modern uygulama mimarilerinin temel bir bileşenidir.

Bu öğreticide gösterilmiştir nasıl toouse hello [Azure portal](https://portal.azure.com) toocreate bir event hub. C# kullanarak yazılmış bir konsol uygulaması kullanarak toosend olayları tooan olay hub'ı hello .NET Framework nasıl gösterir. Merhaba, .NET Framework kullanarak tooreceive olaylara bakın hello [hello .NET Framework kullanarak olayları alma](event-hubs-dotnet-framework-getstarted-receive-eph.md) makale ya da uygun alıcı dili hello sol İçindekiler hello tıklatın.

toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

* [Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com). Bu öğreticide Hello ekran görüntüleri, Visual Studio 2017 kullanın.
* Etkin bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs ad alanı ve bir olay hub’ı oluşturma

Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate ad alanı bir olay hub'ları yazın ve hello uygulamanız gereken toocommunicate hello olay hub'ı ile yönetim kimlik bilgilerini alın. toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md), sonra Bu öğreticide adımları izleyerek hello ile devam edin.

## <a name="create-a-sender-console-application"></a>Gönderen konsol uygulaması oluşturma

Bu bölümde, tooyour olay hub'ı olaylar gönderir bir Windows konsol uygulamasını yazacaksınız.

1. Visual Studio'da hello kullanarak yeni bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu. Ad hello proje **gönderen**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. Çözüm Gezgini'nde hello sağ **gönderen** proje ve ardından **çözüm için NuGet paketlerini Yönet**. 
3. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio indirir, yükler ve başvuru toohello ekler [Azure Service Bus kitaplığı NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Aşağıdaki alanları toohello hello eklemek **Program** hello yer tutucu değerlerini hello event hub'ı hello önceki bölümde oluşturduğunuz ve daha önce kaydettiğiniz hello ad alanı düzeyinde bağlantı dizesi hello adıyla değiştirerek sınıfı.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:
   
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
   
  Bu yöntem, olayları tooyour olay hub'ı 200 ms gecikmeyle sürekli olarak gönderir.
7. Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.
  
Tebrikler! İletileri tooan olay hub'ı şimdi gönderdiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bir olay hub'ı oluşturur ve veri gönderir çalışan bir uygulama oluşturduğunuza göre aşağıdaki senaryoları toohello üzerinde hareket edebilirsiniz:

* [Merhaba olay işleyicisi konağı kullanarak olayları alma](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Olay İşlemcisi Konağı başvurusu](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

