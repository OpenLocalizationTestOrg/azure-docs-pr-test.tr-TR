---
title: "aaaWindows Phone Silverlight SDK yükseltme yordamları"
description: "Windows Phone Silverlight SDK yükseltme yordamları için Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Windows Phone Silverlight SDK yükseltme yordamları
Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir. 0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.

## <a name="from-200-too330"></a>2.0.0 gelen too3.3.0
### <a name="test-logs"></a>Test günlükleri
Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir. toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>1.1.1 gelen too2.0.0
Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır. 

> [!IMPORTANT]
> Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular. Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ
> 
> 

Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.1.1 ilk başvurun sonra hello aşağıdaki yordamı uygulayın

### <a name="nuget-package"></a>Nuget paketi
Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.

### <a name="applying-mobile-engagement"></a>Mobil katılım uygulama
Merhaba SDK kullanan hello terim `Engagement`. Proje toomatch tooupdate gereken bu değişikliği.

Toouninstall, geçerli Capptain nuget paketi gerekir. Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun. Tookeep istiyorsanız, bu dosyaların bir kopyasını sonra yapın.

Bundan sonra projenizde hello yeni Microsoft Azure katılım nuget paketini yükleyin. Doğrudan üzerinde bulabilirsiniz [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Tüm kaynak dosyaları katılım tarafından kullanılan ve hello yeni katılım DLL tooyour ekler bu eylem değiştirir başvuruları yansıtın.

Proje başvuruları Capptain DLL başvurularını silerek tooclean sahip. Bunu yapmazsanız Capptain hello sürümü çakışır ve hataları gerçekleşir.

Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları hello yeni katılım dosyalarında yapıştırın. Xaml ve cs dosyaları güncelleştirilmiş toobe gerektiğini unutmayın.

Bu adımlar tamamlandığında tooreplace eski Capptain başvurular hello yeni katılım başvurular tarafından yeterlidir.

1. Tüm Capptain ad güncelleştirilmiş toobe sahip.
   
    Geçişten önce:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Geçişten sonra:
   
        using Microsoft.Azure.Engagement;
2. "Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.
   
    Geçişten önce:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Geçişten sonra:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.
   
    Geçişten önce:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Geçişten sonra:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. İçin diğer kaynakları Capptain resimler gibi Merhaba, bunlar da yeniden adlandırılmış toouse "Katılım" kaldırılmış lütfen unutmayın.

### <a name="application-id--sdk-key"></a>Uygulama Kimliği / SDK anahtarı
Katılım bağlantı dizesini kullanır. Bir uygulama kimliği ve Mobile Engagement SDK'sı anahtarla toospecify yoksa, toospecify bir bağlantı dizesi yeterlidir. Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.

Merhaba katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.

Bu dosya toospecify düzenleyin:

* Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.

Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için hello Klasik Azure portalı görüntülenir.

### <a name="items-name-change"></a>Öğe adı değişikliği
Tüm öğeleri adlı *capptain* adlandırılmış *engagement*. Benzer şekilde *Capptain* çok*Engagement*.

Yaygın olarak kullanılan Capptain öğeleri örnekleri:

* Şimdi EngagementConfiguration adlı CapptainConfiguration
* Şimdi EngagementAgent adlı CapptainAgent
* Şimdi EngagementReach adlı CapptainReach
* Şimdi EngagementHttpConfig adlı CapptainHttpConfig
* Şimdi GetEngagementPageName adlı GetCapptainPageName

Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.

