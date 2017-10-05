---
title: "Azure Mobile Engagement tanıtım uygulamasını | Microsoft Docs"
description: "Karşıdan yükleme konumu, nasıl kullanılacağını ve Azure Mobile Engagement tanıtım uygulamasını kullanmanın avantajları açıklanmıştır"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 8381edb569e19a85c1259f7791b477cfa6e51ea3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-demo-app"></a><span data-ttu-id="c7919-103">Azure Mobile Engagement tanıtım uygulamasını</span><span class="sxs-lookup"><span data-stu-id="c7919-103">Azure Mobile Engagement demo app</span></span>
<span data-ttu-id="c7919-104">Bir Azure Mobile Engagement tanıtım uygulamasını için yayımlanan **iOS**, **Android**, ve **Windows** platformları kullanışlı kaynaklar bulmak ve Mobile Engagement hakkında daha fazla bilgi için Yardım.</span><span class="sxs-lookup"><span data-stu-id="c7919-104">We've published an Azure Mobile Engagement demo app for **iOS**, **Android**, and **Windows** platforms to help you to find useful resources and learn more about Mobile Engagement.</span></span>

<span data-ttu-id="c7919-105">Uygulama, yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="c7919-105">The app helps you to:</span></span>

* <span data-ttu-id="c7919-106">Kolayca videoları, belgeler, Destek Forumu ve özellik istekleri yükseltmek için yapılması gerekenler gibi Mobile Engagement kaynaklarına yararlı bağlantılar bulma.</span><span class="sxs-lookup"><span data-stu-id="c7919-106">Easily find useful links to Mobile Engagement resources like videos, documentation, the support forum, and where to go to raise feature requests.</span></span>
* <span data-ttu-id="c7919-107">Kendi mobil uygulamalar için fikir almak için Mobile Engagement tarafından desteklenen deneyimi örnek bildirimler.</span><span class="sxs-lookup"><span data-stu-id="c7919-107">Experience sample notifications that are supported by Mobile Engagement to get ideas for your own mobile applications.</span></span>
* <span data-ttu-id="c7919-108">Mobile Engagement, kendi uygulamanıza uygulamak nasıl incelemek için bir başvuru uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7919-108">Use a reference implementation to study how to implement Mobile Engagement into your own app.</span></span> <span data-ttu-id="c7919-109">İçin bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7919-109">You can learn to:</span></span>
  
  * <span data-ttu-id="c7919-110">Analytics veri toplar.</span><span class="sxs-lookup"><span data-stu-id="c7919-110">Collect analytics data.</span></span>
  * <span data-ttu-id="c7919-111">Uygulama bildirimi senaryolarını türleri gibi gelişmiş *tam ekran Interstitial* veya *açılır*.</span><span class="sxs-lookup"><span data-stu-id="c7919-111">Implement advanced notification scenarios of types such as *Full-screen interstitial* or *Pop-up*.</span></span>
  * <span data-ttu-id="c7919-112">Anketler ve anketler uygular.</span><span class="sxs-lookup"><span data-stu-id="c7919-112">Implement surveys and polls.</span></span>
  * <span data-ttu-id="c7919-113">Sessiz anında veri ve itme senaryolarında uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c7919-113">Implement silent push data and push scenarios.</span></span>   

## <a name="app-installation"></a><span data-ttu-id="c7919-114">Uygulama yükleme</span><span class="sxs-lookup"><span data-stu-id="c7919-114">App installation</span></span>
<span data-ttu-id="c7919-115">Bu uygulama aşağıdaki uygulama mağazasında edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="c7919-115">This app is available in the following app stores:</span></span>

* <span data-ttu-id="c7919-116">**Windows Evrensel tanıtım uygulamasını**:</span><span class="sxs-lookup"><span data-stu-id="c7919-116">**Windows Universal demo app**:</span></span>
  
  * <span data-ttu-id="c7919-117">Uygulamaya karşıdan [Windows uygulama mağazası](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span><span class="sxs-lookup"><span data-stu-id="c7919-117">Download the app at the [Windows App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span></span>
  * <span data-ttu-id="c7919-118">Uygulamayı Windows 10 Universal bir uygulama olarak geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7919-118">The app was developed as a Windows 10 Universal app.</span></span> <span data-ttu-id="c7919-119">Kaynak kodu kullanılabilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span><span class="sxs-lookup"><span data-stu-id="c7919-119">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span></span>
* <span data-ttu-id="c7919-120">**iOS uygulama gösteri**:</span><span class="sxs-lookup"><span data-stu-id="c7919-120">**iOS demo app**:</span></span>
  
  * <span data-ttu-id="c7919-121">Uygulamaya karşıdan [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span><span class="sxs-lookup"><span data-stu-id="c7919-121">Download the app at the [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span></span>
  * <span data-ttu-id="c7919-122">Uygulama iOS Swift geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7919-122">The app was developed in iOS Swift.</span></span> <span data-ttu-id="c7919-123">Kaynak kodu kullanılabilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span><span class="sxs-lookup"><span data-stu-id="c7919-123">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span></span>
* <span data-ttu-id="c7919-124">**Android tanıtım uygulamasını**:</span><span class="sxs-lookup"><span data-stu-id="c7919-124">**Android demo app**:</span></span>
  
  * <span data-ttu-id="c7919-125">Uygulamaya karşıdan [Google Play mağazasına](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span><span class="sxs-lookup"><span data-stu-id="c7919-125">Download the app at the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span></span>
  * <span data-ttu-id="c7919-126">Kaynak kodu kullanılabilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span><span class="sxs-lookup"><span data-stu-id="c7919-126">The source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span></span>

![Windows Evrensel tanıtım uygulamasını][1]

<span data-ttu-id="c7919-128">![iOS uygulama gösteri][2]
![Android tanıtım uygulamasını][3]</span><span class="sxs-lookup"><span data-stu-id="c7919-128">![iOS demo app][2]
![Android demo app][3]</span></span>

## <a name="usage"></a><span data-ttu-id="c7919-129">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c7919-129">Usage</span></span>
<span data-ttu-id="c7919-130">Bu uygulama aşağıdaki yollarla kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7919-130">You can use this app in the following ways:</span></span>

<span data-ttu-id="c7919-131">**Cihazınızda uygulamayı (daha önce sağlanan) uygulama mağazası bağlantılarından yükleyin:**</span><span class="sxs-lookup"><span data-stu-id="c7919-131">**Download the app on your device from the application store links (provided earlier):**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7919-132">Bir Azure hesabı veya uygulamaya bağlanmak için bir arka uç gerek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c7919-132">You don't need an Azure account or need to connect the app to a back end.</span></span> <span data-ttu-id="c7919-133">Uygulama bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="c7919-133">The app works independently.</span></span>
> 
> 

* <span data-ttu-id="c7919-134">Cihazınızda uygulamayı sonra Mobile Engagement hakkında yararlı kaynakları bulmak için sol taraftaki menüde bağlantılar yoluyla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-134">After you have the app on your device, then you can go through the links in the left-side menu to find the useful resources about Mobile Engagement.</span></span>
* <span data-ttu-id="c7919-135">Ekledik [hizmetin RSS akışı](https://aka.ms/azmerssfeed) bu uygulamaya böylece her zaman en son ürün güncelleştirmelerini hakkında güncelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="c7919-135">We've added the [service's RSS feed](https://aka.ms/azmerssfeed) into this application so that you're always updated about the latest product updates.</span></span>
* <span data-ttu-id="c7919-136">Her platform için Mobile Engagement tarafından desteklenen bildirim türünü yaşamaya bildirim senaryolar üzerinden gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-136">You can also go through the sample notification scenarios to experience the type of notifications that are supported by Mobile Engagement for each platform.</span></span> <span data-ttu-id="c7919-137">Bu bildirimler yerel olarak--olan yaşadı, Mobile Engagement platformundan bildirimleri göndermeyi aynıdır bildirimler deneyimini göstermek için ekranlar çubuğundaki düğmeler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c7919-137">These notifications can be experienced locally--that is, you can click the buttons on the screens to show you the notifications experience, which is identical to sending the notifications from the Mobile Engagement platform.</span></span>

![Windows için uygulama menüsü][4]

<span data-ttu-id="c7919-139">![İOS için uygulama menüsünden][5]
![Android için uygulama menüsü][6]</span><span class="sxs-lookup"><span data-stu-id="c7919-139">![App menu for iOS][5]
![App menu for Android][6]</span></span>

<span data-ttu-id="c7919-140">**Kaynak kodu (daha önce sağlanan) GitHub bağlantılarından yükleyin:**</span><span class="sxs-lookup"><span data-stu-id="c7919-140">**Download the source code from the GitHub links (provided earlier):**</span></span>

* <span data-ttu-id="c7919-141">Kaynak kodu indirdikten sonra ilgili geliştirme ortamında--XCode iOS, Android ve Windows için Visual Studio için Android Studio açın.</span><span class="sxs-lookup"><span data-stu-id="c7919-141">After you've downloaded the source code, open it in the respective development environment--XCode for iOS, Android Studio for Android, and Visual Studio for Windows.</span></span>
* <span data-ttu-id="c7919-142">Sonraki izlemeniz gereken bizim [Temel SDK tümleştirme adımları](mobile-engagement-windows-store-dotnet-get-started.md) böylece bu uygulamayı kendi Mobile Engagement arka uç örneğine bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="c7919-142">You should next follow our [basic SDK integration steps](mobile-engagement-windows-store-dotnet-get-started.md) so that you're able to connect this app to its own Mobile Engagement back-end instance.</span></span>
  * <span data-ttu-id="c7919-143">Uygulamada bir bağlantı dizesi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7919-143">You need to configure a connection string in the app.</span></span>
  * <span data-ttu-id="c7919-144">Ayrıca, uygulamanızı anında iletme bildirimi platformu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7919-144">You also need to configure the push notification platform for your app.</span></span>
* <span data-ttu-id="c7919-145">Mobile Engagement ile uygulama izlenmiş olan fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-145">You'll notice that the app itself is instrumented with Mobile Engagement.</span></span> <span data-ttu-id="c7919-146">Arka uç bağlandıktan sonra uygulamayı açmak gibi bu nedenle, kullanıcı oturumu, etkinlikleri, olayları ve benzeri görmek kullanabileceksiniz **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c7919-146">Therefore, as you open the app after connecting it to the back end, you'll be able to see the user session, activities, events, and so on, on the **Monitor** tab.</span></span>
* <span data-ttu-id="c7919-147">Yerel bildirimler kullanmak yerine kendi Mobile Engagement örneğinden bu uygulamaya bildirimleri gönderebilmesi için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c7919-147">You'll also be able to send notifications to this app from your own Mobile Engagement instance, instead of using local notifications.</span></span>
  
  * <span data-ttu-id="c7919-148">Bir test cihazı kullanarak Cihazınızı buraya ekleyebilirsiniz **cihaz Kimliğinizi alma** menü öğesi için uygulama.</span><span class="sxs-lookup"><span data-stu-id="c7919-148">Here you can add your device as a test device by using the **Get the Device ID** menu item in the app.</span></span> <span data-ttu-id="c7919-149">Bu platform arka uç örneğinizle ardından bir test cihazı kaydetmek bir cihaz kimliği verir.</span><span class="sxs-lookup"><span data-stu-id="c7919-149">This gives you a device ID that you then register as a test device with your platform back-end instance.</span></span>
    
    ![Windows aygıt kimliği][7]
    
    <span data-ttu-id="c7919-151">![İOS cihaz kimliği][8]
    ![Android cihaz kimliği][9]</span><span class="sxs-lookup"><span data-stu-id="c7919-151">![Device ID on iOS][8]
![Device ID on Android][9]</span></span>

## <a name="key-features-of-the-demo-app"></a><span data-ttu-id="c7919-152">Tanıtım uygulamasını temel özellikleri</span><span class="sxs-lookup"><span data-stu-id="c7919-152">Key features of the demo app</span></span>
* <span data-ttu-id="c7919-153">Bu uygulama ile daha önce belirtildiği gibi anahtar tüm kaynakları el ile Mobile Engagement için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c7919-153">As mentioned earlier, with this app, you have all the key resources for Mobile Engagement in your hand.</span></span> <span data-ttu-id="c7919-154">Soldaki menüden bağlantılar aracılığıyla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-154">You can go through the links on the left menu.</span></span>
* <span data-ttu-id="c7919-155">Her platform için uygulama bildirimler yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-155">You can experience out-of-app notifications for each platform.</span></span> <span data-ttu-id="c7919-156">Bu bildirimler olarak teslim edilebilir **yalnızca bildirim**, burada bildirim tıklatılması yalnızca yerel bir uygulama ekran yukarı açar (kullanarak **derin bağlama**)--ya da farklı bir **Web duyuru**, bildirim tıklatıldığında görüntülenecek Mobile Engagement arka uçtan ek HTML içeriğini sağlayabileceğiniz burada.</span><span class="sxs-lookup"><span data-stu-id="c7919-156">These notifications can be delivered as **Notification only**, where clicking the notification simply opens up a native screen of the application (by using **deep linking**)--or as a **Web announcement**, where you can deliver additional HTML content from the Mobile Engagement back end to be displayed when the notification is clicked.</span></span>
  
    ![App bildirimler][29]
* <span data-ttu-id="c7919-158">İOS, uygulama ya da sistem anında iletme bildirimleri görmek için uygulamaya kapatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7919-158">On iOS, you have to close the app to see the out-of-app or system push notifications.</span></span> <span data-ttu-id="c7919-159">Uygulama ekleme burada bakabilir **eylem düğmeleri**, ister için bu uygulama bildirimi eklenen olanları *geri bildirim* ve *paylaşımı* (Kullanıcı bildirim sağ eylemden yararlanabilmeniz).</span><span class="sxs-lookup"><span data-stu-id="c7919-159">You can look at the implementation here for adding **Action buttons**, like the ones that are added to this out-of-app notification for *Feedback* and *Share* (so that the user can take action right from the notification itself).</span></span>
  
    ![İOS uygulama bildirimler][11] ![İOS uygulama bildirim görüntüleme][14]
* <span data-ttu-id="c7919-162">Android, desteklenen seçenekler çok satırlı metin eklemekte olduğunuz (**büyük metin**) veya bir bildirim görüntüsü (**büyük resmi**) için bildirimi ile birlikte **eylem düğmeleri** (iOS tarafından desteklenen gibi).</span><span class="sxs-lookup"><span data-stu-id="c7919-162">On Android, the options that are supported are adding multiline text (**Big Text**) or a notification image (**Big Picture**) to the notification, along with the **Action buttons** (as supported by iOS).</span></span>
  
    ![Android uygulama bildirimlerini][12] ![Android uygulama bildirim ekranı][15]
* <span data-ttu-id="c7919-165">Windows 10'bildirimleri PC'de nasıl göründüğünü görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-165">On Windows 10, you can see how the notifications look on the PC.</span></span> <span data-ttu-id="c7919-166">Bu bildirim ayrıca Windows 10 görüntülenir **bildirim Merkezi**.</span><span class="sxs-lookup"><span data-stu-id="c7919-166">This notification also shows up in the Windows 10 **Notification Center**.</span></span> <span data-ttu-id="c7919-167">Ekleme desteği yoktur **eylem düğmeleri** Windows SDK'sındaki anda.</span><span class="sxs-lookup"><span data-stu-id="c7919-167">There is no support for adding **Action buttons** at the moment in the Windows SDK.</span></span>
  
    ![Windows uygulama bildirimler][10] ![Windows uygulama görüntüleme][13]
* <span data-ttu-id="c7919-170">Her platform için varsayılan "uygulama" bildirimleri yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-170">You can experience default "in-app" notifications for each platform.</span></span> <span data-ttu-id="c7919-171">Bu iki adımlı bir deneyimdir burada bir **bildirim** penceresi ilk görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c7919-171">This is a two-step experience where a **Notification** window is displayed first.</span></span> <span data-ttu-id="c7919-172">Tıklattığınızda, bir tam ekran yukarı açılır **duyuru**, aşağıdaki ekran görüntüsünde gösterildiği.</span><span class="sxs-lookup"><span data-stu-id="c7919-172">When you click it, it opens up a full screen **Announcement**, as displayed in the following screenshot.</span></span> <span data-ttu-id="c7919-173">Bu Duyurunun içeriğini, Mobile Engagement arka uç örneğinden gelir.</span><span class="sxs-lookup"><span data-stu-id="c7919-173">The content of this announcement comes from your Mobile Engagement back-end instance.</span></span> <span data-ttu-id="c7919-174">SDK bildirimler ve duyuruları için şablon yok.</span><span class="sxs-lookup"><span data-stu-id="c7919-174">The SDK has the templates for both notifications and announcements.</span></span> <span data-ttu-id="c7919-175">Bunları, bizim logo ve renklendirme olan bu tanıtım uygulamasını gösterildiği gibi kolaylıkla özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-175">You can easily customize them, as shown in this demo app with the addition of our logo and coloring.</span></span>  
  
    ![Windows uygulama bildirimleri][16]
  
    ![İOS uygulama bildirimleri][17]  ![Android'daki uygulama bildirimleri][18]
  
    <span data-ttu-id="c7919-179">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="c7919-179">**iOS**, **Android**</span></span>
* <span data-ttu-id="c7919-180">Aynı zamanda **kategori** Mobile Engagement'ın bu varsayılan deneyimini özelleştirmek özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="c7919-180">You can also use the **Category** feature of Mobile Engagement to customize this default experience.</span></span> <span data-ttu-id="c7919-181">Tanıtım uygulamasını biz bildirimler deneyimini değiştirmek için iki genel yolu gösterilen.</span><span class="sxs-lookup"><span data-stu-id="c7919-181">In the demo app, we've demonstrated two common ways to change the experience of the notifications.</span></span> <span data-ttu-id="c7919-182">Kategori özelliği Windows SDK'ın henüz desteklenmiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c7919-182">Note that the Category feature is not yet supported in the Windows SDK.</span></span>
  
    <span data-ttu-id="c7919-183">**Tam ekran Interstitial:**</span><span class="sxs-lookup"><span data-stu-id="c7919-183">**Full-screen interstitial:**</span></span>
  
    ![Uygulama içi bildirim - Interstitial kategorisi][30]
  
    ![İOS Interstitial kategorisi][21]     ![Android'de Interstitial kategorisi][22]
  
    <span data-ttu-id="c7919-187">**Açılır bildirimi:**</span><span class="sxs-lookup"><span data-stu-id="c7919-187">**Pop-up notification:**</span></span>
  
    ![Uygulama içi bildirim - açılır kategorisi][31]
  
    ![İOS açılır bildirim][19]    ![Android açılır bildirimi][20]

<span data-ttu-id="c7919-191">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="c7919-191">**iOS**, **Android**</span></span>

* <span data-ttu-id="c7919-192">Mobile Engagement Ayrıca, uygulama içi bildirim olarak adlandırılan uzmanlaşmış bir türü destekler **yoklamalar**.</span><span class="sxs-lookup"><span data-stu-id="c7919-192">Mobile Engagement also supports a specialized type of in-app notification called **Polls**.</span></span> <span data-ttu-id="c7919-193">Bu bölümlenmiş uygulama kullanıcılarınıza hızlı anketler göndermenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7919-193">This allows you to send out quick surveys to your segmented app users.</span></span> <span data-ttu-id="c7919-194">Sorular ve aşağıdaki ekran görüntüsünde olduğu gibi her bir soru için seçenekleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7919-194">You can add questions and options for each question as in the following screenshot.</span></span> <span data-ttu-id="c7919-195">Bu daha sonra uygulama kullanıcıya bir uygulama bildirimi görüntülendiğini.</span><span class="sxs-lookup"><span data-stu-id="c7919-195">This will then get displayed as an in-app notification to the app user.</span></span>   
  
    ![Yoklama bildirimleri][32]
  
    ![Windows'da anket][26]
  
    ![İos'ta anket][27]   ![Android'de anket][28]

<span data-ttu-id="c7919-200">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="c7919-200">**iOS**, **Android**</span></span>

* <span data-ttu-id="c7919-201">Mobile Engagement ayrıca destekler sessiz gönderme **veri gönderme** bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="c7919-201">Mobile Engagement also supports sending silent **Data Push** notifications.</span></span> <span data-ttu-id="c7919-202">Bu bildirimler ile (örneğin, JSON verilerini aşağıdaki örnekte) hizmetinizden veri gönderebilir uygulamanızda işlemek ve bazı adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c7919-202">With these notifications, you can send data from your service (like the JSON data in the following example), which you can handle in your app and take some action.</span></span> <span data-ttu-id="c7919-203">Nasıl biz öğeyi fiyat seçmeli olarak veri anında iletme bildirimleri kullanarak değiştirirsiniz bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="c7919-203">An example is how we're changing the price of an item selectively by using data push notifications.</span></span>
  
    ![Veri anında iletme bildirimi][33]
  
    ![Windows üzerinde veri anında iletme bildirimi][23]
  
    ![İOS veri anında iletme bildirimi][24]  ![Android veri anında iletme bildirimi][25]

<span data-ttu-id="c7919-208">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="c7919-208">**iOS**, **Android**</span></span>

> [!NOTE]
> <span data-ttu-id="c7919-209">Ayrıntılı adım adım yönergeler için bu bildirimler hiçbirini tıklatarak görüntüleyebileceğiniz **Mobile Engagement platformundan bu bildirimleri göndermek yönergeler için buraya tıklayın** herhangi örnek bildirim ekranında.</span><span class="sxs-lookup"><span data-stu-id="c7919-209">You can view detailed step-by-step instructions for any of these notifications by clicking **Click here for instructions on how to send these notifications from Mobile Engagement platform** on any sample notification screen.</span></span>
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
