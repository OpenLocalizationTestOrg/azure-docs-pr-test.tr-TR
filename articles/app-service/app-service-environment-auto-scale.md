---
title: "aaaAutoscaling ve uygulama hizmeti ortamı v1"
description: "Otomatik ölçeklendirme ve uygulama hizmeti ortamı"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="0b11e-103">Otomatik ölçeklendirme ve uygulama hizmeti ortamı v1</span><span class="sxs-lookup"><span data-stu-id="0b11e-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="0b11e-104">Uygulama hizmeti ortamı v1 hello hakkında makaledir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="0b11e-105">Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var.</span><span class="sxs-lookup"><span data-stu-id="0b11e-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="0b11e-106">Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="0b11e-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="0b11e-107">Azure uygulama hizmeti ortamları desteği *otomatik ölçeklendirmeyi*.</span><span class="sxs-lookup"><span data-stu-id="0b11e-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="0b11e-108">Ölçümleri veya zamanlamaya göre otomatik ölçeklendirme ayrı ayrı çalışan havuzlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b11e-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Bir çalışan havuzu için otomatik ölçeklendirme seçenekleri.][intro]

<span data-ttu-id="0b11e-110">Otomatik ölçeklendirmeyi kaynak kullanımını otomatik olarak büyüyen ve bir uygulama hizmeti ortamı toofit küçültme bütçe ve/veya yük profilinizi en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="0b11e-111">Çalışan havuzu otomatik ölçeklendirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0b11e-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="0b11e-112">Merhaba otomatik ölçeklendirme işlevleri hello erişebilirsiniz **ayarları** hello çalışan havuzunda sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="0b11e-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Ayarlar sekmesinde hello çalışan havuzu.][settings-scale]

<span data-ttu-id="0b11e-114">Buradan, hello arabirimi olmalıdır ne zaman bir uygulama hizmeti ölçeklendirmek gördüğünüz aynı deneyimi planlama hello bu yana oldukça alışkın olduğu.</span><span class="sxs-lookup"><span data-stu-id="0b11e-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![El ile ölçek ayarları.][scale-manual]

<span data-ttu-id="0b11e-116">Bir otomatik ölçeklendirme profili de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b11e-116">You can also configure an autoscale profile.</span></span>

![Otomatik ölçeklendirme ayarları.][scale-profile]

<span data-ttu-id="0b11e-118">Otomatik ölçeklendirme profili, ölçekte yararlı tooset kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="0b11e-119">Bu şekilde, bir alt sınır ölçek değeri (1) ve tahmin edilebilir harcama cap bir üst sınır (2) ayarlayarak ayarlayarak deneyimi tutarlı bir performans olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Ölçek ayarları profilinde.][scale-profile2]

<span data-ttu-id="0b11e-121">Bir profili tanımladıktan sonra otomatik ölçeklendirme kurallarını tooscale yukarı veya aşağı hello sayısının hello çalışan havuzunda hello profiliyle tanımlanan hello sınırları içinde ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b11e-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="0b11e-122">Otomatik ölçeklendirme kurallarını ölçümleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-122">Autoscale rules are based on metrics.</span></span>

![Ölçek kuralı.][scale-rule]

 <span data-ttu-id="0b11e-124">Herhangi bir çalışan havuzu veya ön uç ölçümleri kullanılan toodefine otomatik ölçeklendirme kurallarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="0b11e-125">Bu ölçümler aynı ölçümleri hello kaynak dikey grafiklerde izlemek veya ayarlamak için uyarıları hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="0b11e-126">Otomatik ölçeklendirme örneği</span><span class="sxs-lookup"><span data-stu-id="0b11e-126">Autoscale example</span></span>
<span data-ttu-id="0b11e-127">Otomatik ölçeklendirme bir uygulama hizmeti ortamında en iyi bir senaryo adım adım ilerlemenizi sağlayarak gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="0b11e-128">Otomatik ölçeklendirme ayarladığınızda, bu makalede tüm hello gerekli konuları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="0b11e-129">Merhaba makale, uygulama hizmeti ortamı'nda barındırılan uygulama hizmeti ortamları otomatik ölçeklendirmeyi içinde faktörü olduğunda içine gelen etkileşimleri yürütmek hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="0b11e-130">Senaryo giriş</span><span class="sxs-lookup"><span data-stu-id="0b11e-130">Scenario introduction</span></span>
<span data-ttu-id="0b11e-131">Frank kendisinin tooan uygulama hizmeti ortamı yönetir hello iş yükleri bir kısmı geçirildiğini bir kuruluş için bir sysadmin ' dir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="0b11e-132">Merhaba uygulama hizmeti ortamı toomanual ölçek aşağıdaki gibi yapılandırılmış:</span><span class="sxs-lookup"><span data-stu-id="0b11e-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="0b11e-133">**Ön Uçları:** 3</span><span class="sxs-lookup"><span data-stu-id="0b11e-133">**Front ends:** 3</span></span>
* <span data-ttu-id="0b11e-134">**Çalışan havuzunda 1**: 10</span><span class="sxs-lookup"><span data-stu-id="0b11e-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="0b11e-135">**Çalışan havuzunda 2**: 5</span><span class="sxs-lookup"><span data-stu-id="0b11e-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="0b11e-136">**Çalışan havuzunda 3**: 5</span><span class="sxs-lookup"><span data-stu-id="0b11e-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="0b11e-137">Çalışan havuzunda 2 ve 3 çalışan havuzunda kalite güvence (QA) ve geliştirme iş yükleri için kullanılan sırasında çalışan havuzu 1 üretim iş yükleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="0b11e-138">QA ve geliştirme için hello App Service planlarına toomanual ölçek yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="0b11e-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="0b11e-139">Merhaba üretim uygulama hizmeti planı yükünü ve trafik tooautoscale toodeal Çeşitlemeler ile ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="0b11e-140">Frank hello uygulamayla bilgili ' dir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="0b11e-141">Ki bu çalışanların hello ofiste oldukları sırada kullanan bir satır iş kolu (LOB) uygulaması olduğundan hello yoğun saatler yük 9: 00'da ve 6:00 arasında olduğunu bilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="0b11e-142">Kullanıcılar o gün için bittiğinde kullanım bundan sonra bırakır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="0b11e-143">Yoğun saatler dışında yoktur hala bazı yük kullanıcılar hello uygulama uzaktan kendi mobil aygıtlar veya ev bilgisayarları kullanarak erişebildiğinden.</span><span class="sxs-lookup"><span data-stu-id="0b11e-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="0b11e-144">Uygulama hizmeti planı zaten hello üretim kuralları aşağıdaki hello ile CPU kullanımı dikkate alarak tooautoscale yapılandırılmış:</span><span class="sxs-lookup"><span data-stu-id="0b11e-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![LOB uygulaması için özel ayarlar.][asp-scale]

| <span data-ttu-id="0b11e-146">**Otomatik ölçeklendirme profili – haftanın günlerini – uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="0b11e-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="0b11e-147">**Otomatik ölçeklendirme profili – hafta sonları – uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="0b11e-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="0b11e-148">**Ad:** haftanın günü profili</span><span class="sxs-lookup"><span data-stu-id="0b11e-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="0b11e-149">**Ad:** hafta sonu profili</span><span class="sxs-lookup"><span data-stu-id="0b11e-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="0b11e-150">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="0b11e-151">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="0b11e-152">**Profil:** haftanın günü</span><span class="sxs-lookup"><span data-stu-id="0b11e-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="0b11e-153">**Profil:** hafta sonu</span><span class="sxs-lookup"><span data-stu-id="0b11e-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="0b11e-154">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="0b11e-154">**Type:** Recurrence</span></span> |<span data-ttu-id="0b11e-155">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="0b11e-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="0b11e-156">**Hedef aralık:** 5 too20 örnekleri</span><span class="sxs-lookup"><span data-stu-id="0b11e-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="0b11e-157">**Hedef aralık:** 3 too10 örnekleri</span><span class="sxs-lookup"><span data-stu-id="0b11e-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="0b11e-158">**Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma</span><span class="sxs-lookup"><span data-stu-id="0b11e-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="0b11e-159">**Gün sayısı:** Cumartesi, Pazar</span><span class="sxs-lookup"><span data-stu-id="0b11e-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="0b11e-160">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="0b11e-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="0b11e-161">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="0b11e-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="0b11e-162">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="0b11e-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="0b11e-163">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="0b11e-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="0b11e-164">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="0b11e-165">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="0b11e-166">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="0b11e-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="0b11e-167">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="0b11e-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="0b11e-168">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-168">**Metric:** CPU %</span></span> |<span data-ttu-id="0b11e-169">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="0b11e-170">**İşlem:** % 60 daha büyük</span><span class="sxs-lookup"><span data-stu-id="0b11e-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="0b11e-171">**İşlem:** % 80 daha büyük</span><span class="sxs-lookup"><span data-stu-id="0b11e-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="0b11e-172">**Süresi:** 5 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="0b11e-173">**Süresi:** 10 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="0b11e-174">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="0b11e-175">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-176">**Eylem:** sayısı 2 ile artırın</span><span class="sxs-lookup"><span data-stu-id="0b11e-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="0b11e-177">**Eylem:** sayısı 1 ile artırın</span><span class="sxs-lookup"><span data-stu-id="0b11e-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="0b11e-178">**(Dakika) basılı güzel:** 15</span><span class="sxs-lookup"><span data-stu-id="0b11e-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="0b11e-179">**(Dakika) basılı güzel:** 20</span><span class="sxs-lookup"><span data-stu-id="0b11e-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="0b11e-180">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="0b11e-181">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="0b11e-182">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="0b11e-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="0b11e-183">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="0b11e-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="0b11e-184">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-184">**Metric:** CPU %</span></span> |<span data-ttu-id="0b11e-185">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="0b11e-186">**İşlem:** % 30'den az</span><span class="sxs-lookup"><span data-stu-id="0b11e-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="0b11e-187">**İşlem:** % 20'den az</span><span class="sxs-lookup"><span data-stu-id="0b11e-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="0b11e-188">**Süresi:** 10 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="0b11e-189">**Süresi:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="0b11e-190">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="0b11e-191">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-192">**Eylem:** sayısı 1 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="0b11e-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="0b11e-193">**Eylem:** sayısı 1 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="0b11e-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="0b11e-194">**(Dakika) basılı güzel:** 20</span><span class="sxs-lookup"><span data-stu-id="0b11e-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="0b11e-195">**(Dakika) basılı güzel:** 10</span><span class="sxs-lookup"><span data-stu-id="0b11e-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="0b11e-196">Uygulama hizmeti plan Enflasyon oranı</span><span class="sxs-lookup"><span data-stu-id="0b11e-196">App Service plan inflation rate</span></span>
<span data-ttu-id="0b11e-197">Saat başına en yüksek bir hızda yapılandırılmış tooautoscale olan uygulama hizmeti planları bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="0b11e-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="0b11e-198">Bu oran tabanlı hello otomatik ölçeklendirme kuralı sağlanan hello değerlere hesaplanabilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="0b11e-199">Anlama ve hesaplama hello *uygulama hizmeti plan Enflasyon oranı* ölçek değişiklikleri tooa çalışan havuzu olmadığından anlık uygulama hizmeti ortamı ölçeklendirme için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="0b11e-200">Uygulama hizmeti plan Enflasyon oranı Hello aşağıdaki gibi hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="0b11e-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![Uygulama hizmeti planı Enflasyon oranı hesaplama.][ASP-Inflation]

<span data-ttu-id="0b11e-202">Merhaba otomatik ölçeklendirme – ölçeği Artır kural hello haftanın günü profili hello üretim uygulama hizmeti planı için temel:</span><span class="sxs-lookup"><span data-stu-id="0b11e-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation1]

<span data-ttu-id="0b11e-204">Hello otomatik ölçeklendirme – ölçeği Artır hello hafta sonu profili hello üretim uygulama hizmeti planı için kuralı hello durumda hello formülü çözümlenmesi:</span><span class="sxs-lookup"><span data-stu-id="0b11e-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation2]

<span data-ttu-id="0b11e-206">Bu değer de ölçek azaltma işlemleri için hesaplanabilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="0b11e-207">Merhaba otomatik ölçeklendirme – ölçek aşağı hello haftanın günü profili hello üretim uygulama hizmeti planı için kuralı göre bunu şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="0b11e-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation3]

<span data-ttu-id="0b11e-209">Hello otomatik ölçeklendirme – ölçek aşağı hello hafta sonu profili hello üretim uygulama hizmeti planı için kuralı hello durumda hello formülü çözümlenmesi:</span><span class="sxs-lookup"><span data-stu-id="0b11e-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation4]

<span data-ttu-id="0b11e-211">Merhaba üretim uygulama hizmeti planı, maksimum oran hello hafta sırasında sekiz örnekleri/saat ve dört örnekleri/saat hello hafta boyunca büyüyebilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="0b11e-212">En fazla dört örnekleri/saat hello hafta sırasında örnekleri ve hafta sonları sırasında altı örnekleri saate serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b11e-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="0b11e-213">Çalışan havuzunda birden çok uygulama hizmeti planları barındırılan toocalculate hello varsa *toplam Enflasyon oranı* hello toplam uygulama hizmeti planları yükleniyor tüm hello hello Enflasyon oranındaki olarak, bir çalışan havuzunda barındırma.</span><span class="sxs-lookup"><span data-stu-id="0b11e-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![Çalışan havuzunda barındırılan birden çok uygulama hizmeti planları için toplam Enflasyon oran hesaplaması.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="0b11e-215">Kullanım hello uygulama hizmeti planı Enflasyon oranı toodefine çalışan havuzu otomatik ölçeklendirme kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="0b11e-216">Çalışan barındıran yapılandırılmış tooautoscale olan uygulama hizmeti planları kapasitesinin bir arabellek ayrılması gereken havuza alır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="0b11e-217">Merhaba arabellek gerektiği gibi uygulama hizmeti planı küçültmek ve hello otomatik ölçeklendirme işlemleri toogrow için izin verir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="0b11e-218">Merhaba en küçük arabellek hello toplam uygulama hizmeti planı Enflasyon oranı hesaplanan olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="0b11e-219">Uygulama hizmeti ortamı ölçeklendirme işlemleri bazı zaman tooapply tuttuğundan, herhangi bir değişiklik bir ölçeklendirme işlemi devam ederken ortaya çıkar daha fazla isteğe bağlı değişiklikler için hesap.</span><span class="sxs-lookup"><span data-stu-id="0b11e-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="0b11e-220">tooaccommodate bu gecikme, kullanmanızı öneririz hello toplam uygulama hizmeti planı Enflasyon oranı hello en az her otomatik ölçeklendirme işlemi için eklenen örnek sayısı olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="0b11e-221">Bu bilgiyle Frank hello tanımlayabilirsiniz otomatik ölçeklendirme profili ve kurallar aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0b11e-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![LOB örnek için otomatik ölçeklendirme profili kuralları.][Worker-Pool-Scale]

| <span data-ttu-id="0b11e-223">**Otomatik ölçeklendirme profili – haftanın günü**</span><span class="sxs-lookup"><span data-stu-id="0b11e-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="0b11e-224">**Otomatik ölçeklendirme profili – hafta sonları**</span><span class="sxs-lookup"><span data-stu-id="0b11e-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="0b11e-225">**Ad:** haftanın günü profili</span><span class="sxs-lookup"><span data-stu-id="0b11e-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="0b11e-226">**Ad:** hafta sonu profili</span><span class="sxs-lookup"><span data-stu-id="0b11e-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="0b11e-227">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="0b11e-228">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="0b11e-229">**Profil:** haftanın günü</span><span class="sxs-lookup"><span data-stu-id="0b11e-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="0b11e-230">**Profil:** hafta sonu</span><span class="sxs-lookup"><span data-stu-id="0b11e-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="0b11e-231">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="0b11e-231">**Type:** Recurrence</span></span> |<span data-ttu-id="0b11e-232">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="0b11e-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="0b11e-233">**Hedef aralık:** 13 too25 örnekleri</span><span class="sxs-lookup"><span data-stu-id="0b11e-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="0b11e-234">**Hedef aralık:** 6 too15 örnekleri</span><span class="sxs-lookup"><span data-stu-id="0b11e-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="0b11e-235">**Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma</span><span class="sxs-lookup"><span data-stu-id="0b11e-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="0b11e-236">**Gün sayısı:** Cumartesi, Pazar</span><span class="sxs-lookup"><span data-stu-id="0b11e-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="0b11e-237">**Başlangıç zamanı:** 7: 00'da</span><span class="sxs-lookup"><span data-stu-id="0b11e-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="0b11e-238">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="0b11e-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="0b11e-239">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="0b11e-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="0b11e-240">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="0b11e-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="0b11e-241">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="0b11e-242">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="0b11e-243">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="0b11e-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="0b11e-244">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="0b11e-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="0b11e-245">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="0b11e-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="0b11e-246">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="0b11e-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="0b11e-247">**İşlem:** değerinden 8</span><span class="sxs-lookup"><span data-stu-id="0b11e-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="0b11e-248">**İşlem:** 3'ten az</span><span class="sxs-lookup"><span data-stu-id="0b11e-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="0b11e-249">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="0b11e-250">**Süresi:** 30 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="0b11e-251">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="0b11e-252">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-253">**Eylem:** sayısı 8 ile artırın</span><span class="sxs-lookup"><span data-stu-id="0b11e-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="0b11e-254">**Eylem:** artırmak sayısı 3 ile</span><span class="sxs-lookup"><span data-stu-id="0b11e-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="0b11e-255">**(Dakika) basılı güzel:** 180</span><span class="sxs-lookup"><span data-stu-id="0b11e-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="0b11e-256">**(Dakika) basılı güzel:** 180</span><span class="sxs-lookup"><span data-stu-id="0b11e-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="0b11e-257">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="0b11e-258">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="0b11e-259">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="0b11e-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="0b11e-260">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="0b11e-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="0b11e-261">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="0b11e-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="0b11e-262">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="0b11e-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="0b11e-263">**İşlem:** 8 büyük</span><span class="sxs-lookup"><span data-stu-id="0b11e-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="0b11e-264">**İşlem:** 3'ten büyük</span><span class="sxs-lookup"><span data-stu-id="0b11e-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="0b11e-265">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="0b11e-266">**Süresi:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="0b11e-267">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="0b11e-268">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-269">**Eylem:** sayısı 2 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="0b11e-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="0b11e-270">**Eylem:** sayısı 3 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="0b11e-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="0b11e-271">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="0b11e-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="0b11e-272">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="0b11e-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="0b11e-273">Merhaba hello profilinde tanımlanan hedef aralık hello uygulama hizmeti planı için profili + arabellek tanımlanan hello minimum örnekler tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="0b11e-274">Merhaba en fazla aralık hello çalışan havuzunda barındırılan tüm uygulama hizmeti planları için tüm hello maksimum aralıklarını hello toplamı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="0b11e-275">Merhaba kuralları hello ölçek artırma sayısı yukarı ölçek için uygulama hizmeti planı Enflasyon oranı X kümesi tooat en az 1 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b11e-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="0b11e-276">1 X uygulama hizmeti planı Enflasyon oranı aşağı için ölçek hello veya azaltma sayısı 1/2 X arasında ayarlanmış toosomething olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="0b11e-277">Ön uç havuzu için otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="0b11e-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="0b11e-278">Ön uç otomatik ölçeklendirme kurallarını çalışan havuzlarında daha basittir.</span><span class="sxs-lookup"><span data-stu-id="0b11e-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="0b11e-279">Öncelikle yapmanız gerekenler</span><span class="sxs-lookup"><span data-stu-id="0b11e-279">Primarily, you should</span></span>  
<span data-ttu-id="0b11e-280">süresi hello ölçüm ve hello cooldown zamanlayıcılar bir uygulama hizmeti planı üzerinde ölçeklendirme işlemleri anlık olmayan dikkate aldığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0b11e-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="0b11e-281">Bu senaryo için o hello hata oranı % 80 CPU kullanımı ön uçlar eriştikten sonra artırır ve hello otomatik ölçeklendirme kural tooincrease örneklerinin gibi ayarlar Frank bilir:</span><span class="sxs-lookup"><span data-stu-id="0b11e-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![Ön uç havuzu için otomatik ölçeklendirme ayarları.][Front-End-Scale]

| <span data-ttu-id="0b11e-283">**Otomatik ölçeklendirme profili – ön Uçlar**</span><span class="sxs-lookup"><span data-stu-id="0b11e-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="0b11e-284">**Ad:** otomatik ölçeklendirme – ön Uçlar</span><span class="sxs-lookup"><span data-stu-id="0b11e-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="0b11e-285">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="0b11e-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="0b11e-286">**Profil:** her gün</span><span class="sxs-lookup"><span data-stu-id="0b11e-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="0b11e-287">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="0b11e-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="0b11e-288">**Hedef aralık:** 3 too10 örnekleri</span><span class="sxs-lookup"><span data-stu-id="0b11e-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="0b11e-289">**Gün sayısı:** her gün</span><span class="sxs-lookup"><span data-stu-id="0b11e-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="0b11e-290">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="0b11e-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="0b11e-291">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="0b11e-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="0b11e-292">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="0b11e-293">**Kaynak:** ön uç havuzu</span><span class="sxs-lookup"><span data-stu-id="0b11e-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="0b11e-294">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="0b11e-295">**İşlem:** % 60 daha büyük</span><span class="sxs-lookup"><span data-stu-id="0b11e-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="0b11e-296">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="0b11e-297">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-298">**Eylem:** artırmak sayısı 3 ile</span><span class="sxs-lookup"><span data-stu-id="0b11e-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="0b11e-299">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="0b11e-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="0b11e-300">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="0b11e-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="0b11e-301">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="0b11e-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="0b11e-302">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="0b11e-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="0b11e-303">**İşlem:** % 30'den az</span><span class="sxs-lookup"><span data-stu-id="0b11e-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="0b11e-304">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="0b11e-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="0b11e-305">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="0b11e-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="0b11e-306">**Eylem:** sayısı 3 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="0b11e-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="0b11e-307">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="0b11e-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
