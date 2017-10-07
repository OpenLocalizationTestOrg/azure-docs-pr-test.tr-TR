---
title: aaaCreate Mobile Apps kullanan bir evrensel Windows Platformu (UWP) | Microsoft Docs
description: "C#, Visual Basic ya da JavaScript'te Evrensel Windows Platformu (UWP) uygulaması geliştirme için Azure mobil uygulaması arka uçlarını kullanmaya ile Bu öğretici tooget izleyin."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="e6468-103">Windows uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6468-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="e6468-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e6468-104">Overview</span></span>
<span data-ttu-id="e6468-105">Bu öğretici nasıl tooadd bir bulut tabanlı arka uç hizmeti tooa Evrensel Windows Platformu (UWP) uygulamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6468-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="e6468-106">Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="e6468-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="e6468-107">Merhaba ekran tamamlandı hello uygulamadan yakalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e6468-107">hello following are screen captures from hello completed app:</span></span>

![Tamamlanmış masaüstü uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="e6468-109">Masaüstünde çalışma.</span><span class="sxs-lookup"><span data-stu-id="e6468-109">Running on a desktop.</span></span>

![Tamamlanmış. telefon uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="e6468-111">Telefonda çalışma</span><span class="sxs-lookup"><span data-stu-id="e6468-111">Running on a phone</span></span>

<span data-ttu-id="e6468-112">Bu öğreticiyi tamamlamak UWP uygulamalarına ilişkin tüm Mobil Uygulama öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="e6468-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6468-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e6468-113">Prerequisites</span></span>
<span data-ttu-id="e6468-114">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6468-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e6468-115">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="e6468-115">An active Azure account.</span></span> <span data-ttu-id="e6468-116">Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın.</span><span class="sxs-lookup"><span data-stu-id="e6468-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="e6468-117">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6468-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e6468-118">[Visual Studio Community 2015] ya da daha yeni sürümü.</span><span class="sxs-lookup"><span data-stu-id="e6468-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="e6468-119">Yeni bir Azure Mobil Uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6468-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="e6468-120">Bu adımları toocreate yeni bir mobil uygulama arka ucu izleyin.</span><span class="sxs-lookup"><span data-stu-id="e6468-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="e6468-121">Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız.</span><span class="sxs-lookup"><span data-stu-id="e6468-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="e6468-122">Ardından, basit bir "Yapılacaklar listesi" için bir sunucu projesi yükleyecek arka uç ve tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e6468-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="e6468-123">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="e6468-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="e6468-124">Karşıdan yükleme ve hello istemci projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e6468-124">Download and run hello client project</span></span>
<span data-ttu-id="e6468-125">Mobil uygulama arka ucunuzu yapılandırdıktan sonra yeni bir istemci uygulaması oluşturabilir veya var olan bir uygulama tooconnect tooAzure değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e6468-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="e6468-126">Bu bölümde, özelleştirilmiş tooconnect tooyour mobil uygulama arka ucu olan bir UWP uygulaması şablonu projesi indirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6468-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="e6468-127">Hello edilene **Hızlı Başlangıç** , mobil uygulama arka ucu için dikey tıklayın **yeni uygulama oluştur** > **karşıdan**, hello sıkıştırılmış proje dosyalarını ayıklayın tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="e6468-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Windows hızlı başlangıç projesi indirme](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="e6468-129">(İsteğe bağlı) Merhaba UWP uygulaması projesi toohello eklemek hello sunucu projesi olarak aynı çözüme.</span><span class="sxs-lookup"><span data-stu-id="e6468-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="e6468-130">Bu, daha kolay toodebug ve her ikisi de uygulama ve hello arka uç hello test kılar toodo Bunu seçerseniz, aynı Visual Studio çözümü hello.</span><span class="sxs-lookup"><span data-stu-id="e6468-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="e6468-131">bir UWP uygulaması projesi toohello çözüm tooadd, Visual Studio 2015 veya sonraki bir sürümünü kullanıyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6468-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="e6468-132">Merhaba başlangıç projesi olarak Hello UWP uygulaması ile hello F5 anahtar toodeploy ve çalışma hello uygulama basın.</span><span class="sxs-lookup"><span data-stu-id="e6468-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="e6468-133">Merhaba uygulamada gibi anlamlı bir metin yazın *tam hello öğretici*, hello içinde **Todoıtem Ekle** metin kutusuna ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e6468-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows hızlı başlangıç tamamlanmış masaüstü](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="e6468-135">Bu, Azure'da barındırılan bir POST isteği toohello yeni mobil uygulama arka ucu gönderir.</span><span class="sxs-lookup"><span data-stu-id="e6468-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="e6468-136">(İsteğe bağlı) Merhaba uygulamayı durdurun ve farklı cihaz veya mobil öykünücü üzerinde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e6468-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Windows hızlı başlangıç tamamlanmış telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="e6468-138">Merhaba önceki adımda kaydedilen verilerin Hello UWP uygulaması başladıktan sonra Azure'dan yüklenip yüklenmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e6468-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6468-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6468-139">Next steps</span></span>
* [<span data-ttu-id="e6468-140">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="e6468-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="e6468-141">Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="e6468-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="e6468-142">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="e6468-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="e6468-143">Mobil uygulama arka uç toouse Azure Notification Hubs toosend anında iletme bildirimleri yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e6468-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="e6468-144">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e6468-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="e6468-145">Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="e6468-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="e6468-146">Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="e6468-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
