---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - ulaşmak içerik"
description: "Nasıl Azure Mobile Engagement toomanage hello benzersiz içerik türlerinin hello farklı anında iletme bildirimi kampanyaları öğrenin"
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
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="14432-103">Nasıl toomanage hello hello farklı türde anında iletme bildirimi kampanyaları benzersiz içerik</span><span class="sxs-lookup"><span data-stu-id="14432-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="14432-104">Merhaba içerik bölümü yeni reach kampanya toomodify hello içerik Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14432-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="14432-105">Merhaba içerik anında iletme kampanyalarını kampanya belirli toohello türü ayarıdır.</span><span class="sxs-lookup"><span data-stu-id="14432-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="14432-106">İçerik türleri:</span><span class="sxs-lookup"><span data-stu-id="14432-106">Content types:</span></span>
* <span data-ttu-id="14432-107">Duyurular</span><span class="sxs-lookup"><span data-stu-id="14432-107">Announcements</span></span>
* <span data-ttu-id="14432-108">Anketler</span><span class="sxs-lookup"><span data-stu-id="14432-108">Polls</span></span>
* <span data-ttu-id="14432-109">Veri gönderimleri</span><span class="sxs-lookup"><span data-stu-id="14432-109">Data pushes</span></span>
* <span data-ttu-id="14432-110">Kutucuklar (yalnızca Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="14432-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="14432-111">Duyurular içeriği</span><span class="sxs-lookup"><span data-stu-id="14432-111">Content of Announcements</span></span>
 ![Reach Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="14432-113">Merhaba duyurunuzun türünü seçin:</span><span class="sxs-lookup"><span data-stu-id="14432-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="14432-114">Yalnızca bildirim: Basit standart bir bildirim değil.</span><span class="sxs-lookup"><span data-stu-id="14432-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="14432-115">Kullanıcı üzerinde tıklatır, ek görünüm yok görünür, ancak yalnızca hello eylem ilişkili tooit ortaya çıkar anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="14432-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="14432-116">Metin duyuru: hello kullanıcı toohave metin görünümü göz prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="14432-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="14432-117">Web duyuru: hello kullanıcı toohave bir web görünümü göz prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="14432-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="14432-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14432-118">See also</span></span>
* <span data-ttu-id="14432-119">[Ulaşmaya - nasıl yapılır - duyuruları][Link 3]</span><span class="sxs-lookup"><span data-stu-id="14432-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="14432-120">Web görünümü duyuruları hakkında:</span><span class="sxs-lookup"><span data-stu-id="14432-120">About Web View Announcements:</span></span>
<span data-ttu-id="14432-121">Merhaba desende "{DeviceID}" Merhaba HTML kodunda veya JavaScript kodunda Burada sağladığınız oluşumları hello cihazın tanımlayıcısı ile Merhaba duyuru görüntüleme hello tarafından otomatik olarak değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="14432-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="14432-122">Bir dış bir kolay bir yolu tooretrieve Azure Mobile Engagement cihaz tanımlayıcılarının budur web işlem arka ofisinizde barındırılan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="14432-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="14432-123">Toocreate istiyorsanız, bir tam ekran web görünümü (sağladığımız hello varsayılan eylem ve çıkış düğmeleri olmadan) işlevleri, web görünümü duyurularının JavaScript kodundan aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14432-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="14432-124">Merhaba duyuru eylemini gerçekleştir: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="14432-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="14432-125">Merhaba duyurudan Çık: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="14432-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="14432-126">Eylem seçin:</span><span class="sxs-lookup"><span data-stu-id="14432-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="14432-127">Eylem URL'ler hakkında:</span><span class="sxs-lookup"><span data-stu-id="14432-127">About Action URLs:</span></span>
<span data-ttu-id="14432-128">Hedeflenen cihazın işletim sistemi tarafından yorumlanabilen herhangi bir URL, eylem URL'si olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="14432-129">Herhangi bir ayrılmış uygulamanız olabilir URL (örneğin tooa belirli ekran atlama toomake kullanıcılar) desteği eylem URL'si olarak da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="14432-130">Merhaba {DeviceID} deseninin her oluşumu hello cihazın tanımlayıcısı ile Merhaba eylemi gerçekleştirmeden hello tarafından otomatik olarak değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="14432-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="14432-131">Bu işlem arka ofisinizde barındırılan bir dış web hizmeti aracılığıyla kullanılan tooeasily alma Azure Mobile Engagement cihaz tanımlayıcılarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="14432-132">**Android + iOS Eylemler**</span><span class="sxs-lookup"><span data-stu-id="14432-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="14432-133">Web sayfası aç</span><span class="sxs-lookup"><span data-stu-id="14432-133">Open a web page</span></span>
  * <span data-ttu-id="14432-134">http://\[web-sitesi-etki alanı\]</span><span class="sxs-lookup"><span data-stu-id="14432-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="14432-135">Örnek: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="14432-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="14432-136">E-posta gönder</span><span class="sxs-lookup"><span data-stu-id="14432-136">Send an e-mail</span></span>
  * <span data-ttu-id="14432-137">mailto:\[e-posta alıcı\]? konu =\[konu\]& Gövde =\[iletisi\]</span><span class="sxs-lookup"><span data-stu-id="14432-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="14432-138">Example:mailto:foo@example.com? Konu Tebrikler % 20from % 20Azure % 20Mobile % 20Engagement =! & Gövde iyi % 20stuff =!</span><span class="sxs-lookup"><span data-stu-id="14432-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="14432-139">SMS gönder</span><span class="sxs-lookup"><span data-stu-id="14432-139">Send a SMS</span></span>
  * <span data-ttu-id="14432-140">SMS:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="14432-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="14432-141">Örnek: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="14432-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="14432-142">Telefon numarası çevir</span><span class="sxs-lookup"><span data-stu-id="14432-142">Dial a phone number</span></span>
  * <span data-ttu-id="14432-143">Tel:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="14432-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="14432-144">Örnek: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="14432-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="14432-145">**Android yalnızca Eylemler**</span><span class="sxs-lookup"><span data-stu-id="14432-145">**Android only actions**</span></span>
  * <span data-ttu-id="14432-146">Merhaba Play Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="14432-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="14432-147">Market://details?id=\[uygulama paketi\]</span><span class="sxs-lookup"><span data-stu-id="14432-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="14432-148">Örnek: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="14432-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="14432-149">Coğrafi olarak yerelleştirilmiş arama başlat</span><span class="sxs-lookup"><span data-stu-id="14432-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="14432-150">GEO:0, 0? q =\[arama sorgusu\]</span><span class="sxs-lookup"><span data-stu-id="14432-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="14432-151">Örnek: geo:0, 0? q starbucks, paris =</span><span class="sxs-lookup"><span data-stu-id="14432-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="14432-152">**iOS yalnızca Eylemler**</span><span class="sxs-lookup"><span data-stu-id="14432-152">**iOS only actions**</span></span>
  * <span data-ttu-id="14432-153">Merhaba App Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="14432-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="14432-154">http://iTunes.apple.com/ [Ülke] /app/ [uygulama adı] /id [uygulama kimliği]? mt = 8</span><span class="sxs-lookup"><span data-stu-id="14432-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="14432-155">Örnek: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="14432-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="14432-156">Windows işlemleri</span><span class="sxs-lookup"><span data-stu-id="14432-156">Windows Actions</span></span>
  * <span data-ttu-id="14432-157">Web sayfası aç</span><span class="sxs-lookup"><span data-stu-id="14432-157">Open a web page</span></span>
  * <span data-ttu-id="14432-158">http://\[web-sitesi-etki alanı\]</span><span class="sxs-lookup"><span data-stu-id="14432-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="14432-159">Örnek: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="14432-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="14432-160">E-posta gönder</span><span class="sxs-lookup"><span data-stu-id="14432-160">Send an e-mail</span></span>
  * <span data-ttu-id="14432-161">mailto:\[e-posta alıcı\]? konu =\[konu\]& Gövde =\[iletisi\]</span><span class="sxs-lookup"><span data-stu-id="14432-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="14432-162">Example:mailto:foo@example.com? Konu Tebrikler % 20from % 20Azure % 20Mobile % 20Engagement =! & Gövde iyi % 20stuff =!</span><span class="sxs-lookup"><span data-stu-id="14432-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="14432-163">SMS gönder (Skype Store App gerekli)</span><span class="sxs-lookup"><span data-stu-id="14432-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="14432-164">SMS:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="14432-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="14432-165">Örnek: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="14432-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="14432-166">Telefon numarası çevir (Skype Store App gereklidir)</span><span class="sxs-lookup"><span data-stu-id="14432-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="14432-167">Tel:\[telefon numarası\]</span><span class="sxs-lookup"><span data-stu-id="14432-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="14432-168">Örnek: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="14432-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="14432-169">Merhaba Play Store'dan bir uygulama indirin</span><span class="sxs-lookup"><span data-stu-id="14432-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="14432-170">MS-windows-deposu: PDP? PFN =\[uygulama paket kimliği\]</span><span class="sxs-lookup"><span data-stu-id="14432-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="14432-171">Örnek: ms-windows-deposu: PDP? PFN 4d91298a-07cb-40fb-aecc-4cb5615d53c1 =</span><span class="sxs-lookup"><span data-stu-id="14432-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="14432-172">Bingmaps araması başlat</span><span class="sxs-lookup"><span data-stu-id="14432-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="14432-173">bingmaps:? q =\[arama sorgusu\]</span><span class="sxs-lookup"><span data-stu-id="14432-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="14432-174">Örnek: bingmaps:? q starbucks, paris =</span><span class="sxs-lookup"><span data-stu-id="14432-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="14432-175">Özel şema kullan</span><span class="sxs-lookup"><span data-stu-id="14432-175">Use a custom scheme</span></span>
  * <span data-ttu-id="14432-176">\[Özel şema\]://\[özel şema parametreleri\]</span><span class="sxs-lookup"><span data-stu-id="14432-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="14432-177">Örnek: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="14432-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="14432-178">Paket verileri (Store App gerekli okuma uzantısı) kullan</span><span class="sxs-lookup"><span data-stu-id="14432-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="14432-179">\[klasör\]\[veri\].\[ uzantısı\]</span><span class="sxs-lookup"><span data-stu-id="14432-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="14432-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="14432-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="14432-181">Bir izleme URL'si oluşturun:</span><span class="sxs-lookup"><span data-stu-id="14432-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="14432-182">Bkz: hello "Ayarlar" bölümünü hello <UI Documentation> için bir izleme URL'si oluşturmak üzerinde yönerge kullanıcılar toodownload diğer uygulamalarınızı birini izin verir.</span><span class="sxs-lookup"><span data-stu-id="14432-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="14432-183">Merhaba duyurunuzun metinlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="14432-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="14432-184">Merhaba başlık, içerik ve düğmesi duyurunuzun metinlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="14432-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="14432-185">Bir izleyici kullanıcıları toothis kampanya nasıl yanıt verdiğini, hello ulaşma geri bildirimi doğrultusunda gelecekteki bir kampanyanın hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14432-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="14432-186">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen, hello geribildirim bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="14432-187">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14432-187">See also</span></span>
* <span data-ttu-id="14432-188">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="14432-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="14432-189">Anketler içeriği</span><span class="sxs-lookup"><span data-stu-id="14432-189">Content of Polls</span></span>
![Reach Content2][31] 

<span data-ttu-id="14432-191">Merhaba başlık, açıklama ve düğmesi duyurunuzun metinlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="14432-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="14432-192">Ardından, sorular ve seçenekleri hello yanıtlar tooyour sorular için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="14432-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="14432-193">Bir izleyici kullanıcıları toothis kampanya nasıl yanıt verdiğini, hello ulaşma geri bildirimi doğrultusunda gelecekteki bir kampanyanın hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14432-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="14432-194">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="14432-195">Dinleyici ayrıca hello soru ve yanıt seçim ölçütü olarak kullanılan burada yoklama yanıt geri bildirim temel alabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="14432-196">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14432-196">See also</span></span>
* <span data-ttu-id="14432-197">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="14432-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="14432-198">Veri gönderimleri içeriği</span><span class="sxs-lookup"><span data-stu-id="14432-198">Content of Data Pushes</span></span>
![Reach Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="14432-200">Verilerinizi Hello türünü seçin:</span><span class="sxs-lookup"><span data-stu-id="14432-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="14432-201">Metin</span><span class="sxs-lookup"><span data-stu-id="14432-201">Text</span></span>
* <span data-ttu-id="14432-202">İkili veriler</span><span class="sxs-lookup"><span data-stu-id="14432-202">Binary data</span></span>
* <span data-ttu-id="14432-203">Base64 veri</span><span class="sxs-lookup"><span data-stu-id="14432-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="14432-204">Merhaba, verilerinizin içeriğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="14432-204">Define hello content of your data</span></span>
* <span data-ttu-id="14432-205">Toopush metin veri seçtiyseniz, kopyalamak ve hello metin hello "içerik" kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="14432-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="14432-206">Toopush seçtiyseniz, ikili veya base64 veri dosyanızın hello "dosyanızı karşıya yükle" düğmesini tooupload kullanın.</span><span class="sxs-lookup"><span data-stu-id="14432-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="14432-207">Bir izleyici kullanıcıları toothis kampanya nasıl yanıt verdiğini, hello ulaşma geri bildirimi doğrultusunda gelecekteki bir kampanyanın hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14432-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="14432-208">Dinleyici olup bu kampanyayı yalnızca, yanıtlanan, eylem yapılan veya Çıkılan gönderilen bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="14432-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="14432-209">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14432-209">See also</span></span>
* <span data-ttu-id="14432-210">[UI belgeleri - Reach - yeni itme ölçüt][Link 28]</span><span class="sxs-lookup"><span data-stu-id="14432-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="14432-211">İçerik döşeme (yalnızca Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="14432-211">Content of Tiles (Windows Phone only)</span></span>
![Reach Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="14432-213">Merhaba kutucuğunuzun içeriğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="14432-213">Define hello content of your tile</span></span>
<span data-ttu-id="14432-214">Windows Phone cihazlarda, uygulamanızın hello kutucuğunda görüntülenen hello metin toobe Hello döşeme yükü olduğu.</span><span class="sxs-lookup"><span data-stu-id="14432-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="14432-215">Döşeme push hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS), Windows Phone için bir yerel gönderim sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="14432-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="14432-216">Merhaba döşeme itme türü, yanıt yok hello yalnızca anında iletme türü ve bu nedenle gelecekteki Kampanyalar hello İzleyici döşeme itme kampanya hello sonuçlarını oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="14432-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="14432-217">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="14432-217">See also</span></span>
* <span data-ttu-id="14432-218">[API belgelerine - ulaşma API - yerel gönderim][Link 4]</span><span class="sxs-lookup"><span data-stu-id="14432-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

