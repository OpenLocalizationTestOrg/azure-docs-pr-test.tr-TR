---
title: "aaaSend olayları tooAzure Event Hubs Java kullanarak | Microsoft Docs"
description: "Java kullanarak tooEvent hub gönderme kullanmaya başlama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="8ea61-103">Olayları tooAzure olay hub'ın Java kullanarak Gönder</span><span class="sxs-lookup"><span data-stu-id="8ea61-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="8ea61-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="8ea61-104">Introduction</span></span>
<span data-ttu-id="8ea61-105">Olay hub'ları bir uygulama tooprocess etkinleştirme saniye başına milyonlarca olayı alma ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz bir yüksek düzeyde ölçeklenebilir bir alım sistem olur.</span><span class="sxs-lookup"><span data-stu-id="8ea61-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="8ea61-106">Bir olay hub'ına toplandığında, dönüştürme ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya depolama kümesi kullanarak verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="8ea61-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="8ea61-107">Daha fazla bilgi için bkz: Merhaba [Event Hubs'a genel bakış][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="8ea61-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="8ea61-108">Bu öğreticide gösterilmiştir nasıl Java konsol uygulaması kullanarak toosend olayları tooan olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="8ea61-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="8ea61-109">Merhaba Java olay işleyicisi konağı kitaplığını kullanarak tooreceive olaylara bakın [bu makalede](event-hubs-java-get-started-receive-eph.md), veya hello uygun alıcı dilde hello sol İçindekiler'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8ea61-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="8ea61-110">Sipariş toocomplete Bu öğreticiyi izleyerek hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8ea61-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="8ea61-111">Java geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="8ea61-111">A Java development environment.</span></span> <span data-ttu-id="8ea61-112">Bu öğretici için varsayıyoruz [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="8ea61-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="8ea61-113">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="8ea61-113">An active Azure account.</span></span> <br/><span data-ttu-id="8ea61-114">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea61-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="8ea61-115">Ayrıntılı bilgi için bkz. <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.</span><span class="sxs-lookup"><span data-stu-id="8ea61-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="8ea61-116">TooEvent hub iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="8ea61-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="8ea61-117">Merhaba olay hub'ları için Java istemci kitaplığı hello projelerden Maven içinde kullanılabilir [Maven merkezi bir depoya](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="8ea61-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="8ea61-118">Bağımlılık bildirimi Maven projesi dosyanızı içinde aşağıdaki hello kullanarak bu kitaplığı başvurusu yapabilir:</span><span class="sxs-lookup"><span data-stu-id="8ea61-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="8ea61-119">Derleme ortamları farklı türleri için açıkça hello son yayımlanan hello JAR dosyalarını edinebilirsiniz [Maven merkezi bir depoya](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="8ea61-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="8ea61-120">Basit olay yayımcısı hello alma *com.microsoft.azure.eventhubs* hello olay hub'ları istemci sınıfları ve hello paketi *com.microsoft.azure.servicebus* gibi yardımcı program sınıfları için paketi Genel özel durumlar olarak, hello Azure Service Bus ileti sistemi istemcisi ile paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="8ea61-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="8ea61-121">Örnek aşağıdaki hello için önce sık kullanılan Java geliştirme ortamı konsol/Kabuk uygulama için yeni bir Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ea61-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="8ea61-122">Ad hello sınıfı `Send`.</span><span class="sxs-lookup"><span data-stu-id="8ea61-122">Name hello class `Send`.</span></span>     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="8ea61-123">Merhaba ad alanı ve olay hub'ı adları hello olay hub'ı oluşturduğunuzda kullanılan hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8ea61-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="8ea61-124">Ardından, bir dize, UTF-8 bayt kodlamaya dönüştürerek tekil bir olay oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ea61-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="8ea61-125">Sonra yeni bir olay hub'ları istemci örnek hello bağlantı dizesinden oluşturun ve hello ileti gönderin.</span><span class="sxs-lookup"><span data-stu-id="8ea61-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="8ea61-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ea61-126">Next steps</span></span>
<span data-ttu-id="8ea61-127">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ea61-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="8ea61-128">Merhaba EventProcessorHost kullanarak olayları alma</span><span class="sxs-lookup"><span data-stu-id="8ea61-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="8ea61-129">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="8ea61-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="8ea61-130">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ea61-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8ea61-131">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="8ea61-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md