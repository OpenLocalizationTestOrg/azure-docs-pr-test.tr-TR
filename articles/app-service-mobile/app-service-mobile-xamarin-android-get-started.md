---
title: "Xamarin.Android uygulamaları için Azure Mobile Apps ile başlatıldı aaaGet"
description: "Xamarin Android geliştirme için Azure Mobile Apps kullanmaya Bu öğretici tooget izleyin"
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="2067d-103">Xamarin.Android Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2067d-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2067d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2067d-104">Overview</span></span>
<span data-ttu-id="2067d-105">Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Xamarin.Android uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="2067d-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="2067d-106">Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="2067d-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="2067d-107">Merhaba tamamlanmış uygulamadan bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2067d-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="2067d-108">Bu öğreticiyi tamamlamak Xamarin Android uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="2067d-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2067d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2067d-109">Prerequisites</span></span>
<span data-ttu-id="2067d-110">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2067d-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="2067d-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="2067d-111">An active Azure account.</span></span> <span data-ttu-id="2067d-112">Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve too10 ücretsiz mobil uygulamalar edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2067d-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="2067d-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2067d-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2067d-114">Xamarin ile Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2067d-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="2067d-115">Yönergeler için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="2067d-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="2067d-116">Azure Mobil Uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2067d-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="2067d-117">Bu adımları toocreate bir mobil uygulama arka ucu izleyin.</span><span class="sxs-lookup"><span data-stu-id="2067d-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="2067d-118">Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız.</span><span class="sxs-lookup"><span data-stu-id="2067d-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="2067d-119">Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi indirme arka uç ve tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="2067d-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="2067d-120">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="2067d-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="2067d-121">Merhaba Xamarin.Android uygulamasını indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2067d-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="2067d-122">Altında **indirin ve Xamarin.Android projenizi çalıştırma**, hello tıklatın **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2067d-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="2067d-123">Merhaba sıkıştırılmış proje dosyasını tooyour yerel bilgisayara kaydedin ve kaydettiğiniz yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="2067d-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="2067d-124">Tuşuna hello **F5** anahtarı toobuild hello proje ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="2067d-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="2067d-125">Merhaba uygulamada gibi anlamlı bir metin yazın *tam hello öğretici* ve hello ardından **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2067d-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="2067d-126">Veriler hello istek hello Todoıtem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="2067d-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="2067d-127">Merhaba tabloda depolanan öğeler hello mobil uygulama arka ucu tarafından döndürülür ve veriler hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="2067d-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2067d-128">Mobil uygulama arka uç tooquery erişen hello kodu gözden geçirin ve hello ToDoActivity.cs C# dosyasına bulunan verileri, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2067d-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="2067d-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2067d-129">Next steps</span></span>
* [<span data-ttu-id="2067d-130">Çevrimdışı eşitleme tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="2067d-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="2067d-131">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="2067d-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="2067d-132">Anında iletme bildirimleri tooyour Xamarin.Android uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="2067d-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="2067d-133">Nasıl toouse hello Azure Mobile Apps için yönetilen</span><span class="sxs-lookup"><span data-stu-id="2067d-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
