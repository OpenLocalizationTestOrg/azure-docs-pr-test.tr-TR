---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - ulaşmak ölçütü"
description: "Nasıl Azure Mobile Engagement kullanarak, kullanıcı alt kümesini seçin toouse hedefleme ölçütleri toosend anında iletme kampanyalarını tooa öğrenin"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="03e18-103">Nasıl toouse hedefleme ölçütleri toosend anında iletme kampanyalarını tooa, kullanıcı alt kümesini seçin</span><span class="sxs-lookup"><span data-stu-id="03e18-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="03e18-104">Merhaba "Yeni ölçüt" düğmesiyle belirli ölçütlere göre kitlenizi hedefleme anında iletme bildirimleri hello müşteriler herkes istenmeyen posta olarak tooinstead yanıtlar ilgili gönderdiğiniz yardımcı hello en güçlü kavramlarını Azure Mobile Engagement biridir.</span><span class="sxs-lookup"><span data-stu-id="03e18-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="03e18-105">Standart ölçütlere göre kitlenizi sınırlayabilir ve iter toodetermine benzetimini kaç kişinin hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="03e18-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="03e18-106">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="03e18-106">**See also:**</span></span>

* <span data-ttu-id="03e18-107">[UI belgeleri - Reach - yeni itme kampanya][Link 27]</span><span class="sxs-lookup"><span data-stu-id="03e18-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="03e18-108">Hedef kitle ölçüt içerebilir:</span><span class="sxs-lookup"><span data-stu-id="03e18-108">Audience criteria can include:</span></span>
* <span data-ttu-id="03e18-109">** Technicals: ** göre hello hedefleyebilirsiniz aynı teknik bilgileri hello analizi ve izleme bölümleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e18-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="03e18-110">**Ayrıca bkz:** [UI belgeleri - Analytics'i][Link 15], [UI belgeleri - izleme][Link 16]</span><span class="sxs-lookup"><span data-stu-id="03e18-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="03e18-111">**Konumu:** "gerçek zamanlı konum Raporlama" ile Coğrafı kullanan uygulamalar coğrafi konum ölçütleri tootarget hello GPS konumu gelen bir dinleyici olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e18-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="03e18-112">"Yavaş alan konumu Raporlama" çağrısı kullanılan tootarget hello cep telefonu konumdan bir izleyici de ("gerçek zamanlı konum Raporlama" ve "Yavaş alan konumu Raporlama" etkinleştirilmesi gerekir hello SDK ').</span><span class="sxs-lookup"><span data-stu-id="03e18-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="03e18-113">**Ayrıca bkz:** [SDK Belgeleri - iOS - tümleştirme][Link 5], [SDK Belgeleri - Android - tümleştirme][Link 5]</span><span class="sxs-lookup"><span data-stu-id="03e18-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="03e18-114">**Reach geri bildirim:** kitlenizi ulaşma görüşleri Duyurular, anketler ve veri iter aracılığıyla önceki ulaşma bildirimleri kendi görüşleri göre hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e18-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="03e18-115">Bu, toobetter hedef kitlenizi daha Kampanyalar iki veya üç eriştikten sonra ilk kez hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="03e18-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="03e18-116">Ayrıca kullanılabilir toofilter zaten bir kampanya tooNOT ayarlayarak benzer içeriği içeren bir bildirim alındı kullanıcılar çıkışı, belirli bir önceki kampanya zaten alınan toousers gönderilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="03e18-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="03e18-117">Kullanıcılar bile dışlayabilirsiniz kimin yeni iter almasını hala etkin olan belirli bir kampanyaya eklenir.</span><span class="sxs-lookup"><span data-stu-id="03e18-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="03e18-118">**Ayrıca bkz:** [UI belgeleri - Reach - anında içeriği][Link 29]</span><span class="sxs-lookup"><span data-stu-id="03e18-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="03e18-119">**Yükleme izlemesi:** bilgileri kullanıcılarınızın uygulamanızın yüklendiği göre izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03e18-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="03e18-120">**Ayrıca bkz:** [UI belgeleri - ayarlar][Link 20]</span><span class="sxs-lookup"><span data-stu-id="03e18-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="03e18-121">**Kullanıcı profili:** , standart kullanıcı bilgilerine göre hedef olabilir ve hedef oluşturduğunuz hello özel uygulama bilgilerini dayalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="03e18-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="03e18-122">Bu, oturum açmış ve yalnızca nasıl bunlar tooprevious Kampanyalar yanıtladığını yerine hello uygulamasında kendisini tooset istediniz belirli sorulara verdiğiniz yanıtlara kullanıcılar içerir.</span><span class="sxs-lookup"><span data-stu-id="03e18-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="03e18-123">Tüm uygulama bilgilerini 's bu listede, uygulama gösteri için tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="03e18-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="03e18-124">Segment: Şunları da yapabilirsiniz oluşturduğunuz kesimlerinde göre hedef tabanlı birden çok ölçüt içeren belirli bir kullanıcı davranışı.</span><span class="sxs-lookup"><span data-stu-id="03e18-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="03e18-125">Uygulamanız için tanımlanan segmentlerinizi tümünün bu listede gösterilir.</span><span class="sxs-lookup"><span data-stu-id="03e18-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="03e18-126">**Ayrıca bkz:** [UI belgeleri - parçaları][Link 18]</span><span class="sxs-lookup"><span data-stu-id="03e18-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="03e18-127">**Uygulama bilgileri:** özel uygulama bilgisi etiketleri "Ayarlar" tootrack kullanıcı davranışından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="03e18-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="03e18-128">**Ayrıca bkz:** [UI belgeleri - ayarlar][Link 20]</span><span class="sxs-lookup"><span data-stu-id="03e18-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="03e18-129">Örnek:</span><span class="sxs-lookup"><span data-stu-id="03e18-129">Example:</span></span>
<span data-ttu-id="03e18-130">Toopush istiyorsanız bir duyuru yalnızca toohello alt kümesi kullanıcılarınızın bir uygulama gerçekleştirilen eylem satın alın.</span><span class="sxs-lookup"><span data-stu-id="03e18-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="03e18-131">Tooyour uygulama ayarları sayfasına gidin, hello "Uygulama bilgisini" menüsünü seçin ve "Yeni uygulama bilgileri" seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="03e18-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="03e18-132">"İnAppPurchase" adlı yeni bir mantıksal uygulama bilgisi kaydetme</span><span class="sxs-lookup"><span data-stu-id="03e18-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="03e18-133">Hello kullanıcı bir uygulama içi satın alma başarıyla gerçekleştirdiğinde, uygulamanız bu uygulama bilgisinde ayarlanmış çok "true" yapın (Merhaba sendAppInfo ("inAppPurchase",...) kullanarak işlevi)</span><span class="sxs-lookup"><span data-stu-id="03e18-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="03e18-134">Bu toodo uygulamanızdan istemiyorsanız, arka ucunuzdan hello cihaz API'sini kullanarak bunu yapabilirsiniz)</span><span class="sxs-lookup"><span data-stu-id="03e18-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="03e18-135">Ardından, "inAppPurchase" olması, İzleyici toousers sınırlama sahip bir ölçüt duyurunuzun, "true" çok ayarlamak toocreate yeterlidir)</span><span class="sxs-lookup"><span data-stu-id="03e18-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="03e18-136">Hello itme gönderilir ve bu nedenle bir gecikmeye neden olabilir önce uygulama bilgisi etiketleri başka ölçütlere göre hedefleme Azure Mobile Engagement toogather bilgileri, kullanıcıların cihazlarından gerektirir.</span><span class="sxs-lookup"><span data-stu-id="03e18-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="03e18-137">Karmaşık gönderim yapılandırması (rozetleri güncelleştirme gibi) seçenekler de geciktirebilir iter.</span><span class="sxs-lookup"><span data-stu-id="03e18-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="03e18-138">Hello mutlak hızlı itme yönteminde Azure Mobile Engagement bir "tek seferde" kampanya hello itme API kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="03e18-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="03e18-139">Uygulama bilgileri etiketleri hello sunucu tarafında depolandığından Reach Kampanya (ya da hello Reach API'sini veya hello UI) için anında iletme ölçüt olarak yalnızca uygulama bilgisi etiketleri kullanarak hello sonraki en hızlı yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="03e18-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="03e18-140">Azure Mobile Engagement sipariş toosend hello kampanya tooquery hello aygıtları olduğundan hedefleme diğer ölçütleri için bir itme kampanya hello en esnek ancak yavaş gönderme yöntemini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="03e18-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Reach Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="03e18-142">Ölçüt seçenekleri için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="03e18-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="03e18-143">**Technicals**</span><span class="sxs-lookup"><span data-stu-id="03e18-143">**Technicals**</span></span>     
* <span data-ttu-id="03e18-144">Bellenim name: ürün bilgisi adı</span><span class="sxs-lookup"><span data-stu-id="03e18-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="03e18-145">Bellenim sürümü: bellenim sürümü</span><span class="sxs-lookup"><span data-stu-id="03e18-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="03e18-146">Cihaz modeli: cihaz modeli</span><span class="sxs-lookup"><span data-stu-id="03e18-146">Device model:    Device model</span></span>
* <span data-ttu-id="03e18-147">Aygıt üreticisi: aygıt üreticisi</span><span class="sxs-lookup"><span data-stu-id="03e18-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="03e18-148">Uygulama sürümü: uygulama sürümü</span><span class="sxs-lookup"><span data-stu-id="03e18-148">Application version:    Application version</span></span>
* <span data-ttu-id="03e18-149">Taşıyıcı Adı: tanımsız taşıyıcı adı</span><span class="sxs-lookup"><span data-stu-id="03e18-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="03e18-150">Taşıyıcı Ülke: taşıyıcı ülke, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="03e18-151">Ağ türü: ağ türü</span><span class="sxs-lookup"><span data-stu-id="03e18-151">Network type:    Network type</span></span>
* <span data-ttu-id="03e18-152">Yerel ayar: yerel ayar</span><span class="sxs-lookup"><span data-stu-id="03e18-152">Locale:    Locale</span></span>
* <span data-ttu-id="03e18-153">Ekran boyutu: ekran boyutu</span><span class="sxs-lookup"><span data-stu-id="03e18-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="03e18-154">**Konum**</span><span class="sxs-lookup"><span data-stu-id="03e18-154">**Location**</span></span>      
* <span data-ttu-id="03e18-155">Alan bilinen son: ülke, bölge, Yerleşim Yeri</span><span class="sxs-lookup"><span data-stu-id="03e18-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="03e18-156">Gerçek zamanlı coğrafi yalıtma: POIs listesi (adı, Eylemler), döngüsel POI (adı, enlem, boylam, RADIUS metre içinde)</span><span class="sxs-lookup"><span data-stu-id="03e18-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="03e18-157">**Geri bildirim ulaşmak**</span><span class="sxs-lookup"><span data-stu-id="03e18-157">**Reach feedback**</span></span>     
* <span data-ttu-id="03e18-158">Duyuru geri bildirim: duyuru, geri bildirim</span><span class="sxs-lookup"><span data-stu-id="03e18-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="03e18-159">Yoklama geri bildirim: yoklama, geri bildirim</span><span class="sxs-lookup"><span data-stu-id="03e18-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="03e18-160">Yoklama yanıt geri bildirim: yoklama yanıt geri bildirim, soru, seçim</span><span class="sxs-lookup"><span data-stu-id="03e18-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="03e18-161">Verileri gönderme geri bildirim: veri gönderimi, geri bildirim</span><span class="sxs-lookup"><span data-stu-id="03e18-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="03e18-162">**Yükleme izlemesi**</span><span class="sxs-lookup"><span data-stu-id="03e18-162">**Install Tracking**</span></span>     
* <span data-ttu-id="03e18-163">Depo: Deposu, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="03e18-164">Kaynak: Kaynak, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="03e18-165">**Kullanıcı profili**</span><span class="sxs-lookup"><span data-stu-id="03e18-165">**User profile**</span></span>     
* <span data-ttu-id="03e18-166">Cinsiyetiniz: Erkek veya kadın, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="03e18-167">Doğum Tarihi: işleci, undefined tarihi</span><span class="sxs-lookup"><span data-stu-id="03e18-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="03e18-168">Katılımı: true veya false, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="03e18-169">**Uygulama bilgileri**</span><span class="sxs-lookup"><span data-stu-id="03e18-169">**App Info**</span></span>      
* <span data-ttu-id="03e18-170">Dizesi: tanımsız dize</span><span class="sxs-lookup"><span data-stu-id="03e18-170">String:    String, undefined</span></span>
* <span data-ttu-id="03e18-171">Tarihi: işleci, undefined tarihi</span><span class="sxs-lookup"><span data-stu-id="03e18-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="03e18-172">Tamsayı: işleç, sayı, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="03e18-173">Boole değeri: true veya false değerini, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="03e18-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="03e18-174">**Segment**</span><span class="sxs-lookup"><span data-stu-id="03e18-174">**Segment**</span></span>    
* <span data-ttu-id="03e18-175">Segment adını (aşağı açılan listeden), dışlama (Bu segmentin parçası olmayan kullanıcıları hedefleyin).</span><span class="sxs-lookup"><span data-stu-id="03e18-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

