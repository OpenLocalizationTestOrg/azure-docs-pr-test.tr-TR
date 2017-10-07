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
# <a name="send-events-tooazure-event-hubs-using-java"></a>Olayları tooAzure olay hub'ın Java kullanarak Gönder

## <a name="introduction"></a>Giriş
Olay hub'ları bir uygulama tooprocess etkinleştirme saniye başına milyonlarca olayı alma ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki hello analiz bir yüksek düzeyde ölçeklenebilir bir alım sistem olur. Bir olay hub'ına toplandığında, dönüştürme ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya depolama kümesi kullanarak verileri depolar.

Daha fazla bilgi için bkz: Merhaba [Event Hubs'a genel bakış][Event Hubs overview].

Bu öğreticide gösterilmiştir nasıl Java konsol uygulaması kullanarak toosend olayları tooan olay hub'ı. Merhaba Java olay işleyicisi konağı kitaplığını kullanarak tooreceive olaylara bakın [bu makalede](event-hubs-java-get-started-receive-eph.md), veya hello uygun alıcı dilde hello sol İçindekiler'ı tıklatın.

Sipariş toocomplete Bu öğreticiyi izleyerek hello gerekir:

* Java geliştirme ortamı. Bu öğretici için varsayıyoruz [Eclipse](https://www.eclipse.org/).
* Etkin bir Azure hesabı. <br/>Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.

## <a name="send-messages-tooevent-hubs"></a>TooEvent hub iletileri gönder
Merhaba olay hub'ları için Java istemci kitaplığı hello projelerden Maven içinde kullanılabilir [Maven merkezi bir depoya](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Bağımlılık bildirimi Maven projesi dosyanızı içinde aşağıdaki hello kullanarak bu kitaplığı başvurusu yapabilir:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Derleme ortamları farklı türleri için açıkça hello son yayımlanan hello JAR dosyalarını edinebilirsiniz [Maven merkezi bir depoya](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Basit olay yayımcısı hello alma *com.microsoft.azure.eventhubs* hello olay hub'ları istemci sınıfları ve hello paketi *com.microsoft.azure.servicebus* gibi yardımcı program sınıfları için paketi Genel özel durumlar olarak, hello Azure Service Bus ileti sistemi istemcisi ile paylaşılır. 

Örnek aşağıdaki hello için önce sık kullanılan Java geliştirme ortamı konsol/Kabuk uygulama için yeni bir Maven projesi oluşturun. Ad hello sınıfı `Send`.     

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

Merhaba ad alanı ve olay hub'ı adları hello olay hub'ı oluşturduğunuzda kullanılan hello değerlerle değiştirin.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Ardından, bir dize, UTF-8 bayt kodlamaya dönüştürerek tekil bir olay oluşturun. Sonra yeni bir olay hub'ları istemci örnek hello bağlantı dizesinden oluşturun ve hello ileti gönderin.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Merhaba EventProcessorHost kullanarak olayları alma](event-hubs-java-get-started-receive-eph.md)
* [Event Hubs'a genel bakış][Event Hubs overview]
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md