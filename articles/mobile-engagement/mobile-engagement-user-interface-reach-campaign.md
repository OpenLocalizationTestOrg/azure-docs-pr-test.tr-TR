---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - Reach kampanya"
description: "Laern nasıl toocreate ve Azure Mobile Engagement kullanarak anında iletme bildirimi kampanyaları yönetme"
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="bdd96-103">Nasıl toocreate ve anında iletme bildirimi kampanyaları yönetme</span><span class="sxs-lookup"><span data-stu-id="bdd96-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="bdd96-104">Toosend bir anında iletme bildirimi gereksinim duyduğunuz tüm hello bilgileri sağlayarak karmaşık formül hello hello UI toocreate yeni bir itme kampanya ulaşma bölümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="bdd96-105">Merhaba seçenekler itme kampanyanın biraz hello dört kampanya türlerine bağlı olarak değişir: Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="bdd96-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="bdd96-106">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bdd96-106">Option Applies to:</span></span>
* <span data-ttu-id="bdd96-107">Diller: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-108">Kampanya: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-109">Bildirim: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="bdd96-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="bdd96-110">İçeriği: Her kampanya türü için benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="bdd96-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="bdd96-111">İzleyici: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-112">Zaman çerçevesi: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="bdd96-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="bdd96-113">Sınama: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach Campaign1][20]

## <a name="languages"></a><span data-ttu-id="bdd96-115">Diller</span><span class="sxs-lookup"><span data-stu-id="bdd96-115">Languages</span></span>
<span data-ttu-id="bdd96-116">Merhaba dilleri açılan menü toosend toouse farklı dillerde ayarlayın, anında iletme toodevices farklı bir sürümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="bdd96-117">Varsayılan olarak, tüm cihazlar aynı hangi dilde toouse ayarlandıktan bağımsız olarak Anında hello alır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="bdd96-118">Kendi cihaz kümesi tooa farklı dil kullanıcılarla hello itme hello varsayılan dil sürümünü alır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="bdd96-119">Merhaba itme kampanya seçeneklerinin birçoğu toospecify alternatif içerik her seçtiğiniz hello ek diller için sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdd96-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="bdd96-121">Dil farklar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bdd96-121">Language differences apply to:</span></span>
* <span data-ttu-id="bdd96-122">Diller: Benzersiz dilleri toplama toohello varsayılan dilde seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="bdd96-123">Kampanya: Aynı tüm diller için</span><span class="sxs-lookup"><span data-stu-id="bdd96-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="bdd96-124">Bildirim: Her dil için benzersiz ayrıca toohello varsayılan dil</span><span class="sxs-lookup"><span data-stu-id="bdd96-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="bdd96-125">İçeriği: Her dil için benzersiz ayrıca toohello varsayılan dil</span><span class="sxs-lookup"><span data-stu-id="bdd96-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="bdd96-126">İzleyici: ayrı dil ölçüte göre filtre uygulanabilir</span><span class="sxs-lookup"><span data-stu-id="bdd96-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="bdd96-127">Zaman çerçevesi: tüm diller için aynı</span><span class="sxs-lookup"><span data-stu-id="bdd96-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="bdd96-128">Sınama: tooeach dil aynı anda gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="bdd96-129">Desteklenen diller:</span><span class="sxs-lookup"><span data-stu-id="bdd96-129">Supported Languages:</span></span>
* <span data-ttu-id="bdd96-130">Arapça (ar)</span><span class="sxs-lookup"><span data-stu-id="bdd96-130">Arabic (ar)</span></span> 
* <span data-ttu-id="bdd96-131">Bulgarca (bg)</span><span class="sxs-lookup"><span data-stu-id="bdd96-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="bdd96-132">Katalanca (ca)</span><span class="sxs-lookup"><span data-stu-id="bdd96-132">Catalan (ca)</span></span> 
* <span data-ttu-id="bdd96-133">Çince (zh)</span><span class="sxs-lookup"><span data-stu-id="bdd96-133">Chinese (zh)</span></span> 
* <span data-ttu-id="bdd96-134">Hırvatça (hr)</span><span class="sxs-lookup"><span data-stu-id="bdd96-134">Croatian (hr)</span></span> 
* <span data-ttu-id="bdd96-135">Czech (cs)</span><span class="sxs-lookup"><span data-stu-id="bdd96-135">Czech (cs)</span></span> 
* <span data-ttu-id="bdd96-136">Danca (da)</span><span class="sxs-lookup"><span data-stu-id="bdd96-136">Danish (da)</span></span> 
* <span data-ttu-id="bdd96-137">Felemenkçe (nl)</span><span class="sxs-lookup"><span data-stu-id="bdd96-137">Dutch (nl)</span></span> 
* <span data-ttu-id="bdd96-138">İngilizce (TR)</span><span class="sxs-lookup"><span data-stu-id="bdd96-138">English (en)</span></span> 
* <span data-ttu-id="bdd96-139">Fince (fi)</span><span class="sxs-lookup"><span data-stu-id="bdd96-139">Finnish (fi)</span></span> 
* <span data-ttu-id="bdd96-140">Fransızca (fr)</span><span class="sxs-lookup"><span data-stu-id="bdd96-140">French (fr)</span></span> 
* <span data-ttu-id="bdd96-141">Almanca (de)</span><span class="sxs-lookup"><span data-stu-id="bdd96-141">German (de)</span></span> 
* <span data-ttu-id="bdd96-142">Yunanca (el)</span><span class="sxs-lookup"><span data-stu-id="bdd96-142">Greek (el)</span></span> 
* <span data-ttu-id="bdd96-143">İbranice (.)</span><span class="sxs-lookup"><span data-stu-id="bdd96-143">Hebrew (he)</span></span> 
* <span data-ttu-id="bdd96-144">Hintçe (yüksek)</span><span class="sxs-lookup"><span data-stu-id="bdd96-144">Hindi (hi)</span></span> 
* <span data-ttu-id="bdd96-145">Macarca (hu)</span><span class="sxs-lookup"><span data-stu-id="bdd96-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="bdd96-146">Endonezya dili (ID)</span><span class="sxs-lookup"><span data-stu-id="bdd96-146">Indonesian (id)</span></span> 
* <span data-ttu-id="bdd96-147">İtalyanca ()</span><span class="sxs-lookup"><span data-stu-id="bdd96-147">Italian (it)</span></span> 
* <span data-ttu-id="bdd96-148">Japonca (ja)</span><span class="sxs-lookup"><span data-stu-id="bdd96-148">Japanese (ja)</span></span> 
* <span data-ttu-id="bdd96-149">Korece (ko)</span><span class="sxs-lookup"><span data-stu-id="bdd96-149">Korean (ko)</span></span> 
* <span data-ttu-id="bdd96-150">Letonca (lv)</span><span class="sxs-lookup"><span data-stu-id="bdd96-150">Latvian (lv)</span></span> 
* <span data-ttu-id="bdd96-151">Litvanca (lt)</span><span class="sxs-lookup"><span data-stu-id="bdd96-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="bdd96-152">Malay (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="bdd96-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="bdd96-153">Norveççe Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="bdd96-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="bdd96-154">Lehçe (pl)</span><span class="sxs-lookup"><span data-stu-id="bdd96-154">Polish (pl)</span></span> 
* <span data-ttu-id="bdd96-155">Portekizce (pt)</span><span class="sxs-lookup"><span data-stu-id="bdd96-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="bdd96-156">Rumence (ro)</span><span class="sxs-lookup"><span data-stu-id="bdd96-156">Romanian (ro)</span></span> 
* <span data-ttu-id="bdd96-157">Rusça (ru)</span><span class="sxs-lookup"><span data-stu-id="bdd96-157">Russian (ru)</span></span> 
* <span data-ttu-id="bdd96-158">Sırpça (sr)</span><span class="sxs-lookup"><span data-stu-id="bdd96-158">Serbian (sr)</span></span> 
* <span data-ttu-id="bdd96-159">Slovakça (sk)</span><span class="sxs-lookup"><span data-stu-id="bdd96-159">Slovak (sk)</span></span> 
* <span data-ttu-id="bdd96-160">Slovence (sl)</span><span class="sxs-lookup"><span data-stu-id="bdd96-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="bdd96-161">İspanyolca (es)</span><span class="sxs-lookup"><span data-stu-id="bdd96-161">Spanish (es)</span></span> 
* <span data-ttu-id="bdd96-162">İsveç dili (sv)</span><span class="sxs-lookup"><span data-stu-id="bdd96-162">Swedish (sv)</span></span> 
* <span data-ttu-id="bdd96-163">Tagalog dili (tl)</span><span class="sxs-lookup"><span data-stu-id="bdd96-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="bdd96-164">Tay dili (th)</span><span class="sxs-lookup"><span data-stu-id="bdd96-164">Thai (th)</span></span> 
* <span data-ttu-id="bdd96-165">Türkçe (tr)</span><span class="sxs-lookup"><span data-stu-id="bdd96-165">Turkish (tr)</span></span> 
* <span data-ttu-id="bdd96-166">Ukrayna dili (TR)</span><span class="sxs-lookup"><span data-stu-id="bdd96-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="bdd96-167">Vietnam dili (VI)</span><span class="sxs-lookup"><span data-stu-id="bdd96-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="bdd96-168">Kampanya</span><span class="sxs-lookup"><span data-stu-id="bdd96-168">Campaign</span></span>
<span data-ttu-id="bdd96-169">Tooignore hello İzleyici itme kampanya bölümünü planlamak ve bu kampanyayı hello Reach API'sini aracılığıyla (ve bazı öğeler hello düşük düzey itme API ile) yerine göndermek gibi hello kampanya bölüm tooset hello adı ve kategori kampanyanızın de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="bdd96-170">Kategoriler, önceden tanımlanmış ayarlarına dayanarak bir özel bildirim şablonu toocontrol uygulama bildirimleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="bdd96-171">Varolan "Kategoriler" Merhaba Reach API'sini aracılığıyla listesini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="bdd96-172">Merhaba kampanya otomatik olarak göndermez, hello seçeneği "Yoksay İzleyici toousers hello API aracılığıyla bir gönderim" hello "Kampanya" bölümünde Reach kampanya kullanırsanız toosend gerekir, hello Reach API'sini kullanarak el ile.</span><span class="sxs-lookup"><span data-stu-id="bdd96-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="bdd96-174">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bdd96-174">Option Applies to:</span></span>
* <span data-ttu-id="bdd96-175">Ad: tüm</span><span class="sxs-lookup"><span data-stu-id="bdd96-175">Name:    All</span></span>
* <span data-ttu-id="bdd96-176">Kategori: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="bdd96-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="bdd96-177">Hedef kitleyi yok sayın itme toousers hello API üzerinden gönderilir: tüm</span><span class="sxs-lookup"><span data-stu-id="bdd96-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="bdd96-178">Bildirim</span><span class="sxs-lookup"><span data-stu-id="bdd96-178">Notification</span></span>
<span data-ttu-id="bdd96-179">Merhaba bildirim bölümü tooset temel ayarları, anında iletme dahil etmek için kullanabilirsiniz: Merhaba hello anında iletme, selamlama iletisine, bir uygulama görüntüsü başlığını veya atlanabilir tüm ise.</span><span class="sxs-lookup"><span data-stu-id="bdd96-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="bdd96-180">Birçok bildirim belirli toohello platform aygıtınızın ayarlardır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="bdd96-181">"Uygulama" veya "uygulama dışında" bir gönderim seçebilirsiniz veya her ikisini de.</span><span class="sxs-lookup"><span data-stu-id="bdd96-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="bdd96-182">(Kullanıcılar can "katılımı" veya "çevirin" dışında "uygulamasının" iter Merhaba işletim sistemi düzeyinde cihazlarına ve Azure Mobile Engagement almayacak unutmayın mümkün toooverride bu ayarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="bdd96-183">Ayrıca "uygulama" Merhaba ulaşma API işler ve "uygulama dışı" iter unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bdd96-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="bdd96-184">"Hello itme API"uygulamasının out"çok iter kullanılan toohandle olabilir.) İter, resim veya HTML içeriğini, uygulama veya tooanother konumunuzda uygulamanız (Android SDK 2.1.0 veya gerekli sonraki hedefi kategorileri) dışında bağlama için ayrıntılı bağlantılar dahil olmak üzere özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="bdd96-185">Merhaba simgesini veya iOS rozet değiştirmek ve metin veya web içerik (html içerik, URL bağlantı tooanother konum içinde veya dışında hello uygulama popup) gönderin.</span><span class="sxs-lookup"><span data-stu-id="bdd96-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="bdd96-186">Ayrıca, Android cihazları çaldır veya itme hello ile Titret.</span><span class="sxs-lookup"><span data-stu-id="bdd96-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="bdd96-187">(, Android SDK izinler dosya tooring bildirim veya bir cihazı Titret doğru hello olduğunu unutmayın.) Var. şu anda hiçbir endüstri Android "büyük resimdeki" boyutları için standart ekran boyutlarına her cihazda farklı ancak neredeyse her ekran boyutuna 400 x 100 resimleri iş beri.</span><span class="sxs-lookup"><span data-stu-id="bdd96-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="bdd96-188">Teslim türleri:</span><span class="sxs-lookup"><span data-stu-id="bdd96-188">Delivery Types:</span></span>
* <span data-ttu-id="bdd96-189">Yalnızca uygulama dışında: hello bildirim teslim edilemiyor hello kullanıcı Merhaba uygulaması kullanılmadığında.</span><span class="sxs-lookup"><span data-stu-id="bdd96-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="bdd96-190">Uygulama yalnızca bildirim dışında Hello Apple veya Google (GCM ya da APNS sertifikası) bir sertifika gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="bdd96-191">Uygulama yalnızca: hello bildirim görüntülendiğinde yalnızca hello uygulama çalışırken.</span><span class="sxs-lookup"><span data-stu-id="bdd96-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="bdd96-192">Merhaba bildirim hello Capptain teslim sistemi tooreach hello kullanıcı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="bdd96-193">Merhaba düzeni/görünümünü, anında tam olarak özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="bdd96-194">Herhangi bir zaman: Veya değil ya da Merhaba uygulaması çalıştıran bildirim göndermek bu seçeneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdd96-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="bdd96-196">Seçenek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bdd96-196">Option Applies to:</span></span>
* <span data-ttu-id="bdd96-197">Bildirim: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="bdd96-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="bdd96-198">İçerik</span><span class="sxs-lookup"><span data-stu-id="bdd96-198">Content</span></span>
<span data-ttu-id="bdd96-199">Merhaba içerik bölümü toomodify hello içerik Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="bdd96-200">Merhaba içerik anında iletme kampanyalarını kampanya belirli toohello türü ayarıdır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="bdd96-201">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-201">See also</span></span>
* <span data-ttu-id="bdd96-202">[UI belgeleri - ulaşmak - içerik gönderme][Link 29]</span><span class="sxs-lookup"><span data-stu-id="bdd96-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach Campaign5][24]

## <a name="audience"></a><span data-ttu-id="bdd96-204">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="bdd96-204">Audience</span></span>
<span data-ttu-id="bdd96-205">Kampanya veya kampanyanızı özelleştirilmiş ölçütlere göre sınırları hello İzleyici bölüm toodefine standart öğeleri toolimit listesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="bdd96-206">Merhaba standart seçenekleri tooLimit kümesinin kitlenizi toopush tooeither yeni veya eski kullanıcılara veya yalnızca yerel gönderim kullanıcılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdd96-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="bdd96-207">Merhaba itme alma kullanıcıların kota toolimit hello sayısını da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="bdd96-208">El ile nasıl kampanyanızı filtrelenmiş tooinclude olduğu için hello ifade düzenleyebileceğiniz bir veya daha fazla ölçüt tootarget kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="bdd96-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="bdd96-209">Bir hedef kitle ifadesi el ile yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-209">You can manually type an audience expression.</span></span> <span data-ttu-id="bdd96-210">Bu tür bir ifade hello ölçütler arasındaki ilişkiyi açıkça tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="bdd96-211">Bir ölçüt büyük harfle başlamalı ve boşluk içeremez bir tanımlayıcı tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="bdd96-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="bdd96-212">Merhaba ölçütler arasındaki ilişkiyi Hello kullanarak tanımlanabilen 'and', 'or', 'not' işleçleri yanı sıra '(',')'.</span><span class="sxs-lookup"><span data-stu-id="bdd96-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="bdd96-213">Örnek: "Criterion1 veya (Criterion1 ve değil Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="bdd96-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="bdd96-214">Kampanyalarda bulunan büyük bir izleyici ile tarama hedefleme hello sunucu tarafı yavaş olabilir, özellikle toostart çalışırsanız, birden çok Kampanyalar aynı hello zaman.</span><span class="sxs-lookup"><span data-stu-id="bdd96-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="bdd96-215">Mümkünse, yalnızca bir kampanya aynı anda başlatın.</span><span class="sxs-lookup"><span data-stu-id="bdd96-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="bdd96-216">En çok yalnızca başlangıç dört kampanyaları birer birer hello.</span><span class="sxs-lookup"><span data-stu-id="bdd96-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="bdd96-217">Yalnızca tooyour etkin kullanıcıları itme (onay kutusu "yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye" ve "yalnızca etkin kullanıcıları göster") böylece hala hello uygulamasını yüklemediyseniz ve kullanmak, kullanıcılarınızın taranan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="bdd96-218">Kitlenizi tanımlandığında hello kullanabilirsiniz kaç kullanıcının bu anında alacaksınız çıkışı düğmesi toofind benzetimini.</span><span class="sxs-lookup"><span data-stu-id="bdd96-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="bdd96-219">Bu, büyük olasılıkla (Bu kullanıcıların rastgele bir örneği temel alarak bir tahmindir) Bu İzleyici tarafından hedeflenen bilinen kullanıcıların sayısını hello işlem.</span><span class="sxs-lookup"><span data-stu-id="bdd96-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="bdd96-220">Merhaba uygulamayı kaldırmış kullanıcıların da bu hedef kitleye dahil olduğu, ancak ulaşılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bdd96-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="bdd96-221">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-221">See also</span></span>
* <span data-ttu-id="bdd96-222">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="bdd96-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="bdd96-224">İfade Düzenle</span><span class="sxs-lookup"><span data-stu-id="bdd96-224">Edit expression</span></span>
![Reach Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="bdd96-226">Hedef kitle seçeneğinizi uygulandığı sınırı:</span><span class="sxs-lookup"><span data-stu-id="bdd96-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="bdd96-227">Yalnızca bir kullanıcı alt kümesini göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-228">Yalnızca eski kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-229">Yalnızca yeni kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-230">Yalnızca boştaki kullanıcıları göster: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="bdd96-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="bdd96-231">Yalnızca etkin kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)</span><span class="sxs-lookup"><span data-stu-id="bdd96-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="bdd96-232">Yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye sok: Duyurular, anketler</span><span class="sxs-lookup"><span data-stu-id="bdd96-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="bdd96-233">Zaman çerçevesi</span><span class="sxs-lookup"><span data-stu-id="bdd96-233">Time Frame</span></span>
<span data-ttu-id="bdd96-234">Merhaba gönderim veya başlangıç zamanını boş toostart hello kampanya hemen bırakabilirsiniz hello zaman çerçevesi bölüm tooset kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="bdd96-235">Hello son saat dilimi kullanarak hello kampanya kullanıcılarınızın Asya'da bekler ve iter birer birer hello world eşleşme hello zaman çerçevesi içindeki tüm saat dilimleri için kampanyanızı ayarlanıncaya kadar küçük toplu Gönder'den önceki bir gün başlayabilir, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bdd96-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="bdd96-236">Merhaba itme başlatmadan önce toorequest hello zaman hello telefondan olduğundan hello son kullanıcıların saat dilimi kullanarak da gecikmeler kampanyalarda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd96-237">Bitiş tarihi önbelleğe alabilir olmadan kampanyaları iter yerel olarak hala görünen ve bunları sonra el ile tam kampanyalar.</span><span class="sxs-lookup"><span data-stu-id="bdd96-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="bdd96-238">tooavoid Bu davranış, özel kampanyalar için bitiş zamanı.</span><span class="sxs-lookup"><span data-stu-id="bdd96-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="bdd96-239">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-239">See also</span></span>
* <span data-ttu-id="bdd96-240">[Ulaşmaya - nasıl yapılır – planlama][Link 3]</span><span class="sxs-lookup"><span data-stu-id="bdd96-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="bdd96-242">Ayarlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="bdd96-242">Settings Apply to:</span></span>
* <span data-ttu-id="bdd96-243">Zaman çerçevesi: Duyurular, anketler, döşeme</span><span class="sxs-lookup"><span data-stu-id="bdd96-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="bdd96-244">Test etme</span><span class="sxs-lookup"><span data-stu-id="bdd96-244">Test</span></span>
<span data-ttu-id="bdd96-245">Merhaba kampanya kaydetmeden önce bu itme tooyour kendi test aygıt hello Test bölümü toosend kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="bdd96-246">Bu kampanya için özel tüm diller yapılandırdıysanız, her dilde hello itme test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="bdd96-247">"Hesabım" test aygıttan ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd96-248">Merhaba düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı çok "test" iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bdd96-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="bdd96-249">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bdd96-249">See also</span></span>
* <span data-ttu-id="bdd96-250">[UI belgeleri - hesabım][Link 14]</span><span class="sxs-lookup"><span data-stu-id="bdd96-250">[UI Documentation - My Account][Link 14]</span></span>

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

