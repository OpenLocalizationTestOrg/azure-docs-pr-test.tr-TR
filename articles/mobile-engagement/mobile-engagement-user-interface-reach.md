---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - ulaşma"
description: "Bilgi nasıl Azure Mobile Engagement kullanarak anında iletme bildirimleri ile uygulamanızın toohello kullanıcıları çıkışı tooreach"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="d848e-103">Nasıl tooreach toohello kullanıcılara anında iletme bildirimleri ile uygulamanızın çıkışı</span><span class="sxs-lookup"><span data-stu-id="d848e-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="d848e-104">Bu makalede hello **ULAŞMAK** hello sekmesinde **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="d848e-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="d848e-105">Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin.</span><span class="sxs-lookup"><span data-stu-id="d848e-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="d848e-106">İlk ihtiyacınız toocreate hello portalını kullanarak bu toostart Not bir **Azure Mobile Engagement** hesabı.</span><span class="sxs-lookup"><span data-stu-id="d848e-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="d848e-107">Daha fazla bilgi için bkz: [bir Azure Mobile Engagement hesabı oluşturma](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="d848e-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="d848e-108">Merhaba UI hello bölümünü hello itme kampanya yönetim aracı oluşturma/düzenleme/etkinleştirmek/bitiş/İzleyici yapabileceğiniz ulaşmak ve anında iletme bildirimi kampanyaları ve ayrıca hello Reach API'sini (ve bazı öğelerini hello düşük erişilebilen özelliklere istatistikleri almak Düzey itme API).</span><span class="sxs-lookup"><span data-stu-id="d848e-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="d848e-109">Merhaba API'leri veya hello UI kullanıp kullanmadığınızı toointegrate gerekeceğini unutmayın Azure Mobile Engagement ve Reach hello kullanabilmeniz için önce SDK ile her platform için uygulamanıza Reach kampanyaları.</span><span class="sxs-lookup"><span data-stu-id="d848e-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="d848e-110">Merhaba birçok bölümlerini **Mobile Engagement** portal UI içeren hello **YARDIMINI Göster** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d848e-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="d848e-111">Bu düğme tooget bir bölümü hakkında daha fazla kavramsal bilgi tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="d848e-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="d848e-112">Dört tür anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d848e-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="d848e-113">Duyurular - uygulamanızı veya toosend içinde tooanother konum yönlendirmek toosend reklam iletileri toousers izin bunları tooa Web sayfası veya mağaza uygulamanızı dışında.</span><span class="sxs-lookup"><span data-stu-id="d848e-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="d848e-114">Anketler - izin, son kullanıcılardan toogather bilgi sorular sorarak.</span><span class="sxs-lookup"><span data-stu-id="d848e-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="d848e-115">Veri gönderimleri - toosend bir ikili veya base64 veri dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="d848e-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="d848e-116">Veri gönderiminde yer alan hello bilgileri tooyour uygulama toomodify kullanıcılarınızın geçerli deneyimi uygulamanızda gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="d848e-117">Veri gönderimi toobe mümkün tooprocess hello verileri uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d848e-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="d848e-118">Kampanya ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d848e-118">Campaign Details</span></span>
<span data-ttu-id="d848e-119">Düzenleme, kopyalama, silme veya henüz adlarını gelerek etkinleştirilmedi Kampanyalar etkinleştirmek veya tooopen tıklatabilirsiniz bunları.</span><span class="sxs-lookup"><span data-stu-id="d848e-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="d848e-120">Adlarını gelerek zaten etkinleştirilmiş Kampanyalar kopyalayabilir veya tooopen tıklatabilirsiniz bunları.</span><span class="sxs-lookup"><span data-stu-id="d848e-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="d848e-121">Ancak, etkinleştirildikten sonra bir kampanya değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d848e-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="d848e-123">Geri bildirim ulaşmak</span><span class="sxs-lookup"><span data-stu-id="d848e-123">Reach Feedback</span></span>
<span data-ttu-id="d848e-124">Tıklayın **istatistikleri** Reach kampanya toosee hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="d848e-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="d848e-125">Merhaba **basit** hello biçiminde bir kampanyanın etkinleştirildiği sonra ne hakkında bir sütun çubuk grafik görsel bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="d848e-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="d848e-126">Merhaba **Gelişmiş** görünümü hello itme kampanyayla ilgili daha ayrıntılı ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d848e-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="d848e-127">Bir test kampanya bir itme gönderilen tooa test cihazı yani gönderiyorsanız, bu ayrıntıları kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="d848e-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="d848e-128">Bu ayrıntılar nasıl yorumlanacağı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d848e-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="d848e-129">**Gönderilen** -bu hello toohello cihazlara gönderilen ileti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d848e-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="d848e-130">Bu sayı hello itme kampanya oluşturulurken belirtilen hello hedef kitle bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d848e-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="d848e-131">Hiçbir hedef kitle belirtmezseniz, bu itme tooall hello kayıtlı cihazlar gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="d848e-132">Diğer tüm itme Hizmetleri gibi biz hello anında iletme bildirimleri değil doğrudan toohello cihazlara ancak bunun yerine bunları toohello ilgili platformun gönderme belirli anında bildirim Hizmetleri (PNS - GCM/APNS/WNS) böylece toohello cihazların Merhaba bildirimleri sunabilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="d848e-133">**Teslim** -bu Mobile Engagement SDK'sı tarafından alınan olarak hello başarıyla hello PNS toohello aygıt tarafından sunulan ve onaylanan ileti sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d848e-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="d848e-134">*Teslim edildi nedenlerle basılmış sayısından daha az olan sayısı:*</span><span class="sxs-lookup"><span data-stu-id="d848e-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="d848e-135">Merhaba kullanıcı hello uygulama hello CİHAZDAN kaldırdı. ancak hello PNS hakkında size hello itme toohello PNS göndereceğiz hello zamanında bilmiyor selamlama iletisine bırakılır.</span><span class="sxs-lookup"><span data-stu-id="d848e-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="d848e-136">Merhaba uygulama Hello aygıt varsa ancak hello aygıtları kendilerini uzun bir süre için çevrimdışı, ardından hello PNS toodeliver hello ileti toohello aygıt başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d848e-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="d848e-137">Merhaba ileti toohello aygıt teslim ancak hello Mobile Engagement SDK'sı hello uygulamasında selamlama iletisine Merhaba içeriğine tanımıyor, sonra bu iletiyi bırakır.</span><span class="sxs-lookup"><span data-stu-id="d848e-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="d848e-138">Merhaba bildirim hello uygulamasında Hello özelleştirmesini hello SDK ve açılan hello iletisinde, biz catch özel durum oluşturursa bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="d848e-139">Bu da hello cihaza hello uygulamanın ise hello platformundan hello mümkün toounderstand hello daha yeni sürümü hello anında iletme iletisi değil Mobile Engagement SDK'ın bir sürümü kullanılarak gönderilen ancak yalnızca hello uygulama hello bildirim sonra yükseltildiğinde bu oluşabilir Merhaba hizmet platformundan gönderildi.</span><span class="sxs-lookup"><span data-stu-id="d848e-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="d848e-140">Merhaba **Gelişmiş** sekmesi, kaç tane iletileri bırakılan olmadığını bildirir.</span><span class="sxs-lookup"><span data-stu-id="d848e-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="d848e-141">İOS cihazlarda iletileri bazen ya da hello cihaz düşük pil gücüyle ise veya hello uygulama güç önemli miktarda uzak bildirimler işlerken kullanıp kullanmadığına teslim.</span><span class="sxs-lookup"><span data-stu-id="d848e-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="d848e-142">Merhaba iOS cihazları kısıtlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d848e-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="d848e-143">**Görüntülenen** -bu hello başarıyla toohello uygulama kullanıcı bir sistem itme/çıkış-in-uygulama bildirimi hello bildirim merkezinde veya bir uygulama bildirimi hello içinde hello biçiminde hello aygıtta Mobil gösterilen iletilerinin sayısını belirtir uygulama.</span><span class="sxs-lookup"><span data-stu-id="d848e-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="d848e-144">Merhaba **Gelişmiş** sekmesini söyleyin, sistem bildirimleri kaç tane ve uygulama içi bildirimler kaç tane.</span><span class="sxs-lookup"><span data-stu-id="d848e-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="d848e-145">*Görüntülenen nedenlerle (bekleme toobe görüntülenen) teslim edildi sayısından daha az olan Say*</span><span class="sxs-lookup"><span data-stu-id="d848e-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="d848e-146">Hello bildirimi kampanyası hello bildirim teslim edildi ancak zaman hello zaman tooopen gelen mümkündür sonra bir bitiş tarihi üzerinde var ve toohello uygulama kullanıcı görüntülemek, hiçbir zaman gösterilen şekilde zaten dolmuştur.</span><span class="sxs-lookup"><span data-stu-id="d848e-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="d848e-147">Ardından Hello bildirim bir uygulama bildirimi ise hello uygulama hello uygulama kullanıcı oturum açtığında hello bildirim yalnızca görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d848e-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="d848e-148">Merhaba uygulama kullanıcı hello uygulama burada açmadığını durumlarda hello SDK hello bildirim teslim ancak hello uygulama açılıncaya kadar henüz görüntülenen rapor eder.</span><span class="sxs-lookup"><span data-stu-id="d848e-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="d848e-149">Merhaba bildirim bir uygulama bildirimi ise ve ayrıca hello bildirim teslim olarak bildirilir sonra belirli bir etkinlik/ekranda gösterilen toobe yapılandırılmış ancak kadar teslim edilmedi hello kullanıcı belirli bir ekranda hello uygulama açar.</span><span class="sxs-lookup"><span data-stu-id="d848e-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="d848e-150">**Kullanıcı etkileşimleri** -bu hello hangi hello uygulama kullanıcı ile etkileşime ve eylem yapılan veya Çıkılan hello iletileri içerecektir iletilerinin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d848e-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="d848e-151">*Merhaba uygulama kullanıcı, yolu izleyerek hello birindeki bir bildirim işlem yapabilir:*</span><span class="sxs-lookup"><span data-stu-id="d848e-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="d848e-152">Merhaba, bir sistem/çıkış-in-uygulama bildirimi bildirimidir veya bir uygulama bildirimi yalnızca bildirim olarak gönderilen sonra hello uygulama kullanıcı hello bildirim.</span><span class="sxs-lookup"><span data-stu-id="d848e-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="d848e-153">Merhaba bildirim metin ya da web görünümü içeren bir uygulama bildirimi ya yoklamalar sonra uygulama kullanıcı hello ise üzerinde hello hello bildirim eylem düğmesine tıklar.</span><span class="sxs-lookup"><span data-stu-id="d848e-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="d848e-154">Bir web görünümü içeren bir uygulama bildirimi ardından Hello bildirim ise, uygulama kullanıcı tıklar hello web [Android yalnızca görüntüleme] bir URL'de hello</span><span class="sxs-lookup"><span data-stu-id="d848e-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="d848e-155">*Merhaba uygulama kullanıcı, yolu izleyerek hello birindeki bir bildirim çıkabilirsiniz:*</span><span class="sxs-lookup"><span data-stu-id="d848e-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="d848e-156">Merhaba bildirim Hello Kapat düğmesini doğrudan tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="d848e-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="d848e-157">Hemen geçirmeyi veya hello bildirim siliniyor.</span><span class="sxs-lookup"><span data-stu-id="d848e-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="d848e-158">Metin/web içeriği ve anketler ile uygulama bildirimleri genellikle görüntülenen toohello uygulama kullanıcı iki adımlı bir işlem var.</span><span class="sxs-lookup"><span data-stu-id="d848e-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="d848e-159">Bir bildirim ilk görür ve üzerinde'ı tıklattığınızda hello sonraki metin/web/yoklama içeriğin görürler.</span><span class="sxs-lookup"><span data-stu-id="d848e-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="d848e-160">Merhaba uygulama kullanıcı ya da bu adımları bildiriminde çıkabilirsiniz ve hello Gelişmiş görünümde hello ayrıntılar bu yakalar.</span><span class="sxs-lookup"><span data-stu-id="d848e-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="d848e-161">**İşleme alınan** -bu hello hello uygulama kullanıcı tarafından açıkça işleme alınan iletilerin sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d848e-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="d848e-162">Bu, hello bildiriminde gönderilen selamlama iletisine tarafından kaç uygulama kullanıcıların ilgileniyor söylerken bu hello en ilginç numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="d848e-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="d848e-163">Merhaba kullanıcının hello uygulamasını açın ve hello kampanya varsa dışında uygulama ve uygulama içi bildirimler hem de başlangıç görüntülenir mümkündür iOS & Windows platformları, "Her zaman" kampanya olduğu aynı anda.</span><span class="sxs-lookup"><span data-stu-id="d848e-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="d848e-164">Bu teslim edildi hello yüksek bir görüntülenen sayısı neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="d848e-165">Merhaba kullanıcı etkileşim isterseniz Eylemler hello bildirim sonra bile hello kullanıcı etkileşimleri/Actioned sayısı teslim edildi büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="d848e-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="d848e-167">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d848e-167">See also</span></span>
* <span data-ttu-id="d848e-168">[Kavramları][Link 6]</span><span class="sxs-lookup"><span data-stu-id="d848e-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="d848e-169">[Sorun giderme kılavuzu hizmeti][Link 24]</span><span class="sxs-lookup"><span data-stu-id="d848e-169">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

