---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - hizmet"
description: "Azure Mobile Engagement için kılavuzları sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="f0d99-103">Hizmet sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f0d99-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="f0d99-104">Merhaba, nasıl Azure Mobile Engagement çalışır karşılaşabileceğiniz olası sorunlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="f0d99-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="f0d99-105">Hizmet kesintisi</span><span class="sxs-lookup"><span data-stu-id="f0d99-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="f0d99-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="f0d99-106">Issue</span></span>
* <span data-ttu-id="f0d99-107">Azure Mobile Engagement hizmet kesintileri tarafından neden toobe görünür sorunları.</span><span class="sxs-lookup"><span data-stu-id="f0d99-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="f0d99-108">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="f0d99-108">Causes</span></span>
* <span data-ttu-id="f0d99-109">Azure Mobile Engagement hizmet kesintileri tarafından neden toobe görünür sorunları birkaç farklı nedenlerden kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="f0d99-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="f0d99-110">İlk olarak Azure Mobile Engagement, sistemle ilgili tooall görünür yalıtılmış sorunları</span><span class="sxs-lookup"><span data-stu-id="f0d99-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="f0d99-111">Bilinen sorunlar sunucu kesintileri (her zaman sunucu durumunda gösterir) nedeni:</span><span class="sxs-lookup"><span data-stu-id="f0d99-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="f0d99-112">Gecikmeler, hedefleme hataları, rozet güncelleştirmesini sorunları, toplama, çalışma anında durakları istatistikleri durdurma zamanlama, API'nin Dur çalışma, yeni uygulamalar veya kullanıcılar oluşturulamaz, DNS hataları ve zaman aşımı hataları hello UI, API veya uygulamaları bir cihazda.</span><span class="sxs-lookup"><span data-stu-id="f0d99-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="f0d99-113">Bulut bağımlılık kesintileri [Azure hizmet durumu](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f0d99-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="f0d99-114">Bildirim Hizmetleri (PNS) bağımlılık kesintileri bildirme</span><span class="sxs-lookup"><span data-stu-id="f0d99-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="f0d99-115">Uygulama mağazası kesintileri</span><span class="sxs-lookup"><span data-stu-id="f0d99-115">App Store Outages</span></span>

1) <span data-ttu-id="f0d99-116">Merhaba sorunun sistemle ilgili olup olmadığını tootest toosee aynı farklı bir işlevi hello test edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f0d99-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="f0d99-117">Azure Mobile Engagement uygulama tümleşik</span><span class="sxs-lookup"><span data-stu-id="f0d99-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="f0d99-118">Test cihazı</span><span class="sxs-lookup"><span data-stu-id="f0d99-118">Test device</span></span>
* <span data-ttu-id="f0d99-119">Test aygıt işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="f0d99-119">Test device OS version</span></span>
* <span data-ttu-id="f0d99-120">Kampanya</span><span class="sxs-lookup"><span data-stu-id="f0d99-120">Campaign</span></span>
* <span data-ttu-id="f0d99-121">Yönetici kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="f0d99-121">Administrator user account</span></span>
* <span data-ttu-id="f0d99-122">Tarayıcı (IE, Firefox, Chrome, vb.)</span><span class="sxs-lookup"><span data-stu-id="f0d99-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="f0d99-123">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="f0d99-123">Computer</span></span>

2) <span data-ttu-id="f0d99-124">Merhaba sorun yalnızca hello UI veya hello API'nin etkilerse tootest:</span><span class="sxs-lookup"><span data-stu-id="f0d99-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="f0d99-125">Aynı hem hello Azure Mobile Engagement UI işlev ve Azure Mobile Engagement API'nin hello hello sınayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="f0d99-126">Cep telefonu ağınızla Hello sorun olması durumunda tootest:</span><span class="sxs-lookup"><span data-stu-id="f0d99-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="f0d99-127">Bağlı toohello Internet WIFI üzerinden ve 3 G cep telefonu ağınız bağlıyken sırasında test edin.</span><span class="sxs-lookup"><span data-stu-id="f0d99-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="f0d99-128">Güvenlik duvarınızın hello Azure Mobile Engagement IP adresleri ya da bağlantı noktalarını herhangi birini engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f0d99-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="f0d99-129">Merhaba cihazınızla sorunsa tootest:</span><span class="sxs-lookup"><span data-stu-id="f0d99-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="f0d99-130">Cihazınızı başka bir Azure Mobile Engagement tümleşik uygulaması ile Mobile Engagement mümkün tooconnect tooAzure ise test edin.</span><span class="sxs-lookup"><span data-stu-id="f0d99-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="f0d99-131">Hello Azure Mobile Engagement UI görülebilir telefonunuzdan gelen olayları, işler ve kilitlenme oluşturabilir sınayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="f0d99-132">Kendi cihaz Kimliği'nde dayalı hello Azure Mobile Engagement UI tooyour aygıttan anında iletme bildirimleri göndermek, test etme</span><span class="sxs-lookup"><span data-stu-id="f0d99-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="f0d99-133">Merhaba, uygulamanızı sorunsa tootest:</span><span class="sxs-lookup"><span data-stu-id="f0d99-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="f0d99-134">Yükleyin ve yerine bir öykünücü fiziksel CİHAZDAN uygulamanızı test edin:</span><span class="sxs-lookup"><span data-stu-id="f0d99-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="f0d99-135">işletim sistemi yükseltmeleri tooend kullanıcıyla SDK yükseltme tooresolve gerektiren cihazlar Hello sorun olması durumunda tootest:</span><span class="sxs-lookup"><span data-stu-id="f0d99-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="f0d99-136">Uygulamanızın farklı sürümlerini hello işletim sistemi ile farklı cihazlarda sınayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="f0d99-137">Merhaba hello SDK en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f0d99-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="f0d99-138">Bağlantısı ve yanlış bilgi sorunları</span><span class="sxs-lookup"><span data-stu-id="f0d99-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="f0d99-139">Sorun</span><span class="sxs-lookup"><span data-stu-id="f0d99-139">Issue</span></span>
* <span data-ttu-id="f0d99-140">Oturum açma sorunları Azure Mobile Engagement UI hello.</span><span class="sxs-lookup"><span data-stu-id="f0d99-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="f0d99-141">Bağlantı hatalarını hello Azure Mobile Engagement API's ile.</span><span class="sxs-lookup"><span data-stu-id="f0d99-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="f0d99-142">Uygulama bilgileri etiketleri hello aygıt API karşıya yükleme sorunları.</span><span class="sxs-lookup"><span data-stu-id="f0d99-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="f0d99-143">Sorunları günlüklerini veya dışarı aktarılan verileri Azure Mobile Engagement'tan yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="f0d99-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="f0d99-144">Hello Azure Mobile Engagement UI gösterilen yanlış bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0d99-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="f0d99-145">Azure Mobile Engagement günlüklerde gösterilen yanlış bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0d99-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="f0d99-146">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="f0d99-146">Causes</span></span>
* <span data-ttu-id="f0d99-147">Kullanıcı hesabınızın yeterli izinleri tooperform hello görev sahip olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="f0d99-148">Bu hello sorunu yalıtılmış tooone bilgisayar ya da yerel ağınızda değil onaylayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="f0d99-149">Bu hello Azure Mobile Engagement hizmet hiçbir rapor edilen kesintileri onaylayın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="f0d99-150">Uygulama bilgileri etiketi dosyalarınızı bu kuralların hepsi izleyin onaylayın:</span><span class="sxs-lookup"><span data-stu-id="f0d99-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="f0d99-151">Kullanım yalnızca hello UTF8 karakter kümesi (Merhaba ANSI karakter kümesini desteklenmez).</span><span class="sxs-lookup"><span data-stu-id="f0d99-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="f0d99-152">Virgül "," Merhaba ayırıcı karakter olarak (bir hizmet isteği toorequest toochange hello .csv ayırıcı karakter virgül açabilirsiniz "," tooanother karakter noktalı virgül gibi ";").</span><span class="sxs-lookup"><span data-stu-id="f0d99-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="f0d99-153">Tüm küçük Boole değerleri için "true" ve "false" kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="f0d99-154">Merhaba en büyük dosya boyutu 35 MB daha küçük bir dosya kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0d99-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

