---
title: "Azure Mobile Engagement kullanıcı arabirimi - Reach kampanya"
description: "Laern oluşturmak ve anında iletme bildirimi yönetmek için Azure Mobile Engagement kullanarak kampanyaları nasıl"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="d45d9-103">Oluşturma ve anında iletme bildirimi kampanyaları yönetme</span><span class="sxs-lookup"><span data-stu-id="d45d9-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="d45d9-104">Kullanıcı arabirimini ulaşma bölümünü bir anında iletme bildirimi göndermek için gereken tüm bilgileri sağlayarak karmaşık bir formülü yeni bir itme kampanya oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="d45d9-105">Anında iletme kampanya seçenekleri dört kampanya türlerine bağlı olarak biraz farklılık: Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="d45d9-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="d45d9-106">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d45d9-106">Option Applies to:</span></span>
* <span data-ttu-id="d45d9-107">Diller: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-108">Kampanya: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-109">Bildirim: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="d45d9-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="d45d9-110">İçeriği: Her kampanya türü için benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="d45d9-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="d45d9-111">İzleyici: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-112">Zaman çerçevesi: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="d45d9-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="d45d9-113">Sınama: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach Campaign1][20]

## <a name="languages"></a><span data-ttu-id="d45d9-115">Diller</span><span class="sxs-lookup"><span data-stu-id="d45d9-115">Languages</span></span>
<span data-ttu-id="d45d9-116">Dilleri açılan menüsünde, anında iletme farklı bir sürümünü farklı dillerde kullanacak şekilde ayarlanmış olan cihazlara göndermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="d45d9-117">Varsayılan olarak, tüm cihazlar aynı itme kullanmak üzere ayarlanmış hangi dilde bağımsız olarak alır.</span><span class="sxs-lookup"><span data-stu-id="d45d9-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="d45d9-118">Kullanıcılar için farklı bir dil cihazını itme varsayılan dil sürümünü alır.</span><span class="sxs-lookup"><span data-stu-id="d45d9-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="d45d9-119">Anında iletme kampanya seçeneklerinin birçoğu, her seçtiğiniz ek diller için alternatif içerik belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d45d9-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="d45d9-121">Dil farklar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d45d9-121">Language differences apply to:</span></span>
* <span data-ttu-id="d45d9-122">Diller: Benzersiz dilleri yanı sıra varsayılan dili seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="d45d9-123">Kampanya: Aynı tüm diller için</span><span class="sxs-lookup"><span data-stu-id="d45d9-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="d45d9-124">Bildirim: Varsayılan dil yanı sıra her dil için benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="d45d9-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="d45d9-125">İçeriği: Varsayılan dil yanı sıra her dil için benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="d45d9-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="d45d9-126">İzleyici: ayrı dil ölçüte göre filtre uygulanabilir</span><span class="sxs-lookup"><span data-stu-id="d45d9-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="d45d9-127">Zaman çerçevesi: tüm diller için aynı</span><span class="sxs-lookup"><span data-stu-id="d45d9-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="d45d9-128">Sınama: her dil için aynı anda gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="d45d9-129">Desteklenen diller:</span><span class="sxs-lookup"><span data-stu-id="d45d9-129">Supported Languages:</span></span>
* <span data-ttu-id="d45d9-130">Arapça (ar)</span><span class="sxs-lookup"><span data-stu-id="d45d9-130">Arabic (ar)</span></span> 
* <span data-ttu-id="d45d9-131">Bulgarca (bg)</span><span class="sxs-lookup"><span data-stu-id="d45d9-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="d45d9-132">Katalanca (ca)</span><span class="sxs-lookup"><span data-stu-id="d45d9-132">Catalan (ca)</span></span> 
* <span data-ttu-id="d45d9-133">Çince (zh)</span><span class="sxs-lookup"><span data-stu-id="d45d9-133">Chinese (zh)</span></span> 
* <span data-ttu-id="d45d9-134">Hırvatça (hr)</span><span class="sxs-lookup"><span data-stu-id="d45d9-134">Croatian (hr)</span></span> 
* <span data-ttu-id="d45d9-135">Czech (cs)</span><span class="sxs-lookup"><span data-stu-id="d45d9-135">Czech (cs)</span></span> 
* <span data-ttu-id="d45d9-136">Danca (da)</span><span class="sxs-lookup"><span data-stu-id="d45d9-136">Danish (da)</span></span> 
* <span data-ttu-id="d45d9-137">Felemenkçe (nl)</span><span class="sxs-lookup"><span data-stu-id="d45d9-137">Dutch (nl)</span></span> 
* <span data-ttu-id="d45d9-138">İngilizce (TR)</span><span class="sxs-lookup"><span data-stu-id="d45d9-138">English (en)</span></span> 
* <span data-ttu-id="d45d9-139">Fince (fi)</span><span class="sxs-lookup"><span data-stu-id="d45d9-139">Finnish (fi)</span></span> 
* <span data-ttu-id="d45d9-140">Fransızca (fr)</span><span class="sxs-lookup"><span data-stu-id="d45d9-140">French (fr)</span></span> 
* <span data-ttu-id="d45d9-141">Almanca (de)</span><span class="sxs-lookup"><span data-stu-id="d45d9-141">German (de)</span></span> 
* <span data-ttu-id="d45d9-142">Yunanca (el)</span><span class="sxs-lookup"><span data-stu-id="d45d9-142">Greek (el)</span></span> 
* <span data-ttu-id="d45d9-143">İbranice (.)</span><span class="sxs-lookup"><span data-stu-id="d45d9-143">Hebrew (he)</span></span> 
* <span data-ttu-id="d45d9-144">Hintçe (yüksek)</span><span class="sxs-lookup"><span data-stu-id="d45d9-144">Hindi (hi)</span></span> 
* <span data-ttu-id="d45d9-145">Macarca (hu)</span><span class="sxs-lookup"><span data-stu-id="d45d9-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="d45d9-146">Endonezya dili (ID)</span><span class="sxs-lookup"><span data-stu-id="d45d9-146">Indonesian (id)</span></span> 
* <span data-ttu-id="d45d9-147">İtalyanca ()</span><span class="sxs-lookup"><span data-stu-id="d45d9-147">Italian (it)</span></span> 
* <span data-ttu-id="d45d9-148">Japonca (ja)</span><span class="sxs-lookup"><span data-stu-id="d45d9-148">Japanese (ja)</span></span> 
* <span data-ttu-id="d45d9-149">Korece (ko)</span><span class="sxs-lookup"><span data-stu-id="d45d9-149">Korean (ko)</span></span> 
* <span data-ttu-id="d45d9-150">Letonca (lv)</span><span class="sxs-lookup"><span data-stu-id="d45d9-150">Latvian (lv)</span></span> 
* <span data-ttu-id="d45d9-151">Litvanca (lt)</span><span class="sxs-lookup"><span data-stu-id="d45d9-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="d45d9-152">Malay (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="d45d9-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="d45d9-153">Norveççe Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="d45d9-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="d45d9-154">Lehçe (pl)</span><span class="sxs-lookup"><span data-stu-id="d45d9-154">Polish (pl)</span></span> 
* <span data-ttu-id="d45d9-155">Portekizce (pt)</span><span class="sxs-lookup"><span data-stu-id="d45d9-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="d45d9-156">Rumence (ro)</span><span class="sxs-lookup"><span data-stu-id="d45d9-156">Romanian (ro)</span></span> 
* <span data-ttu-id="d45d9-157">Rusça (ru)</span><span class="sxs-lookup"><span data-stu-id="d45d9-157">Russian (ru)</span></span> 
* <span data-ttu-id="d45d9-158">Sırpça (sr)</span><span class="sxs-lookup"><span data-stu-id="d45d9-158">Serbian (sr)</span></span> 
* <span data-ttu-id="d45d9-159">Slovakça (sk)</span><span class="sxs-lookup"><span data-stu-id="d45d9-159">Slovak (sk)</span></span> 
* <span data-ttu-id="d45d9-160">Slovence (sl)</span><span class="sxs-lookup"><span data-stu-id="d45d9-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="d45d9-161">İspanyolca (es)</span><span class="sxs-lookup"><span data-stu-id="d45d9-161">Spanish (es)</span></span> 
* <span data-ttu-id="d45d9-162">İsveç dili (sv)</span><span class="sxs-lookup"><span data-stu-id="d45d9-162">Swedish (sv)</span></span> 
* <span data-ttu-id="d45d9-163">Tagalog dili (tl)</span><span class="sxs-lookup"><span data-stu-id="d45d9-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="d45d9-164">Tay dili (th)</span><span class="sxs-lookup"><span data-stu-id="d45d9-164">Thai (th)</span></span> 
* <span data-ttu-id="d45d9-165">Türkçe (tr)</span><span class="sxs-lookup"><span data-stu-id="d45d9-165">Turkish (tr)</span></span> 
* <span data-ttu-id="d45d9-166">Ukrayna dili (TR)</span><span class="sxs-lookup"><span data-stu-id="d45d9-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="d45d9-167">Vietnam dili (VI)</span><span class="sxs-lookup"><span data-stu-id="d45d9-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="d45d9-168">Kampanya</span><span class="sxs-lookup"><span data-stu-id="d45d9-168">Campaign</span></span>
<span data-ttu-id="d45d9-169">Kampanya bölüm adı ve kategoriyi de kampanyanızın itme kampanya İzleyici bölümünü yoksay ve bunun yerine bu kampanyayı Reach API'sini (ve bazı öğeler düşük düzeyde anında API) aracılığıyla göndermek planlıyorsanız olarak ayarlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="d45d9-170">Kategoriler denetim uygulama bildirimleri önceden tanımlanmış ayarlarınızı temel alan özel bildirim şablonu ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="d45d9-171">Varolan "Kategoriler" Reach API'sini aracılığıyla listesini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="d45d9-172">Kampanya otomatik olarak göndermez, Reach kampanya "Kampanyası" bölümünde "Yoksay İzleyici API aracılığıyla kullanıcılara bir gönderim" seçeneğini kullanırsanız, el ile ulaşmak API üzerinden göndermek gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="d45d9-174">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d45d9-174">Option Applies to:</span></span>
* <span data-ttu-id="d45d9-175">Ad: tüm</span><span class="sxs-lookup"><span data-stu-id="d45d9-175">Name:    All</span></span>
* <span data-ttu-id="d45d9-176">Kategori: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="d45d9-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="d45d9-177">Hedef kitleyi yok sayın anında iletme, API üzerinden kullanıcılara gönderilecek: tüm</span><span class="sxs-lookup"><span data-stu-id="d45d9-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="d45d9-178">Bildirim</span><span class="sxs-lookup"><span data-stu-id="d45d9-178">Notification</span></span>
<span data-ttu-id="d45d9-179">Bildirim bölümü, anında iletme dahil etmek için temel ayarları ayarlamak için kullanabileceğiniz: gönderme, ileti, bir uygulama görüntüsü başlığı veya atlanabilir tüm ise.</span><span class="sxs-lookup"><span data-stu-id="d45d9-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="d45d9-180">Birçok bildirim ayarlarını Cihazınızı platforma özgüdür.</span><span class="sxs-lookup"><span data-stu-id="d45d9-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="d45d9-181">"Uygulama" veya "uygulama dışında" bir gönderim seçebilirsiniz veya her ikisini de.</span><span class="sxs-lookup"><span data-stu-id="d45d9-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="d45d9-182">(Kullanıcılar can "katılımı" veya "çevirin" dışında "uygulamasının" işletim sistemi cihazlarını düzeyi iter ve Azure Mobile Engagement bu ayarı geçersiz kılmak mümkün olmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="d45d9-183">Ayrıca "uygulama" Reach API'sini işler ve "uygulama dışı" iter unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="d45d9-184">Anında iletme API "uygulama dışında" iter çok işlemek için kullanılabilir.) İter, resim veya HTML içeriğini, uygulamanızı dışında veya başka bir konuma uygulamanız (Android SDK 2.1.0 veya gerekli sonraki hedefi kategorileri) içinde bağlama için ayrıntılı bağlantılar dahil olmak üzere özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="d45d9-185">Simge veya iOS rozet değiştirmek ve metin veya web içerik (html içerik, URL bağlantı başka bir konum içinde veya dışında uygulama ile popup) gönderin.</span><span class="sxs-lookup"><span data-stu-id="d45d9-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="d45d9-186">Ayrıca, Android cihazları çaldır veya itme Titret.</span><span class="sxs-lookup"><span data-stu-id="d45d9-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="d45d9-187">(Doğru gerekeceğini unutmayın Android SDK izinleri bildirim halka veya bir cihazı Titret dosyaya.) Var. şu anda hiçbir endüstri Android "büyük resimdeki" boyutları için standart ekran boyutlarına her cihazda farklı ancak neredeyse her ekran boyutuna 400 x 100 resimleri iş beri.</span><span class="sxs-lookup"><span data-stu-id="d45d9-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="d45d9-188">Teslim türleri:</span><span class="sxs-lookup"><span data-stu-id="d45d9-188">Delivery Types:</span></span>
* <span data-ttu-id="d45d9-189">Yalnızca uygulama dışında: kullanıcı uygulamayı kullanmadığında bildirim teslim edilecek.</span><span class="sxs-lookup"><span data-stu-id="d45d9-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="d45d9-190">Uygulama yalnızca bildirim dışı Apple veya Google (GCM ya da APNS sertifikası) bir sertifika gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="d45d9-191">Uygulama yalnızca: yalnızca uygulama çalışırken bildirim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="d45d9-192">Bildirim Capptain teslim sistemi kullanıcı erişmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d45d9-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="d45d9-193">Düzen/görünümünü, anında tam olarak özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="d45d9-194">Herhangi bir zaman: Ya da uygulama veya çalıştığı bildirim göndermek bu seçeneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="d45d9-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="d45d9-196">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d45d9-196">Option Applies to:</span></span>
* <span data-ttu-id="d45d9-197">Bildirim: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="d45d9-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="d45d9-198">İçerik</span><span class="sxs-lookup"><span data-stu-id="d45d9-198">Content</span></span>
<span data-ttu-id="d45d9-199">İçerik bölümü içeriği Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone) değiştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="d45d9-200">İçerik anında iletme kampanyalarını kampanya türüne belirli ayarıdır.</span><span class="sxs-lookup"><span data-stu-id="d45d9-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="d45d9-201">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-201">See also</span></span>
* <span data-ttu-id="d45d9-202">[UI belgeleri - ulaşmak - içerik gönderme][Link 29]</span><span class="sxs-lookup"><span data-stu-id="d45d9-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach Campaign5][24]

## <a name="audience"></a><span data-ttu-id="d45d9-204">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="d45d9-204">Audience</span></span>
<span data-ttu-id="d45d9-205">Hedef kitle bölümü, standart bir kampanya veya kampanyanızı özelleştirilmiş ölçütlere göre sınırları sınırlamak için öğe listesi tanımlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="d45d9-206">Standart kitlenizi sınırlamak için seçenekleri kümesi, yeni veya eski kullanıcılara veya yalnızca yerel gönderim kullanıcılara anında iletme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d45d9-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="d45d9-207">Anında iletme alan kullanıcıların sayısını sınırlamak için bir kota de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="d45d9-208">Hedef kullanıcılar için bir veya daha fazla ölçüt eklemek için kampanyanızı nasıl filtre için ifade el ile düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="d45d9-209">Bir hedef kitle ifadesi el ile yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-209">You can manually type an audience expression.</span></span> <span data-ttu-id="d45d9-210">Bu tür bir ifade, ölçütler arasındaki ilişkiyi açıkça tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="d45d9-211">Bir ölçüt büyük harfle başlamalı ve boşluk içeremez bir tanımlayıcı tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d45d9-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="d45d9-212">Ölçütler arasındaki ilişkiyi kullanılarak tanımlanabilir 'and', 'or', 'not' işleçleri yanı sıra '(',')'.</span><span class="sxs-lookup"><span data-stu-id="d45d9-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="d45d9-213">Örnek: "Criterion1 veya (Criterion1 ve değil Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="d45d9-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="d45d9-214">Kampanyalarda bulunan büyük bir izleyici ile tarama hedefleme sunucu tarafı özellikle aynı anda birden çok Kampanyalar başlatmayı denerseniz yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="d45d9-215">Mümkünse, yalnızca bir kampanya aynı anda başlatın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="d45d9-216">En fazla yalnızca dört Kampanyalar aynı anda başlatın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="d45d9-217">Yalnızca etkin kullanıcılara anında iletme (onay kutusu "yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye" ve "yalnızca etkin kullanıcıları göster") böylece hala uygulamasını yüklemediyseniz ve kullanmak, kullanıcılarınızın taranacak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="d45d9-218">Kitlenizi tanımlandıktan sonra bu itme kaç kullanıcı alacak bulmak için benzetim düğmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="d45d9-219">Bu, büyük olasılıkla (Bu kullanıcıların rastgele bir örneği temel alarak bir tahmindir) Bu İzleyici tarafından hedeflenen bilinen kullanıcıların sayısını hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="d45d9-220">Uygulamayı kaldırmış kullanıcıların da bu hedef kitleye dahil olduğu, ancak ulaşılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="d45d9-221">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-221">See also</span></span>
* <span data-ttu-id="d45d9-222">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="d45d9-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="d45d9-224">İfade Düzenle</span><span class="sxs-lookup"><span data-stu-id="d45d9-224">Edit expression</span></span>
![Reach Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="d45d9-226">Hedef kitle seçeneğinizi uygulandığı sınırı:</span><span class="sxs-lookup"><span data-stu-id="d45d9-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="d45d9-227">Yalnızca bir kullanıcı alt kümesini göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-228">Yalnızca eski kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-229">Yalnızca yeni kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-230">Yalnızca boştaki kullanıcıları göster: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="d45d9-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="d45d9-231">Yalnızca etkin kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="d45d9-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="d45d9-232">Yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye sok: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="d45d9-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="d45d9-233">Zaman çerçevesi</span><span class="sxs-lookup"><span data-stu-id="d45d9-233">Time Frame</span></span>
<span data-ttu-id="d45d9-234">Gönderim veya zaman çerçevesi kampanya hemen başlatmak için boş bırakabilirsiniz ayarlamak için zaman çerçevesi bölüm kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="d45d9-235">Son kullanıcılar saat dilimi kullanarak kampanya kullanıcılarınızın Asya'da beklediğiniz ve kampanyanızı için zaman çerçevesi dünyadaki tüm saat dilimleri eşleşen kadar bir seferde iter küçük toplu göndermek'den önceki bir gün başlayabilir, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d45d9-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="d45d9-236">İstek süresi telefonunuzdan itme başlatmadan önce olduğundan son kullanıcının saat dilimi kullanarak da gecikmeler kampanyalarda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="d45d9-237">Bitiş tarihi önbelleğe alabilir olmadan kampanyaları iter yerel olarak hala görünen ve bunları sonra el ile tam kampanyalar.</span><span class="sxs-lookup"><span data-stu-id="d45d9-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="d45d9-238">Özel bir bitiş saati kampanyalar için bu davranışı önlemek için.</span><span class="sxs-lookup"><span data-stu-id="d45d9-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="d45d9-239">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-239">See also</span></span>
* <span data-ttu-id="d45d9-240">[Ulaşmaya - nasıl yapılır – planlama][Link 3]</span><span class="sxs-lookup"><span data-stu-id="d45d9-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="d45d9-242">Ayarlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d45d9-242">Settings Apply to:</span></span>
* <span data-ttu-id="d45d9-243">Zaman çerçevesi: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="d45d9-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="d45d9-244">Test etme</span><span class="sxs-lookup"><span data-stu-id="d45d9-244">Test</span></span>
<span data-ttu-id="d45d9-245">Test bölümü kampanya kaydetmeden önce bu itme kendi test aygıta göndermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="d45d9-246">Tüm özel diller bu kampanya için yapılandırdıysanız, her dilde göndererek test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="d45d9-247">"Hesabım" test aygıttan ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="d45d9-248">"Test etmek için" düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d45d9-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="d45d9-249">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d45d9-249">See also</span></span>
* <span data-ttu-id="d45d9-250">[UI belgeleri - hesabım][Link 14]</span><span class="sxs-lookup"><span data-stu-id="d45d9-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach Campaign9][28]

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

