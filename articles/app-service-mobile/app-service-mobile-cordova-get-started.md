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
# <a name="create-an-apache-cordova-app"></a>Apache Cordova uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooan Apache Cordova mobil uygulamasına Azure mobil uygulaması arka ucunu kullanarak gösterir.  Yeni bir mobil uygulama arka ucu ve uygulama verilerini Azure'da depolayan basit bir *Yapılacaklar listesi* Apache Cordova uygulaması oluşturacaksınız.

Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Apache Cordova öğreticileri için önkoşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

* [Visual Studio Community 2017] ya da daha yeni sürümünü içeren bir bilgisayar.
* [Apache Cordova için Visual Studio Araçları].
* [Etkin bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/).

Ayrıca Visual Studio'yu atlayabilir ve doğrudan hello Apache Cordova komut satırını kullanın.  Merhaba komut satırını kullanarak hello öğreticiyi bir Mac bilgisayarda tamamladığınızda kullanışlıdır.  Merhaba komut satırını kullanarak Apache Cordova istemci uygulamalarını derleme Bu öğretici kapsamında değildir.

## <a name="create-an-azure-mobile-app-backend"></a>Azure mobil uygulama arka ucu oluşturma
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Benzer adımları gösteren bir video izleyin](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Merhaba Apache Cordova uygulamasını indirme ve çalıştırma
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Bu hızlı başlangıç öğreticisini tamamladığınıza göre öğreticileri aşağıdaki hello tooone üzerinde Taşı:

* [Çevrimdışı veri ekleme](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova uygulaması.
* [Kimlik doğrulaması ekleme](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova uygulaması.
* [Anında iletme bildirimleri ekleme](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova uygulaması.

Azure App Service temel kavramları hakkında daha fazla bilgi edinin.

* [Çevrimdışı Veri]
* [Kimlik doğrulaması]
* [Anında İletme Bildirimleri]

Nasıl toouse hello SDK'ları hakkında bilgi edinin.

* [Apache Cordova SDK]
* [ASP.NET Sunucusu SDK]
* [Node.js Sunucusu SDK]

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
