---
title: "Sorun giderme kılavuzu - hizmet azure Mobile Engagement"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="c0195-103">Hizmet sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="c0195-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="c0195-104">Azure Mobile Engagement nasıl çalıştığı ile karşılaşabileceğiniz olası sorunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c0195-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="c0195-105">Hizmet kesintisi</span><span class="sxs-lookup"><span data-stu-id="c0195-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="c0195-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="c0195-106">Issue</span></span>
* <span data-ttu-id="c0195-107">Azure Mobile Engagement hizmet kesintileri tarafından nedeni görünmesini sorunları.</span><span class="sxs-lookup"><span data-stu-id="c0195-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="c0195-108">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="c0195-108">Causes</span></span>
* <span data-ttu-id="c0195-109">Azure Mobile Engagement hizmet kesintileri tarafından nedeni görünmesini sorunları birkaç farklı nedenlerden kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="c0195-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="c0195-110">İlk olarak sistemle ilgili tüm Azure Mobile Engagement görünür yalıtılmış sorunları</span><span class="sxs-lookup"><span data-stu-id="c0195-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="c0195-111">Bilinen sorunlar sunucu kesintileri (her zaman sunucu durumunda gösterir) nedeni:</span><span class="sxs-lookup"><span data-stu-id="c0195-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="c0195-112">Gecikmeler, hedefleme hataları, rozet güncelleştirmesini sorunları, toplama, çalışma anında durakları istatistikleri durdurma zamanlama, API'nin Dur çalışma, yeni uygulamalar veya kullanıcılar oluşturulamaz, DNS hataları ve zaman aşımı hataları UI, API veya uygulamaları bir aygıtta.</span><span class="sxs-lookup"><span data-stu-id="c0195-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="c0195-113">Bulut bağımlılık kesintileri [Azure hizmet durumu](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="c0195-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="c0195-114">Bildirim Hizmetleri (PNS) bağımlılık kesintileri bildirme</span><span class="sxs-lookup"><span data-stu-id="c0195-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="c0195-115">Uygulama mağazası kesintileri</span><span class="sxs-lookup"><span data-stu-id="c0195-115">App Store Outages</span></span>

1) <span data-ttu-id="c0195-116">Sorun sistemle ilgili olup olmadığını sınamak için aynı işlevin farklı bir test edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c0195-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="c0195-117">Azure Mobile Engagement uygulama tümleşik</span><span class="sxs-lookup"><span data-stu-id="c0195-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="c0195-118">Test cihazı</span><span class="sxs-lookup"><span data-stu-id="c0195-118">Test device</span></span>
* <span data-ttu-id="c0195-119">Test aygıt işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="c0195-119">Test device OS version</span></span>
* <span data-ttu-id="c0195-120">Kampanya</span><span class="sxs-lookup"><span data-stu-id="c0195-120">Campaign</span></span>
* <span data-ttu-id="c0195-121">Yönetici kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="c0195-121">Administrator user account</span></span>
* <span data-ttu-id="c0195-122">Tarayıcı (IE, Firefox, Chrome, vb.)</span><span class="sxs-lookup"><span data-stu-id="c0195-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="c0195-123">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="c0195-123">Computer</span></span>

2) <span data-ttu-id="c0195-124">Sorun kullanıcı Arabirimi veya API'nin yalnızca etkilerse test etmek için:</span><span class="sxs-lookup"><span data-stu-id="c0195-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="c0195-125">Azure Mobile Engagement UI ve Azure Mobile Engagement API'nin aynı işlevin sınayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="c0195-126">Cep telefonu ağınızla sorunun olup olmadığını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="c0195-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="c0195-127">WIFI üzerinden ve 3 G cep telefonu ağınız bağlıyken internet bağlıyken sınayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="c0195-128">Güvenlik duvarını herhangi bir Azure Mobile Engagement IP adreslerini veya bağlantı noktalarını engellemediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0195-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="c0195-129">Sorunun cihazınızla olup olmadığını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="c0195-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="c0195-130">Cihazınızı Azure Mobile Engagement için başka bir Azure Mobile Engagement tümleşik uygulamayla bağlanabiliyor ise test edin.</span><span class="sxs-lookup"><span data-stu-id="c0195-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="c0195-131">Azure Mobile Engagement Arabiriminde görülebilir telefonunuzdan gelen olayları, işler ve kilitlenme oluşturabilir sınayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="c0195-132">Kendi cihaz Kimliği'nde tabanlı aygıtınıza Azure Mobile Engagement Arabiriminden anında iletme bildirimleri gönderebilir, test etme</span><span class="sxs-lookup"><span data-stu-id="c0195-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="c0195-133">Uygulamanızla sorunun olup olmadığını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="c0195-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="c0195-134">Yükleyin ve yerine bir öykünücü fiziksel CİHAZDAN uygulamanızı test edin:</span><span class="sxs-lookup"><span data-stu-id="c0195-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="c0195-135">İşletim sistemi yükseltmeleri son kullanıcıya çözümlemek için SDK yükseltme gerektiren cihazlar ile sorunun olup olmadığını test etmek için:</span><span class="sxs-lookup"><span data-stu-id="c0195-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="c0195-136">İşletim sisteminin farklı sürümlerini farklı cihazlarda uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="c0195-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="c0195-137">SDK'ın en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0195-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="c0195-138">Bağlantısı ve yanlış bilgi sorunları</span><span class="sxs-lookup"><span data-stu-id="c0195-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="c0195-139">Sorun</span><span class="sxs-lookup"><span data-stu-id="c0195-139">Issue</span></span>
* <span data-ttu-id="c0195-140">Azure Mobile Engagement UI günlüğü sorunları.</span><span class="sxs-lookup"><span data-stu-id="c0195-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="c0195-141">Azure Mobile Engagement API'nin hatalarla bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c0195-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="c0195-142">Uygulama bilgileri etiketleri Device API'si aracılığıyla karşıya yükleme sorunları.</span><span class="sxs-lookup"><span data-stu-id="c0195-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="c0195-143">Sorunları günlüklerini veya dışarı aktarılan verileri Azure Mobile Engagement'tan yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="c0195-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="c0195-144">Azure Mobile Engagement Arabiriminde gösterilecek yanlış bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c0195-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="c0195-145">Azure Mobile Engagement günlüklerde gösterilen yanlış bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c0195-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="c0195-146">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="c0195-146">Causes</span></span>
* <span data-ttu-id="c0195-147">Kullanıcı hesabınızın görevi gerçekleştirmek için yeterli izinlere sahip olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="c0195-148">Sorun bir bilgisayar veya yerel ağınızdaki yalıtılmış olmadığını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="c0195-149">Azure Mobile Engagement hizmet sahip olmayan kesintileri bildirilen onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c0195-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="c0195-150">Uygulama bilgileri etiketi dosyalarınızı bu kuralların hepsi izleyin onaylayın:</span><span class="sxs-lookup"><span data-stu-id="c0195-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="c0195-151">Yalnızca UTF8 karakter kümesi (ANSI karakter kümesini desteklenmiyor) kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0195-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="c0195-152">Virgül "," ayırıcı karakter olarak (bir hizmet virgül .csv Ayırıcı karakterini değiştirmek için istemek için açabilirsiniz "," noktalı virgül gibi başka bir karakter için ";").</span><span class="sxs-lookup"><span data-stu-id="c0195-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="c0195-153">Tüm küçük Boole değerleri için "true" ve "false" kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0195-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="c0195-154">35 MB maksimum dosya boyutundan daha küçük bir dosya kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0195-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

