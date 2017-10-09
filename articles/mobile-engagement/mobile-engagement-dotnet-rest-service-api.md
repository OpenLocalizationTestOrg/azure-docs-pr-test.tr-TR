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
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="9a990-103">REST tooaccess Azure Mobile Engagement hizmet API'leri kullanarak</span><span class="sxs-lookup"><span data-stu-id="9a990-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="9a990-104">Azure Mobile Engagement sağlar hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) , toomanage aygıtları için Reach/anında iletme kampanyalarını vb..</span><span class="sxs-lookup"><span data-stu-id="9a990-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="9a990-105">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="9a990-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="9a990-106">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="9a990-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="9a990-107">Toouse hello REST API'lerini doğrudan istemiyorsanız de sunuyoruz bir [Swagger dosyası](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) araçları toogenerate SDK'ları için tercih ettiğiniz dili ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a990-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="9a990-108">Merhaba kullanmanızı öneririz [AutoRest](https://github.com/Azure/AutoRest) toogenerate bizim Swagger dosyasından, SDK aracı.</span><span class="sxs-lookup"><span data-stu-id="9a990-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="9a990-109">Bir C# sarmalayıcı kullanarak bu API'leri ile toointeract sağlayan benzer şekilde bir .NET SDK'sı oluşturduk ve kimlik doğrulama belirteci anlaşma hello ve kendiniz yenileyin toodo yok.</span><span class="sxs-lookup"><span data-stu-id="9a990-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="9a990-110">Bkz: [hizmeti API .NET SDK'sı örneği](mobile-engagement-dotnet-sdk-service-api.md) toolearn nasıl toouse hello .net SDK'sı için API</span><span class="sxs-lookup"><span data-stu-id="9a990-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
