---
title: "aaaAzure olay Hubs API'sine genel bakış | Microsoft Docs"
description: "Kullanılabilir Azure olay hub'ları API'larının genel bakış"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>Kullanılabilir olay hub'ları API'leri

## <a name="runtime-apis"></a>Çalışma zamanı API'leri

Merhaba, şu anda kullanılabilir tüm Azure Event Hubs çalışma zamanı istemcileri açıklaması verilmiştir. Bu kitaplıklar de sınırlı yönetim işlevselliğine bazıları olsa da vardır [belirli kitaplıkları](#management-apis) ayrılmış toomanagement işlemleri. Bu kitaplıklar Hello çekirdek odağını toosend olan iletiler ve bir event hub'ından alabilirsiniz.

Bkz: [ek bilgi](#additional-information) her çalışma zamanı kitaplığı hello geçerli durumu ile ilgili daha fazla ayrıntı için.

| Dil/Platform | İstemci paketi | EventProcessorHost paketi | Depo |
| --- | --- | --- | --- |
| .NET standart | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | Yok |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Node | [NPM](https://www.npmjs.com/package/azure-event-hubs) | Yok | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | Yok | Yok | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Ek bilgiler

#### <a name="net"></a>.NET
birden çok çalışma zamanları Hello .NET ekosistemi vardır, bu nedenle olay hub'ları için birden çok .NET kitaplıklarına vardır. Merhaba .NET standart kitaplığı hello .NET Framework kitaplığı yalnızca bir .NET Framework ortamında çalıştırılabilir .NET Core veya Merhaba, .NET Framework kullanarak çalıştırabilirsiniz. .NET Framework ile ilgili daha fazla bilgi için bkz: [framework sürümlerini](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Node

Merhaba Node.js kitaplığı şu anda önizlemede ve yan projesi olarak Microsoft çalışanlarına ve dış katkıda bulunanlar tarafından korunur. Kaynak kodu da dahil olmak üzere tüm katılımlar Hoş Geldiniz ve incelenecektir.

## <a name="management-apis"></a>Yönetim API'leri

Merhaba, tüm şu anda kullanılabilir yönetim belirli kitaplıkları bir listesi verilmiştir. Bu kitaplıklar hiçbiri çalışma zamanı işlemleri içerir ve Event Hubs varlıkları yönetme hello tek amacı olan.

| Dil/Platform | Yönetim Paketi | Depo |
| --- | --- | --- | --- |
| .NET standart | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)