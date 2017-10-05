---
title: "Xamarin.Android uygulamaları için Azure Mobile Apps kullanmaya başlama"
description: "Xamarin Android geliştirme için Azure Mobile Apps’i kullanmaya başlamak için bu öğreticiden yararlanın"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="112d6-103">Xamarin.Android Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="112d6-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="112d6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="112d6-104">Overview</span></span>
<span data-ttu-id="112d6-105">Bu öğreticide, bir Xamarin.Android uygulamasına bulut tabanlı arka uç hizmetini nasıl ekleyeceğiniz gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="112d6-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="112d6-106">Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="112d6-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="112d6-107">Aşağıda tamamlanmış uygulamadan bir ekran görüntüsünü görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="112d6-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="112d6-108">Bu öğreticiyi tamamlamak Xamarin Android uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="112d6-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="112d6-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="112d6-109">Prerequisites</span></span>
<span data-ttu-id="112d6-110">Bu öğreticiyi tamamlamak için aşağıdaki önkoşulları karşılamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="112d6-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="112d6-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="112d6-111">An active Azure account.</span></span> <span data-ttu-id="112d6-112">Hesabınız yoksa Azure deneme sürümü için kaydolun ve 10 ücretsiz Mobil Uygulama edinin.</span><span class="sxs-lookup"><span data-stu-id="112d6-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="112d6-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="112d6-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="112d6-114">Xamarin ile Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="112d6-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="112d6-115">Yönergeler için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="112d6-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="112d6-116">Azure Mobil Uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="112d6-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="112d6-117">Mobil Uygulama arka ucu oluşturmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="112d6-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="112d6-118">Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız.</span><span class="sxs-lookup"><span data-stu-id="112d6-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="112d6-119">Ardından, basit bir "Yapılacaklar listesi" arka ucu için sunucu projesi indirin ve Azure’a yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="112d6-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="112d6-120">Sunucu projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="112d6-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="112d6-121">Xamarin Android uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="112d6-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="112d6-122">Altında **Xamarin.Android projenizi indirme ve çalıştırma** altında **İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="112d6-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="112d6-123">Sıkıştırılmış proje dosyasını yerel bilgisayarınıza kaydedin ve kaydettiğiniz yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="112d6-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="112d6-124">Projeyi oluşturmak ve uygulamayı başlatmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="112d6-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="112d6-125">Uygulamada, *Öğreticiyi tamamla* gibi anlamlı bir metin yazın ve ardından **Ekle** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="112d6-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="112d6-126">İstekten alınan veriler TodoItem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="112d6-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="112d6-127">Tabloda depolanan öğeler mobil uygulama arka ucu tarafından döndürülür ve veriler listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="112d6-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="112d6-128">Sorgulamak ve ToDoActivity.cs C# dosyasında bulunan verileri eklemek için, mobil uygulamanızın arka ucuna erişen kodu gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="112d6-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="112d6-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="112d6-129">Next steps</span></span>
* [<span data-ttu-id="112d6-130">Uygulamanıza Çevrimdışı Eşitleme ekleme</span><span class="sxs-lookup"><span data-stu-id="112d6-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="112d6-131">Uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="112d6-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="112d6-132">Xamarin.Android uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="112d6-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="112d6-133">Azure Mobile Apps için yönetilen istemciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="112d6-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
