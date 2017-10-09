---
title: "aaaAzure uygulama Insights Telemetri veri modeli - Telemetri bağlamı | Microsoft Docs"
description: "Uygulama Insights telemetri bağlamı veri modeli"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="63b2b-103">Telemetri bağlamı: Application Insights veri modeli</span><span class="sxs-lookup"><span data-stu-id="63b2b-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="63b2b-104">Her telemetri öğeyi kesin türü belirtilmiş bağlam alanları olabilir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="63b2b-105">Her alan belirli bir izleme senaryosu sağlar.</span><span class="sxs-lookup"><span data-stu-id="63b2b-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="63b2b-106">Merhaba özel özellikler koleksiyonu toostore veya uygulamaya özgü özel bağlamsal bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="63b2b-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="63b2b-107">Uygulama sürümü</span><span class="sxs-lookup"><span data-stu-id="63b2b-107">Application version</span></span>

<span data-ttu-id="63b2b-108">Hello uygulama içerik alanlarında her zaman hello telemetri gönderiyor hello uygulama hakkındaki bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="63b2b-109">Uygulama, kullanılan tooanalyze eğilim değişiklikler hello uygulama davranışına ve bağıntı toohello dağıtımları sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="63b2b-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="63b2b-110">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="63b2b-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="63b2b-111">İstemci IP adresi</span><span class="sxs-lookup"><span data-stu-id="63b2b-111">Client IP address</span></span>

<span data-ttu-id="63b2b-112">Merhaba istemci aygıt Hello IP adresi.</span><span class="sxs-lookup"><span data-stu-id="63b2b-112">hello IP address of hello client device.</span></span> <span data-ttu-id="63b2b-113">IPv4 ve IPv6 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="63b2b-114">Telemetri bir hizmetten gönderildiğinde, hello konumu bağlam hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="63b2b-115">Application Insights hello coğrafi konum bilgileri hello istemci IP ayıklayın ve ardından kesme.</span><span class="sxs-lookup"><span data-stu-id="63b2b-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="63b2b-116">Bu nedenle istemci IP kendisi tarafından son kullanıcı bilgilerinizle kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="63b2b-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="63b2b-117">En fazla uzunluk: 46</span><span class="sxs-lookup"><span data-stu-id="63b2b-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="63b2b-118">Aygıt türü</span><span class="sxs-lookup"><span data-stu-id="63b2b-118">Device type</span></span>

<span data-ttu-id="63b2b-119">Bu alan kullanılan hello aygıt hello son kullanıcı hello uygulamasının tooindicate hello türü kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="63b2b-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="63b2b-120">Bugün öncelikle toodistinguish JavaScript telemetri hello cihaz türünden 'Browser' sunucu tarafı telemetri 'PC' hello cihaz türüyle ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="63b2b-121">En fazla uzunluk: 64</span><span class="sxs-lookup"><span data-stu-id="63b2b-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="63b2b-122">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-122">Operation id</span></span>

<span data-ttu-id="63b2b-123">Merhaba kök işlemi benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="63b2b-124">Bu tanımlayıcı toogroup telemetri arasında birden çok bileşen sağlar.</span><span class="sxs-lookup"><span data-stu-id="63b2b-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="63b2b-125">Bkz: [telemetri bağıntı](application-insights-correlation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="63b2b-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="63b2b-126">Merhaba işlem kimliği, bir istek veya bir sayfa görünümü tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="63b2b-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="63b2b-127">Diğer tüm telemetri isteği ya da sayfa görünümü içeren hello için bu alan toohello değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="63b2b-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="63b2b-128">En fazla uzunluk: 128</span><span class="sxs-lookup"><span data-stu-id="63b2b-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="63b2b-129">Üst işlem kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-129">Parent operation ID</span></span>

<span data-ttu-id="63b2b-130">Merhaba telemetri öğesi'nin en yakın üst benzersiz tanıtıcısı hello.</span><span class="sxs-lookup"><span data-stu-id="63b2b-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="63b2b-131">Bkz: [telemetri bağıntı](application-insights-correlation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="63b2b-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="63b2b-132">En fazla uzunluk: 128</span><span class="sxs-lookup"><span data-stu-id="63b2b-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="63b2b-133">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="63b2b-133">Operation name</span></span>

<span data-ttu-id="63b2b-134">Merhaba (Grup) hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="63b2b-135">Merhaba işlem adı, bir istek veya bir sayfa görünümü tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="63b2b-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="63b2b-136">Diğer tüm telemetri öğeleri istek veya sayfa görünümü içeren hello için bu alan toohello değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="63b2b-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="63b2b-137">İşlem adı işlemlerini (örneğin ' GET Home/Index') grubu için tüm hello telemetri öğeleri bulmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="63b2b-138">"Bu sayfada oluşturulan hello tipik özel durumları nelerdir." gibi soruları kullanılan tooanswer bu bağlam özelliğidir</span><span class="sxs-lookup"><span data-stu-id="63b2b-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="63b2b-139">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="63b2b-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="63b2b-140">Merhaba işlemin yapay kaynak</span><span class="sxs-lookup"><span data-stu-id="63b2b-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="63b2b-141">Yapay kaynağının adı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-141">Name of synthetic source.</span></span> <span data-ttu-id="63b2b-142">Birkaç telemetri hello uygulamasından yapay trafiği temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="63b2b-143">Web Gezgin dizin hello web sitesi, site kullanılabilirlik testleri veya Application Insights SDK kendisini gibi tanılama kitaplıklarından izlemeleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="63b2b-144">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="63b2b-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="63b2b-145">Oturum kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-145">Session id</span></span>

<span data-ttu-id="63b2b-146">Oturum kimliği - hello uygulama hello kullanıcının etkileşim hello örneği.</span><span class="sxs-lookup"><span data-stu-id="63b2b-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="63b2b-147">Merhaba oturum bağlamı alanları her zaman hello son kullanıcı bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="63b2b-148">Telemetri bir hizmetten gönderildiğinde, hello oturum bağlamı hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="63b2b-149">En fazla uzunluk: 64</span><span class="sxs-lookup"><span data-stu-id="63b2b-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="63b2b-150">Anonim kullanıcı kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-150">Anonymous user id</span></span>

<span data-ttu-id="63b2b-151">Anonim kullanıcı kimliği. Merhaba son kullanıcı hello uygulamasının temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63b2b-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="63b2b-152">Telemetri bir hizmetten gönderildiğinde, hello kullanıcı bağlamı hello işlemi hello hizmetinde başlatılan hello kullanıcı hakkındadır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="63b2b-153">[Örnekleme](app-insights-sampling.md) hello teknikleri toominimize hello toplanan telemetri miktarı biridir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="63b2b-154">Algoritma denemeleri tooeither örnekleme örnek giriş veya çıkış tüm hello telemetri bağıntılı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="63b2b-155">Anonim kullanıcı kimliği, puan nesil örnekleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="63b2b-156">Bu nedenle anonim kullanıcı kimliği yeterince rastgele bir değeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="63b2b-157">Anonim kullanıcı kimliği toostore kullanıcı adı kötüye hello alanının kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="63b2b-158">Kimliği doğrulanmış kullanıcı kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="63b2b-158">Use Authenticated user id.</span></span>

<span data-ttu-id="63b2b-159">En fazla uzunluk: 128</span><span class="sxs-lookup"><span data-stu-id="63b2b-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="63b2b-160">Kimliği doğrulanmış kullanıcı kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-160">Authenticated user id</span></span>

<span data-ttu-id="63b2b-161">Kimliği doğrulanmış kullanıcı kimliği. Anonim kullanıcı kimliği, bu alan ters Hello kolay bir ad ile Merhaba kullanıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63b2b-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="63b2b-162">PII bilgilerini bu yana çoğu SDK'sı tarafından varsayılan olarak toplanmaz.</span><span class="sxs-lookup"><span data-stu-id="63b2b-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="63b2b-163">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="63b2b-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="63b2b-164">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="63b2b-164">Account id</span></span>

<span data-ttu-id="63b2b-165">Çok kiracılı uygulamalara hello hesap kimliği veya adı, hangi hello kullanıcı ile hareket budur.</span><span class="sxs-lookup"><span data-stu-id="63b2b-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="63b2b-166">Örnekler, abonelik kimliği için Azure portal veya blog adı blog platformu olabilir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="63b2b-167">En fazla uzunluk: 1024</span><span class="sxs-lookup"><span data-stu-id="63b2b-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="63b2b-168">Bulut rolü</span><span class="sxs-lookup"><span data-stu-id="63b2b-168">Cloud role</span></span>

<span data-ttu-id="63b2b-169">Merhaba rol hello uygulamanın adını, bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="63b2b-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="63b2b-170">Doğrudan azure toohello rol adını eşler.</span><span class="sxs-lookup"><span data-stu-id="63b2b-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="63b2b-171">Ayrıca kullanılan toodistinguish tek bir uygulamanın parçası olan mikro hizmetler olabilir.</span><span class="sxs-lookup"><span data-stu-id="63b2b-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="63b2b-172">En fazla uzunluk: 256</span><span class="sxs-lookup"><span data-stu-id="63b2b-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="63b2b-173">Bulut rol örneği</span><span class="sxs-lookup"><span data-stu-id="63b2b-173">Cloud role instance</span></span>

<span data-ttu-id="63b2b-174">Merhaba uygulaması çalıştığı hello örneğinin adı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="63b2b-175">Bilgisayar adı şirket içi, Azure için örnek adı.</span><span class="sxs-lookup"><span data-stu-id="63b2b-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="63b2b-176">En fazla uzunluk: 256</span><span class="sxs-lookup"><span data-stu-id="63b2b-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="63b2b-177">Dahili: SDK sürümü</span><span class="sxs-lookup"><span data-stu-id="63b2b-177">Internal: SDK version</span></span>

<span data-ttu-id="63b2b-178">SDK sürümü.</span><span class="sxs-lookup"><span data-stu-id="63b2b-178">SDK version.</span></span> <span data-ttu-id="63b2b-179">Https://github.com/Microsoft/ApplicationInsights-Home/BLOB/master/SDK-AUTHORING.MD#SDK-Version-Specification bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="63b2b-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="63b2b-180">En fazla uzunluk: 64</span><span class="sxs-lookup"><span data-stu-id="63b2b-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="63b2b-181">Dahili: Düğüm adı</span><span class="sxs-lookup"><span data-stu-id="63b2b-181">Internal: Node name</span></span>

<span data-ttu-id="63b2b-182">Bu alan, fatura amacıyla kullanılan hello düğüm adı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63b2b-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="63b2b-183">Toooverride hello standart algılama düğümlerinin kullanın.</span><span class="sxs-lookup"><span data-stu-id="63b2b-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="63b2b-184">En fazla uzunluk: 256</span><span class="sxs-lookup"><span data-stu-id="63b2b-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="63b2b-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63b2b-185">Next steps</span></span>

- <span data-ttu-id="63b2b-186">Nasıl çok öğrenin[genişletmek ve filtre telemetri](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="63b2b-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="63b2b-187">Bkz: [veri modeli](application-insights-data-model.md) Application Insights türleri ve veri modeli için.</span><span class="sxs-lookup"><span data-stu-id="63b2b-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="63b2b-188">Standart bağlam özellikleri koleksiyonunu denetleyin [yapılandırma](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="63b2b-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
