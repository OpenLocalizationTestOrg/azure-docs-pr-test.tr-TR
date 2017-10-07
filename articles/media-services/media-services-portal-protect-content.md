---
title: "aaaConfiguring içerik koruma ilkeleri kullanılarak hello Azure portalı | Microsoft Docs"
description: "Bu makalede, nasıl toouse hello Azure portal tooconfigure içerik koruma ilkeleri gösterilmektedir. Merhaba makale ayrıca gösterir nasıl tooenable dinamik şifreleme varlıklarınızı için."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Hello Azure portal kullanarak içerik koruma ilkelerini yapılandırma
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Genel Bakış
Microsoft Azure Media Services (AMS), depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan, toosecure sağlar. Media Services toodeliver verir içeriğinizi Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile), PlayReady ve/veya Widevine DRM ve Apple FairPlay kullanarak ortak şifreleme (CENC) dinamik olarak şifrelenmiş. 

AMS DRM lisansları teslim etmek için bir hizmet sunar ve AES anahtarları tooauthorized istemcileri temizleyin. Hello Azure portal, toocreate bir sağlar **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.

Bu makalede nasıl tooconfigure içerik koruma ilkeleri hello Azure portal ile gösterilir. Merhaba makale ayrıca gösterir nasıl tooapply dinamik şifreleme tooyour varlıklar.


> [!NOTE]
> Hello Azure Klasik portalı toocreate koruma ilkeleri kullandıysanız, hello ilkeleri hello görünmeyebilir [Azure portal](https://portal.azure.com/). Ancak, eski tüm hello hala ilkeler yok. Bunları inceleyebilirsiniz kullanarak Azure Media Services .NET SDK veya hello hello [Azure-Media-Services-Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer/releases) Aracı (toosee hello ilkeleri hello varlık üzerinde sağ -> görüntü bilgileri (F4) -> içerik anahtarları sekmesi ->'ı tıklatın Merhaba anahtarını tıklatın). 
> 
> Yeni ilkeleri kullanarak, varlık tooencrypt istiyorsanız hello Azure portal ile yapılandırmak, Kaydet'i tıklatın ve dinamik şifreleme yeniden uygulayın. 
> 
> 

## <a name="start-configuring-content-protection"></a>İçerik koruma yapılandırma Başlat
İçerik koruma, genel tooyour AMS hesabının yapılandırma toouse hello portal toostart hello aşağıdaki:

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Seçin **ayarları** > **içerik koruma**.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>Anahtar/lisans yetkilendirme ilkesi
AMS anahtarını veya lisans isteğinde kullanıcıların kimliklerini doğrulama birden çok yöntemini destekler. Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve sırayla hello anahtar/lisans toobe delived toohello istemcisi için istemci tarafından karşılanır. Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama.

Hello Azure portal, toocreate bir sağlar **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.

### <a name="open"></a>Açık
Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone göndereceği anlamına gelir. Bu kısıtlama, test amaçları için yararlı olabilir. 

### <a name="token"></a>Belirteç
Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir. Media Services, hello basit Web belirteçleri (SWT) biçimi ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler. Media Services, güvenli belirteç hizmetleri sağlamaz. Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın. Merhaba STS bir belirteci imzalayan belirtilen hello ile yapılandırılmış toocreate olmalıdır hello belirteç kısıtlamasına yapılandırmasında belirtilen anahtarı ve çıkış talep. Bu yapılandırılmış hello belirteci için eşleşme hello anahtarı (veya lisans) Hello Media Services anahtar teslim hizmeti hello istenen hello belirteci geçerliyse, anahtarı (veya lisans) toohello istemci ve hello döndürülecek talepleri.

Merhaba belirteç kısıtlamalı ilkenin yapılandırırken hello birincil doğrulama anahtarı, veren ve İzleyici parametreleri belirtmeniz gerekir. Merhaba birincil doğrulama anahtarı içeren hello hello belirteci imzalayan, veren hello belirteci veren hello güvenli belirteç hizmeti olan anahtar. Merhaba kaynak hello belirteci erişimini yetkilendirir veya (bazen kapsam denir) hello İzleyici hello belirteci hello amacı açıklanır. Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>PlayReady haklar şablonu
Merhaba PlayReady haklar şablonu hakkında ayrıntılı bilgi için bkz: [Media Services PlayReady lisans şablonu genel bakış](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Kalıcı olmayan
Lisans kalıcı olarak yapılandırırsanız, hello player hello lisans kullanırken, yalnızca bellekte tutulur.  

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Kalıcı
Merhaba lisans kalıcı olarak yapılandırırsanız, hello istemcide kalıcı depolama alanına kaydedilir.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Widevine haklar şablonu
Merhaba Widevine haklar şablonu hakkında ayrıntılı bilgi için bkz: [Widevine lisans şablonu genel bakış](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Temel
Seçtiğinizde, **temel**, hello şablonu tüm varsayılanları değerlerle oluşturulur.

### <a name="advanced"></a>Gelişmiş
Widevine yapılandırmalarının öncelikli seçeneği hakkında ayrıntılı açıklamalar için bkz: [bu](media-services-widevine-license-template-overview.md) konu.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>FairPlay yapılandırma
tooenable FairPlay şifreleme hello FairPlay yapılandırma seçeneği tooprovide hello uygulaması sertifikası ve uygulama gizli anahtarı (İSTEYİN) gerekir. FairPlay yapılandırması ve gereksinimleri hakkında ayrıntılı bilgi için bkz: [bu](media-services-protect-hls-with-fairplay.md) makalesi.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Dinamik şifreleme tooyour varlık Uygula
tootake avantajı dinamik şifrelenmesi tooencode kaynak dosyanızı bit hızı Uyarlamalı MP4 dosyaları kümesine ihtiyacınız.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Tooencrypt istediğiniz varlığı seçin
toosee, varlıklar seçin **ayarları** > **varlıklar**.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>AES veya DRM ile şifreleme
Tuşuna sonra **şifrele** bir varlık üzerinde iki seçenek sunulur: **AES** veya **DRM**. 

#### <a name="aes"></a>AES
AES anahtar şifrelemesi tüm akış protokollerine etkinleştirilecek Temizle: kesintisiz akış, HLS ve MPEG-DASH.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Merhaba DRM sekmesini seçin, içerik koruma ilkelerinin farklı seçenek sunulur (hangi artık yapılandırmış olmanız gerekir) + akış protokolleri kümesi.

* **PlayReady ve Widevine MPEG-DASH ile** -PlayReady ve Widevine DRMs MPEG-DASH akışınızı dinamik olarak şifreler.
* **PlayReady ve Widevine MPEG-DASH ile + HLS ile FairPlay** -PlayReady ve Widevine DRMs olan MPEG-DASH akış dinamik olarak şifreler. Ayrıca, HLS akış FairPlay ile şifreler.
* **PlayReady yalnızca kesintisiz akış, HLS ve MPEG-DASH ile** -kesintisiz akış, HLS, MPEG-DASH akışları PlayReady DRM ile dinamik olarak şifreler.
* **Yalnızca MPEG-DASH ile Widevine** -, MPEG-DASH Widevine DRM ile dinamik olarak şifreler.
* **FairPlay yalnızca HLS ile** -FairPlay olan, HLS akış dinamik olarak şifreler.

tooenable FairPlay şifreleme hello içerik koruma ayarlar dikey FairPlay yapılandırma seçeneğini hello tooprovide hello uygulaması sertifikası ve uygulama gizli anahtarı (İSTEYİN) gerekir.

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Merhaba şifreleme seçimi yaptıktan sonra basın **Uygula**.

>[!NOTE] 
>Tooplay planlıyorsanız bir AES HLS Safari'de şifrelenmiş bkz [bu blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

