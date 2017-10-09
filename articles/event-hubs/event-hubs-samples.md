---
title: "aaaAzure olay hub'ları örnekleri | Microsoft Docs"
description: "Azure Event Hubs örnekleri"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Olay hub'ları örnekleri 

Hello Azure Event Hubs örnekler kümesi gösterilmektedir anahtar özellikleri [Azure Event Hubs](/azure/event-hubs/). Bu makalede, kategorilere ayırır ve hello örnekleri ile bağlantı tooeach kullanılabilir açıklar.

Bu yazma Hello anda olay hub'ları örnekleri birkaç farklı yerlerde bulunur:

- [MSDN Geliştirici kod örnekleri](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

.NET Framework hello farklı sürümleri hakkında daha fazla bilgi için bkz: [çerçeveler ve hedefleri](/dotnet/articles/standard/frameworks).

Daha fazla örnekleri olacaktır zamanla eklenir, böylece geri burada sık Güncelleştirmeleri denetle.

## <a name="net-standard"></a>.NET standart

Merhaba aşağıdaki örnekleri göstermek nasıl toosend hello kullanarak olayları alıp [Event Hubs istemcisi](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) hello için [.NET standart Kitaplığı](/dotnet/articles/standard/library).

### <a name="send-events"></a>Olayları gönderme 

Merhaba [göndermeye başlamak](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) örnek göstermektedir nasıl toowrite .NET Core konsol tooan olay hub'ı olaylar gönderir uygulaması.

### <a name="receive-events"></a>Olayları alma 

Merhaba [olay işleyicisi konağı hello ile almaya başlamak](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) hello olay işleyicisi konağı kullanarak bir event hub iletileri alan bir .NET Core konsol uygulaması örnektir.

## <a name="net-framework"></a>.NET framework   

Bu örnekler çeşitli hello hedefleme Azure Event Hubs özelliklerini göstermek [.NET Framework Kitaplığı](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Alınan olayların kullanıcıları bildir

Merhaba [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) örnek algılayıcılar veya diğer sistemler alınan veri kullanıcılarına bildirir.

### <a name="get-started-with-event-hubs"></a>Event Hubs kullanmaya başlayın 

Merhaba [olay hub'ları Başlarken](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) örnek gösterilmektedir hello temel özellikleri nasıl toocreate bir event hub tooan event hub'ı olayları göndermek ve gibi hello kullanarak olayları tüketmek Event hubs [olay işleyicisi konağı](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Olay işleme çıkışı ölçeklendirme 

Merhaba [olay işleme genişletme](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) örnek gösterilmektedir nasıl toouse hello [olay işleyicisi konağı](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) olay hub'ları akış tüketiminin toodistribute hello iş yükü. Bunu gösterir nasıl tooimplement hello **EventProcessor** ve **EventProcessorFactory** nesneleri toomanage hello olay akışı. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Bir olay hub'ına SQL'den veri çekme

Merhaba [çekme SQL veri](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) örnek nasıl toopull verileri bir SQL tablosunu ve tooan olay hub'ı, aşağı akış analitik uygulamalarında bir girdi olarak toouse anında gösterir.

### <a name="pull-web-data-into-an-event-hub"></a>Bir olay hub'ına Web veri çekme 

Merhaba [hello web sunucusundan veri içeri aktarma](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) örnek, nasıl ortak toopull verileri (akışı departmanı, taşıma'nın trafiği bilgilerini hello gibi) akışları ve tooan olay hub'ı itme gösterir.

## <a name="next-steps"></a>Sonraki adımlar

.NET Framework sürümleri hakkında daha fazla bağlantılar aşağıdaki hello ziyaret ederek bilgi:

- [Çerçeveler ve hedefler](/dotnet/articles/standard/frameworks)
- [.NET framework 4.6 ve 4.5](/dotnet/framework/index)

Event Hubs hakkında daha fazla bilgi makaleler hello edinebilirsiniz:

- [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
- [Olay Hub’ı oluşturma](event-hubs-create.md)
- [Event Hubs ile ilgili SSS](event-hubs-faq.md)