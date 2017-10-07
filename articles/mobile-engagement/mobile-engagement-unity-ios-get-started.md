---
title: "Unity iOS dağıtımı için aaaGet Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl tooiOS aygıtları dağıtma Unity uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Unity iOS dağıtımı için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve nasıl toosend anında iletme bildirimleri toosegmented kullanıcılar bir Unity uygulamasının tooan iOS cihazına dağıtırken.
Bu öğretici kullanır Klasik Unity Roll bir küre öğretici hello başlangıç noktası hello. Bu başlangıç adımları izlemelisiniz [öğretici](mobile-engagement-unity-roll-a-ball.md) hello hello aşağıdaki öğreticide gösterdiğimiz Mobile Engagement tümleştirmesi işlemine devam etmeden önce. 

Bu öğretici hello aşağıdakileri gerektirir:

* [Unity Düzenleyicisi](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* XCode Düzenleyicisi

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma
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
1. Merhaba açın **EngagementConfiguration** hello SDK klasörü ve güncelleştirme hello betik dosyasından **IOS\_bağlantı\_dize** daha önce aldığınız hello bağlantı dizesiyle Azure portal Hello.  
   
    ![][73]
2. Merhaba dosyasını kaydedin. 

### <a name="configure-hello-app-for-basic-tracking"></a>Merhaba uygulamayı temel izleme için yapılandırma
1. Merhaba açın **PlayerController** iliştirilmiş düzenlemek için Player nesnesine toohello komut dosyası. 
2. Merhaba aşağıdaki ekleme deyimini kullanarak:
   
        using Microsoft.Azure.Engagement.Unity;
3. Toohello aşağıdaki hello eklemek `Start()` yöntemi
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Dağıtma ve hello uygulamayı çalıştırma
1. Bir iOS aygıtı tooyour makineyi bağlayın. 
2. **Dosya -> Yapı Ayarları**’nı açın 
   
    ![][40]
3. **iOS**’u seçin ve ardından **Anahtar Platformu**’na tıklayın
   
    ![][41]
   
    ![][42]
4. **Player ayarları**’na tıklayın ve geçerli bir Paket Tanımlayıcısı girin. 
   
    ![][53]
5. Son olarak, **Derle ve Çalıştır**’a tıklayın.
   
    ![][54]
6. Olabilir bir klasör adı toostore hello iOS paketini tooprovide istedi. 
   
    ![][43]
7. Her şey yolunda giderse, hello Proje derlenir ve XCode uygulamanızda açmanız. 
8. Bu hello emin olun **paket tanımlayıcı** hello projede doğru olduğundan.  
   
    ![][75]
9. Şimdi hello uygulama hello paketi dağıtılan tooyour bağlı cihaz ve telefonunuzda Unity oyununuzu görmelisiniz böylece Xcode'da çalıştırın! 

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Toodo uygulama tooreceive bildirimlerinizi herhangi bir ek yapılandırma yoktur ve onu zaten ayarlıdır.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
