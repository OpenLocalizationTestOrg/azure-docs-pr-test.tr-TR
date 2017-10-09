---
title: "aaaGet Web uygulamaları için Azure Mobile Engagement ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl Web uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Web Apps için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand Web uygulama kullanımınızı.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Bu öğretici hello aşağıdakileri gerektirir:

* Visual Studio 2015 veya tercih ettiğiniz başka bir düzenleyici
* [Web SDK](http://aka.ms/P7b453)

Bu Web SDK Önizleme aşamasındadır ve yalnızca Analytics hello şu anda destekler ve gönderen tarayıcı veya uygulama anında iletme bildirimleri henüz desteklemiyor. 

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Web uygulamanız için Mobile Engagement ayarlama
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğretici "Merhaba gerekli en küçük kümesi toocollect verileri olan bir temel tümleştirme" gösterilmektedir.

Visual Studio dışında da oluşturulan herhangi bir web uygulaması ile Merhaba adımları takip edebilirsiniz ancak Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir web uygulaması oluşturacağız. 

### <a name="create-a-new-web-app"></a>Yeni bir Web Uygulaması oluşturma
Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır. 

1. Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.
2. Merhaba açılır pencerede seçin **Web** -> **ASP.Net Web uygulaması**. Merhaba doldurup **adı**, **konumu** ve **çözüm adı**ve ardından **Tamam**.
3. Merhaba, **bir şablon seçin** açılan, select **boş** altında **ASP.Net 4.5 şablonları** tıklatıp **Tamam**. 

İçine biz hello Azure Mobile Engagement Web SDK tümleştirecek yeni boş bir Web uygulaması proje oluşturdunuz.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Adlı yeni bir klasör oluşturun **javascript** çözümünüzdeki ve hello Web SDK JS dosyası ekleme **azure engagement.js** içine. 
2. Adlı yeni bir dosya ekleme **main.js** bu javascript klasörde koddan hello sahip. Tooupdate hello bağlantı dizesi emin olun. Bu `azureEngagement` nesne kullanılan tooaccess Web SDK yöntemleri olacaktır. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Js dosyaları ile Visual Studio][1]

## <a name="enable-real-time-monitoring"></a>Gerçek zamanlı izlemeyi etkinleştirme
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir etkinlik toohello Mobile Engagement arka göndermeniz gerekir. Bir web uygulaması Merhaba içeriğine bir etkinlikte bir web sayfasıdır. 

1. Adlı yeni bir sayfa oluşturma **home.html** çözüm ve hello başlangıç olarak sayfasında web uygulamanız için ayarlama. 
2. Merhaba iki JavaScript'ler hello gövde etiketi içinde hello aşağıdakileri ekleyerek bu sayfada daha önce eklediğimiz içerir. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Merhaba gövde etiketi toocall EngagementAgent's güncelleştirme `startActivity` yöntemi
   
        <body onload="engagement.agent.startActivity('Home')">
4. **home.html** dosyanız bu şekilde görünür
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Analizi genişletme
Web analizi için kullanabileceğiniz SDK'sı şu anda kullanılabilir tüm hello yöntemler şunlardır:

1. Etkinlikler/Web sayfaları:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Olaylar
   
        engagement.agent.sendEvent(name, extras);
3. Hatalar
   
        engagement.agent.sendError(name, extras);
4. İşler
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

