---
title: "Azure Uygulama Hizmeti Mobile Apps’de iOS uygulaması oluşturma | Microsoft Belgeleri"
description: "Objective-C ya da Swift’te iOS geliştirme için Azure mobil uygulaması arka uçlarını kullanmaya başlamak için bu öğreticiden yararlanın."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="ac5ef-103">iOS uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac5ef-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ac5ef-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ac5ef-104">Overview</span></span>
<span data-ttu-id="ac5ef-105">Bu öğreticide, bir iOS uygulamasına bulut tabanlı arka uç hizmeti olan [Azure Mobile Apps](app-service-mobile-value-prop.md)’i nasıl ekleyeceğiniz gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ac5ef-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="ac5ef-106">Önce yeni bir mobil arka uç oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ac5ef-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="ac5ef-107">Ardından, Azure’da verileri depolamak için basit bir *Yapılacaklar listesi* iOS uygulaması kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ac5ef-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="ac5ef-108">Bu öğreticiyi tamamlamak için bir [Mac bilgisayar](https://azure.microsoft.com/pricing/free-trial/) ve Azure hesabınızın olması gerekir</span><span class="sxs-lookup"><span data-stu-id="ac5ef-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="ac5ef-109">Adım I: Yeni bir Azure mobil uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac5ef-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="ac5ef-110">Adım II: Arka uç projesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac5ef-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="ac5ef-111">Adım III: iOS uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ac5ef-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
