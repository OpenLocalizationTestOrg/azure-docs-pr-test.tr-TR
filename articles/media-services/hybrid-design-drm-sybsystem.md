---
title: "Azure Media Services'i kullanarak DRM subsystem(s) aaaHybrid tasarımını | Microsoft Docs"
description: "Bu konu Azure Media Services'i kullanarak DRM subsystem(s) karma tasarımını açıklar."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>DRM subsystem(s) karma tasarımı

Bu konu Azure Media Services'i kullanarak DRM subsystem(s) karma tasarımını açıklar.

## <a name="overview"></a>Genel Bakış

Azure Media Services üç DRM sistem aşağıdaki hello için destek sağlar:

* PlayReady
* Widevine (modüler)
* FairPlay

Merhaba DRM desteği, Azure Media Player tarayıcı player SDK'sı tüm 3 DRMs destekleme ile DRM şifreleme (dinamik şifreleme) ve lisans teslimat içerir.

DRM/CENC alt sistemi tasarım ve uygulama ayrıntılı işlenmesi için lütfen başlıklı hello belgesine bakın [çoklu DRM ve erişim denetimi ile CENC](media-services-cenc-with-multidrm-access-control.md).

Bazen üç DRM sistemi için tam destek sunuyoruz rağmen müşterilerin kendi altyapı/alt toplama tooAzure Media Services toobuild karma DRM alt sistemi çeşitli kısımlarını toouse gerekir.

Aşağıda bazı sık sorulan soruları müşteriler tarafından istenir:

* "Kendi DRM lisans sunucularını kullanabilir miyim?" (Bu durumda, müşterilerin DRM lisans sunucusu grubunda katıştırılmış iş mantığı ile yatırım yapmış kullanıcılar).
* "Yalnızca, DRM lisans teslimat Azure Media Services AMS içeriği barındırma olmadan kullanabilir miyim?"

## <a name="modularity-of-hello-ams-drm-platform"></a>Merhaba AMS DRM platform modülerlik

Kapsamlı bulut video platformu bir parçası olarak, Azure Media Services DRM göz önünde esneklik ve modülerlik ile bir tasarıma sahiptir. Azure Media Services, farklı birleşimler (Merhaba tablosunda kullanılan hello gösterimi açıklaması izleyen) hello aşağıdaki tabloda açıklanan aşağıdaki hello biriyle kullanabilirsiniz. 

|**Barındırma & Kaynak içerik**|**İçerik şifreleme**|**DRM lisansı teslimi**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|Üçüncü taraf|
|AMS|Üçüncü taraf|AMS|
|AMS|Üçüncü taraf|Üçüncü taraf|
|Üçüncü taraf|Üçüncü taraf|AMS|

### <a name="content-hosting--origin"></a>Barındırma & Kaynak içerik

* AMS: varlığı AMS içinde barındırılır ve akış AMS akış uç noktalarını (ancak mutlaka dinamik paketleme) kullanılır.
* Üçüncü taraf: video barındırılan ve AMS dışında bir üçüncü taraf akış platformunda teslim.

### <a name="content-encryption"></a>İçerik şifreleme

* AMS: gerçekleştirilen dinamik olarak/isteğe bağlı AMS dinamik şifreleme tarafından içerik şifrelemesidir.
* Üçüncü taraf: işleme öncesi iş akışını kullanarak AMS dışında içerik şifreleme gerçekleştirilir.

### <a name="drm-license-delivery"></a>DRM lisansı verme

* AMS: DRM lisans AMS lisans teslimat hizmeti tarafından teslim edilir.
* Üçüncü taraf: DRM lisans AMS dışında bir üçüncü taraf DRM lisans sunucusu tarafından teslim edilir.

## <a name="configure-based-on-your-hybrid-scenario"></a>Yapılandırma karma senaryoyu temel

### <a name="content-key"></a>İçerik anahtarı

Bir içerik anahtarı yapılandırma yoluyla, AMS dinamik şifreleme ve AMS lisans teslimat hizmeti özniteliklerini aşağıdaki hello denetleyebilirsiniz:

* dinamik DRM şifreleme için kullanılan hello içerik anahtarı.
* DRM lisans içerik toobe lisans teslim hizmetleri tarafından sunulan: hakları, içerik anahtarı ve kısıtlamaları.
* Tür **içerik anahtarı yetkilendirme ilkesini kısıtlama**: IP veya belirteç kısıtlamasına açın.
* Varsa **belirteci** türü **içerik anahtarı yetkilendirme ilkesini kısıtlama kullanılır**, hello **içerik anahtarı yetkilendirme ilkesini kısıtlama** lisans verilmeden önce karşılanması gerekir.

### <a name="asset-delivery-policy"></a>Varlık teslim ilkesini

Bir varlık teslim ilkesini yapılandırma yoluyla, AMS dinamik Paketleyici ve akış uç noktası bir AMS dinamik şifreleme tarafından kullanılan öznitelikleri aşağıdaki hello denetleyebilirsiniz:

* Protokol ve DRM şifreleme birleşimi, tire (PlayReady ve Widevine), CENC altında gibi altında PlayReady, Widevine veya PlayReady altında HLS akış kesintisiz akış.
* Merhaba varsayılan ve katıştırılmış lisans teslimat URL'leri her hello DRMs dahil.
* Olup tire MPD (LA_URLs) URL'lerinde edinme lisans veya HLS çalma listesi içeren sorgu dizesi kimliği (çocuk) anahtarının Widevine ve FairPlay, sırasıyla.

## <a name="scenarios-and-samples"></a>Senaryolar ve örnekler

Merhaba önceki bölümdeki hello açıklamaları bağlı olarak, beş karma senaryolar aşağıdaki hello kullanmak ilgili **içerik anahtarı**-**varlık teslim ilkesini** yapılandırması bileşimleri (Merhaba Merhaba son sütununda belirtilen örnekleri hello tablo izleyin):

|**Barındırma & Kaynak içerik**|**DRM şifreleme**|**DRM lisansı teslimi**|**İçerik anahtarı yapılandırın**|**Varlık teslim ilkesini yapılandırma**|**Örnek**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|Evet|Evet|Örnek 1|
|AMS|AMS|Üçüncü taraf|Evet|Evet|Örnek 2|
|AMS|Üçüncü taraf|AMS|Evet|Hayır|Örnek 3|
|AMS|Üçüncü taraf|Dışında|Hayır|Hayır|Örnek 4|
|Üçüncü taraf|Üçüncü taraf|AMS|Evet|Hayır|    

Merhaba örneklerinde PlayReady koruma tire hem de kesintisiz akış için çalışır. Kesintisiz akış URL'lerini Hello aşağıda bir video URL. tooget karşılık gelen tire URL'leri Merhaba, yalnızca Ekle "(biçim mpd zaman csf =)". Merhaba kullanabileceğinizi [azure media player test](http://aka.ms/amtest) bir tarayıcıda tootest. Tooconfigure izin verir, hangi teknik altında Protokolü toouse akış. IE11 ve Windows 10 MS Edge PlayReady EME aracılığıyla destekler. Daha fazla bilgi için bkz: [hello ayrıntılarını test aracı](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).

### <a name="sample-1"></a>Örnek 1

* Kaynak (Temel) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* PlayReady LA_URL (tire & kesintisiz): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>Örnek 2

* Kaynak (Temel) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* PlayReady LA_URL (tire & kesintisiz): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>Örnek 3

* Kaynak URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL (tire & kesintisiz): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>Örnek 4

* Kaynak URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* PlayReady LA_URL (tire & kesintisiz): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>Özet

Özet olarak, Azure Media Services DRM bileşenlerini esnektir, bunları bir karma senaryoda düzgün içerik anahtarı ve varlık teslim ilkesini yapılandırarak bu konu başlığı altında açıklandığı gibi kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Görünüm Media Services'i öğrenme yolları.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

