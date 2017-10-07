---
title: "Unity Android dağıtımı için aaaGet Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl tooiOS aygıtları dağıtma Unity uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Unity Android dağıtımı için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve nasıl toosend anında iletme bildirimleri toosegmented kullanıcılar bir Unity uygulamasının tooan Android cihazına dağıtırken.
Bu öğretici kullanır Klasik Unity Roll bir küre öğretici hello başlangıç noktası hello. Bu başlangıç adımları izlemelisiniz [öğretici](mobile-engagement-unity-roll-a-ball.md) hello hello aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesi işlemine devam etmeden önce. 

Bu öğretici hello aşağıdakileri gerektirir:

* [Unity Düzenleyicisi](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Android uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
### <a name="import-hello-unity-package"></a>Merhaba Unity paketini içeri aktarma
1. Merhaba karşıdan [Mobile Engagement Unity paketini](https://aka.ms/azmeunitysdk) ve tooyour yerel makine kaydedin. 
2. Çok Git**varlıklar -> paketi İçeri Aktar -> özel paket** ve indirilen Yukarıdaki adımı hello içindeki select hello paketi. 
   
    ![][70] 
3. Tüm dosyaların seçildiğinden emin olun ve **İçeri Aktar** düğmesine tıklayın. 
   
    ![][71] 
4. İçeri aktarma başarılı olduktan sonra hello içeri aktarılan SDK dosyalarını projenizde görürsünüz.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Merhaba EngagementConfiguration güncelleştir
1. Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **ANDROID\_bağlantı\_dize** aldığınız hello bağlantı dizesiyle daha önce hello Azure portalı.  
   
    ![][73]
2. Merhaba dosyasını kaydedin 
3. **Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün. Bu hello Mobile Engagement SDK tarafından eklenen hello eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir. 
   
    ![][74]

> [!IMPORTANT]
> Merhaba güncelleştirdiğiniz her sefer emin tooexecute bunu yap **EngagementConfiguration** dosya Aksi takdirde değişiklikleriniz hello uygulamada yansıtılmaz. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Merhaba uygulamayı temel izleme için yapılandırma
1. Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası. 
2. Merhaba aşağıdaki ekleme deyimini kullanarak:
   
        using Microsoft.Azure.Engagement.Unity;
3. Toohello aşağıdaki hello eklemek `Start()` yöntemi
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Dağıtma ve hello uygulamayı çalıştırma
Android SDK toodeploy bu Unity uygulamasını tooyour aygıt çalışmadan önce makinenizde yüklü olduğundan emin olun. 

1. Bir Android cihaz tooyour makineyi bağlayın. 
2. **Dosya -> Yapı Ayarları**’nı açın 
   
    ![][40]
3. **Android**’i seçin ve ardından **Anahtar Platformu**’na tıklayın
   
    ![][51]
   
    ![][52]
4. **Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin. 
   
    ![][53]
5. Son olarak, **Derle ve Çalıştır**’a tıklayın.
   
    ![][54]
6. Olabilir bir klasör adı toostore hello Android paketini tooprovide istedi. 
7. Merhaba paket bağlı dağıtılan tooyour sonra her şey ince, giderse Unity oyununuzu cihaz ve telefonunuzda görmeniz gerekir! 

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Merhaba EngagementConfiguration güncelleştir
1. Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **ANDROID\_GOOGLE\_numarası** hello ile **Google proje Sayı** önceki hello Google Cloud Developer portaldan aldığınız. Bu bir dizedir değeri nedenle emin tooenclose olun çift tırnak işareti içinde. 
   
    ![][75]
2. Merhaba dosyasını kaydedin. 
3. **Dosya -> Engagement -> Android Derleme Bildirimi Oluştur**’yürütün. Bu hello Mobile Engagement SDK tarafından eklenen hello eklentidir ve buna tıklamak proje ayarlarınızı otomatik olarak güncelleştirir. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Merhaba uygulama tooreceive bildirimleri yapılandırma
1. Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası. 
2. Toohello aşağıdaki hello eklemek `Start()` yöntemi
   
        EngagementReachAgent.Initialize();
3. Merhaba uygulama güncelleştirildiğine göre dağıtın ve hello yönergeler aşağıda sağlanan her bir cihazda hello uygulamayı çalıştırın. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
