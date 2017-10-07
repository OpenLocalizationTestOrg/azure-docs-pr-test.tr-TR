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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Günlükleri toplama

Bu makalede, böylece özel ilkelerinizi sorunları tanılama günlüklerini Azure AD B2C ' toplanması için adımları sağlar.

>[!NOTE]
>Şu anda hello burada açıklanan ayrıntılı etkinlik günlükleri tasarlanmış **yalnızca** tooaid özel ilkeler geliştirme. Geliştirme modunu üretimde kullanmayın.  Günlükleri tooand hello kimlik sağlayıcılardan geliştirme sırasında gönderilen tüm talepler toplayın.  Üretimde kullandıysanız, hello Geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları hello App Insights günlüğünde toplanan sorumluluğunu varsayar.  Bu ayrıntılı günlükler yalnızca Hello İlkesi yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.


## <a name="use-application-insights"></a>Application Insights kullanın

Azure AD B2C, veri tooApplication Öngörüler göndermek için bir özelliği destekler.  Application Insights şekilde toodiagnose özel durumlar sağlar ve uygulama performans sorunlarını görselleştirin.

### <a name="setup-application-insights"></a>Kurulum Application Insights

1. Toohello Git [Azure portal](https://portal.azure.com). Azure aboneliğinizle (Azure AD B2C kiracısına değil) hello Kiracı içinde olduğundan emin olun.
1. Tıklatın **+ yeni** hello sol taraftaki gezinti menüsünde.
1. Aramak ve seçmek **Application Insights**, ardından **oluşturma**.
1. Merhaba form tamamlamak ve ' **oluşturma**. Seçin **genel** hello için **uygulama türü**.
1. Merhaba kaynak oluşturulduktan sonra hello Application Insights kaynağı açın.
1. Bul **özellikleri** içinde sol menü hello ve tıklayın.
1. Kopya hello **izleme anahtarını** ve hello için sonraki bölüme kaydedin.

### <a name="set-up-hello-custom-policy"></a>Merhaba özel ilke ayarla

1. Merhaba RP dosyasını (örneğin, SignUpOrSignin.xml) açın.
1. Öznitelikleri toohello aşağıdaki hello eklemek `<TrustFrameworkPolicy>` öğe:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Zaten yoksa, bir alt düğüm eklemek `<UserJourneyBehaviors>` toohello `<RelyingParty>` düğümü. Hemen sonra hello yer alması gerekir`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Merhaba alt sitesi olarak düğümünü izleyen hello eklemek `<UserJourneyBehaviors>` öğesi. Emin tooreplace olun `{Your Application Insights Key}` hello ile **izleme anahtarını** Application Insights hello önceki bölümdeki öğesinden edinilen.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`en yüksek hacim rakamlarına kısıtlanmış ancak geliştirme Applicationınsights tooexpedite hello telemetri hello işleme ardışık düzeninden iyi söyler.
  * `ClientEnabled="true"`Sayfa görünümü ve istemci tarafı hataları (gerekli) izlemek için hello Applicationınsights istemci tarafı komut dosyası gönderir.
  * `ServerEnabled="true"`gönderir varolan UserJourneyRecorder JSON özel olay tooApplication Öngörüler hello.
Örnek:

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

3. Hello İlkesi karşıya yükleyin.

### <a name="see-hello-logs-in-application-insights"></a>Application Insights'ta Hello günlüklerini bakın

>[!NOTE]
> Olduğundan yeni günlükler Application ınsights'ta görmek için kısa bir gecikme (beş dakikadan daha az).

1. Hello oluşturduğunuz hello Application Insights kaynağını açma [Azure portal](https://portal.azure.com).
1. Merhaba, **genel bakış** menüsünde tıklatın **Analytics**.
1. Application Insights'ta yeni bir sekme açın.
1. İşte bir listesi, toosee hello günlüklerini kullanabileceğiniz sorgu

| Sorgu | Açıklama |
|---------------------|--------------------|
İzlemeler | Tüm Azure AD B2C tarafından oluşturulan hello günlükleri bakın |
izlemeler \| Burada zaman damgası > ago(1d) | Azure AD B2C tarafından son günü hello için oluşturulan hello günlüklerin bakın

Merhaba girişleri uzun olabilir.  Daha ayrıntılı bir bakış için tooCSV verin.

Merhaba analiz aracı hakkında daha fazla bilgiyi [burada](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Merhaba topluluk bir kullanıcı gezisine Görüntüleyicisi toohelp kimlik geliştiriciler geliştirmiştir.  Bu değil Microsoft tarafından desteklenir ve kesin olarak kullanılabilir hale-değil.  Application Insights örneğinden okur ve hello kullanıcı gezisine olayları iyi yapısı görünümünü sağlar.  Merhaba kaynak kodu alın ve kendi çözümde dağıtın.

>[!NOTE]
>Şu anda hello burada açıklanan ayrıntılı etkinlik günlükleri tasarlanmış **yalnızca** tooaid özel ilkeler geliştirme. Geliştirme modunu üretimde kullanmayın.  Günlükleri tooand hello kimlik sağlayıcılardan geliştirme sırasında gönderilen tüm talepler toplayın.  Üretimde kullandıysanız, hello Geliştirici PII (özel olarak tanımlanabilen bilgiler) sahip oldukları hello App Insights günlüğünde toplanan sorumluluğunu varsayar.  Bu ayrıntılı günlükler yalnızca Hello İlkesi yerleştirildiği olduğunda toplanır **geliştirme MODUNU**.

[Desteklenmeyen özel ilkesi örnekleri ve ilgili araçlar için Github depo](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Sonraki Adımlar

Application Insights toohelp anladığınızdan Hello keşfedin kimlik deneyimi temel B2C çalışır kendi kimlik karşılaştığında toodeliver Çerçevesi'ne hello.
