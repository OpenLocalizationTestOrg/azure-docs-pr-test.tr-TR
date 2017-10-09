---
title: "aaaProtect içeriğinizi Azure Media Services ile | Microsoft Docs"
description: "Bu makaleler, Media Services ile içerik koruma genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>İçerik koruma genel bakış
Microsoft Azure Media Services, toosecure, depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan sağlar. Media Services sağlar, canlı ve isteğe bağlı içerik şifrelenmiş dinamik olarak ile toodeliver Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES) ya da herhangi bir önemli DRMs hello: Microsoft PlayReady, Google Widevine ve Apple FairPlay. Tooauthorized istemcileri (PlayReady, Widevine ve FairPlay) DRM lisansları ve Media Services de AES anahtarları teslim etmek için bir hizmet sağlar. 

Görüntü aşağıdaki hello AMS destekleyen hello içerik koruma iş akışlarını gösterir. 

![PlayReady ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

Bu konuda açıklanmaktadır [kavramları ve terminolojiyi](media-services-content-protection-overview.md) AMS ile ilgili toounderstanding içerik koruma. Merhaba konu aynı zamanda içerir [bağlantılar](media-services-content-protection-overview.md#common-scenarios) nasıl tooachieve içerik koruma görevleri göster tootopics. 

## <a name="dynamic-encryption"></a>Dinamik şifreleme
Microsoft Azure Media Services, içeriğinizin şifrelenmiş dinamik olarak AES temizleyin anahtar veya DRM şifreleme toodeliver sağlar: Microsoft PlayReady, Google Widevine ve Apple FairPlay.

Şu anda, akış biçimlerine aşağıdaki hello şifreleyebilirsiniz: HLS, MPEG DASH ve kesintisiz akış. Aşamalı indirme şifrelenemiyor.

Bir varlık için Media Services tooencrypt istiyorsanız, varlıkla tooassociate bir şifreleme anahtarı (CommonEncryption veya EnvelopeEncryption) gerekir ve ayrıca hello anahtarı için yetkilendirme ilkelerini yapılandırabilirsiniz.

Ayrıca tooconfigure hello varlığın teslim ilkesini gerekir. Toostream depolama şifrelenmiş varlık istiyorsanız, istediğiniz emin toospecify toodeliver olun, varlık teslim ilkesini yapılandırarak.

Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically şifreleme, AES temizleyin anahtar kullanarak içerik veya DRM şifreleme. toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin. tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.


## <a name="storage-encryption"></a>Depolama şifrelemesi
AES 256 bit şifreleme kullanarak yerel olarak Temizle içeriğinizi depolama şifreleme tooencrypt kullanın ve tooAzure nerede depolandığı depolama şifrelenen karşıya yükleyin. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur.

Sipariş toodeliver depolama şifrelenmiş varlık'da, Media Services toodeliver içeriğinizi nasıl istediğiniz bilmesi için hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini (örneğin, AES, ortak şifreleme veya şifreleme) belirtildi.

## <a name="common-encryption-cenc"></a>Ortak şifreleme (CENC)
Ortak şifreleme içeriğinizi PlayReady ile şifrelerken kullanılan veya / ve Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Cbcs-aapl şifreleme kullanma
Cbcs-aapl içeriğinizi FairPlay ile şifrelerken kullanılır.

## <a name="envelope-encryption"></a>Zarf şifreleme
AES-128 şifresiz anahtarla içeriğinizi tooprotect istiyorsanız bu seçeneği kullanın. Daha güvenli bir seçenek istiyorsanız, bu konuda listelenen hello DRMs birini seçin. 

## <a name="licenses-and-keys-delivery-service"></a>Lisansları ve anahtarları teslimat hizmeti
AES anahtarları tooauthorized istemcileri temizleyin ve Media Services (PlayReady, Widevine, FairPlay) DRM lisansları teslim etmek için bir hizmet sağlar. Kullanabileceğiniz [Azure portal hello](media-services-portal-protect-content.md), REST API veya lisansları ve anahtarları için .NET tooconfigure yetkilendirme ve kimlik doğrulama ilkeleri için Media Services SDK.

## <a name="token-restriction"></a>Belirteç kısıtlama
Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama. Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services, hello basit Web belirteçleri (SWT) biçimi ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler. Media Services, güvenli belirteç hizmetleri sağlamaz. Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın. Merhaba STS bir belirteci imzalayan belirtilen hello ile yapılandırılmış toocreate olmalıdır hello belirteç kısıtlamasına yapılandırmasında belirtilen anahtarı ve çıkış talep. Bu yapılandırılmış hello belirteci için eşleşme hello anahtarı (veya lisans) Hello Media Services anahtar teslim hizmeti hello istenen hello belirteci geçerliyse, anahtarı (veya lisans) toohello istemci ve hello döndürülecek talepleri.

Merhaba belirteç kısıtlamalı ilkenin yapılandırırken hello birincil doğrulama anahtarı, veren ve İzleyici parametreleri belirtmeniz gerekir. Merhaba birincil doğrulama anahtarı içeren hello hello belirteci imzalayan, veren hello belirteci veren hello güvenli belirteç hizmeti olan anahtar. Merhaba kaynak hello belirteci erişimini yetkilendirir veya (bazen kapsam denir) hello İzleyici hello belirteci hello amacı açıklanır. Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.

## <a name="streaming-urls"></a>Akış URL'leri
Varlığınızı birden çok DRM ile şifrelenmiş bir şifreleme etiketi akış URL'si hello kullanmalısınız: (biçimi 'm3u8-aapl' = şifreleme = 'xxx').

ilgili önemli noktalar aşağıdaki hello Uygula:

* Yalnızca sıfır veya bir şifreleme türü belirtilebilir.
* Şifreleme türü bir şifreleme uygulanan toohello varlık ise yalnızca hello URL'sinde belirtilen toobe sahip değil.
* Şifreleme türü büyük küçük harfe duyarlı değil.
* şu şifreleme türlerini hello belirtilebilir:  
  * **cenc**: ortak şifreleme (Playready veya Widevine)
  * **cbcs-aapl**: Fairplay
  * **CBC**: AES zarfı şifreleme.

## <a name="common-scenarios"></a>Genel senaryolar
Merhaba aşağıdaki konular göstermek tooprotect içerik depolama ileten nasıl media akışı dinamik olarak şifrelenmiş AMS anahtarı/lisans teslimat hizmetinin kullanın

* [AES ile koruma](media-services-protect-with-aes128.md) 
* [PlayReady ve/veya Widevine ile koruma](media-services-protect-with-drm.md)
* [HLS içerik korumalı Apple FairPlay ve/veya PlayReady ile akışı](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>İlave senaryolar
* [Nasıl toointegrate Azure PlayReady lisans hizmeti, kendi Şifreleyici ve akış sunucuyla](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [CastLabs toodeliver DRM lisansları tooAzure Media Services'i kullanma](media-services-castlabs-integration.md)

>[!NOTE]
>Bir dış DRM server(technology) ve AMS akıştan kullanmak bir senaryo şu anda desteklenmiyor.


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[PlayReady hizmet ve AES dinamik şifreleme Azure Media Services ile tanışın](http://mingfeiy.com/playready)

[Azure Media Services PlayReady lisans teslimat fiyatlandırma açıklanmıştır](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Toodebug AES için Azure Media Services akışı nasıl şifreli](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[JWT belirteci kimlik doğrulaması](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Azure Media Services OWIN MVC tabanlı uygulama Azure Active Directory ile tümleştirme ve JWT talepleri temelinde içerik anahtar teslim kısıtlamak](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Azure ACS tooissue belirteçlerini kullanmak](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
