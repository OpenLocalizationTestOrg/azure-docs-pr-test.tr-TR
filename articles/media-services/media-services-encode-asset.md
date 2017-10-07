---
title: "aaaOverview ve Azure üzerinde karşılaştırması isteğe bağlı medya kodlayıcılar | Microsoft Docs"
description: "Bu konuda, genel bir bakış ve Azure karşılaştırma isteğe bağlı medya kodlayıcılar üzerine sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Genel bakış ve isteğe bağlı medya kodlayıcılar üzerinde Azure karşılaştırması
## <a name="encoding-overview"></a>Kodlama genel bakış
Azure Media Services hello hello bulutta medya kodlama için birden fazla seçeneği sağlar.

Media Services ile başlıyor codec bileşenleri ve dosya biçimlerini arasındaki önemli toounderstand hello fark olur.
Codec bileşenleri hello sıkıştırma/açma algoritmaları dosya biçimleri sıkıştırılmış hello video tutan kapsayıcılar ise uygulayan hello yazılımlardır.

Media Services, toore-package bu kalmadan olmadan, bit hızı Uyarlamalı MP4 veya kesintisiz akış kodlanmış (MPEG DASH, HLS, kesintisiz akış) Media Services tarafından desteklenen akış biçimlerinde içeriği toodeliver sağlayan dinamik paketleme sağlar. Akış biçimlerine.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. tootake avantajlarından [dinamik paketleme](media-services-dynamic-packaging-overview.md), toodo hello aşağıdakilere sahip olmanız gerekir:
>
>Ayrıca, kaynak dosyanızı Uyarlamalı bit hızlı MP4 dosyaları veya (Merhaba kodlama adımları Bu öğreticinin ilerleyen bölümlerinde gösterilmektedir) Uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine kodlayın.

Media Services, bu makalede açıklanan isteğe bağlı kodlayıcılar üzerinde hello aşağıdakileri destekler:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium İş Akışı](media-services-encode-asset.md#media-encoder-premium-workflow)

Bu makalede, kısa bir genel bakış isteğe bağlı medya kodlayıcılar sağlar ve daha ayrıntılı bilgi vermek bağlantılar tooarticles sağlar. Merhaba konu aynı zamanda hello kodlayıcılar karşılaştırması sağlar.

>[!NOTE]
>Varsayılan olarak, aynı anda bir etkin kodlama görev her Media Services hesabına sahip olabilir. Eşzamanlı olarak, satın aldığınız her kodlama ayrılmış birim için bir tane çalışan birden çok kodlama görevleri toohave izin kodlama birimleri ayırabilirsiniz. Bilgi için bkz: [kodlama birimleri ölçeklendirme](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Media Encoder Standard
### <a name="how-toouse"></a>Nasıl toouse
[Nasıl tooencode Medya Kodlayıcısı standart ile](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Biçimleri
[Biçimleri ve codec bileşenleri](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Hazır
Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Giriş ve çıkış meta verileri
Merhaba kodlayıcılar giriş meta verileri açıklanan [burada](media-services-input-metadata-schema.md).

Merhaba kodlayıcılar çıkış meta verileri açıklanan [burada](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Küçük resimler oluşturma
Bilgi için bkz: [nasıl medya Kodlayıcı standart kullanarak toogenerate küçük resimleri](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Videoları (kırpma) kırpma
Bilgi için bkz: [nasıl medya Kodlayıcı standart kullanarak tootrim videolar](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Yer paylaşımları oluşturma
Bilgi için bkz: [nasıl toocreate yer paylaşımları medya Kodlayıcı standart kullanarak](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Ayrıca bkz.
[Merhaba Media Services blogu](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Media Encoder Premium İş Akışı
### <a name="overview"></a>Genel Bakış
[Premium Azure Media Services kodlama Tanıtımı](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Nasıl toouse
Medya Kodlayıcısı Premium iş akışı, karmaşık iş akışları kullanılarak yapılandırılır. İş akışı dosyalarını oluşturulabilir ve hello kullanarak güncelleştirilen [iş akışı Tasarımcısı](media-services-workflow-designer.md) aracı.

[Nasıl tooUse Premium Azure Media Services kodlama](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Bilinen sorunlar
Giriş videonuzun kapalı açıklamalı alt yazı içermiyorsa hello varlık hala boş bir TTML dosya içerecektir çıktı.


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>İlgili makaleler
* [Medya Kodlayıcısı standart hazır özelleştirerek gelişmiş kodlama görevleri gerçekleştirme](media-services-custom-mes-presets-with-dotnet.md)
* [Kotalar ve kısıtlamaları](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
