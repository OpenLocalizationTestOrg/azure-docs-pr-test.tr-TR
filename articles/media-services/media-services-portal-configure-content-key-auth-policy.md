---
title: "İçerik anahtarı yetkilendirme ilkesini aaaConfigure kullanarak hello Azure portalı | Microsoft Docs"
description: "Bilgi nasıl tooconfigure bir içerik anahtarı için bir yetkilendirme ilkesi."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>İçerik anahtarı yetkilendirme ilkesini yapılandırma
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Genel Bakış
Microsoft Azure Media Services sağlar toodeliver MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) korumalı veya [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS Ayrıca, Widevine DRM ile şifrelenmiş, toodeliver DASH akışları sağlar. PlayReady ve Widevine, ortak şifreleme (ISO/IEC 23001-7 CENC) belirtimi hello şifrelenir.

Medya Hizmetleri de sağlar bir **anahtarı/lisans teslimat hizmeti** hangi istemcilerin AES anahtarları elde edebilirsiniz veya PlayReady/Widevine lisansları tooplay hello şifrelenmiş içerik.

Bu konu, nasıl toouse hello Azure portal tooconfigure hello içerik anahtarı yetkilendirme ilkesini gösterir. başlangıç anahtarı daha sonra kullanılabilir toodynamically şifrelemek içeriğinizi. Şu anda, akış biçimlerine aşağıdaki hello şifreleyebilirsiniz olduğunu unutmayın: HLS, MPEG DASH ve kesintisiz akış. Aşamalı indirme şifrelenemiyor.

Bir oyuncu dinamik olarak şifrelenmiş toobe ayarlanmış bir akış istediğinde, Media Services kullanır yapılandırılmış hello anahtar toodynamically AES veya DRM şifreleme kullanarak içeriğinizi şifreleyin. toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin. tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.

Birden çok içerik anahtarı toohave plan veya toospecify istiyorsanız bir **anahtarı/lisans teslimat hizmeti** Media Services .NET SDK veya REST API'leri hello Media Services anahtar teslim hizmeti dışındaki URL'yi kullanın.

[Media Services .NET SDK kullanarak içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-dotnet-configure-content-key-auth-policy.md)

[Media Services REST API kullanarak içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Bazı dikkate alınması gereken noktalar vardır:
* AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı, dinamik paketleme ve dinamik şifreleme, akış uç noktanızı akış toostart sahip toobe hello **çalıştıran** durumu. 
* Varlığınızı Uyarlamalı bit hızlı MP4s ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları içermelidir. Daha fazla bilgi için bkz: [bir varlık kodla](media-services-encode-asset.md).
* Merhaba anahtar teslim hizmeti ContentKeyAuthorizationPolicy ve ilişkili nesnelerini (ilkesi seçenekleri ve kısıtlamaları) 15 dakika için önbelleğe alır.  Bir ContentKeyAuthorizationPolicy oluşturmak ve toouse "Token" kısıtlama belirtirseniz ardından test ve hello İlkesi güncelleştirmesi çok kısıtlama "Aç", hello İlkesi anahtarları toohello "Açık" Merhaba ilkesinin sürümü önce yaklaşık 15 dakika sürer.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Nasıl yapılır: başlangıç anahtarı yetkilendirme ilkesini yapılandırın
tooconfigure hello anahtar yetkilendirme ilkesi, select hello **içerik koruma** sayfa.

Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesini olabilir **açmak**, **belirteci**, veya **IP** yetkilendirme kısıtlamaları (**IP** yapılandırılabilir REST veya .NET SDK'sı).

### <a name="open-restriction"></a>Açık kısıtlama
Merhaba **açmak** sınırlama hello sistemini anahtar isteği yapan hello anahtar tooanyone teslim anlamına gelir. Bu kısıtlama sınama amacıyla yararlı olabilir.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Belirteç kısıtlama
toochoose hello belirteci kısıtlanmış tuşuna hello İlkesi **BELİRTECİ** düğmesi.

Merhaba **belirteci** sınırlı İlkesi eşlik, tarafından verilmiş bir belirteç tarafından bir **güvenli belirteç hizmeti** (STS). Media Services hello belirteçleri destekler **basit Web belirteçleri** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) biçimi ve **JSON Web belirteci** (JWT) biçimi. Bilgi için bkz: [JWT belirteci kimlik doğrulaması](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Media Services sağlamaz **güvenli belirteç Hizmetleri**. Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın. Merhaba STS bir belirteci imzalayan belirtilen hello ile yapılandırılmış toocreate olmalıdır hello belirteç kısıtlamasına yapılandırmasında belirtilen anahtarı ve çıkış talep. Merhaba Media Services anahtar teslim hizmeti hello şifreleme anahtar toohello istemcisi hello belirteci geçerliyse ve hello hello belirtecinizdeki talepleri hello içerik anahtarı için yapılandırılan eşleşen döndürür. Daha fazla bilgi için bkz: [kullanım Azure ACS tooissue belirteçleri](http://mingfeiy.com/acs-with-key-services).

Merhaba yapılandırırken **BELİRTECİ** sınırlı İlkesi değerlerini ayarlamanız gerekir **doğrulama anahtarı**, **veren** ve **İzleyici**. Merhaba birincil doğrulama anahtarı içeren hello hello belirteci imzalayan, veren hello belirteci veren hello güvenli belirteç hizmeti olan anahtar. Merhaba kaynak hello belirteci erişimini yetkilendirir veya (bazen kapsam denir) hello İzleyici hello belirteci hello amacı açıklanır. Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.

### <a name="playready"></a>PlayReady
İçeriğinizi ile korurken **PlayReady**, bir gereksinim duyduğunuz hello şey toospecify Yetkilendirme İlkesi'nde hello PlayReady lisans şablonu tanımlar XML dizesidir. Varsayılan olarak, ilke aşağıdaki hello ayarlanır:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates> <PlayReadyLicenseTemplate> <AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>izin verilen</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates></PlayReadyLicenseResponseTemplate>

Merhaba tıklayabilirsiniz **ilke XML'yi içe** düğmesine tıklayın ve XML Şeması tanımlanan toohello uyan farklı bir XML sağlamak [burada](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

