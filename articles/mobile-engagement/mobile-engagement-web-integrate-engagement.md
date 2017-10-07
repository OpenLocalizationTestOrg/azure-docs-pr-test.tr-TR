---
title: "aaaAzure Mobile Engagement Web SDK tümleştirmesi | Microsoft Docs"
description: "en son güncelleştirmeler ve yordamlar hello Azure Mobile Engagement Web SDK'sı için hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Bir web uygulamasına Azure Mobile Engagement tümleştirme
> [!div class="op_single_selector"]
> * [Windows Evrensel](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Bu makalede Hello yordamlarda hello en basit yolu tooactivate hello analizi ve Azure Mobile Engagement işlevlerde web uygulamanızda izleme açıklanmıştır.

Gerekli toocompute hello adımları tooactivate hello günlük raporlar kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve technicals ilgili tüm İstatistikler izleyin. Olaylar, hatalar ve işleri gibi uygulama bağımlı istatistikler için günlüğü raporları el ile hello Azure Mobile Engagement API'sini kullanarak etkinleştirmeniz gerekir. Daha fazla bilgi için bilgi [nasıl toouse hello Mobile Engagement bir web uygulamasında API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Giriş
[Hello Azure Mobile Engagement Web SDK Yükle](http://aka.ms/P7b453).
Mobil katılım Web SDK'sı tek bir JavaScript dosyası sevk hello, sahip olduğunuz azure-engagement.js, site veya web uygulamanızın her bir sayfasında tooinclude.

> [!IMPORTANT]
> Bu komut dosyasını çalıştırmadan önce komut dosyası çalıştırma veya kod parçacığında, tooconfigure Mobile Engagement uygulamanız için yazdığınız kodu.
> 
> 

## <a name="browser-compatibility"></a>Tarayıcı uyumluluğu
Merhaba Mobile Engagement Web SDK kodlama ve kod çözme, ayrıca (Merhaba W3C CORS belirtimi olan) toocross etki alanı AJAX istekleri yerel JSON kullanır. Tarayıcılar aşağıdaki hello ile uyumludur:

* Microsoft Edge 12 +
* Internet Explorer 10 +
* Firefox 3.5 +
* Chrome 4 +
* Safari 6 +
* Opera 12 +

## <a name="configure-mobile-engagement"></a>Mobil katılım yapılandırın
Bir genel oluşturan bir komut dosyası yazma `azureEngagement` aşağıdaki örneğine hello olduğu gibi JavaScript nesne. Sitenizi katları sayfaları olabileceğinden, bu örnek, bu komut dosyası her sayfada dahil olduğunu varsayar. Bu örnekte, hello JavaScript nesne adlı `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Merhaba `connectionString` değeri, uygulamanızın görüntülenen için Azure portal hello.

> [!NOTE]
> `appVersionName`ve `appVersionCode` isteğe bağlıdır. Ancak, böylece analytics sürüm bilgileri işleyebilmesi için bunları yapılandırmanızı öneririz.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Mobile Engagement betikleri sayfalarınızda içerir
Mobile Engagement betikleri tooyour sayfaları yolları aşağıdaki hello ekleyin:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Veya bu:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Diğer ad
Merhaba Mobile Engagement Web SDK komut yüklendikten sonra hello oluşturduğu **katılım** diğer tooaccess hello SDK API'leri. Bu diğer ad toodefine hello SDK yapılandırma kullanamazsınız. Bu diğer adı, bu belgede bir başvuru olarak kullanılır.

Merhaba varsayılan diğer sayfanızdan başka bir genel değişkeni ile çakışırsa, hello Mobile Engagement Web SDK yükleme önce onu hello yapılandırmasında şu şekilde tanımlayabilirsiniz olduğunu unutmayın:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Temel raporlama
Temel Mobile Engagement ' raporlama, kullanıcılar, oturumlar, etkinlikler ile çökmeler ilgili istatistikler gibi oturum düzeyi istatistikleri ele alınmaktadır.

### <a name="session-tracking"></a>Oturum izleme
Mobile Engagement oturum etkinlikler dizisini bölünür, her bir ad tarafından tanımlanır.

Klasik Web sitesinde, sitenizin her sayfada farklı bir etkinlik bildirmek öneririz. Geçerli sayfada hiçbir zaman hangi hello değiştirir bir Web sitesi veya web uygulaması için daha küçük bir ölçek tootrack hello etkinliklerini gibi hello sayfasında isteyebilirsiniz.

Ya da şekilde toostart ya da değişiklik hello geçerli kullanıcı etkinliği, çağrı hello `engagement.agent.startActivity` işlevi. Örneğin:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Merhaba Mobile Engagement sunucu otomatik olarak üç hello uygulama sayfası kapatıldıktan sonra dakika içinde açık bir oturumu sona erer.

Alternatif olarak, bir oturumu el ile çağırarak sonlandırabilir `engagement.agent.endActivity`. Bu ayarlar hello geçerli kullanıcı etkinliği too'Idle.'  Merhaba oturumunu 10 saniye sonra sürece yeni bir çok çağrı`engagement.agent.startActivity` hello oturum sürdürür.

Merhaba 10 saniye arasında bir gecikme hello genel katılım nesnesinde aşağıdaki gibi yapılandırabilirsiniz:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Kullanamazsınız `engagement.agent.endActivity` hello içinde `onunload` geri çağırma çünkü bu aşamada AJAX çağrıları yapamazsınız.
> 
> 

## <a name="advanced-reporting"></a>Gelişmiş raporlama
İsteğe bağlı olarak, tooreport uygulamaya özgü olaylar, hatalar ve işleri istiyorsanız, toouse hello Mobile Engagement API gerekir. Merhaba Mobile Engagement API hello erişim `engagement.agent` nesnesi.

Tüm Gelişmiş hello Mobile Engagement API, Mobile Engagement'ın özellikleri hello erişebilirsiniz. Merhaba API hello makalesinde ayrıntılı [nasıl toouse hello Mobile Engagement bir web uygulamasında API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>AJAX çağrıları için kullanılan hello URL'leri özelleştirme
Mobile Engagement Web SDK kullanan bu hello URL'leri özelleştirebilirsiniz. Örneğin, hello yapılandırma kılabilirsiniz tooredefine hello günlük URL'si (Merhaba SDK uç noktası için günlük), şöyle:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

URL işlevlerinizi ile başlayan bir dize döndürecek varsa `/`, `//`, `http://`, veya `https://`, hello varsayılan düzeni kullanılmaz. Varsayılan olarak, hello `https://` düzeni, bu URL'ler için kullanılır. Toocustomize hello varsayılan düzeni istiyorsanız, bu gibi hello yapılandırma geçersiz kıl:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
