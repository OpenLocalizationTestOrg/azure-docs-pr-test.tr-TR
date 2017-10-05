---
title: "Azure AD B2C özel ilkeleri - gidermek için application Insights | Microsoft Docs"
description: "Kurulum özel ilkeler yürütülmesini izlemek için Application Insights nasıl"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="8ec02-103">Azure Active Directory B2C: Günlükleri toplama</span><span class="sxs-lookup"><span data-stu-id="8ec02-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="8ec02-104">Bu makalede, böylece özel ilkelerinizi sorunları tanılama günlüklerini Azure AD B2C ' toplanması için adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ec02-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="8ec02-105">Burada açıklanan ayrıntılı etkinlik günlükleri şu anda tasarlanmış **yalnızca** özel ilkeler geliştirmeye yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="8ec02-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="8ec02-106">Geliştirme modunu üretimde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="8ec02-107">Geliştirme sırasında gönderilen ve kimlik sağlayıcılardan gelen tüm talepler günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="8ec02-108">Üretimde kullandıysanız, geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları App Insights günlüğünde toplanan sorumluluğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8ec02-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="8ec02-109">Bu ayrıntılı günlükler yalnızca ilke yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="8ec02-110">Application Insights kullanın</span><span class="sxs-lookup"><span data-stu-id="8ec02-110">Use Application Insights</span></span>

<span data-ttu-id="8ec02-111">Azure AD B2C, Application Insights'a veri göndermek için bir özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="8ec02-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="8ec02-112">Application Insights özel durumlar tanılama ve uygulama performans sorunlarını görselleştirmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ec02-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="8ec02-113">Kurulum Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ec02-113">Setup Application Insights</span></span>

1. <span data-ttu-id="8ec02-114">[Azure Portal](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="8ec02-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ec02-115">Kiracısı'nda, Azure aboneliğinizle (Azure AD B2C kiracısına değil) olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8ec02-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="8ec02-116">Tıklatın **+ yeni** sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8ec02-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="8ec02-117">Aramak ve seçmek **Application Insights**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="8ec02-118">Formu tamamlayıp tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="8ec02-119">Seçin **genel** için **uygulama türü**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="8ec02-120">Kaynak oluşturulduktan sonra Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="8ec02-121">Bul **özellikleri** sol menü ve onu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="8ec02-122">Kopya **izleme anahtarını** ve için sonraki bölüme kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8ec02-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="8ec02-123">Özel ilke ayarla</span><span class="sxs-lookup"><span data-stu-id="8ec02-123">Set up the custom policy</span></span>

1. <span data-ttu-id="8ec02-124">RP dosyasını (örneğin, SignUpOrSignin.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="8ec02-125">Aşağıdaki öznitelikler eklemek `<TrustFrameworkPolicy>` öğe:</span><span class="sxs-lookup"><span data-stu-id="8ec02-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="8ec02-126">Zaten yoksa, bir alt düğüm eklemek `<UserJourneyBehaviors>` için `<RelyingParty>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="8ec02-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="8ec02-127">Hemen sonra bulunmalıdır`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="8ec02-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="8ec02-128">Bir alt öğesi olarak aşağıdaki düğüm eklemek `<UserJourneyBehaviors>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="8ec02-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="8ec02-129">Değiştirdiğinizden emin olun `{Your Application Insights Key}` ile **izleme anahtarını** gelen Application Insights önceki bölümde edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="8ec02-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="8ec02-130">`DeveloperMode="true"`en yüksek hacim rakamlarına kısıtlanmış ancak geliştirme için işleme ardışık düzeninden telemetri iyi hızlandırmak için Applicationınsights söyler.</span><span class="sxs-lookup"><span data-stu-id="8ec02-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="8ec02-131">`ClientEnabled="true"`Sayfa görünümü ve istemci tarafı hataları (gerekli) izlemek için Applicationınsights istemci tarafı komut dosyası gönderir.</span><span class="sxs-lookup"><span data-stu-id="8ec02-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="8ec02-132">`ServerEnabled="true"`Varolan UserJourneyRecorder JSON özel bir olay Application Insights'a gönderir.</span><span class="sxs-lookup"><span data-stu-id="8ec02-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="8ec02-133">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8ec02-133">Sample:</span></span>

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

3. <span data-ttu-id="8ec02-134">İlke karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8ec02-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="8ec02-135">Application Insights günlüklerine bakın</span><span class="sxs-lookup"><span data-stu-id="8ec02-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="8ec02-136">Olduğundan yeni günlükler Application ınsights'ta görmek için kısa bir gecikme (beş dakikadan daha az).</span><span class="sxs-lookup"><span data-stu-id="8ec02-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="8ec02-137">Oluşturduğunuz Application Insights kaynağını açma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ec02-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="8ec02-138">İçinde **genel bakış** menüsünde tıklatın **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="8ec02-139">Application Insights'ta yeni bir sekme açın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="8ec02-140">Burada bir listesidir günlükleri görmek için kullanabileceğiniz sorgular</span><span class="sxs-lookup"><span data-stu-id="8ec02-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="8ec02-141">Sorgu</span><span class="sxs-lookup"><span data-stu-id="8ec02-141">Query</span></span> | <span data-ttu-id="8ec02-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ec02-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="8ec02-143">İzlemeler</span><span class="sxs-lookup"><span data-stu-id="8ec02-143">traces</span></span> | <span data-ttu-id="8ec02-144">Tüm Azure AD B2C tarafından oluşturulan günlükler bakın</span><span class="sxs-lookup"><span data-stu-id="8ec02-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="8ec02-145">izlemeler \\</span><span class="sxs-lookup"><span data-stu-id="8ec02-145">traces \\</span></span>| <span data-ttu-id="8ec02-146">Burada zaman damgası > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="8ec02-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="8ec02-147">Tüm son gündür Azure AD B2C tarafından oluşturulan günlükler bakın</span><span class="sxs-lookup"><span data-stu-id="8ec02-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="8ec02-148">Girişleri uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ec02-148">The entries may be long.</span></span>  <span data-ttu-id="8ec02-149">Daha ayrıntılı bir bakış için CSV'ye aktarın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="8ec02-150">Analiz aracı hakkında daha fazla bilgiyi [burada](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="8ec02-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="8ec02-151">Topluluk kimlik geliştiricilere yardımcı olmak için bir kullanıcı gezisine Görüntüleyici geliştirmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ec02-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="8ec02-152">Bu değil Microsoft tarafından desteklenir ve kesin olarak kullanılabilir hale-değil.</span><span class="sxs-lookup"><span data-stu-id="8ec02-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="8ec02-153">Application Insights örneğinden okur ve gezisine olayları kullanıcı iyi yapısı görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ec02-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="8ec02-154">Kaynak kodu alın ve kendi çözümde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="8ec02-155">Burada açıklanan ayrıntılı etkinlik günlükleri şu anda tasarlanmış **yalnızca** özel ilkeler geliştirmeye yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="8ec02-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="8ec02-156">Geliştirme modunu üretimde kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-156">Do not use development mode in production.</span></span>  <span data-ttu-id="8ec02-157">Geliştirme sırasında gönderilen ve kimlik sağlayıcılardan gelen tüm talepler günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="8ec02-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="8ec02-158">Üretimde kullandıysanız, geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları App Insights günlüğünde toplanan sorumluluğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8ec02-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="8ec02-159">Bu ayrıntılı günlükler yalnızca ilke yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.</span><span class="sxs-lookup"><span data-stu-id="8ec02-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="8ec02-160">Desteklenmeyen özel ilkesi örnekleri ve ilgili araçlar için Github depo</span><span class="sxs-lookup"><span data-stu-id="8ec02-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="8ec02-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8ec02-161">Next Steps</span></span>

<span data-ttu-id="8ec02-162">Application Insights'ı nasıl kimlik deneyimi kendi kimlik sunmak için temel alınan B2C çalışır Framework deneyimlerini anlamanıza yardımcı olması için verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="8ec02-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
