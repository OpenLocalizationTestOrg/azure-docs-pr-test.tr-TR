---
title: "aaaAzure Mobile Engagement tanıtım uygulamasını | Microsoft Docs"
description: "Nerede tanımlar toodownload, nasıl toouse ve Azure Mobile Engagement kullanmanın yararları hello uygulama gösteri"
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
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a><span data-ttu-id="68b75-103">Azure Mobile Engagement tanıtım uygulamasını</span><span class="sxs-lookup"><span data-stu-id="68b75-103">Azure Mobile Engagement demo app</span></span>
<span data-ttu-id="68b75-104">Bir Azure Mobile Engagement tanıtım uygulamasını için yayımlanan **iOS**, **Android**, ve **Windows** platformları toohelp, toofind kullanışlı kaynaklar ve mobil hakkında daha fazla bilgi edinin Katılım.</span><span class="sxs-lookup"><span data-stu-id="68b75-104">We've published an Azure Mobile Engagement demo app for **iOS**, **Android**, and **Windows** platforms toohelp you toofind useful resources and learn more about Mobile Engagement.</span></span>

<span data-ttu-id="68b75-105">Merhaba uygulaması size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="68b75-105">hello app helps you to:</span></span>

* <span data-ttu-id="68b75-106">Yararlı bağlantılar videoları, belgeleri, hello Destek Forumu gibi tooMobile katılım kaynaklarını kolayca bulmak ve burada toogo tooraise özelliği ister.</span><span class="sxs-lookup"><span data-stu-id="68b75-106">Easily find useful links tooMobile Engagement resources like videos, documentation, hello support forum, and where toogo tooraise feature requests.</span></span>
* <span data-ttu-id="68b75-107">Mobile Engagement tooget fikir mobil uygulamalarınız için tarafından desteklenen deneyimi örnek bildirimler.</span><span class="sxs-lookup"><span data-stu-id="68b75-107">Experience sample notifications that are supported by Mobile Engagement tooget ideas for your own mobile applications.</span></span>
* <span data-ttu-id="68b75-108">Bir başvuru uygulaması toostudy kullanma tooimplement Mobile Engagement kendi uygulamada.</span><span class="sxs-lookup"><span data-stu-id="68b75-108">Use a reference implementation toostudy how tooimplement Mobile Engagement into your own app.</span></span> <span data-ttu-id="68b75-109">İçin bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="68b75-109">You can learn to:</span></span>
  
  * <span data-ttu-id="68b75-110">Analytics veri toplar.</span><span class="sxs-lookup"><span data-stu-id="68b75-110">Collect analytics data.</span></span>
  * <span data-ttu-id="68b75-111">Uygulama bildirimi senaryolarını türleri gibi gelişmiş *tam ekran Interstitial* veya *açılır*.</span><span class="sxs-lookup"><span data-stu-id="68b75-111">Implement advanced notification scenarios of types such as *Full-screen interstitial* or *Pop-up*.</span></span>
  * <span data-ttu-id="68b75-112">Anketler ve anketler uygular.</span><span class="sxs-lookup"><span data-stu-id="68b75-112">Implement surveys and polls.</span></span>
  * <span data-ttu-id="68b75-113">Sessiz anında veri ve itme senaryolarında uygulayın.</span><span class="sxs-lookup"><span data-stu-id="68b75-113">Implement silent push data and push scenarios.</span></span>   

## <a name="app-installation"></a><span data-ttu-id="68b75-114">Uygulama yükleme</span><span class="sxs-lookup"><span data-stu-id="68b75-114">App installation</span></span>
<span data-ttu-id="68b75-115">Bu uygulama, uygulama mağazaları aşağıdaki hello edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="68b75-115">This app is available in hello following app stores:</span></span>

* <span data-ttu-id="68b75-116">**Windows Evrensel tanıtım uygulamasını**:</span><span class="sxs-lookup"><span data-stu-id="68b75-116">**Windows Universal demo app**:</span></span>
  
  * <span data-ttu-id="68b75-117">Merhaba Hello uygulamaya karşıdan [Windows uygulama mağazası](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span><span class="sxs-lookup"><span data-stu-id="68b75-117">Download hello app at hello [Windows App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).</span></span>
  * <span data-ttu-id="68b75-118">Merhaba uygulama Windows 10 Universal bir uygulama olarak geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="68b75-118">hello app was developed as a Windows 10 Universal app.</span></span> <span data-ttu-id="68b75-119">Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span><span class="sxs-lookup"><span data-stu-id="68b75-119">hello source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).</span></span>
* <span data-ttu-id="68b75-120">**iOS uygulama gösteri**:</span><span class="sxs-lookup"><span data-stu-id="68b75-120">**iOS demo app**:</span></span>
  
  * <span data-ttu-id="68b75-121">Merhaba Hello uygulamaya karşıdan [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span><span class="sxs-lookup"><span data-stu-id="68b75-121">Download hello app at hello [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).</span></span>
  * <span data-ttu-id="68b75-122">Merhaba uygulama iOS Swift geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="68b75-122">hello app was developed in iOS Swift.</span></span> <span data-ttu-id="68b75-123">Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span><span class="sxs-lookup"><span data-stu-id="68b75-123">hello source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).</span></span>
* <span data-ttu-id="68b75-124">**Android tanıtım uygulamasını**:</span><span class="sxs-lookup"><span data-stu-id="68b75-124">**Android demo app**:</span></span>
  
  * <span data-ttu-id="68b75-125">Merhaba Hello uygulamaya karşıdan [Google Play mağazasına](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span><span class="sxs-lookup"><span data-stu-id="68b75-125">Download hello app at hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).</span></span>
  * <span data-ttu-id="68b75-126">Merhaba kaynak kodu edinilebilir [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span><span class="sxs-lookup"><span data-stu-id="68b75-126">hello source code is available on [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).</span></span>

![Windows Evrensel tanıtım uygulamasını][1]

<span data-ttu-id="68b75-128">![iOS uygulama gösteri][2]
![Android tanıtım uygulamasını][3]</span><span class="sxs-lookup"><span data-stu-id="68b75-128">![iOS demo app][2]
![Android demo app][3]</span></span>

## <a name="usage"></a><span data-ttu-id="68b75-129">Kullanım</span><span class="sxs-lookup"><span data-stu-id="68b75-129">Usage</span></span>
<span data-ttu-id="68b75-130">Bu uygulama yolu şu hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="68b75-130">You can use this app in hello following ways:</span></span>

<span data-ttu-id="68b75-131">**(Daha önce sağlanan) hello uygulama mağazası bağlantıları Cihazınızda Hello uygulamasını yükleyin:**</span><span class="sxs-lookup"><span data-stu-id="68b75-131">**Download hello app on your device from hello application store links (provided earlier):**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68b75-132">Bir Azure hesabı gerekmez veya tooconnect hello uygulama tooa arka uç.</span><span class="sxs-lookup"><span data-stu-id="68b75-132">You don't need an Azure account or need tooconnect hello app tooa back end.</span></span> <span data-ttu-id="68b75-133">Merhaba uygulaması bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="68b75-133">hello app works independently.</span></span>
> 
> 

* <span data-ttu-id="68b75-134">Cihazınızda hello uygulamanız sonra hello sol taraftaki menü toofind hello kullanışlı kaynaklar hakkında Mobile Engagement hello bağlantılar yoluyla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-134">After you have hello app on your device, then you can go through hello links in hello left-side menu toofind hello useful resources about Mobile Engagement.</span></span>
* <span data-ttu-id="68b75-135">Merhaba ekledik [hizmetin RSS akışı](https://aka.ms/azmerssfeed) bu uygulamaya böylece her zaman hello en son ürün güncelleştirmelerini hakkında güncelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="68b75-135">We've added hello [service's RSS feed](https://aka.ms/azmerssfeed) into this application so that you're always updated about hello latest product updates.</span></span>
* <span data-ttu-id="68b75-136">Mobile Engagement tarafından desteklenen her platform için bildirimler hello örnek bildirim senaryoları tooexperience hello türü aracılığıyla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-136">You can also go through hello sample notification scenarios tooexperience hello type of notifications that are supported by Mobile Engagement for each platform.</span></span> <span data-ttu-id="68b75-137">Bu bildirimler olabilir deneyimli yerel olarak--diğer bir deyişle, tıklayabilirsiniz hello ekranlar tooshow hello düğmeleri, aynı toosending hello bildirimleri hello Mobile Engagement platformu olan bildirimler deneyimini hello.</span><span class="sxs-lookup"><span data-stu-id="68b75-137">These notifications can be experienced locally--that is, you can click hello buttons on hello screens tooshow you hello notifications experience, which is identical toosending hello notifications from hello Mobile Engagement platform.</span></span>

![Windows için uygulama menüsü][4]

<span data-ttu-id="68b75-139">![İOS için uygulama menüsünden][5]
![Android için uygulama menüsü][6]</span><span class="sxs-lookup"><span data-stu-id="68b75-139">![App menu for iOS][5]
![App menu for Android][6]</span></span>

<span data-ttu-id="68b75-140">**Merhaba kaynak kodu (daha önce sağlanan) GitHub bağlantılarını hello yükleyin:**</span><span class="sxs-lookup"><span data-stu-id="68b75-140">**Download hello source code from hello GitHub links (provided earlier):**</span></span>

* <span data-ttu-id="68b75-141">Merhaba kaynak kodu indirdikten sonra hello ilgili geliştirme ortamında--XCode iOS, Android ve Windows için Visual Studio için Android Studio açın.</span><span class="sxs-lookup"><span data-stu-id="68b75-141">After you've downloaded hello source code, open it in hello respective development environment--XCode for iOS, Android Studio for Android, and Visual Studio for Windows.</span></span>
* <span data-ttu-id="68b75-142">Sonraki izlemeniz gereken bizim [Temel SDK tümleştirme adımları](mobile-engagement-windows-store-dotnet-get-started.md) mümkün tooconnect kodlarla bu uygulama tooits kendi Mobile Engagement arka uç örneği.</span><span class="sxs-lookup"><span data-stu-id="68b75-142">You should next follow our [basic SDK integration steps](mobile-engagement-windows-store-dotnet-get-started.md) so that you're able tooconnect this app tooits own Mobile Engagement back-end instance.</span></span>
  * <span data-ttu-id="68b75-143">Tooconfigure hello uygulamasında bir bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="68b75-143">You need tooconfigure a connection string in hello app.</span></span>
  * <span data-ttu-id="68b75-144">Ayrıca tooconfigure hello anında iletme bildirimi platform uygulamanız için gerekir.</span><span class="sxs-lookup"><span data-stu-id="68b75-144">You also need tooconfigure hello push notification platform for your app.</span></span>
* <span data-ttu-id="68b75-145">Bu hello uygulaması ile Mobile Engagement izlenmiş olan fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-145">You'll notice that hello app itself is instrumented with Mobile Engagement.</span></span> <span data-ttu-id="68b75-146">Toohello arka uç bağlandıktan sonra hello uygulamasını açın, bu nedenle, hello üzerinde mümkün toosee hello kullanıcı oturumunu, etkinlikleri, olayları vb. olması **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="68b75-146">Therefore, as you open hello app after connecting it toohello back end, you'll be able toosee hello user session, activities, events, and so on, on hello **Monitor** tab.</span></span>
* <span data-ttu-id="68b75-147">Yerel bildirimler kullanmak yerine kendi Mobile Engagement örneğinden mümkün toosend bildirimleri toothis uygulama de.</span><span class="sxs-lookup"><span data-stu-id="68b75-147">You'll also be able toosend notifications toothis app from your own Mobile Engagement instance, instead of using local notifications.</span></span>
  
  * <span data-ttu-id="68b75-148">Bir test cihazı hello kullanarak Cihazınızı buraya ekleyebilirsiniz **Get hello cihaz kimliği** hello uygulamasında menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="68b75-148">Here you can add your device as a test device by using hello **Get hello Device ID** menu item in hello app.</span></span> <span data-ttu-id="68b75-149">Bu platform arka uç örneğinizle ardından bir test cihazı kaydetmek bir cihaz kimliği verir.</span><span class="sxs-lookup"><span data-stu-id="68b75-149">This gives you a device ID that you then register as a test device with your platform back-end instance.</span></span>
    
    ![Windows aygıt kimliği][7]
    
    <span data-ttu-id="68b75-151">![İOS cihaz kimliği][8]
    ![Android cihaz kimliği][9]</span><span class="sxs-lookup"><span data-stu-id="68b75-151">![Device ID on iOS][8]
![Device ID on Android][9]</span></span>

## <a name="key-features-of-hello-demo-app"></a><span data-ttu-id="68b75-152">Merhaba tanıtım uygulamasını temel özellikleri</span><span class="sxs-lookup"><span data-stu-id="68b75-152">Key features of hello demo app</span></span>
* <span data-ttu-id="68b75-153">Bu uygulama ile daha önce belirtildiği gibi tüm hello anahtar kaynaklar, el ile Mobile Engagement için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="68b75-153">As mentioned earlier, with this app, you have all hello key resources for Mobile Engagement in your hand.</span></span> <span data-ttu-id="68b75-154">Merhaba soldaki menüden hello bağlantılar aracılığıyla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-154">You can go through hello links on hello left menu.</span></span>
* <span data-ttu-id="68b75-155">Her platform için uygulama bildirimler yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-155">You can experience out-of-app notifications for each platform.</span></span> <span data-ttu-id="68b75-156">Bu bildirimler olarak teslim edilebilir **yalnızca bildirim**, burada hello bildirim tıklatılması yalnızca yerel bir hello uygulama ekran yukarı açar (kullanarak **derin bağlama**)--ya da farklı bir **Web Duyuru**, burada, ek HTML içeriğini Mobile Engagement bitiş hello hello bildirim tıklatıldığında görüntülenen toobe sunabilir.</span><span class="sxs-lookup"><span data-stu-id="68b75-156">These notifications can be delivered as **Notification only**, where clicking hello notification simply opens up a native screen of hello application (by using **deep linking**)--or as a **Web announcement**, where you can deliver additional HTML content from hello Mobile Engagement back end toobe displayed when hello notification is clicked.</span></span>
  
    ![App bildirimler][29]
* <span data-ttu-id="68b75-158">İos'ta, tooclose hello uygulama toosee hello uygulama ya da sistem anında iletme bildirimleri sahip.</span><span class="sxs-lookup"><span data-stu-id="68b75-158">On iOS, you have tooclose hello app toosee hello out-of-app or system push notifications.</span></span> <span data-ttu-id="68b75-159">Eklemek için buraya hello uygulama bakabilir **eylem düğmeleri**uygulama bildirim için eklenen toothis olan olanları hello gibi *geri bildirim* ve *paylaşımı* (böylece "Hello kullanıcı hello bildirim kendisini eylem sağdan sürebilir).</span><span class="sxs-lookup"><span data-stu-id="68b75-159">You can look at hello implementation here for adding **Action buttons**, like hello ones that are added toothis out-of-app notification for *Feedback* and *Share* (so that hello user can take action right from hello notification itself).</span></span>
  
    ![İOS uygulama bildirimler][11] ![İOS uygulama bildirim görüntüleme][14]
* <span data-ttu-id="68b75-162">Android, desteklenen hello seçenekleri çok satırlı metin eklemekte olduğunuz (**büyük metin**) veya bir bildirim görüntüsü (**büyük resmi**) hello birlikte toohello bildirim **eylem düğmeleri** (iOS tarafından desteklenen gibi).</span><span class="sxs-lookup"><span data-stu-id="68b75-162">On Android, hello options that are supported are adding multiline text (**Big Text**) or a notification image (**Big Picture**) toohello notification, along with hello **Action buttons** (as supported by iOS).</span></span>
  
    ![Android uygulama bildirimlerini][12] ![Android uygulama bildirim ekranı][15]
* <span data-ttu-id="68b75-165">Windows 10'hello bildirimleri PC hello üzerinde nasıl göründüğünü görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-165">On Windows 10, you can see how hello notifications look on hello PC.</span></span> <span data-ttu-id="68b75-166">Bu bildirim ayrıca hello Windows 10 görüntülenir **bildirim Merkezi**.</span><span class="sxs-lookup"><span data-stu-id="68b75-166">This notification also shows up in hello Windows 10 **Notification Center**.</span></span> <span data-ttu-id="68b75-167">Ekleme desteği yoktur **eylem düğmeleri** hello anda hello Windows SDK.</span><span class="sxs-lookup"><span data-stu-id="68b75-167">There is no support for adding **Action buttons** at hello moment in hello Windows SDK.</span></span>
  
    ![Windows uygulama bildirimler][10] ![Windows uygulama görüntüleme][13]
* <span data-ttu-id="68b75-170">Her platform için varsayılan "uygulama" bildirimleri yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-170">You can experience default "in-app" notifications for each platform.</span></span> <span data-ttu-id="68b75-171">Bu iki adımlı bir deneyimdir burada bir **bildirim** penceresi ilk görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="68b75-171">This is a two-step experience where a **Notification** window is displayed first.</span></span> <span data-ttu-id="68b75-172">Tıklattığınızda, bir tam ekran yukarı açılır **duyuru**, ekran aşağıdaki hello görüntülendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="68b75-172">When you click it, it opens up a full screen **Announcement**, as displayed in hello following screenshot.</span></span> <span data-ttu-id="68b75-173">Bu duyuru Merhaba içeriğine, Mobile Engagement arka uç örneğinden gelir.</span><span class="sxs-lookup"><span data-stu-id="68b75-173">hello content of this announcement comes from your Mobile Engagement back-end instance.</span></span> <span data-ttu-id="68b75-174">Merhaba SDK bildirimler ve duyuruları için hello şablon yok.</span><span class="sxs-lookup"><span data-stu-id="68b75-174">hello SDK has hello templates for both notifications and announcements.</span></span> <span data-ttu-id="68b75-175">Bunları, hello ayrıca bizim logo ve renklendirme olan bu tanıtım uygulamasını gösterildiği gibi kolaylıkla özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-175">You can easily customize them, as shown in this demo app with hello addition of our logo and coloring.</span></span>  
  
    ![Windows uygulama bildirimleri][16]
  
    ![İOS uygulama bildirimleri][17]  ![Android'daki uygulama bildirimleri][18]
  
    <span data-ttu-id="68b75-179">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="68b75-179">**iOS**, **Android**</span></span>
* <span data-ttu-id="68b75-180">Merhaba de kullanabilirsiniz **kategori** Mobile Engagement toocustomize özelliği bu varsayılan deneyimi.</span><span class="sxs-lookup"><span data-stu-id="68b75-180">You can also use hello **Category** feature of Mobile Engagement toocustomize this default experience.</span></span> <span data-ttu-id="68b75-181">Hello demo uygulamada, biz iki genel yolu toochange hello deneyimi hello bildirimler gösterilen.</span><span class="sxs-lookup"><span data-stu-id="68b75-181">In hello demo app, we've demonstrated two common ways toochange hello experience of hello notifications.</span></span> <span data-ttu-id="68b75-182">Merhaba kategori özellik hello Windows SDK henüz desteklenmeyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68b75-182">Note that hello Category feature is not yet supported in hello Windows SDK.</span></span>
  
    <span data-ttu-id="68b75-183">**Tam ekran Interstitial:**</span><span class="sxs-lookup"><span data-stu-id="68b75-183">**Full-screen interstitial:**</span></span>
  
    ![Uygulama içi bildirim - Interstitial kategorisi][30]
  
    ![İOS Interstitial kategorisi][21]     ![Android'de Interstitial kategorisi][22]
  
    <span data-ttu-id="68b75-187">**Açılır bildirimi:**</span><span class="sxs-lookup"><span data-stu-id="68b75-187">**Pop-up notification:**</span></span>
  
    ![Uygulama içi bildirim - açılır kategorisi][31]
  
    ![İOS açılır bildirim][19]    ![Android açılır bildirimi][20]

<span data-ttu-id="68b75-191">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="68b75-191">**iOS**, **Android**</span></span>

* <span data-ttu-id="68b75-192">Mobile Engagement Ayrıca, uygulama içi bildirim olarak adlandırılan uzmanlaşmış bir türü destekler **yoklamalar**.</span><span class="sxs-lookup"><span data-stu-id="68b75-192">Mobile Engagement also supports a specialized type of in-app notification called **Polls**.</span></span> <span data-ttu-id="68b75-193">Bu, hızlı anketler kesimli tooyour uygulama kullanıcılarınızın çıkışı toosend sağlar.</span><span class="sxs-lookup"><span data-stu-id="68b75-193">This allows you toosend out quick surveys tooyour segmented app users.</span></span> <span data-ttu-id="68b75-194">Sorular ve ekran aşağıdaki hello olduğu gibi her bir soru için seçenekleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68b75-194">You can add questions and options for each question as in hello following screenshot.</span></span> <span data-ttu-id="68b75-195">Bu daha sonra bir uygulama içi bildirim toohello uygulama kullanıcısı olarak görüntülenen.</span><span class="sxs-lookup"><span data-stu-id="68b75-195">This will then get displayed as an in-app notification toohello app user.</span></span>   
  
    ![Yoklama bildirimleri][32]
  
    ![Windows'da anket][26]
  
    ![İos'ta anket][27]   ![Android'de anket][28]

<span data-ttu-id="68b75-200">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="68b75-200">**iOS**, **Android**</span></span>

* <span data-ttu-id="68b75-201">Mobile Engagement ayrıca destekler sessiz gönderme **veri gönderme** bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="68b75-201">Mobile Engagement also supports sending silent **Data Push** notifications.</span></span> <span data-ttu-id="68b75-202">Bu bildirimler ile hizmetinizden (gibi hello JSON verileri aşağıdaki örneğine hello), veri gönderebilir uygulamanızda işlemek ve bazı adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="68b75-202">With these notifications, you can send data from your service (like hello JSON data in hello following example), which you can handle in your app and take some action.</span></span> <span data-ttu-id="68b75-203">Nasıl biz hello fiyat öğenin seçmeli olarak veri anında iletme bildirimleri kullanarak değiştirirsiniz bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="68b75-203">An example is how we're changing hello price of an item selectively by using data push notifications.</span></span>
  
    ![Veri anında iletme bildirimi][33]
  
    ![Windows üzerinde veri anında iletme bildirimi][23]
  
    ![İOS veri anında iletme bildirimi][24]  ![Android veri anında iletme bildirimi][25]

<span data-ttu-id="68b75-208">**iOS**, **Android**</span><span class="sxs-lookup"><span data-stu-id="68b75-208">**iOS**, **Android**</span></span>

> [!NOTE]
> <span data-ttu-id="68b75-209">Ayrıntılı adım adım yönergeler için bu bildirimler hiçbirini tıklatarak görüntüleyebileceğiniz **hakkında yönergeler için buraya tıklayın toosend Mobile Engagement platformu Bu bildirimler** herhangi örnek bildirim ekranında.</span><span class="sxs-lookup"><span data-stu-id="68b75-209">You can view detailed step-by-step instructions for any of these notifications by clicking **Click here for instructions on how toosend these notifications from Mobile Engagement platform** on any sample notification screen.</span></span>
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
