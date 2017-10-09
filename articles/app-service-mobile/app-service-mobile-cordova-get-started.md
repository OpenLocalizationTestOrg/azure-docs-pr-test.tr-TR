---
title: "aaaCreate bir Cordova uygulamasını Azure App Service Mobile Apps | Microsoft Docs"
description: "Apache Cordova geliştirme için Azure mobil uygulaması arka uçlarını kullanmaya Bu öğretici tooget izleyin"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova,javascript,mobil,istemci
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="50030-104">Apache Cordova uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="50030-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="50030-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="50030-105">Overview</span></span>
<span data-ttu-id="50030-106">Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooan Apache Cordova mobil uygulamasına Azure mobil uygulaması arka ucunu kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="50030-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="50030-107">Yeni bir mobil uygulama arka ucu ve uygulama verilerini Azure'da depolayan basit bir *Yapılacaklar listesi* Apache Cordova uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="50030-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="50030-108">Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Apache Cordova öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="50030-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50030-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="50030-109">Prerequisites</span></span>
<span data-ttu-id="50030-110">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="50030-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="50030-111">[Visual Studio Community 2017] ya da daha yeni sürümünü içeren bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="50030-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="50030-112">[Apache Cordova için Visual Studio Araçları].</span><span class="sxs-lookup"><span data-stu-id="50030-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="50030-113">[Etkin bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50030-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="50030-114">Ayrıca Visual Studio'yu atlayabilir ve doğrudan hello Apache Cordova komut satırını kullanın.</span><span class="sxs-lookup"><span data-stu-id="50030-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="50030-115">Merhaba komut satırını kullanarak hello öğreticiyi bir Mac bilgisayarda tamamladığınızda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="50030-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="50030-116">Merhaba komut satırını kullanarak Apache Cordova istemci uygulamalarını derleme Bu öğretici kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="50030-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="50030-117">Azure mobil uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="50030-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="50030-118">Benzer adımları gösteren bir video izleyin</span><span class="sxs-lookup"><span data-stu-id="50030-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="50030-119">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="50030-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="50030-120">Merhaba Apache Cordova uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="50030-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="50030-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="50030-121">Next Steps</span></span>
<span data-ttu-id="50030-122">Bu hızlı başlangıç öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde Taşı:</span><span class="sxs-lookup"><span data-stu-id="50030-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="50030-123">[Çevrimdışı veri ekleme](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="50030-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="50030-124">[Kimlik doğrulaması ekleme](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="50030-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="50030-125">[Anında iletme bildirimleri ekleme](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="50030-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="50030-126">Azure App Service temel kavramları hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="50030-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="50030-127">[Çevrimdışı Veri]</span><span class="sxs-lookup"><span data-stu-id="50030-127">[Offline Data]</span></span>
* <span data-ttu-id="50030-128">[Kimlik doğrulaması]</span><span class="sxs-lookup"><span data-stu-id="50030-128">[Authentication]</span></span>
* <span data-ttu-id="50030-129">[Anında İletme Bildirimleri]</span><span class="sxs-lookup"><span data-stu-id="50030-129">[Push Notifications]</span></span>

<span data-ttu-id="50030-130">Nasıl toouse hello SDK'ları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="50030-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="50030-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="50030-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="50030-132">[ASP.NET Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="50030-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="50030-133">[Node.js Sunucusu SDK]</span><span class="sxs-lookup"><span data-stu-id="50030-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Apache Cordova için Visual Studio Araçları]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Çevrimdışı Veri]: app-service-mobile-offline-data-sync.md
[Kimlik doğrulaması]: app-service-mobile-auth.md
[Anında İletme Bildirimleri]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Sunucusu SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Sunucusu SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
