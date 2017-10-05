---
title: "Otomatik ölçeklendirme ve uygulama hizmeti ortamı v1"
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
ms.openlocfilehash: f32affd285f3918feb0e893543f2a28f678b7b10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="36357-103">Otomatik ölçeklendirme ve uygulama hizmeti ortamı v1</span><span class="sxs-lookup"><span data-stu-id="36357-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="36357-104">Bu makale hakkında uygulama hizmeti ortamı v1 yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="36357-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="36357-105">Uygulama hizmeti ortamı kullanmak daha kolay ve daha güçlü altyapısı üzerinde çalışan daha yeni bir sürümü var.</span><span class="sxs-lookup"><span data-stu-id="36357-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="36357-106">Yeni sürüm Başlarken hakkında daha fazla bilgi edinmek için [uygulama hizmeti ortamı giriş](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="36357-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="36357-107">Azure uygulama hizmeti ortamları desteği *otomatik ölçeklendirmeyi*.</span><span class="sxs-lookup"><span data-stu-id="36357-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="36357-108">Ölçümleri veya zamanlamaya göre otomatik ölçeklendirme ayrı ayrı çalışan havuzlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36357-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![Bir çalışan havuzu için otomatik ölçeklendirme seçenekleri.][intro]

<span data-ttu-id="36357-110">Otomatik ölçeklendirmeyi kaynak kullanımını otomatik olarak büyüyen ve bütçenizi sığacak ve veya yük profili için bir uygulama hizmeti ortamı küçültme en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="36357-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment to fit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="36357-111">Çalışan havuzu otomatik ölçeklendirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="36357-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="36357-112">Otomatik ölçeklendirme işlevinden erişebilirsiniz **ayarları** çalışan havuzunda sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="36357-112">You can access the autoscale functionality from the **Settings** tab of the worker pool.</span></span>

![Çalışan havuzunda Ayarlar sekmesinde.][settings-scale]

<span data-ttu-id="36357-114">Buradan, arabirim olmalıdır ne zaman bir uygulama hizmeti planı ölçeklendirmek gördüğünüz aynı bu yana oldukça tanıdık deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="36357-114">From there, the interface should be fairly familiar since it is the same experience that you see when you scale an App Service plan.</span></span> 

![El ile ölçek ayarları.][scale-manual]

<span data-ttu-id="36357-116">Bir otomatik ölçeklendirme profili de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36357-116">You can also configure an autoscale profile.</span></span>

![Otomatik ölçeklendirme ayarları.][scale-profile]

<span data-ttu-id="36357-118">Otomatik ölçeklendirme profilleri, Ölçek sınırlarını ayarlamak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="36357-118">Autoscale profiles are useful to set limits on your scale.</span></span> <span data-ttu-id="36357-119">Bu şekilde, bir alt sınır ölçek değeri (1) ve tahmin edilebilir harcama cap bir üst sınır (2) ayarlayarak ayarlayarak deneyimi tutarlı bir performans olabilir.</span><span class="sxs-lookup"><span data-stu-id="36357-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![Ölçek ayarları profilinde.][scale-profile2]

<span data-ttu-id="36357-121">Bir profili tanımladıktan sonra Yukarı veya aşağı profili tarafından tanımlanan sınırları içinde çalışan havuzunda örneklerinin sayısını ölçeklendirmek için otomatik ölçeklendirme kuralı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36357-121">After you define a profile, you can add autoscale rules to scale up or down the number of instances in the worker pool within the bounds defined by the profile.</span></span> <span data-ttu-id="36357-122">Otomatik ölçeklendirme kurallarını ölçümleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="36357-122">Autoscale rules are based on metrics.</span></span>

![Ölçek kuralı.][scale-rule]

 <span data-ttu-id="36357-124">Herhangi bir çalışan havuzu veya ön uç ölçümleri, otomatik ölçeklendirme kurallarını tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36357-124">Any worker pool or front-end metrics can be used to define autoscale rules.</span></span> <span data-ttu-id="36357-125">Bu ölçümler kaynak dikey grafiklerde izlemek ya da uyarılar için aynı ölçümleridir.</span><span class="sxs-lookup"><span data-stu-id="36357-125">These metrics are the same metrics you can monitor in the resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="36357-126">Otomatik ölçeklendirme örneği</span><span class="sxs-lookup"><span data-stu-id="36357-126">Autoscale example</span></span>
<span data-ttu-id="36357-127">Otomatik ölçeklendirme bir uygulama hizmeti ortamında en iyi bir senaryo adım adım ilerlemenizi sağlayarak gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="36357-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="36357-128">Otomatik ölçeklendirme ayarladığınızda, bu makalede gerekli tüm konuları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36357-128">This article explains all the necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="36357-129">Makale, uygulama hizmeti ortamı'nda barındırılan uygulama hizmeti ortamları otomatik ölçeklendirmeyi içinde faktörü yükleyen oyuna gelen etkileşimler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36357-129">The article walks you through the interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="36357-130">Senaryo giriş</span><span class="sxs-lookup"><span data-stu-id="36357-130">Scenario introduction</span></span>
<span data-ttu-id="36357-131">Frank bir kısmı kendisi yönetir iş yükleri için uygulama hizmeti ortamı geçirildiğini bir kuruluş için bir sysadmin ' dir.</span><span class="sxs-lookup"><span data-stu-id="36357-131">Frank is a sysadmin for an enterprise who has migrated a portion of the workloads that he manages to an App Service environment.</span></span>

<span data-ttu-id="36357-132">Uygulama hizmeti ortamı için el ile ölçek aşağıdaki gibi yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="36357-132">The App Service environment is configured to manual scale as follows:</span></span>

* <span data-ttu-id="36357-133">**Ön Uçları:** 3</span><span class="sxs-lookup"><span data-stu-id="36357-133">**Front ends:** 3</span></span>
* <span data-ttu-id="36357-134">**Çalışan havuzunda 1**: 10</span><span class="sxs-lookup"><span data-stu-id="36357-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="36357-135">**Çalışan havuzunda 2**: 5</span><span class="sxs-lookup"><span data-stu-id="36357-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="36357-136">**Çalışan havuzunda 3**: 5</span><span class="sxs-lookup"><span data-stu-id="36357-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="36357-137">Çalışan havuzunda 2 ve 3 çalışan havuzunda kalite güvence (QA) ve geliştirme iş yükleri için kullanılan sırasında çalışan havuzu 1 üretim iş yükleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36357-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="36357-138">Uygulama hizmeti planları QA ve geliştirme için el ile ölçeklendirme için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="36357-138">The App Service plans for QA and dev are configured to manual scale.</span></span> <span data-ttu-id="36357-139">Uygulama hizmeti planı üretim için otomatik ölçeklendirme yükünü ve trafik Çeşitlemeler uğraşmanız ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="36357-139">The production App Service plan is set to autoscale to deal with variations in load and traffic.</span></span>

<span data-ttu-id="36357-140">Frank uygulama ile bilgili ' dir.</span><span class="sxs-lookup"><span data-stu-id="36357-140">Frank is very familiar with the application.</span></span> <span data-ttu-id="36357-141">Ki, bu çalışanlar ofiste oldukları sırada kullanan bir satır iş kolu (LOB) uygulaması olduğundan yük için yoğun saatler 9: 00'da ve 6:00 arasında olduğunu bilir.</span><span class="sxs-lookup"><span data-stu-id="36357-141">He knows that the peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in the office.</span></span> <span data-ttu-id="36357-142">Kullanıcılar o gün için bittiğinde kullanım bundan sonra bırakır.</span><span class="sxs-lookup"><span data-stu-id="36357-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="36357-143">Yoğun saatler dışında yoktur hala bazı yük kullanıcıların uygulamayı uzaktan kendi mobil aygıtlar veya ev bilgisayarları kullanarak erişebildiğinden.</span><span class="sxs-lookup"><span data-stu-id="36357-143">Outside peak hours, there is still some load because users can access the app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="36357-144">Uygulama hizmeti planı üretim aşağıdaki kurallar ile CPU kullanımına bağlı olarak otomatik ölçeklendirme için zaten yapılandırıldı:</span><span class="sxs-lookup"><span data-stu-id="36357-144">The production App Service plan is already configured to autoscale based on CPU usage with the following rules:</span></span>

![LOB uygulaması için özel ayarlar.][asp-scale]

| <span data-ttu-id="36357-146">**Otomatik ölçeklendirme profili – haftanın günlerini – uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="36357-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="36357-147">**Otomatik ölçeklendirme profili – hafta sonları – uygulama hizmeti planı**</span><span class="sxs-lookup"><span data-stu-id="36357-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="36357-148">**Ad:** haftanın günü profili</span><span class="sxs-lookup"><span data-stu-id="36357-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="36357-149">**Ad:** hafta sonu profili</span><span class="sxs-lookup"><span data-stu-id="36357-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="36357-150">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="36357-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="36357-151">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="36357-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="36357-152">**Profil:** haftanın günü</span><span class="sxs-lookup"><span data-stu-id="36357-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="36357-153">**Profil:** hafta sonu</span><span class="sxs-lookup"><span data-stu-id="36357-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="36357-154">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="36357-154">**Type:** Recurrence</span></span> |<span data-ttu-id="36357-155">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="36357-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="36357-156">**Hedef aralık:** 5-20 örnekleri</span><span class="sxs-lookup"><span data-stu-id="36357-156">**Target range:** 5 to 20 instances</span></span> |<span data-ttu-id="36357-157">**Hedef aralık:** 3-10 örnekleri</span><span class="sxs-lookup"><span data-stu-id="36357-157">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="36357-158">**Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma</span><span class="sxs-lookup"><span data-stu-id="36357-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="36357-159">**Gün sayısı:** Cumartesi, Pazar</span><span class="sxs-lookup"><span data-stu-id="36357-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="36357-160">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="36357-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="36357-161">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="36357-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="36357-162">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="36357-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="36357-163">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="36357-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="36357-164">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="36357-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="36357-165">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="36357-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="36357-166">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="36357-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="36357-167">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="36357-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="36357-168">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-168">**Metric:** CPU %</span></span> |<span data-ttu-id="36357-169">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="36357-170">**İşlem:** % 60 daha büyük</span><span class="sxs-lookup"><span data-stu-id="36357-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="36357-171">**İşlem:** % 80 daha büyük</span><span class="sxs-lookup"><span data-stu-id="36357-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="36357-172">**Süresi:** 5 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="36357-173">**Süresi:** 10 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="36357-174">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="36357-175">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-176">**Eylem:** sayısı 2 ile artırın</span><span class="sxs-lookup"><span data-stu-id="36357-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="36357-177">**Eylem:** sayısı 1 ile artırın</span><span class="sxs-lookup"><span data-stu-id="36357-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="36357-178">**(Dakika) basılı güzel:** 15</span><span class="sxs-lookup"><span data-stu-id="36357-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="36357-179">**(Dakika) basılı güzel:** 20</span><span class="sxs-lookup"><span data-stu-id="36357-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="36357-180">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="36357-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="36357-181">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="36357-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="36357-182">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="36357-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="36357-183">**Kaynak:** üretim (uygulama hizmeti ortamı)</span><span class="sxs-lookup"><span data-stu-id="36357-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="36357-184">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-184">**Metric:** CPU %</span></span> |<span data-ttu-id="36357-185">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="36357-186">**İşlem:** % 30'den az</span><span class="sxs-lookup"><span data-stu-id="36357-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="36357-187">**İşlem:** % 20'den az</span><span class="sxs-lookup"><span data-stu-id="36357-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="36357-188">**Süresi:** 10 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="36357-189">**Süresi:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="36357-190">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="36357-191">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-192">**Eylem:** sayısı 1 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="36357-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="36357-193">**Eylem:** sayısı 1 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="36357-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="36357-194">**(Dakika) basılı güzel:** 20</span><span class="sxs-lookup"><span data-stu-id="36357-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="36357-195">**(Dakika) basılı güzel:** 10</span><span class="sxs-lookup"><span data-stu-id="36357-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="36357-196">Uygulama hizmeti plan Enflasyon oranı</span><span class="sxs-lookup"><span data-stu-id="36357-196">App Service plan inflation rate</span></span>
<span data-ttu-id="36357-197">Saat başına en yüksek bir hızda yapılandırılmış olan uygulama hizmeti planları otomatik ölçeklendirme için bunu yapın.</span><span class="sxs-lookup"><span data-stu-id="36357-197">App Service plans that are configured to autoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="36357-198">Bu oran tabanlı otomatik ölçeklendirme kuralı sağlanan değerlere hesaplanabilir.</span><span class="sxs-lookup"><span data-stu-id="36357-198">This rate can be calculated based on the values provided on the autoscale rule.</span></span>

<span data-ttu-id="36357-199">Anlama ve hesaplama *uygulama hizmeti plan Enflasyon oranı* çalışan havuzunda ölçeği değişiklikler anlık olmadığından uygulama hizmeti ortamı ölçeklendirme için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="36357-199">Understanding and calculating the *App Service plan inflation rate* is important for App Service environment autoscale because scale changes to a worker pool are not instantaneous.</span></span>

<span data-ttu-id="36357-200">Uygulama hizmeti plan Enflasyon oranı aşağıdaki gibi hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="36357-200">The App Service plan inflation rate is calculated as follows:</span></span>

![Uygulama hizmeti planı Enflasyon oranı hesaplama.][ASP-Inflation]

<span data-ttu-id="36357-202">Otomatik ölçeklendirme – ölçeği Artır kural uygulama hizmeti planı üretim haftanın günü profili için temel:</span><span class="sxs-lookup"><span data-stu-id="36357-202">Based on the Autoscale – Scale Up rule for the Weekday profile of the production App Service plan:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation1]

<span data-ttu-id="36357-204">Otomatik ölçeklendirme – ölçeği Artır kural uygulama hizmeti planı, üretim hafta sonu profili için söz konusu olduğunda formülü çözümlenmesi:</span><span class="sxs-lookup"><span data-stu-id="36357-204">In the case of the Autoscale – Scale Up rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçeği Artır kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation2]

<span data-ttu-id="36357-206">Bu değer de ölçek azaltma işlemleri için hesaplanabilir.</span><span class="sxs-lookup"><span data-stu-id="36357-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="36357-207">Otomatik ölçeklendirme – ölçek aşağı kural uygulama hizmeti planı, üretim haftanın günü profili için temel bunu şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="36357-207">Based on the Autoscale – Scale Down rule for the Weekday profile of the production App Service plan, this would look as follows:</span></span>

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı haftanın günü için uygulama hizmeti planı Enflasyon oranı.][Equation3]

<span data-ttu-id="36357-209">Otomatik ölçeklendirme – ölçek aşağı kural uygulama hizmeti planı, üretim hafta sonu profili için söz konusu olduğunda formülü çözümlenmesi:</span><span class="sxs-lookup"><span data-stu-id="36357-209">In the case of the Autoscale – Scale Down rule for the Weekend profile of the production App Service plan, the formula would resolve to:</span></span>  

![Otomatik ölçeklendirme üzerinde – ölçek aşağı kural tabanlı hafta sonları için uygulama hizmeti planı Enflasyon oranı.][Equation4]

<span data-ttu-id="36357-211">Uygulama hizmeti planı üretim sekiz örnekleri/saat hafta sırasında en yüksek hızı ve hafta sonu sırasında dört örnekleri saate büyüyebilir.</span><span class="sxs-lookup"><span data-stu-id="36357-211">The production App Service plan can grow at a maximum rate of eight instances/hour during the week and four instances/hour during the weekend.</span></span> <span data-ttu-id="36357-212">En fazla dört örnekleri/saat hafta sırasında örnekleri ve hafta sonları sırasında altı örnekleri saate serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36357-212">It can release instances at a maximum rate of four instances/hour during the week and six instances/hour during weekends.</span></span>

<span data-ttu-id="36357-213">Çalışan havuzunda birden çok uygulama hizmeti planları barındırılan hesaplamak varsa *toplam Enflasyon oranı* yükleniyor tüm uygulama hizmeti planları Enflasyon oranındaki toplamı, bir çalışan havuzunda barındırma.</span><span class="sxs-lookup"><span data-stu-id="36357-213">If multiple App Service plans are being hosted in a worker pool, you have to calculate the *total inflation rate* as the sum of the inflation rate for all the App Service plans that are being hosting in that worker pool.</span></span>

![Çalışan havuzunda barındırılan birden çok uygulama hizmeti planları için toplam Enflasyon oran hesaplaması.][ASP-Total-Inflation]

### <a name="use-the-app-service-plan-inflation-rate-to-define-worker-pool-autoscale-rules"></a><span data-ttu-id="36357-215">Uygulama hizmeti plan Enflasyon oranı çalışan havuzu otomatik ölçeklendirme kurallarını tanımlamak için kullanın</span><span class="sxs-lookup"><span data-stu-id="36357-215">Use the App Service plan inflation rate to define worker pool autoscale rules</span></span>
<span data-ttu-id="36357-216">Çalışan barındıran yapılandırılmış olan uygulama hizmeti planları otomatik ölçeklendirme kapasitesinin bir arabellek ayrılması gereken havuza alır.</span><span class="sxs-lookup"><span data-stu-id="36357-216">Worker pools that host App Service plans that are configured to autoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="36357-217">Arabellek büyümesine ve gerektiği gibi uygulama hizmeti planı küçültmek için otomatik ölçeklendirme işlemlerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="36357-217">The buffer allows for the autoscale operations to grow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="36357-218">En küçük arabellek hesaplanan toplam uygulama hizmeti planı Enflasyon oranı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="36357-218">The minimum buffer would be the calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="36357-219">Uygulama hizmeti ortamı ölçeklendirme işlemleri uygulamak için biraz zaman ayırın ve nedeni herhangi bir değişiklik bir ölçeklendirme işlemi devam ederken ortaya çıkar daha fazla isteğe bağlı değişiklikler için hesap.</span><span class="sxs-lookup"><span data-stu-id="36357-219">Because App Service environment scale operations take some time to apply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="36357-220">Bu gecikme karşılamak için her otomatik ölçeklendirme işlemi için en az sayıda eklenen örnekleri hesaplanan toplam uygulama hizmeti planı Enflasyon oranı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="36357-220">To accommodate this latency, we recommend that you use the calculated Total App Service Plan Inflation Rate as the minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="36357-221">Bu bilgileri kullanarak, aşağıdaki otomatik ölçeklendirme profili ve kuralları Frank tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36357-221">With this information, Frank can define the following autoscale profile and rules:</span></span>

![LOB örnek için otomatik ölçeklendirme profili kuralları.][Worker-Pool-Scale]

| <span data-ttu-id="36357-223">**Otomatik ölçeklendirme profili – haftanın günü**</span><span class="sxs-lookup"><span data-stu-id="36357-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="36357-224">**Otomatik ölçeklendirme profili – hafta sonları**</span><span class="sxs-lookup"><span data-stu-id="36357-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="36357-225">**Ad:** haftanın günü profili</span><span class="sxs-lookup"><span data-stu-id="36357-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="36357-226">**Ad:** hafta sonu profili</span><span class="sxs-lookup"><span data-stu-id="36357-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="36357-227">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="36357-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="36357-228">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="36357-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="36357-229">**Profil:** haftanın günü</span><span class="sxs-lookup"><span data-stu-id="36357-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="36357-230">**Profil:** hafta sonu</span><span class="sxs-lookup"><span data-stu-id="36357-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="36357-231">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="36357-231">**Type:** Recurrence</span></span> |<span data-ttu-id="36357-232">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="36357-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="36357-233">**Hedef aralık:** 13-25 örnekleri</span><span class="sxs-lookup"><span data-stu-id="36357-233">**Target range:** 13 to 25 instances</span></span> |<span data-ttu-id="36357-234">**Hedef aralık:** 6 ila 15 örnekleri</span><span class="sxs-lookup"><span data-stu-id="36357-234">**Target range:** 6 to 15 instances</span></span> |
| <span data-ttu-id="36357-235">**Gün sayısı:** Pazartesi, Salı, Çarşamba, Perşembe, Cuma</span><span class="sxs-lookup"><span data-stu-id="36357-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="36357-236">**Gün sayısı:** Cumartesi, Pazar</span><span class="sxs-lookup"><span data-stu-id="36357-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="36357-237">**Başlangıç zamanı:** 7: 00'da</span><span class="sxs-lookup"><span data-stu-id="36357-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="36357-238">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="36357-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="36357-239">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="36357-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="36357-240">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="36357-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="36357-241">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="36357-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="36357-242">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="36357-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="36357-243">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="36357-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="36357-244">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="36357-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="36357-245">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="36357-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="36357-246">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="36357-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="36357-247">**İşlem:** değerinden 8</span><span class="sxs-lookup"><span data-stu-id="36357-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="36357-248">**İşlem:** 3'ten az</span><span class="sxs-lookup"><span data-stu-id="36357-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="36357-249">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="36357-250">**Süresi:** 30 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="36357-251">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="36357-252">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-253">**Eylem:** sayısı 8 ile artırın</span><span class="sxs-lookup"><span data-stu-id="36357-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="36357-254">**Eylem:** artırmak sayısı 3 ile</span><span class="sxs-lookup"><span data-stu-id="36357-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="36357-255">**(Dakika) basılı güzel:** 180</span><span class="sxs-lookup"><span data-stu-id="36357-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="36357-256">**(Dakika) basılı güzel:** 180</span><span class="sxs-lookup"><span data-stu-id="36357-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="36357-257">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="36357-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="36357-258">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="36357-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="36357-259">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="36357-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="36357-260">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="36357-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="36357-261">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="36357-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="36357-262">**Ölçüm:** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="36357-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="36357-263">**İşlem:** 8 büyük</span><span class="sxs-lookup"><span data-stu-id="36357-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="36357-264">**İşlem:** 3'ten büyük</span><span class="sxs-lookup"><span data-stu-id="36357-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="36357-265">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="36357-266">**Süresi:** 15 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="36357-267">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="36357-268">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-269">**Eylem:** sayısı 2 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="36357-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="36357-270">**Eylem:** sayısı 3 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="36357-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="36357-271">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="36357-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="36357-272">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="36357-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="36357-273">Profilinde tanımlanmış hedef aralığı uygulama hizmeti planı + arabellek profilinde tanımlanan en düşük örnekler tarafından hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="36357-273">The Target range defined in the profile is calculated by the minimum instances defined in the profile for the App Service plan + buffer.</span></span>

<span data-ttu-id="36357-274">En fazla aralık çalışan havuzunda barındırılan tüm uygulama hizmeti planları için tüm maksimum aralıklarını toplamı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="36357-274">The Maximum range would be the sum of all the maximum ranges for all App Service plans hosted in the worker pool.</span></span>

<span data-ttu-id="36357-275">En az 1 X ölçek için uygulama hizmeti planı Enflasyon oranı kuralları ölçek artırma sayısı ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="36357-275">The Increase count for the scale up rules should be set to at least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="36357-276">Azaltma sayısı için bir şeyler 1/2 X veya 1'uygulama hizmeti planı Enflasyon oranı ölçek X arasında aşağı ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="36357-276">Decrease count can be adjusted to something between 1/2X or 1X the App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="36357-277">Ön uç havuzu için otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="36357-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="36357-278">Ön uç otomatik ölçeklendirme kurallarını çalışan havuzlarında daha basittir.</span><span class="sxs-lookup"><span data-stu-id="36357-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="36357-279">Öncelikle yapmanız gerekenler</span><span class="sxs-lookup"><span data-stu-id="36357-279">Primarily, you should</span></span>  
<span data-ttu-id="36357-280">süresi ölçümü ve cooldown zamanlayıcılar bir uygulama hizmeti planı üzerinde ölçeklendirme işlemleri anlık olmayan dikkate aldığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="36357-280">make sure that duration of the measurement and the cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="36357-281">Bu senaryo için hata oranı % 80 CPU kullanımı ön uçlar eriştikten sonra artırır ve örnekler gibi artırmak için otomatik ölçeklendirme kural kümesi Frank bilir:</span><span class="sxs-lookup"><span data-stu-id="36357-281">For this scenario, Frank knows that the error rate increases after front ends reach 80% CPU utilization and sets the autoscale rule to increase instances as follows:</span></span>

![Ön uç havuzu için otomatik ölçeklendirme ayarları.][Front-End-Scale]

| <span data-ttu-id="36357-283">**Otomatik ölçeklendirme profili – ön Uçlar**</span><span class="sxs-lookup"><span data-stu-id="36357-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="36357-284">**Ad:** otomatik ölçeklendirme – ön Uçlar</span><span class="sxs-lookup"><span data-stu-id="36357-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="36357-285">**Ölçek tarafından:** zamanlama ve performans kuralları</span><span class="sxs-lookup"><span data-stu-id="36357-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="36357-286">**Profil:** her gün</span><span class="sxs-lookup"><span data-stu-id="36357-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="36357-287">**Tür:** yineleme</span><span class="sxs-lookup"><span data-stu-id="36357-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="36357-288">**Hedef aralık:** 3-10 örnekleri</span><span class="sxs-lookup"><span data-stu-id="36357-288">**Target range:** 3 to 10 instances</span></span> |
| <span data-ttu-id="36357-289">**Gün sayısı:** her gün</span><span class="sxs-lookup"><span data-stu-id="36357-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="36357-290">**Başlangıç zamanı:** 09:00:00</span><span class="sxs-lookup"><span data-stu-id="36357-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="36357-291">**Saat dilimi:** UTC-08</span><span class="sxs-lookup"><span data-stu-id="36357-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="36357-292">**Otomatik ölçeklendirme kuralı (ölçeklendirme)**</span><span class="sxs-lookup"><span data-stu-id="36357-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="36357-293">**Kaynak:** ön uç havuzu</span><span class="sxs-lookup"><span data-stu-id="36357-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="36357-294">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="36357-295">**İşlem:** % 60 daha büyük</span><span class="sxs-lookup"><span data-stu-id="36357-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="36357-296">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="36357-297">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-298">**Eylem:** artırmak sayısı 3 ile</span><span class="sxs-lookup"><span data-stu-id="36357-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="36357-299">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="36357-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="36357-300">**Otomatik ölçeklendirme kural (Ölçek aşağı)**</span><span class="sxs-lookup"><span data-stu-id="36357-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="36357-301">**Kaynak:** çalışan havuzu 1</span><span class="sxs-lookup"><span data-stu-id="36357-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="36357-302">**Ölçüm:** CPU %</span><span class="sxs-lookup"><span data-stu-id="36357-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="36357-303">**İşlem:** % 30'den az</span><span class="sxs-lookup"><span data-stu-id="36357-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="36357-304">**Süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="36357-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="36357-305">**Zaman toplama:** ortalama</span><span class="sxs-lookup"><span data-stu-id="36357-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="36357-306">**Eylem:** sayısı 3 ile azaltma</span><span class="sxs-lookup"><span data-stu-id="36357-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="36357-307">**(Dakika) basılı güzel:** 120</span><span class="sxs-lookup"><span data-stu-id="36357-307">**Cool down (minutes):** 120</span></span> |

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
