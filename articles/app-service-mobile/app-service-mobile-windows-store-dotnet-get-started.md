---
title: "Mobile Apps’te Evrensel Windows Platformu (UWP) oluşturma | Microsoft Belgeleri"
description: "C#, Visual Basic ya da JavaScript’te Evrensel Windows Platformu (UWP) uygulaması geliştirme için Azure mobil uygulama arka uçlarını kullanmaya başlamak üzere bu öğreticiyi izleyin."
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
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="89bb0-103">Windows uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="89bb0-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="89bb0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="89bb0-104">Overview</span></span>
<span data-ttu-id="89bb0-105">Bu öğreticide, bir evrensel Windows Platformu’na (UWP) bulut tabanlı arka uç hizmetini nasıl ekleyeceğiniz gösterilir.</span><span class="sxs-lookup"><span data-stu-id="89bb0-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="89bb0-106">Daha fazla bilgi için bkz. [Mobile Apps nedir?](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="89bb0-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="89bb0-107">Aşağıdaki ekran görüntüleri tamamlanan şu uygulamalara aittir:</span><span class="sxs-lookup"><span data-stu-id="89bb0-107">The following are screen captures from the completed app:</span></span>

![Tamamlanmış masaüstü uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="89bb0-109">Masaüstünde çalışma.</span><span class="sxs-lookup"><span data-stu-id="89bb0-109">Running on a desktop.</span></span>

![Tamamlanmış. telefon uygulaması](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="89bb0-111">Telefonda çalışma</span><span class="sxs-lookup"><span data-stu-id="89bb0-111">Running on a phone</span></span>

<span data-ttu-id="89bb0-112">Bu öğreticiyi tamamlamak UWP uygulamalarına ilişkin tüm Mobil Uygulama öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="89bb0-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89bb0-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89bb0-113">Prerequisites</span></span>
<span data-ttu-id="89bb0-114">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="89bb0-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="89bb0-115">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="89bb0-115">An active Azure account.</span></span> <span data-ttu-id="89bb0-116">Bir hesabınız yoksa, Azure deneme sürümünü kaydolabilir ve deneme süresi bittikten sonra dahi kullanmaya devam edebileceğiniz 10 ücretsiz mobil uygulama edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89bb0-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="89bb0-117">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89bb0-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="89bb0-118">[Visual Studio Community 2015] ya da daha yeni sürümü.</span><span class="sxs-lookup"><span data-stu-id="89bb0-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="89bb0-119">Yeni bir Azure Mobil Uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="89bb0-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="89bb0-120">Yeni Mobil Uygulama arka ucu oluşturmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="89bb0-121">Artık, mobil istemci uygulamalarınız tarafından kullanılabilecek bir Azure Mobil Uygulama arka ucu sağladınız.</span><span class="sxs-lookup"><span data-stu-id="89bb0-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="89bb0-122">Sonra, basit bir "yapılacaklar listesi" arka ucu için bir sunucu projesi indirecek ve Azure’a yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="89bb0-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="89bb0-123">Sunucu projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="89bb0-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="89bb0-124">İstemci projesi indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="89bb0-124">Download and run the client project</span></span>
<span data-ttu-id="89bb0-125">Mobil Uygulama arka ucunuzu yapılandırdıktan sonra, Azure’a bağlanmak için yeni bir istemci uygulaması oluşturabilir veya mevcut bir uygulamayı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89bb0-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="89bb0-126">Bu bölümde, Mobil Uygulama arka ucunuza bağlanmak için özelleştirilmiş bir UWP uygulaması şablonu projesi indirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89bb0-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="89bb0-127">Mobil Uygulama arka ucunuzun **Hızlı Başlangıç** dikey penceresine dönerek, **Yeni uygulama oluştur** > **İndir**’e tıklayın ve ardından sıkıştırılmış proje dosyalarını yerel bilgisayarınıza çıkarın.</span><span class="sxs-lookup"><span data-stu-id="89bb0-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Windows hızlı başlangıç projesi indirme](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="89bb0-129">(İsteğe bağlı) UWP uygulaması projesini sunucu projesi olarak aynı çözüme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="89bb0-130">Bu, yapmayı seçmeniz halinde, aynı Visual Studio çözümündeki uygulama ve arka uç için hata ayıklama ve test etmeyi daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="89bb0-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="89bb0-131">Bir çözüme UWP uygulaması projesi eklemek için Visual Studio 2015 veya sonraki bir sürümünü kullanıyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="89bb0-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="89bb0-132">Başlangıç projesi olarak UWP uygulamasıyla, uygulamayı dağıtmak ve çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="89bb0-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="89bb0-133">Uygulamada **TodoItem Ekle** metin kutusuna *Öğreticiyi tamamla* gibi anlamlı bir metin yazın ve ardından**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89bb0-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Windows hızlı başlangıç tamamlanmış masaüstü](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="89bb0-135">Bu, Azure üzerinde barındırılan yeni mobil uygulama arka ucuna bir POST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="89bb0-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="89bb0-136">(İsteğe bağlı) Uygulamayı durdurun ve farklı cihaz veya mobil öykünücü üzerinde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="89bb0-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Windows hızlı başlangıç tamamlanmış telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="89bb0-138">Önceki adımda kaydedilen verilerin UWP uygulaması başladıktan sonra Azure’dan yüklenip yüklenmediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89bb0-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89bb0-139">Next steps</span></span>
* [<span data-ttu-id="89bb0-140">Uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="89bb0-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="89bb0-141">Uygulamanızdaki kullanıcıların kimliklerini bir kimlik sağlayıcısı ile nasıl doğrulayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="89bb0-142">Uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="89bb0-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="89bb0-143">Uygulamanıza anında iletme bildirimleri desteği eklemeyi ve anında iletme bildirimleri göndermek için Azure Notification Hubs’ı kullanmak üzere Mobile App arka ucunuzu yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="89bb0-144">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="89bb0-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="89bb0-145">Mobil Uygulama arka ucu kullanarak uygulamanıza çevrimdışı destek eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89bb0-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="89bb0-146">Çevrimdışı eşitleme son kullanıcıların, ağ bağlantısı yokken dahi, mobil uygulama ile etkileşim kurmalarına &mdash;veri görüntüleme, ekleme ya da değiştirme&mdash; olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="89bb0-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="89bb0-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="89bb0-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
