---
title: "Azure App Service Mobile Apps üzerinde Android uygulaması aaaCreate | Microsoft Docs"
description: "Android geliştirme için Azure mobil uygulaması arka uçlarını kullanmaya Bu öğretici tooget izleyin"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a>Android uygulaması oluşturma
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooan Android mobil uygulamanızı Azure mobil uygulaması arka ucunu kullanarak gösterir.  Yeni bir mobil uygulama arka ucu ve uygulama verilerini Azure’da depolayan basit bir *Yapılacaklar listesi* Android uygulaması oluşturacaksınız.

Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Android öğreticileri için önkoşuldur.

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, aşağıdaki hello gerekir:

* [Android Geliştirici Araçları](https://developer.android.com/sdk/index.html), hello Android Studio tümleşik geliştirme ortamını ve en son Android platformunu hello içerir.
* Azure Mobile Android karşıdan hello hızlı başlangıç projesinin bir parçası otomatik başvurulan SDK.
* [Etkin bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-new-azure-mobile-app-backend"></a>Yeni bir Azure mobil uygulama arka ucu oluşturma
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Merhaba sunucu projesi yapılandırmak
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a>Merhaba Android uygulamasını indirme ve çalıştırma
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
