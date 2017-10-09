---
title: aaaUsing hello REST API tooaccess Azure Mobile Engagement hizmet API'leri
description: "Nasıl toouse hello Mobile Engagement REST API'leri tooaccess Azure Mobile Engagement hizmet API'leri açıklar"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a>REST tooaccess Azure Mobile Engagement hizmet API'leri kullanarak
Azure Mobile Engagement sağlar hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) , toomanage aygıtları için Reach/anında iletme kampanyalarını vb..

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Toouse hello REST API'lerini doğrudan istemiyorsanız de sunuyoruz bir [Swagger dosyası](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) araçları toogenerate SDK'ları için tercih ettiğiniz dili ile kullanabilirsiniz. Merhaba kullanmanızı öneririz [AutoRest](https://github.com/Azure/AutoRest) toogenerate bizim Swagger dosyasından, SDK aracı. Bir C# sarmalayıcı kullanarak bu API'leri ile toointeract sağlayan benzer şekilde bir .NET SDK'sı oluşturduk ve kimlik doğrulama belirteci anlaşma hello ve kendiniz yenileyin toodo yok. Bkz: [hizmeti API .NET SDK'sı örneği](mobile-engagement-dotnet-sdk-service-api.md) toolearn nasıl toouse hello .net SDK'sı için API
