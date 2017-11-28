---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - parçaları"
description: "Bilgi nasıl toocreate ve Azure Mobile Engagement kullanarak kullanıcıların tooidentify kullanım desenlerini kesimleri yönetme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="8c916-103">Nasıl toocreate ve kullanıcıların tooidentify kullanım desenlerini kesimleri yönetme</span><span class="sxs-lookup"><span data-stu-id="8c916-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="8c916-104">Bu makalede hello **KESİMLERİ** hello sekmesinde **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="8c916-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="8c916-105">Merhaba kullandığınız **Mobile Engagement** portal toomonitor ve mobil uygulamalarınızı yönetin.</span><span class="sxs-lookup"><span data-stu-id="8c916-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="8c916-106">Merhaba kesimleri hello UI bölümünü hello farklı bir davranışı ve hello uygulamadan elde edebilirsiniz ve hello kesimleri API da erişebilirsiniz analytics göre kullanıcılarınızın kesimlere üzerinde toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c916-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="8c916-107">Segment ilk 24 saat sonra oluşturuldukları ve bunlar her 24 saatte bir hello son analytics bilgilere göre yeniden hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="8c916-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="8c916-108">Kesimi hesaplanan sonra her gün bir "Günün tooday geçmişi" grafiğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8c916-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="8c916-109">Merhaba birçok bölümlerini **Mobile Engagement** portal UI içeren hello **YARDIMINI Göster** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8c916-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="8c916-110">Bu düğme tooget bir bölümü hakkında daha fazla kavramsal bilgi tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="8c916-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="8c916-111">Kesimleri oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c916-111">Create Segments</span></span>
<span data-ttu-id="8c916-112">Üzerinde belirli bir dönem için hello too60 günde yukarı too10 ölçütlerini göre segment oluşturabilirsiniz hello analytics bölümünden geçmiş.</span><span class="sxs-lookup"><span data-stu-id="8c916-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="8c916-113">Örneğin, belirli sayfalarını görüntülenebilir veya son 10 gün içinde Merhaba, uygulamanızın içinde belirli içerik arama hello kişiler üzerinde dayalı bir segment oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c916-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="8c916-114">Bu bilgiler hello analytics bölümünde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8c916-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="8c916-115">Bu nedenle, toocreate kesimi kullanın ve ardından bir anında iletme bildirimi tootarget kullanıcılar tooget bu kısmı ayarlayın bunları toocome geri toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="8c916-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="8c916-116">Bir segment hesaplanan sonra olamaz düzenlenemez; Bunu yalnızca (kopyalanmış) kopyalanması veya (silinmiş) yok.</span><span class="sxs-lookup"><span data-stu-id="8c916-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="8c916-117">Bir kesim içinde hello kopyalanıp aynı uygulamanın (ile aynı AppID hello), ve (ile farklı bir AppID) diğer uygulamalara da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="8c916-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="8c916-119">Örnekler parçaları</span><span class="sxs-lookup"><span data-stu-id="8c916-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="8c916-121">Segment toosegment hello son kullanıcılar, uygulamanızın izin verin.</span><span class="sxs-lookup"><span data-stu-id="8c916-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="8c916-122">Kullanıcılarınızın kesimlere bir önemli pazarlama stratejidir.</span><span class="sxs-lookup"><span data-stu-id="8c916-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="8c916-123">Azure Mobile Engagement tooget geçmiş verileri sağlar ve özel kesimleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="8c916-124">Bu güçlü bir araç uygulamanızda müşterilerinizin deneyimi hakkında toolearn sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c916-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="8c916-125">Kolayca segmentlerinizi çözümlemek ve segmentlerinizi itme hedefleri olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c916-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="8c916-126">Bir ortak kullanın-son kullanıcılar toorate toosend anında iletme bildirimi tooencourage istediğiniz durumdur hello deposu uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="8c916-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="8c916-127">Bir bildirim tooall son kullanıcılarınızı göndermek yerine, yalnızca uygulamanız her gün Merhaba geçen ay kullandınız ve iyi kullanıcı deneyimini beklendiğinden kullanıcılar belirtirsiniz bir segment oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c916-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="8c916-128">Daha az, hedeflenmiş anında iletme bildirimleri göndermek için daha iyi ROI alıyorum.</span><span class="sxs-lookup"><span data-stu-id="8c916-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="8c916-130">Oluşturabileceğiniz kesimleri hello önemli Azure Mobile Engagement öğelere dayanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8c916-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="8c916-131">Olay: hedefleri, bir belirli olay katından fazla bir hafta gerçekleşen hello uygulamasının bir segment oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="8c916-132">Oturumu: Merhaba uygulaması 5 defadan fazla geçen hafta kullanan kullanıcı kesimini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="8c916-133">Etkinliği: bir sayfa veya içeriği 10 saat geçen ay sayısından fazla veya az kullanılan kullanıcılar bir parçasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="8c916-134">Proje: bir iş birden fazla günde tamamladınız kullanıcılar bir parçasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c916-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="8c916-135">Kilitlenme: çökmeyle 10 kereden fazla geçen hafta beklendiğinden tüm hello kullanıcıların bir segment oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="8c916-136">(Bu bir apology veya hatta kupon kesimle itme!)</span><span class="sxs-lookup"><span data-stu-id="8c916-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="8c916-137">Hata: bir hata 100 kez birden fazla son 3 gün beklendiğinden tüm hello kullanıcıların bir segment oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="8c916-138">Uygulama bilgileri: son 25 gün hello sırasında gerçekleşen özel bir uygulama bilgisi hedefleyen bir segment oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="8c916-140">Segment toouse en iyi şekilde, özelleştirilmiş bir hello SDK tümleştirilmesi "Uygulama bilgisini" etiketlerin etiketleme bir plan ile uygulamanızda yapmış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c916-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="8c916-141">Ardından, hello arabiriminin toohello giriş sayfasına gidin, istediğiniz ve hello "Kesimleri" bölümünü tıklatın Merhaba uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="8c916-142">Merhaba "Kesimleri" bölümü seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="8c916-143">Yeni bir segment toocreate düğmesini hello "Yeni bir segment"'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8c916-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="8c916-144">Gerçek yaşam örnek: "Oturum" bilgilerine dayalı basit bir segment oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c916-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="8c916-145">Uygulamanızı hello geçen hafta en az 50 kez kullanmış tüm hello son kullanıcılar bir parçasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c916-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="8c916-146">Buradan, en az 30 saniye uygulamanızda oturum başına harcanan hello son bulur.</span><span class="sxs-lookup"><span data-stu-id="8c916-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="8c916-147">Bu uygulamayı olumlu bir deneyim sahibi tüm hello son kullanıcılar gösterir.</span><span class="sxs-lookup"><span data-stu-id="8c916-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="8c916-148">Sonra oluşturulan hello segment kullanılan toopush bildirim toothese son kullanıcılar tooask olabilir bunları hello uygulamanızda toorate depolar.</span><span class="sxs-lookup"><span data-stu-id="8c916-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="8c916-150">Segmentinize sipariş toofind bir ad verin, hızlı bir şekilde hello "Segment" listesi içinde.</span><span class="sxs-lookup"><span data-stu-id="8c916-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="8c916-151">Merhaba üzerinde "Oluştur" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c916-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="8c916-153">Oturumu seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="8c916-155">"Geçen hafta" Merhaba süre seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="8c916-156">İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8c916-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="8c916-158">Select hello hello liste arasında ilgili işleci: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="8c916-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="8c916-159">Merhaba istediğiniz sayısı girin.</span><span class="sxs-lookup"><span data-stu-id="8c916-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="8c916-160">Merhaba istediğiniz örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="8c916-161">İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8c916-161">Click next.</span></span>
   <span data-ttu-id="8c916-162">Bu örnekte, en az 50 oturumları yapmış olduğunuz kullanıcıları eşleştirmek geçen hafta bu üzerinden hello şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8c916-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="8c916-164">Hello oturum segment için bir ölçüt olarak oturumu başına hello uzunluğu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c916-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="8c916-165">Merhaba işleci hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="8c916-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="8c916-166">Oturum başına Hello uzunluğu belirtin.</span><span class="sxs-lookup"><span data-stu-id="8c916-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="8c916-167">İleri'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c916-167">Click Next.</span></span>
   <span data-ttu-id="8c916-168">Bu örnekte, tüm hello hello oluşumu bölümünde kesimli oturumları seçtiğinizden 30 saniyeden oturum başına harcanan hello kullanıcılar yazacaktır.</span><span class="sxs-lookup"><span data-stu-id="8c916-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="8c916-170">Ölçütünüzle hello içinde tamamlamak sipariş tooretrieve içinde ad Huni ve Son'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8c916-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="8c916-172">Ölçütünüzle ayar tamamlandığında hello segment Huni içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8c916-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="8c916-173">Bir segment çözümleme verilerini dayandığından, kesimleri günde bir kez hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="8c916-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="8c916-174">Bu örnekte, 47,7 hello toplam son kullanıcılar % hello ölçüt eşleşti.</span><span class="sxs-lookup"><span data-stu-id="8c916-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="8c916-175">İyi bir deneyim beklendiğinden hello kullanıcılar olmalıdır ve bunları bir bildirim gönderme varsa daha yüksek bir derecesinde olası tooprovide toorate hello uygulamayı hello Mağazası'nda yönergelerinin olması.</span><span class="sxs-lookup"><span data-stu-id="8c916-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c916-176">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8c916-176">See also</span></span>
* <span data-ttu-id="8c916-177">[Kavramları][Link 6]</span><span class="sxs-lookup"><span data-stu-id="8c916-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="8c916-178">[Sorun giderme kılavuzu hizmeti][Link 24]</span><span class="sxs-lookup"><span data-stu-id="8c916-178">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

