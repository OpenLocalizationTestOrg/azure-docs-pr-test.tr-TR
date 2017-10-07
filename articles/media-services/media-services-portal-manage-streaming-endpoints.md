---
title: "Akış uç noktaları hello Azure portal ile aaaManage | Microsoft Docs"
description: "Bu konu, nasıl Azure portal ile toomanage akış uç noktalarını hello gösterir."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Akış uç hello Azure portal ile yönetin

Bu konu, nasıl toouse hello Azure portal toomanage akış uç noktalarını gösterir. 

>[!NOTE]
>Tooreview hello emin olun [genel bakış](media-services-streaming-endpoints-overview.md) konu. 

Nasıl tooscale hello akış uç noktası hakkında daha fazla bilgi için bkz: [bu](media-services-portal-scale-streaming-endpoints.md) konu.

## <a name="start-managing-streaming-endpoints"></a>Akış uç noktalarını yönetmeye başlama 

hesabınız için akış uç noktalarını yönetme toostart hello aşağıdaki.

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Merhaba, **ayarları** dikey penceresinde, select **akış uç noktaları**.
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Akış uç noktanızı çalışır durumda olduğunda yalnızca faturalandırılır.

## <a name="adddelete-a-streaming-endpoint"></a>Bir akış uç ekleme/silme

>[!NOTE]
>Merhaba varsayılan akış uç noktası silinemiyor.

uç nokta kullanarak akış tooadd/delete Azure portal Merhaba, aşağıdaki hello:

1. tooadd bir akış uç tıklatın hello **+ uç nokta** hello sayfanın üst kısmındaki hello. 

    Toohave düşünüyorsanız, birden çok akış uç noktaları isteyebilirsiniz farklı CDN'ler veya CDN ve doğrudan erişim.

2. toodelete bir akış uç basın **silmek** düğmesi.      
3. Merhaba tıklatın **Başlat** düğmesini toostart hello akış uç noktası.
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Merhaba akış uç noktasını yapılandırma
Akış uç noktası aşağıdaki özelliklere tooconfigure hello sağlar:

* Erişim denetimi
* Önbellek denetimi
* Site erişim ilkeleri arası

Bu özellikler hakkında ayrıntılı bilgi için bkz: [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Merhaba aşağıdakileri yaparak akış uç noktasını yapılandırabilirsiniz:

1. Akış uç noktası tooconfigure istediğiniz hello seçin.
2. Tıklatın **ayarları**.

Merhaba alanları kısa bir açıklamasını izler.

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. En büyük önbellek İlkesi: varlıklar için kullanılan tooconfigure önbellek ömrünü Bu akış uç noktası aracılığıyla sunulan. Herhangi bir değer ayarlarsanız, hello varsayılan kullanılır. Merhaba varsayılan değerleri de doğrudan Azure depolama alanında tanımlanabilir. Azure CDN akış uç noktası Merhaba etkinleştirilirse, hello önbellek İlkesi değeri tooless 600 saniye daha ayarlanmadı.  
2. İzin verilen IP adreslerini: tooconnect toohello yayımlanan akış uç izin toospecify IP adresleri kullanılır. Belirtilen IP adresleri ise, herhangi bir IP adresi mümkün tooconnect olabilir. IP adresleri, tek bir IP adresi (örneğin, ' 10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi (örneğin, ' 10.0.0.1/22') kullanarak bir IP aralığı veya IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı belirtilebilir (örneğin, 10.0.0.1 ' () 255.255.255.0)').
3. Akamai imzası üstbilgi kimlik doğrulaması için yapılandırma: İmza üstbilgi kimlik doğrulama isteği Akamai sunucularından nasıl yapılandırılır toospecify kullanılır. Süre sonu UTC biçiminde değil.

## <a name="scale-your-premium-streaming-endpoint"></a>Akış uç noktası, Premium ölçeklendirme

Daha fazla bilgi için [bu](media-services-portal-scale-streaming-endpoints.md) konu başlığına bakın.

## <a id="enable_cdn"></a>Azure CDN tümleştirmeyi etkinleştir

Yeni bir hesap oluşturduğunuzda, varsayılan akış uç noktası Azure CDN tümleştirme varsayılan olarak etkindir.

Daha sonra toodisable/enable hello CDN istiyorsanız, akış uç noktanızı hello olmalıdır **durduruldu** durumu. Tüm hello arasında CDN POP saatlerini too2 hello değişiklikleri toobe etkin ve etkin hello Azure CDN tümleştirme tooget için sürebilir. Ancak, can akış uç noktası ve akış kesintileri olmadan akış uç noktası hello başlatın ve hello tümleştirme tamamlandıktan sonra CDN hello hello akış teslim edilecek. Akış uç noktanızı olacak süresi sağlama hello sırasında **başlangıç** durumu ve degredad performans gözlemlemek.

CDN tümleştirme tüm hello Azure veri merkezleri execpt Çin ve Federal Government bölgelerde etkinleştirilir.

Etkinleştirildiğinde, hello **erişim denetimi**, **özel ana bilgisayar adı** ve **Akamai imzası kimlik doğrulaması** yapılandırması devre dışı.
 
> [!IMPORTANT]
> Azure CDN ile Azure Media Services tümleştirme uygulandığını **verizon'dan Azure CDN** için standart akış uç noktaları. Akış uç noktaları premium tüm kullanılarak yapılandırılabilir **Azure CDN fiyatlandırma katmanlarına ve sağlayıcıları**. Hello Azure CDN özellikler hakkında daha fazla bilgi için bkz: [CDN'ye genel bakış](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Diğer konular

* CDN akış uç noktası için etkinleştirildiğinde, istemcileri doğrudan hello kaynaktan içerik isteğinde bulunamaz. İçeriğinizi ile veya olmadan CDN hello özelliği tootest gerekiyorsa, CDN etkin olmayan başka bir akış uç noktası oluşturabilirsiniz.
* CDN etkinleştirdikten sonra akış uç noktası ana bilgisayar adı kalır aynı hello. CDN etkinleştirildikten sonra tüm değişiklikleri tooyour media services iş akışı toomake gerekmez. Akış uç noktası ana bilgisayar adı strasbourg.streaming.mediaservices.windows.net, CDN etkinleştirdikten sonra Örneğin, hello tam aynı ana bilgisayar adı kullanılır.
* Yeni akış uç noktaları için yeni bir uç noktası oluşturarak CDN etkinleştirebilirsiniz; Varolan akış uç noktaları için toofirst Dur hello endpoint ve ardından etkinleştir/devre dışı bırak hello CDN gerekir.
* Akış uç noktası standart yalnızca kullanılarak yapılandırılabilir **standart Verizon CDN sağlayıcısı** Azure yönetim portalını kullanarak. Ancak, REST API'lerini kullanarak diğer Azure CDN sağlayıcıları etkinleştirebilirsiniz.

## <a name="configure-cdn-profile"></a>CDN profili yapılandırma

Merhaba seçerek hello CDN profili yapılandırabilirsiniz **yönetmek CDN** hello üst düğmesinden.

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

