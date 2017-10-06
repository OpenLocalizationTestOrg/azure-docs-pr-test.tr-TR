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
# <a name="create-an-android-app"></a><span data-ttu-id="4be66-103">Android uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="4be66-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4be66-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4be66-104">Overview</span></span>
<span data-ttu-id="4be66-105">Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooan Android mobil uygulamanızı Azure mobil uygulaması arka ucunu kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="4be66-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="4be66-106">Yeni bir mobil uygulama arka ucu ve uygulama verilerini Azure’da depolayan basit bir *Yapılacaklar listesi* Android uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4be66-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="4be66-107">Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Android öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="4be66-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4be66-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4be66-108">Prerequisites</span></span>
<span data-ttu-id="4be66-109">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4be66-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4be66-110">[Android Geliştirici Araçları](https://developer.android.com/sdk/index.html), hello Android Studio tümleşik geliştirme ortamını ve en son Android platformunu hello içerir.</span><span class="sxs-lookup"><span data-stu-id="4be66-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="4be66-111">Azure Mobile Android karşıdan hello hızlı başlangıç projesinin bir parçası otomatik başvurulan SDK.</span><span class="sxs-lookup"><span data-stu-id="4be66-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="4be66-112">[Etkin bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4be66-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="4be66-113">Yeni bir Azure mobil uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4be66-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="4be66-114">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="4be66-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="4be66-115">Merhaba Android uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4be66-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
