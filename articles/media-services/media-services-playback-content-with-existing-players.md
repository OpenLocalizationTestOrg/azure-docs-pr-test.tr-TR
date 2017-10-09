---
title: "içeriğinizi - Azure oynatıcıları tooplayback varolan aaaUse | Microsoft Docs"
description: "Bu konuda, içeriğinizin tooplayback kullanabileceğiniz varolan oynatıcıları listelenmiştir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Varolan oyuncularla içeriğinizi oynatma
Azure Media Services, kesintisiz akış, HTTP canlı akış ve MPEG-Dash gibi birçok popüler akış biçimlerine destekler. Bu konu, sizin akışları tootest kullanabileceğiniz tooexisting oynatıcıları işaret eder.

### <a name="hello-azure-portal-media-services-content-player"></a>Hello Azure portal medya Hizmetleri içerik Oynatıcısı
Merhaba **Azure** portalı bir içerik oynatıcı sağlar videonuzu tootest kullanabilirsiniz.

Merhaba tıklatıldığında istenen video (, olduğundan emin olun [yayımlanan](media-services-portal-publish.md)) hello tıklatıp **yürütmek** hello portal hello sonundaki düğmesi.

Bazı dikkate alınması gereken noktalar vardır:

* Merhaba **medya Hizmetleri içerik OYNATICISI** hello varsayılan akış uç noktasından oynatır. Varsayılan olmayan bir akış uç noktasından tooplay istiyorsanız, başka bir oynatıcı kullanın. Örneğin, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Kullanım [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback içeriğinizi (düz veya korumalı) herhangi bir biçimleri aşağıdaki hello:

* Kesintisiz Akış
* MPEG DASH
* HLS
* Aşamalı MP4

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>AES ile şifrelenmiş belirteci ile
[http://aestoken.azurewebsites.NET](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Silverlight oynatıcıları
#### <a name="monitoring"></a>İzleme
[http://smf.cloudapp.NET/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady belirteci ile
[http://sltoken.azurewebsites.NET](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>TİRE oynatıcıları
[http://dashplayer.azurewebsites.NET](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Diğer
tootest HLS URL'leri de kullanabilirsiniz:

* **Safari** bir iOS cihazına veya
* **3ivx HLS Player** Windows.

## <a name="developing-video-players"></a>Video oynatıcı geliştirme
Toodevelop kendi oynatıcıları nasıl görürüm hakkında bilgi için [video oynatıcı geliştirme](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
