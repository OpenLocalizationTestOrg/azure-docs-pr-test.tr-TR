---
title: "aaaAzure geçiş bağlantı noktası ayarları | Microsoft Docs"
description: "Azure geçiş bağlantı noktası değerlerini hakkında ayrıntılar."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: e66785f786ee241c974d250f9ec29dfcc1fdc3fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-port-settings"></a>Azure geçiş bağlantı noktası ayarları

Merhaba aşağıdaki tabloda hello Azure geçiş için bağlantı noktası değerleri için gerekli yapılandırma açıklanmaktadır.

## <a name="hybrid-connections"></a>Karma Bağlantılar
Karma bağlantılar kullanan WebSockets kullanan bir aktarım mekanizması temel hello **HTTPS** yalnızca. 

## <a name="wcf-relays"></a>WCF Geçişleri
  
|Bağlama|Taşıma güvenliği|Bağlantı noktası|  
|-------------|------------------------|----------|  
|[BasicHttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (istemci)|Evet|HTTPS| 
| |" |Hayır|HTTP|  
|[BasicHttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (hizmeti)|Her iki|9351/HTTP|  
|[NetEventRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (istemci)|Evet|9351/HTTPS|  
||" |Hayır|9350/HTTP|  
|[NetEventRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (hizmeti)|Her iki|9351/HTTP|  
|[NetTcpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (istemci/hizmeti)|Her iki|9352/5671/HTTP (9352/karma kullanıyorsanız 9353)|  
|[NetOnewayRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (istemci)|Evet|9351/HTTPS|  
||" |Hayır|9350/HTTP|  
|[NetOnewayRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (hizmeti)|Her iki|9351/HTTP|  
|[WebHttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (istemci)|Evet|HTTPS|  
||" |Hayır|HTTP|  
|[WebHttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (hizmeti)|Her iki|9351/HTTP|  
|[WS2007HttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (istemci)|Evet|HTTPS|  
||" |Hayır|HTTP|  
|[WS2007HttpRelayBinding sınıfı](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (hizmeti)|Her iki|9351/HTTP|

## <a name="next-steps"></a>Sonraki adımlar
toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:
* [Azure Geçiş nedir?](relay-what-is-it.md)
* [Geçiş hakkında SSS](relay-faq.md)