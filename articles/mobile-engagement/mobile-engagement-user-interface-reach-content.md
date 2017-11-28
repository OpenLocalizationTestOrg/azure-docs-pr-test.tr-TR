---
title: "Azure Mobile Engagement kullanıcı arabirimi - ulaşma içeriği"
description: "Anında iletme bildirimi kampanyaları Azure Mobile Engagement, farklı türdeki benzersiz içerik yönetmeyi öğrenin"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="daa09-103">Anında iletme bildirimi kampanyaları farklı türde benzersiz içeriği yönetme</span><span class="sxs-lookup"><span data-stu-id="daa09-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="daa09-104">İçerik Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone) değiştirmek için yeni bir reach kampanya içerik bölümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="daa09-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="daa09-105">İçerik anında iletme kampanyalarını kampanya türüne belirli ayarıdır.</span><span class="sxs-lookup"><span data-stu-id="daa09-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="daa09-106">İçerik türleri:</span><span class="sxs-lookup"><span data-stu-id="daa09-106">Content types:</span></span>
* <span data-ttu-id="daa09-107">Duyurular</span><span class="sxs-lookup"><span data-stu-id="daa09-107">Announcements</span></span>
* <span data-ttu-id="daa09-108">Anketler</span><span class="sxs-lookup"><span data-stu-id="daa09-108">Polls</span></span>
* <span data-ttu-id="daa09-109">Veri gönderimleri</span><span class="sxs-lookup"><span data-stu-id="daa09-109">Data pushes</span></span>
* <span data-ttu-id="daa09-110">Kutucuklar (yalnızca Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="daa09-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="daa09-111">Duyurular içeriği</span><span class="sxs-lookup"><span data-stu-id="daa09-111">Content of Announcements</span></span>
 ![Reach Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="daa09-113">Duyurunuzun türünü seçin:</span><span class="sxs-lookup"><span data-stu-id="daa09-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="daa09-114">Yalnızca bildirim: Basit standart bir bildirim değil.</span><span class="sxs-lookup"><span data-stu-id="daa09-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="daa09-115">Bu kullanıcı üzerinde tıklatır, ek görünüm yok görünür, ancak yalnızca kendisine ilişkili eylemin oluşacağını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="daa09-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="daa09-116">Metin duyuru: metin görünümü bakın kullanıcıya prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="daa09-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="daa09-117">Web duyuru: kullanıcının bir web görünümü göz prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="daa09-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="daa09-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="daa09-118">See also</span></span>
* <span data-ttu-id="daa09-119">[Ulaşmaya - nasıl yapılır - duyuruları][Link 3]</span><span class="sxs-lookup"><span data-stu-id="daa09-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="daa09-120">Web görünümü duyuruları hakkında:</span><span class="sxs-lookup"><span data-stu-id="daa09-120">About Web View Announcements:</span></span>
<span data-ttu-id="daa09-121">Deseninin "{DeviceID}" Burada sağladığınız HTML kodunda veya JavaScript kodunda, duyuruyu görüntüleyen cihazın tanımlayıcısı ile otomatik olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="daa09-122">Bu işlem arka ofisinizde barındırılan bir dış web hizmetindeki Azure Mobile Engagement cihaz tanımlayıcılarının alınması için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="daa09-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="daa09-123">Bir tam ekran web görünümü oluşturmak isterseniz (sağladığımız varsayılan Eylem ve Çıkış düğmeleri olmadan), web görünümü duyurularının JavaScript kodundan aşağıdaki işlevleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="daa09-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="daa09-124">Duyuru eylemini gerçekleştir: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="daa09-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="daa09-125">duyurudan Çık: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="daa09-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="daa09-126">Eylem seçin:</span><span class="sxs-lookup"><span data-stu-id="daa09-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="daa09-127">Eylem URL'ler hakkında:</span><span class="sxs-lookup"><span data-stu-id="daa09-127">About Action URLs:</span></span>
<span data-ttu-id="daa09-128">Hedeflenen cihazın işletim sistemi tarafından yorumlanabilen herhangi bir URL, eylem URL'si olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="daa09-129">Uygulamanızın destekleyebileceği herhangi bir ayrılmış URL de (örn. kullanıcıların belirli bir ekrana atlaması için) eylem URL'si olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="daa09-130">{DeviceID} deseninin her oluşumu, eylemi gerçekleştiren cihazın tanımlayıcısı ile otomatik olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="daa09-131">Bu işlem arka ofisinizde barındırılan bir dış web hizmeti aracılığıyla Azure Mobile Engagement cihaz tanımlayıcılarını kolayca almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="daa09-132">**Android + iOS Eylemler**</span><span class="sxs-lookup"><span data-stu-id="daa09-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="daa09-133">Web sayfası aç</span><span class="sxs-lookup"><span data-stu-id="daa09-133">Open a web page</span></span>
  * <span data-ttu-id="daa09-134">http://\[web-sitesi-etki alanı\]</span><span class="sxs-lookup"><span data-stu-id="daa09-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="daa09-135">Örnek: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="daa09-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="daa09-136">E-posta gönder</span><span class="sxs-lookup"><span data-stu-id="daa09-136">Send an e-mail</span></span>
  * <span data-ttu-id="daa09-137">mailto:\[e-posta alıcı\]? konu =\[konu\]& Gövde =\[iletisi\]</span><span class="sxs-lookup"><span data-stu-id="daa09-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="daa09-138">Example:mailto:foo@example.com? Konu Tebrikler % 20from % 20Azure % 20Mobile % 20Engagement =! & Gövde iyi % 20stuff =!</span><span class="sxs-lookup"><span data-stu-id="daa09-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="daa09-139">SMS gönder</span><span class="sxs-lookup"><span data-stu-id="daa09-139">Send a SMS</span></span>
  * <span data-ttu-id="daa09-140">SMS:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="daa09-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="daa09-141">Örnek: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="daa09-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="daa09-142">Telefon numarası çevir</span><span class="sxs-lookup"><span data-stu-id="daa09-142">Dial a phone number</span></span>
  * <span data-ttu-id="daa09-143">Tel:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="daa09-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="daa09-144">Örnek: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="daa09-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="daa09-145">**Android yalnızca Eylemler**</span><span class="sxs-lookup"><span data-stu-id="daa09-145">**Android only actions**</span></span>
  * <span data-ttu-id="daa09-146">Play Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="daa09-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="daa09-147">Market://details?id=\[uygulama paketi\]</span><span class="sxs-lookup"><span data-stu-id="daa09-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="daa09-148">Örnek: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="daa09-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="daa09-149">Coğrafi olarak yerelleştirilmiş arama başlat</span><span class="sxs-lookup"><span data-stu-id="daa09-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="daa09-150">GEO:0, 0? q =\[arama sorgusu\]</span><span class="sxs-lookup"><span data-stu-id="daa09-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="daa09-151">Örnek: geo:0, 0? q starbucks, paris =</span><span class="sxs-lookup"><span data-stu-id="daa09-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="daa09-152">**iOS yalnızca Eylemler**</span><span class="sxs-lookup"><span data-stu-id="daa09-152">**iOS only actions**</span></span>
  * <span data-ttu-id="daa09-153">App Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="daa09-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="daa09-154">http://iTunes.apple.com/ [Ülke] /app/ [uygulama adı] /id [uygulama kimliği]? mt = 8</span><span class="sxs-lookup"><span data-stu-id="daa09-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="daa09-155">Örnek: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="daa09-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="daa09-156">Windows işlemleri</span><span class="sxs-lookup"><span data-stu-id="daa09-156">Windows Actions</span></span>
  * <span data-ttu-id="daa09-157">Web sayfası aç</span><span class="sxs-lookup"><span data-stu-id="daa09-157">Open a web page</span></span>
  * <span data-ttu-id="daa09-158">http://\[web-sitesi-etki alanı\]</span><span class="sxs-lookup"><span data-stu-id="daa09-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="daa09-159">Örnek: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="daa09-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="daa09-160">E-posta gönder</span><span class="sxs-lookup"><span data-stu-id="daa09-160">Send an e-mail</span></span>
  * <span data-ttu-id="daa09-161">mailto:\[e-posta alıcı\]? konu =\[konu\]& Gövde =\[iletisi\]</span><span class="sxs-lookup"><span data-stu-id="daa09-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="daa09-162">Example:mailto:foo@example.com? Konu Tebrikler % 20from % 20Azure % 20Mobile % 20Engagement =! & Gövde iyi % 20stuff =!</span><span class="sxs-lookup"><span data-stu-id="daa09-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="daa09-163">SMS gönder (Skype Store App gerekli)</span><span class="sxs-lookup"><span data-stu-id="daa09-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="daa09-164">SMS:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="daa09-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="daa09-165">Örnek: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="daa09-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="daa09-166">Telefon numarası çevir (Skype Store App gereklidir)</span><span class="sxs-lookup"><span data-stu-id="daa09-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="daa09-167">Tel:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="daa09-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="daa09-168">Örnek: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="daa09-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="daa09-169">Play Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="daa09-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="daa09-170">MS-windows-deposu: PDP? PFN =\[uygulama paket kimliği\]</span><span class="sxs-lookup"><span data-stu-id="daa09-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="daa09-171">Örnek: ms-windows-deposu: PDP? PFN 4d91298a-07cb-40fb-aecc-4cb5615d53c1 =</span><span class="sxs-lookup"><span data-stu-id="daa09-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="daa09-172">Bingmaps araması başlat</span><span class="sxs-lookup"><span data-stu-id="daa09-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="daa09-173">bingmaps:? q =\[arama sorgusu\]</span><span class="sxs-lookup"><span data-stu-id="daa09-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="daa09-174">Örnek: bingmaps:? q starbucks, paris =</span><span class="sxs-lookup"><span data-stu-id="daa09-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="daa09-175">Özel şema kullan</span><span class="sxs-lookup"><span data-stu-id="daa09-175">Use a custom scheme</span></span>
  * <span data-ttu-id="daa09-176">\[Özel şema\]://\[özel şema parametreleri\]</span><span class="sxs-lookup"><span data-stu-id="daa09-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="daa09-177">Örnek: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="daa09-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="daa09-178">Paket verileri (Store App gerekli okuma uzantısı) kullan</span><span class="sxs-lookup"><span data-stu-id="daa09-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="daa09-179">\[klasör\]\[veri\].\[ uzantısı\]</span><span class="sxs-lookup"><span data-stu-id="daa09-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="daa09-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="daa09-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="daa09-181">Bir izleme URL'si oluşturun:</span><span class="sxs-lookup"><span data-stu-id="daa09-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="daa09-182">"Ayarlar" bölümüne bakın <UI Documentation> için bir izleme URL'si oluşturmak üzerinde yönerge kullanıcıların diğer uygulamalarınızdan birini indirmeye izin verir.</span><span class="sxs-lookup"><span data-stu-id="daa09-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="daa09-183">Duyurunuzun metinlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="daa09-183">Define the texts of your announcement</span></span>
<span data-ttu-id="daa09-184">Başlık, içerik ve düğmesi duyurunuzun metinlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="daa09-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="daa09-185">Kullanıcılar bu kampanyaya nasıl yanıt, erişim görüş dayanarak gelecekteki bir kampanyanın bir izleyici hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daa09-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="daa09-186">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen geribildirim bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="daa09-187">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="daa09-187">See also</span></span>
* <span data-ttu-id="daa09-188">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="daa09-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="daa09-189">Anketler içeriği</span><span class="sxs-lookup"><span data-stu-id="daa09-189">Content of Polls</span></span>
![Reach Content2][31] 

<span data-ttu-id="daa09-191">Başlık, açıklama ve düğmesi duyurunuzun metinlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="daa09-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="daa09-192">Ardından, sorular ve sorularınızın yanıtlarını seçenekleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="daa09-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="daa09-193">Kullanıcılar bu kampanyaya nasıl yanıt, erişim görüş dayanarak gelecekteki bir kampanyanın bir izleyici hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daa09-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="daa09-194">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="daa09-195">Dinleyici da yoklama yanıt geri bildirim, soru ve yanıt seçim ölçütü olarak kullanıldığı temel alabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="daa09-196">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="daa09-196">See also</span></span>
* <span data-ttu-id="daa09-197">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="daa09-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="daa09-198">Veri gönderimleri içeriği</span><span class="sxs-lookup"><span data-stu-id="daa09-198">Content of Data Pushes</span></span>
![Reach Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="daa09-200">Verilerinizin türünü seçin:</span><span class="sxs-lookup"><span data-stu-id="daa09-200">Choose the type of your data:</span></span>
* <span data-ttu-id="daa09-201">Metin</span><span class="sxs-lookup"><span data-stu-id="daa09-201">Text</span></span>
* <span data-ttu-id="daa09-202">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="daa09-202">Binary data</span></span>
* <span data-ttu-id="daa09-203">Base64 veri</span><span class="sxs-lookup"><span data-stu-id="daa09-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="daa09-204">Verilerinizin içeriğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="daa09-204">Define the content of your data</span></span>
* <span data-ttu-id="daa09-205">Metin veri göndermeyi seçtiyseniz, kopyalamak ve metin "içerik" kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="daa09-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="daa09-206">İkili veya base64 veri göndermeyi seçtiyseniz, dosyanızı karşıya yüklemek için "dosyanızı karşıya yükle" düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="daa09-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="daa09-207">Kullanıcılar bu kampanyaya nasıl yanıt, erişim görüş dayanarak gelecekteki bir kampanyanın bir izleyici hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daa09-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="daa09-208">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="daa09-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="daa09-209">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="daa09-209">See also</span></span>
* <span data-ttu-id="daa09-210">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="daa09-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="daa09-211">İçerik döşeme (yalnızca Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="daa09-211">Content of Tiles (Windows Phone only)</span></span>
![Reach Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="daa09-213">Kutucuğunuzun içeriğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="daa09-213">Define the content of your tile</span></span>
<span data-ttu-id="daa09-214">Döşeme yükü uygulamanızı Windows Phone cihazlarda döşemesinin görüntülenecek metindir.</span><span class="sxs-lookup"><span data-stu-id="daa09-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="daa09-215">Döşeme push yerel gönderim Windows Phone için Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="daa09-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="daa09-216">Döşeme anında iletme türü yanıt yok yalnızca gönderme türü ve gelecekteki Kampanyalar İzleyici döşeme itme kampanya sonuçlarına böylece oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="daa09-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="daa09-217">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="daa09-217">See also</span></span>
* <span data-ttu-id="daa09-218">[API belgelerine - ulaşma API - yerel gönderim][Link 4]</span><span class="sxs-lookup"><span data-stu-id="daa09-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

