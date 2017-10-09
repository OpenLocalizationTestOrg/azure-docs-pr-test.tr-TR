---
title: "aaaDevelop video oynatıcı uygulamaları"
description: "Merhaba konu tooPlayer çerçevelerine bağlantılar sağlar ve eklentileri Media Services akış medyadan tüketebileceği kendi istemci uygulamalarınızı toodevelop kullanabilirsiniz."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Video oynatıcı uygulamaları geliştirme
## <a name="overview"></a>Genel Bakış
Azure Media Services sağlar hello araçları toocreate zengin gereksinim dinamik istemci oynatıcı uygulamaları dahil olmak üzere çoğu Platform: iOS cihazları, Android cihazları, Windows, Windows Phone, Xbox ve alıcı kutuları. Bu konu, bağlantılar tooSDKs ve oynatıcı çerçevelerine Azure Media Services akış medyadan tüketebileceği kendi istemci uygulamalarınızı toodevelop kullanabilirsiniz de sağlar.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) web video oynatıcı tooplay geri medya içeriği Microsoft Azure Media Services'den çok çeşitli tarayıcılar ve cihazlar üzerinde oluşturulmuştur. Azure Media Player, HTML5, medya kaynağı Uzantıları (MSE) ve şifrelenmiş medya Uzantıları (EME) tooprovide bir zenginleştirilmiş Uyarlamalı akış deneyimi gibi endüstri standartları kullanır. Bu standartlar bir aygıt veya bir tarayıcıda kullanılabilir olmadığında, Azure Media Player, Flash ve Silverlight temel teknoloji olarak kullanır. Kullanılan hello kayıttan yürütme teknolojiye bakılmaksızın, geliştiricilerin birleşik bir JavaScript arabirimi tooaccess API'leri sahip olur. Bu cihazların ve herhangi bir ek çaba olmayan tarayıcılar geniş aralık boyunca oynanan Azure Media Services toobe tarafından sunulan içeriği sağlar.

Microsoft Azure Media Services TİREYLE, kesintisiz akış, sunulan içerik toobe sağlar ve içerik biçimleri tooplay akışı HLS geri. Azure Media Player bu çeşitli biçimler dikkate alır ve otomatik olarak yürütür hello platform/tarayıcı yetenekleri göre en iyi bağlantıyı hello. Microsoft Azure Media Services da dinamik varlıklar şifrelemeyle PlayReady şifreleme sağlar veya Zarf şifreleme AES-128 bit. PlayReady şifre çözme için Azure Media Player verir ve uygun şekilde yapılandırıldığında şifrelenmiş içerik AES-128 bit. 

Daha fazla bilgi için:

* [Azure Media Player](http://aka.ms/ampinfo)
* [Azure Media Player belgeleri](http://aka.ms/ampdocs) 
* [Blog azure Media Player alma başlatıldı](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Azure Media Player gelen son hello ile toodate yukarı toostay oturum](http://aka.ms/ampsignup)
* [Yeni özellik istekleri, fikirleri, geri bildirim ekleme](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Oynatıcı uygulamaları oluşturmak için diğer araçları
SDK'ları aşağıdaki hello birini de kullanabilirsiniz:

* [Kesintisiz akış istemci SDK'sı](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Kesintisiz akış Windows mağazası uygulaması](media-services-build-smooth-streaming-apps.md)
* [Microsoft ortam platformu: Player Framework](http://playerframework.codeplex.com/) 
* [HTML5 Oynatıcısının Framework belgelerine bakın](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Microsoft için OSMF eklentisi akış kesintisiz](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Kit taşıma lisanslama Microsoft® kesintisiz akış istemcisi](http://aka.ms/sspk) 
* [XBOX Video uygulama geliştirme](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Reklam
Azure Media Services hello Windows Media platformu aracılığıyla ad ekleme için destek sağlar: oynatıcı çerçevelerine. Ad desteğiyle oynatıcı çerçevelerine Windows 8, Silverlight, Windows Phone 8 ve iOS cihazları için kullanılabilir. Her player framework nasıl gösteren örnek kod içeren tooimplement oynatıcı uygulaması. Medyanızı ekleyebilirsiniz ads üç farklı türde bulunmaktadır:

Doğrusal – hello ana videoyu duraklatmak tam çerçeve ads

Doğrusal – hello ana video yürütme gibi görüntülenen katmana reklam, genellikle bir logo veya hello player içinde yerleştirilen diğer statik görüntü

Yardımcı – hello player dışında görüntülenen reklamları

Reklam hello ana videonun Zaman Çizelgesi herhangi bir noktada yerleştirilebilir. Ne zaman tooplay hello ad ve hangi hello player söylemelisiniz ads tooplay. Bu yapılır bir dizi standart XML tabanlı dosyaları kullanılarak: Video Ad Hizmeti şablonu (VAST), Dijital Video birden çok Ad çalma listesi (VMAP), medya soyut sıralama şablonu (a) ve Dijital Video Oynatıcı Ad arabirim tanımı (VPAID). BÜYÜK dosyaları hangi ads toodisplay belirtin. VMAP dosyaları belirttiğiniz tooplay çeşitli reklam ve büyük bir XML içeriyor. A, büyük XML de içeren başka bir şekilde toosequence ads dosyalarıdır. VPAID dosyaları hello video oynatıcı ve hello ad veya ad sunucusu arasında bir arabirim tanımlar. Daha fazla bilgi için bkz: [ekleme Ads](https://msdn.microsoft.com/library/dn387398.aspx).

Kapalı açıklamalı alt yazı ve canlı akış videoları ads desteği hakkında daha fazla bilgi için bkz: [desteklenen alanında Kapalı açıklamalı alt yazı ve Ad ekleme standartları](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[DASH.js ile bir MPEG-DASH Uyarlamalı Akış Videosunu bir HTML5 Uygulamasına ekleme](media-services-embed-mpeg-dash-in-html5.md)

[GitHub dash.js deposu](https://github.com/Dash-Industry-Forum/dash.js)

