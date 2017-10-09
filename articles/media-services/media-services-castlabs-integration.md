---
title: "aaaUsing castLabs toodeliver Widevine lisansları tooAzure Media Services | Microsoft Docs"
description: "Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar. Medya Hizmetleri PlayReady lisans sunucusundan Hello PlayReady lisans gelir ve castLabs lisans sunucusu tarafından Widevine lisans teslim edilir."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>CastLabs toodeliver Widevine lisansları tooAzure Media Services'i kullanma
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar. Merhaba PlayReady lisans Media Services PlayReady lisans sunucusundan gelen ve Widevine lisans teslim tarafından **castLabs** lisans sunucusu.

korunan içeriği akış tooplayback (PlayReady ve/veya Widevine) CENC tarafından kullandığınız [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Bkz: [AMP belge](http://amp.azure.net/libs/amp/latest/docs/) Ayrıntılar için.

bir üst düzey Azure Media Services ve castLabs tümleştirme mimarisi diyagramı aşağıdaki hello gösterir.

![Tümleştirme](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Tipik sistem ayarlama
* Medya içeriği AMS içinde depolanır.
* İçerik anahtarı anahtar kimliklerini castLabs ve AMS içinde depolanır.
* castLabs ve AMS belirteci kimlik doğrulaması yerleşik olarak sahiptir. Aşağıdaki bölümlerde hello kimlik doğrulama belirteçleri tartışın. 
* Bir istemci toostream hello video istediğinde hello içerik ile dinamik olarak şifrelenir **ortak şifreleme** (CENC) ve akış ve tire AMS tooSmooth tarafından dinamik olarak paketlenir. Biz, PlayReady M2TS başlangıç akışı şifreleme HLS Akış Protokolü için de sunar.
* PlayReady lisans AMS lisans sunucusundan alınır ve Widevine lisans castLabs lisans sunucusundan alınır. 
* Media Player hello istemci platformu özelliği temelinde hangi lisans toofetch otomatik olarak karar verir. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Bir lisans almak için kimlik doğrulama belirteci oluşturma
Hem castLabs hem de AMS (JSON Web belirteci) JWT belirteci biçimi kullanılan tooauthorize lisans destekler. 

### <a name="jwt-token-in-ams"></a>AMS JWT belirteci
Aşağıdaki tablonun hello AMS JWT belirteci açıklar. 

| Veren | Güvenli belirteç hizmeti (STS) hello veren dizeden seçildi |
| --- | --- |
| Hedef kitle |STS hello İzleyici dizeden kullanılan |
| Talepleri |Talepler kümesi |
| NotBefore |Merhaba belirtecin geçerliliğini Başlat |
| Süre sonu |Son hello belirtecin geçerliliğini |
| SigningCredentials |Lisans sunucusu ve STS, castLabs olan PlayReady lisans sunucusu arasında paylaşılan hello anahtar simetrik ya da asimetrik anahtar olabilir. |

### <a name="jwt-token-in-castlabs"></a>CastLabs JWT belirteci
Aşağıdaki tablonun hello castLabs JWT belirteci açıklar. 

| Ad | Açıklama |
| --- | --- |
| optData |Sizinle ilgili bilgileri içeren bir JSON dizesi. |
| CRT |Bir hello varlık hakkında bilgi içeren JSON dizesi, lisans bilgileri ve kayıttan yürütme hakları. |
| IAT |Geçerli datetime dönem Hello. |
| jti |(Her belirteci yalnızca bir kez hello castLabs sisteminde kullanılabilir) bu belirteç hakkında benzersiz bir tanımlayıcı. |

## <a name="sample-solution-set-up"></a>Örnek çözümü ayarlayın
Merhaba [örnek çözümü](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) iki projeden oluşan:

* PlayReady ve Widevine DRM kısıtlamaları kullanılan tooset zaten alınan bir varlık üzerinde olabilir bir konsol uygulaması.
* Bir çok Basitleştirilmiş sürümü bir STS olarak görülebilir belirteçleri dışarı aktarır bir Web uygulamasıdır.

toouse hello konsol uygulaması:

1. Merhaba app.config toosetup AMS kimlik bilgileri, castLabs kimlik bilgileri, STS yapılandırma ve paylaşılan anahtar değiştirin.
2. Bir varlık AMS yükleyin.
3. Merhaba gelen Get hello UUID varlık karşıya ve hello Program.cs dosyasındaki satır 32 değiştirin:
   
      var objIAsset _bağlamı =. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf"). FirstOrDefault();
4. Bir AssetID hello castLabs sisteminde (Merhaba Program.cs dosyasındaki satır 44) hello varlık adlandırmak için kullanın.
   
   İçin AssetID ayarlamalısınız **castLabs**; toobe benzersiz bir alfasayısal dize gerekiyor.
5. Merhaba programını çalıştırın.

toouse hello Web uygulaması (STS):

1. Değişiklik hello web.config toosetup castlabs satıcı kimliği, hello STS yapılandırma ve hello paylaşılan anahtar.
2. Web siteleri tooAzure dağıtın.
3. Toohello Web sitesine gidin.

## <a name="playing-back-a-video"></a>Bir video kayıttan yürütme
tooplayback video şifreli ortak şifreleme ile (PlayReady ve/veya Widevine), hello kullanabilirsiniz [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Merhaba konsol uygulaması çalıştırırken hello içerik anahtarı kimliği ve hello bildirim URL echoed.

1. Yeni bir sekme açın ve, STS başlatın: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Çok Git[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Akış URL'si hello yapıştırın.
4. Merhaba tıklatın **Gelişmiş Seçenekler** onay kutusu.
5. Merhaba, **koruma** açılan listesinde, select PlayReady ve/veya Widevine.
6. Merhaba belirteci metin kutusuna, STS dan aldığınız hello belirteci yapıştırın. 
   
   Merhaba castLab lisans sunucusu hello gerek yoktur "taşıyıcı =" hello belirteci önünde öneki. Bu nedenle, hello belirteci göndermeden önce lütfen kaldırın.
7. Merhaba player güncelleştirin.
8. Merhaba video oynatma.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

