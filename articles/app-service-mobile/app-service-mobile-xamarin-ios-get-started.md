---
title: "aaaGet Xamarin.iOS uygulamaları için Azure App Service Mobile Apps ile başlatılan | Microsoft Docs"
description: "Xamarin.iOS geliştirme için Mobile Apps kullanmaya Bu öğretici tooget izleyin."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="38709-103">Yeni bir Xamarin.iOS uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="38709-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="38709-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="38709-104">Overview</span></span>
<span data-ttu-id="38709-105">Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Xamarin.iOS mobil uygulamasına Azure mobil uygulaması arka ucunu kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="38709-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="38709-106">Hem yeni bir mobil arka uç hem de Azure’da uygulama verilerini depolayan basit bir *Yapılacaklar listesi* oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="38709-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="38709-107">Bu öğreticiyi tamamlamak Azure App Service'te hello Mobile Apps özelliğini kullanmayla ilgili diğer tüm Xamarin.iOS öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="38709-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38709-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="38709-108">Prerequisites</span></span>
<span data-ttu-id="38709-109">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="38709-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="38709-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="38709-110">An active Azure account.</span></span> <span data-ttu-id="38709-111">Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın.</span><span class="sxs-lookup"><span data-stu-id="38709-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="38709-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38709-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="38709-113">Xamarin ile Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38709-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="38709-114">Yönergeler için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="38709-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="38709-115">Xcode v7.0 veya daha sonraki sürümü ve Xamarin Studio Community yüklü bir Mac.</span><span class="sxs-lookup"><span data-stu-id="38709-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="38709-116">Bkz. [Visual Studio ve Xamarin için kurulum ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) ve [Mac kullanıcıları için kurulum, yükleme ve doğrulamalar](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="38709-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="38709-117">Azure Mobil Uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="38709-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="38709-118">Bu adımları toocreate bir mobil uygulama arka ucu izleyin.</span><span class="sxs-lookup"><span data-stu-id="38709-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="38709-119">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="38709-119">Configure hello server project</span></span>
<span data-ttu-id="38709-120">Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız.</span><span class="sxs-lookup"><span data-stu-id="38709-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="38709-121">Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi indirme arka uç ve tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="38709-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="38709-122">Aşağıdaki adımları tooconfigure hello sunucu projesi toouse hello ya da hello Node.js veya .NET arka uç izleyin.</span><span class="sxs-lookup"><span data-stu-id="38709-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="38709-123">Merhaba Xamarin.iOS uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38709-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="38709-124">Açık hello [Azure portal] bir tarayıcı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="38709-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="38709-125">Hello ayarları dikey mobil uygulamanızın penceresinde **Get Started** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="38709-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="38709-126">3. adımın altında, henüz seçili değilse **Yeni uygulama oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38709-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="38709-127">Merhaba İleri'yi **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38709-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="38709-128">Tooyour mobil arka uç bağlanan bir istemci uygulaması indirilir.</span><span class="sxs-lookup"><span data-stu-id="38709-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="38709-129">Merhaba sıkıştırılmış proje dosyasını yerel bilgisayarınıza kaydedin ve kaydettiğiniz yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="38709-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="38709-130">İndirdiğiniz Merhaba projeyi çıkarın ve Xamarin Studio (veya Visual Studio) açın.</span><span class="sxs-lookup"><span data-stu-id="38709-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="38709-131">Merhaba F5 anahtar toobuild hello proje tuşuna basın ve hello uygulamayı hello iPhone öykünücüsünde başlatın.</span><span class="sxs-lookup"><span data-stu-id="38709-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="38709-132">Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*ve ardından hello  **+**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="38709-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="38709-133">Veriler hello istek hello Todoıtem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="38709-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="38709-134">Merhaba tabloda depolanan öğeler hello mobil uygulama arka ucu tarafından döndürülür ve veriler hello listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="38709-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="38709-135">Mobil uygulama arka uç tooquery erişen hello kodu gözden geçirin ve hello QSTodoService.cs C# dosyasına veri eklemek.</span><span class="sxs-lookup"><span data-stu-id="38709-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="38709-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38709-136">Next steps</span></span>
* [<span data-ttu-id="38709-137">Çevrimdışı eşitleme tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="38709-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="38709-138">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="38709-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="38709-139">Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="38709-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="38709-140">Nasıl toouse hello Azure Mobile Apps için yönetilen</span><span class="sxs-lookup"><span data-stu-id="38709-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Azure portal]: https://portal.azure.com/
