---
title: "aaaAzure geçiş API genel bakış | Microsoft Docs"
description: "Kullanılabilir Azure geçiş API'larının genel bakış"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>Kullanılabilir geçiş API'leri

## <a name="runtime-apis"></a>Çalışma zamanı API'leri

Merhaba aşağıdaki tabloda şu anda kullanılabilir tüm geçiş çalışma zamanı istemcileri listelenmektedir.

Merhaba [ek bilgi](#additional-information) bölüm her çalışma zamanı kitaplığı hello durumu hakkında daha fazla bilgi içerir.

| Dil/Platform | Kullanılabilir özelliği | İstemci paketi | Depo |
| --- | --- | --- | --- |
| .NET standart | Karma Bağlantılar | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET framework | WCF Geçişi | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | Yok |
| Node | Karma Bağlantılar | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Ek bilgiler

#### <a name="net"></a>.NET
birden çok çalışma zamanları Hello .NET ekosistemi vardır, bu nedenle olay hub'ları için birden çok .NET kitaplıklarına vardır. Merhaba .NET standart kitaplığı hello .NET Framework kitaplığı yalnızca bir .NET Framework ortamında çalıştırılabilir .NET Core veya Merhaba, .NET Framework kullanarak çalıştırabilirsiniz. .NET Framework ile ilgili daha fazla bilgi için bkz: [framework sürümlerini](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Sonraki adımlar
toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:
* [Azure Geçiş nedir?](relay-what-is-it.md)
* [Geçiş hakkında SSS](relay-faq.md)