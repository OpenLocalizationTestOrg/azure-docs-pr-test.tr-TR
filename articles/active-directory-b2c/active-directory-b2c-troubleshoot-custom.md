---
title: "Uygulama Öngörüler tootroubleshoot özel ilkeleri - Azure AD B2C | Microsoft Docs"
description: "nasıl toosetup Application Insights tootrace hello özel ilkeler yürütülmesi"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="e7441-103">Azure Active Directory B2C: Günlükleri toplama</span><span class="sxs-lookup"><span data-stu-id="e7441-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="e7441-104">Bu makalede, böylece özel ilkelerinizi sorunları tanılama günlüklerini Azure AD B2C ' toplanması için adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7441-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="e7441-105">Şu anda hello burada açıklanan ayrıntılı etkinlik günlükleri tasarlanmış **yalnızca** tooaid özel ilkeler geliştirme.</span><span class="sxs-lookup"><span data-stu-id="e7441-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="e7441-106">Geliştirme modunu üretimde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e7441-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="e7441-107">Günlükleri tooand hello kimlik sağlayıcılardan geliştirme sırasında gönderilen tüm talepler toplayın.</span><span class="sxs-lookup"><span data-stu-id="e7441-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="e7441-108">Üretimde kullandıysanız, hello Geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları hello App Insights günlüğünde toplanan sorumluluğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e7441-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="e7441-109">Bu ayrıntılı günlükler yalnızca Hello İlkesi yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.</span><span class="sxs-lookup"><span data-stu-id="e7441-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="e7441-110">Application Insights kullanın</span><span class="sxs-lookup"><span data-stu-id="e7441-110">Use Application Insights</span></span>

<span data-ttu-id="e7441-111">Azure AD B2C, veri tooApplication Öngörüler göndermek için bir özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="e7441-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="e7441-112">Application Insights şekilde toodiagnose özel durumlar sağlar ve uygulama performans sorunlarını görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7441-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="e7441-113">Kurulum Application Insights</span><span class="sxs-lookup"><span data-stu-id="e7441-113">Setup Application Insights</span></span>

1. <span data-ttu-id="e7441-114">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7441-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e7441-115">Azure aboneliğinizle (Azure AD B2C kiracısına değil) hello Kiracı içinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7441-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="e7441-116">Tıklatın **+ yeni** hello sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e7441-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="e7441-117">Aramak ve seçmek **Application Insights**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e7441-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="e7441-118">Merhaba form tamamlamak ve ' **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e7441-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="e7441-119">Seçin **genel** hello için **uygulama türü**.</span><span class="sxs-lookup"><span data-stu-id="e7441-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="e7441-120">Merhaba kaynak oluşturulduktan sonra hello Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="e7441-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="e7441-121">Bul **özellikleri** içinde sol menü hello ve tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7441-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="e7441-122">Kopya hello **izleme anahtarını** ve hello için sonraki bölüme kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e7441-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="e7441-123">Merhaba özel ilke ayarla</span><span class="sxs-lookup"><span data-stu-id="e7441-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="e7441-124">Merhaba RP dosyasını (örneğin, SignUpOrSignin.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="e7441-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="e7441-125">Öznitelikleri toohello aşağıdaki hello eklemek `<TrustFrameworkPolicy>` öğe:</span><span class="sxs-lookup"><span data-stu-id="e7441-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="e7441-126">Zaten yoksa, bir alt düğüm eklemek `<UserJourneyBehaviors>` toohello `<RelyingParty>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="e7441-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="e7441-127">Hemen sonra hello yer alması gerekir`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="e7441-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="e7441-128">Merhaba alt sitesi olarak düğümünü izleyen hello eklemek `<UserJourneyBehaviors>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e7441-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="e7441-129">Emin tooreplace olun `{Your Application Insights Key}` hello ile **izleme anahtarını** Application Insights hello önceki bölümdeki öğesinden edinilen.</span><span class="sxs-lookup"><span data-stu-id="e7441-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="e7441-130">`DeveloperMode="true"`en yüksek hacim rakamlarına kısıtlanmış ancak geliştirme Applicationınsights tooexpedite hello telemetri hello işleme ardışık düzeninden iyi söyler.</span><span class="sxs-lookup"><span data-stu-id="e7441-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="e7441-131">`ClientEnabled="true"`Sayfa görünümü ve istemci tarafı hataları (gerekli) izlemek için hello Applicationınsights istemci tarafı komut dosyası gönderir.</span><span class="sxs-lookup"><span data-stu-id="e7441-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="e7441-132">`ServerEnabled="true"`gönderir varolan UserJourneyRecorder JSON özel olay tooApplication Öngörüler hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="e7441-133">Örnek:</span><span class="sxs-lookup"><span data-stu-id="e7441-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="e7441-134">Hello İlkesi karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7441-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="e7441-135">Application Insights'ta Hello günlüklerini bakın</span><span class="sxs-lookup"><span data-stu-id="e7441-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="e7441-136">Olduğundan yeni günlükler Application ınsights'ta görmek için kısa bir gecikme (beş dakikadan daha az).</span><span class="sxs-lookup"><span data-stu-id="e7441-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="e7441-137">Hello oluşturduğunuz hello Application Insights kaynağını açma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7441-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="e7441-138">Merhaba, **genel bakış** menüsünde tıklatın **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e7441-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="e7441-139">Application Insights'ta yeni bir sekme açın.</span><span class="sxs-lookup"><span data-stu-id="e7441-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="e7441-140">İşte bir listesi, toosee hello günlüklerini kullanabileceğiniz sorgu</span><span class="sxs-lookup"><span data-stu-id="e7441-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="e7441-141">Sorgu</span><span class="sxs-lookup"><span data-stu-id="e7441-141">Query</span></span> | <span data-ttu-id="e7441-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7441-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="e7441-143">İzlemeler</span><span class="sxs-lookup"><span data-stu-id="e7441-143">traces</span></span> | <span data-ttu-id="e7441-144">Tüm Azure AD B2C tarafından oluşturulan hello günlükleri bakın</span><span class="sxs-lookup"><span data-stu-id="e7441-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="e7441-145">izlemeler \\</span><span class="sxs-lookup"><span data-stu-id="e7441-145">traces \\</span></span>| <span data-ttu-id="e7441-146">Burada zaman damgası > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="e7441-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="e7441-147">Azure AD B2C tarafından son günü hello için oluşturulan hello günlüklerin bakın</span><span class="sxs-lookup"><span data-stu-id="e7441-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="e7441-148">Merhaba girişleri uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7441-148">hello entries may be long.</span></span>  <span data-ttu-id="e7441-149">Daha ayrıntılı bir bakış için tooCSV verin.</span><span class="sxs-lookup"><span data-stu-id="e7441-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="e7441-150">Merhaba analiz aracı hakkında daha fazla bilgiyi [burada](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="e7441-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="e7441-151">Merhaba topluluk bir kullanıcı gezisine Görüntüleyicisi toohelp kimlik geliştiriciler geliştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="e7441-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="e7441-152">Bu değil Microsoft tarafından desteklenir ve kesin olarak kullanılabilir hale-değil.</span><span class="sxs-lookup"><span data-stu-id="e7441-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="e7441-153">Application Insights örneğinden okur ve hello kullanıcı gezisine olayları iyi yapısı görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7441-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="e7441-154">Merhaba kaynak kodu alın ve kendi çözümde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e7441-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="e7441-155">Şu anda hello burada açıklanan ayrıntılı etkinlik günlükleri tasarlanmış **yalnızca** tooaid özel ilkeler geliştirme.</span><span class="sxs-lookup"><span data-stu-id="e7441-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="e7441-156">Geliştirme modunu üretimde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="e7441-156">Do not use development mode in production.</span></span>  <span data-ttu-id="e7441-157">Günlükleri tooand hello kimlik sağlayıcılardan geliştirme sırasında gönderilen tüm talepler toplayın.</span><span class="sxs-lookup"><span data-stu-id="e7441-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="e7441-158">Üretimde kullandıysanız, hello Geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları hello App Insights günlüğünde toplanan sorumluluğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e7441-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="e7441-159">Bu ayrıntılı günlükler yalnızca Hello İlkesi yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.</span><span class="sxs-lookup"><span data-stu-id="e7441-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="e7441-160">Desteklenmeyen özel ilkesi örnekleri ve ilgili araçlar için Github depo</span><span class="sxs-lookup"><span data-stu-id="e7441-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="e7441-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e7441-161">Next Steps</span></span>

<span data-ttu-id="e7441-162">Application Insights toohelp anladığınızdan Hello keşfedin kimlik deneyimi temel B2C çalışır kendi kimlik karşılaştığında toodeliver Çerçevesi'ne hello.</span><span class="sxs-lookup"><span data-stu-id="e7441-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
