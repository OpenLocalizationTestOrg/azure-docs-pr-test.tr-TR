---
title: "aaaAzure Media Services sık sorulan sorular | Microsoft Docs"
description: "Sık sorulan sorular (SSS)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Sık sorulan sorular

Bu makalede hello Azure Media Services (AMS) kullanıcı topluluğu tarafından gerçekleştirilen sık sorulan sorular giderir.

## <a name="general-ams-faqs"></a>Genel AMS SSS
S: nasıl dizin ölçeklendirme?

Aşağıdakilere ayrılmış hello birimleri olan hello aynı kodlama ve görevleri dizin oluşturma için. Yönergeleri izleyerek [nasıl tooScale kodlamaya ayrılan birimler](media-services-scale-media-processing-overview.md). **Not** dizin oluşturucu performans ayrılmış birim türü tarafından etkilenmez.

S: karşıya kodlanmış ve video yayımlandı. Toostream çalıştığınızda hello neden hello video ne olacağını oynamaz onu?

Y: birini en yaygın nedenlerinden olan akış uç noktası hello tooplayback içinden çalıştığınız hello sahip olmadığınız hello **çalıştıran** durumu.  

S: bir canlı akış üzerinde birleştirme yapabilirim?

Y: birleştirme Canlı akışlar üzerinde şu anda değil sunulur Azure Media Services'de toopre gerekir böylece-bilgisayarınızda oluşturun.

S: Azure CDN canlı akış ile kullanabilir miyim?

Y: Media Services, Azure CDN ile tümleştirmeyi destekler (daha fazla bilgi için bkz: [nasıl tooManage akış uç noktalarını Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)).  Canlı akış CDN ile kullanabilirsiniz. Azure Media Services, kesintisiz akış, HLS ve MPEG-DASH çıkışları sağlar. Bu biçimler verileri aktarmak için HTTP kullanmasına ve HTTP önbelleğe alma avantajlarını elde edersiniz. Bölünmüş toofragments gerçek video/ses veri akışı dinamik olarak ve bu tek tek parçaları CDN'de önbelleğe. Yalnızca veri gereksinimlerini toobe yenilendi hello bildirim verilerdir. CDN bildirim verileri düzenli aralıklarla yeniler.

S: mu Azure Media services depolanmasını görüntüleri destekliyor?

A:, yalnızca toostore JPEG veya PNG görüntüleri arıyorsanız, Azure Blob Storage de tutmanız gerekir. Video veya ses varlıklar ile ilişkili tookeep istemediğiniz sürece bunları Media Services hesap hiçbir avantajı tooputting yoktur. Veya hello video Kodlayıcısı içindeki yer paylaşımları olarak gerek toouse hello görüntüleri olabilir. Medya Kodlayıcısı standart destekler videolar en üstünde yer paylaşımı görüntüler ve hangi JPEG ve desteklenen gibi PNG listeler olan giriş biçimleri. Daha fazla bilgi için bkz: [oluşturma yer paylaşımları](media-services-advanced-encoding-with-mes.md#overlay).

S: nasıl miyim bir Media Services hesabı tooanother varlıklarını kopyalayabilirsiniz.

A: .NET kullanarak bir Media Services hesabı tooanother toocopy varlıkları kullanmanızı [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) genişletme yöntemi hello kullanılabilir [Azure Media Services .NET SDK uzantıları](https://github.com/Azure/azure-sdk-for-media-services-extensions/) deposu. Daha fazla bilgi için bkz: [bu](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) Forumu iş parçacığı.

S: ne hello karakter AMS ile çalışırken, dosya adlandırma için desteklenir?

A: URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken Media Services hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor. Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Ayrıca, yalnızca bir olabilir '.' Merhaba dosya adı uzantısı.

S: nasıl tooconnect kullanarak REST?

Y: nasıl tooconnect toohello AMS API, bkz. bilgi için [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI. 

S: nasıl ı işlem kodlama hello sırasında bir video döndürebilirsiniz.

Y: hello [Medya Kodlayıcısı standart](media-services-dotnet-encode-with-media-encoder-standard.md) 180/90/270 açıları tarafından dönüşünü destekler. "Auto", burada toodetect hello döndürme meta verilerde hello gelen MP4/MOV dosyası çalışır ve için dengelemek Hello varsayılan davranıştır. Merhaba şunlar **kaynakları** öğesi tooone tanımlanan hello json hazır [burada](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
