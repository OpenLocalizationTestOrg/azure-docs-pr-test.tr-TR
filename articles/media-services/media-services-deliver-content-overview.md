---
title: "aaaDelivering içerik toocustomers | Microsoft Docs"
description: "Bu konuda ne içeriğinizi Azure Media Services ile dağıtımına katılan genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>İçerik toocustomers teslim
Akış veya isteğe bağlı video içerik toocustomers teslim etmek, amacınız toodeliver yüksek kaliteli video toovarious aygıtlar farklı ağ koşulları altında değildir.

tooachieve bu hedef, şunları yapabilirsiniz:

* Akış tooa Çoklu bit hızlı (bit hızı Uyarlamalı) video akışına kodlayın. Bu kalitesini ve ağ koşullarını dikkatli olun.
* Microsoft Azure Media Services'i kullanma [dinamik paketleme](media-services-dynamic-packaging-overview.md) toodynamically yeniden farklı protokollere akışınızı paketi. Bu farklı cihazlarda akış ilgilenebilmek. Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello teslimini destekler: HTTP canlı akışı (HLS), kesintisiz akış ve MPEG-DASH.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

Bu makalede önemli içerik teslim kavramlara genel bakış sunulmaktadır.

bilinen sorunlar, toocheck bkz [bilinen sorunlar](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Dinamik paketleme
Merhaba dinamik paketleme ile Media Services, bit hızı Uyarlamalı MP4 veya kesintisiz akış kodlanmış içeriğinizi Media Services (MPEG-DASH, HLS, kesintisiz akış,) tarafından desteklenen akış biçimlerinde teslim toore pakete gerek kalmadan sağlar Bu akış biçimlerine. Dinamik paketleme ile içeriğinizi teslim etmek öneririz.

tootake avantajı dinamik paketleme, tooencode Ara (kaynak) dosyanızı bit hızı Uyarlamalı MP4 dosyası ya da Uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine ihtiyacınız.

Dinamik paketleme ile depolamak ve tek bir depolama biçiminde hello dosyaları için ödeme yaparsınız. Media Services, isteklerine dayalı hello uygun yanıtı derler ve.

Dinamik paketleme, standart ve premium akış uç noktaları için kullanılabilir. 

Daha fazla bilgi için bkz: [dinamik paketleme](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtreler ve dinamik bildirimleri
Media Services ile varlıklarınızı için filtreleri tanımlayabilirsiniz. Bu filtreler video belirli bir kısmını çalmak gibi şeyler veya bir alt müşterinizin aygıt (yerine hello varlıkla ilişkilendirilen tüm hello yorumlama işleyebilir ses ve video yorumlama belirtin müşterilerinizin yardımcı sunucu tarafı kurallardır ). Bu filtreleme aracılığıyla elde edilen *dinamik bildirimleri* isterken müşteri toostream temel alan bir video veya daha fazla filtreler belirtilen oluşturulur.

Daha fazla bilgi için bkz: [filtreleri ve dinamik bildirimleri](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Belirleyicileri
tooprovide kullanıcı kullanılan toostream bulunabilir veya içeriğinizi karşıdan bir URL ile ilk toopublish varlığınız bir Bulucu oluşturarak gerekir. Bir Bulucu bir varlıkta bulunan dosyalara bir giriş noktası tooaccess hello sağlar. Media Services iki tür bulucuyu destekler:

* OnDemandOrigin bulucuları. Bunlar kullanılan toostream medya (örneğin, MPEG-DASH, HLS veya kesintisiz akış) veya aşamalı olarak dosyalarını indirin.
* Paylaşılan erişim imzası (SAS) URL bulucular. Kullanılan toodownload medya dosyaları tooyour yerel bilgisayara bunlar.

Bir *erişim ilkesi* kullanılan toodefine hello izinleridir (örneğin, okuma, yazma ve liste) ve bir istemci belirli bir varlık için erişim olduğu süre. Merhaba listesi izni (AccessPermissions.List) bir OrDemandOrigin Bulucu oluşturmada kullanılmamalıdır unutmayın.

Bulucular sona erme tarihi vardır. Hello Azure portalında bir sona erme tarihi 100 yıl hello gelecekteki bulucular için ayarlar.

> [!NOTE]
> Mart 2015 öncesinde hello Azure portal toocreate bulucular kullandıysanız, bu konum belirleyicisi iki yıl sonra tooexpire ayarlandı.
> 
> 

Kullanım Bulucunun sona erme tarihi bir tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) veya [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API'leri. Bir SAS Bulucu hello sona erme tarihini güncelleştirdiğinizde hello URL'nin değiştiğini unutmayın.

Bulucular olmayan toomanage kullanıcı başına erişim denetimi tasarlanır. Dijital Hak Yönetimi (DRM) çözümleri kullanılarak hakları tooindividual kullanıcıların farklı erişim verebilirsiniz. Daha fazla bilgi için bkz: [güvenli hale getirme medya](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Bir Bulucu oluşturduğunuzda, Azure storage'da toorequired depolama ve yayma işlemleri nedeniyle 30 saniyelik gecikme olabilir.

## <a name="adaptive-streaming"></a>Akış Bağdaşık
Bit hızı Uyarlamalı teknolojileri video oynatıcı uygulamaları toodetermine ağ koşulları izin verir ve birkaç bit seçin. Ağ iletişimi düşürür olduğunda hello istemci ile alt video kalitesini kayıttan yürütme devam edebilmek için daha düşük bit hızlı seçebilirsiniz. Ağ koşulları geliştirmek gibi hello istemci geliştirilmiş video kalitesini ile tooa daha yüksek bit hızı geçiş yapabilirsiniz. Azure Media Services, bit hızı Uyarlamalı teknolojileri aşağıdaki hello destekler: HTTP canlı akışı (HLS), kesintisiz akış ve MPEG-DASH.

Akış URL'leri tooprovide kullanıcılar, önce bir OnDemandOrigin Bulucu oluşturmanız gerekir. Merhaba hello içeriği temel yolu toohello varlık hello Bulucu verir oluşturma toostream istiyor. Ancak, toobe mümkün toostream bu yolu daha fazla toomodify gereken bu içerik. bildirim dosyası akış tam bir URL toohello hello Bulucu'nın yolu birleştirme gerekir tooconstruct değeri ve hello bildirimi (filename.ism) dosya adı. Ardından append **/bildirimi** ve (gerekirse) uygun biçimde toohello Bulucu yolu.

> [!NOTE]
> Ayrıca, bir SSL bağlantısı üzerinden içeriğinizin akışını sağlayabilirsiniz. toodo Bu, HTTPS ile akış URL'leri başlatma emin olun. Şu anda AMS SSL ile özel etki alanlarını, desteklemez.  
> 


Akış uç noktası içeriğinizi teslim etmek hello 10 Eylül 2014 sonra oluşturduysanız yalnızca SSL üzerinden akışını sağlayabilirsiniz. Akış URL'leri akış uç noktaları 10 Eylül 2014 sonra oluşturulan hello dayanır, "streaming.mediaservices.windows.net." hello URL içerir "Origin.mediaservices.windows.net" (Merhaba eski biçimi) içeren akış URL'leri SSL desteklemez. URL'niz hello eski biçiminde ve SSL üzerinden toobe mümkün toostream istediğiniz varsa, yeni bir akış uç noktası oluşturun. Yeni uç nokta toostream içeriğinizi SSL üzerinden akış hello temel URL kullanın.

## <a name="streaming-url-formats"></a>Akış URL biçimleri
### <a name="mpeg-dash-format"></a>MPEG-DASH biçimi
{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=mpd-Time-CSF)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Apple HTTP canlı akışı (HLS) V4 biçimi
{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Apple HTTP canlı akışı (HLS) V3 biçimi
{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3) akış

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Apple HTTP canlı akışı (HLS) biçimi yalnızca ses filtreli
Varsayılan olarak, yalnızca ses parçaları HLS bildirim hello dahil edilir. Bu cep telefonu ağları için Apple Store sertifika için gereklidir. Bu durumda, bir istemci yeterli bant genişliği yok ya da 2 G bağlantısı üzerinden bağlanmış, kayıttan yürütme yalnızca tooaudio geçer. Bu tookeep içerik akışı arabelleğe alma olmadan yardımcı olur, ancak hiçbir video yok. Bazı senaryolarda, arabelleğe alma player yalnızca ses üzerinden tercih edilen olabilir. Tooremove hello salt ses izlemek isterseniz, ekleme **yalnızca ses = false** toohello URL.

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest(Format=m3u8-aapl-v3,Audio-Only=false)

Daha fazla bilgi için bkz: [dinamik bildirimi oluşturma desteği ve HLS çıkış ek özellikler](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Kesintisiz akış biçimi
{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest

Örnek:

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8B70-203e86b0df58/BigBuckBunny.ism/manifest

### <a id="fmp4_v20"></a>Kesintisiz akış 2.0 bildirimi (eski bildirimi)
Varsayılan olarak, kesintisiz akış bildirim biçimi hello yineleme etiketi (r-tag) içerir. Ancak, bazı oynatıcıları hello r-tag desteklemez. İstemciler bu oyuncularla hello r-tag devre dışı bırakan bir biçimini kullanabilirsiniz:

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20) akış

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Aşamalı indirme
Aşamalı indirme ile Merhaba dosyanın tamamı indirilmeden önce media çalma başlatabilirsiniz. (.İsm * ismv, ISMA, ismt veya ismc) dosyalarını aşamalı indirmek edilemiyor.

tooprogressively içerik indirmek için hello OnDemandOrigin Bulucu türünü kullanın. Merhaba aşağıdaki örnek hello Bulucu OnDemandOrigin türü üzerinde temel hello URL gösterir:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Aşamalı indirme için hello kaynak hizmetinden toostream istediğiniz tüm depolama şifrelenmiş varlıkları şifresini gerekir.

## <a name="download"></a>İndir
toodownload içerik tooa istemci Cihazınızı SAS Bulucu oluşturmanız gerekir. Merhaba SAS Bulucu verir dosyanızı bulunduğu toohello Azure depolama kapsayıcısının erişin. toobuild hello indirme URL'si, tooembed hello dosya adına hello konak ile SAS imza sahip.

Merhaba aşağıdaki örnek hello SAS Bulucu üzerinde temel hello URL gösterir:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

ilgili önemli noktalar aşağıdaki hello Uygula:

* Aşamalı indirme için hello kaynak hizmetinden toostream istediğiniz tüm depolama şifrelenmiş varlıkları şifresini gerekir.
* 12 saat içinde tamamlamadı bir yükleme başarısız olur.

## <a name="streaming-endpoints"></a>Akış uç noktaları

Bir akış uç tooa istemci oynatıcı uygulaması veya tooa içerik teslim ağı (CDN) için daha fazla doğrudan dağıtım içerik ileten bir akış hizmeti temsil eder. bir akış uç noktası hizmetinden Hello giden akış canlı akış veya isteğe bağlı video varlık Media Services hesabınızda olabilir. Akış uç noktaları, iki tür vardır **standart** ve **premium**. Daha fazla bilgi için bkz: [akış uç noktaları genel bakış](media-services-streaming-endpoints-overview.md).

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="changes-toosmooth-streaming-manifest-version"></a>Değişiklikleri tooSmooth akış bildirimi sürümü
Merhaba Medya Kodlayıcısı standart, Medya Kodlayıcısı Premium iş akışı veya hello önceki Azure medya Kodlayıcı akışı dinamik paketleme--hello kesintisiz akış kullanarak tarafından üretilen varlıklar bildirim zaman Temmuz 2016 hizmet sürümü--döndürmeden önce uygun olması tooversion 2.0. Sürüm 2.0 hello parça süreleri hello sözde Yinele ('r') etiketleri kullanmayın. Örneğin:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Hello Temmuz 2016 hizmet sürümü, oluşturulan hello kesintisiz akış bildirimi tooversion 2.2, yineleme etiketleri kullanarak parça süreleri ile uyumludur. Örneğin:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Bazı hello eski kesintisiz akış istemcilerinin hello yineleme etiketleri desteklemiyor olabilir ve tooload hello bildirimi başarısız olur. toomitigate Bu sorun, hello eski bildirim biçimi parametresini kullanabilirsiniz **(biçimi fmp4 v20 =)** veya yineleme etiketleri destekleyen, istemci toohello en son sürümüne güncelleştirin. Daha fazla bilgi için bkz: [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>İlgili konular
[Media Services bulucular depolama anahtarları çalışırken sonra güncelleştirme](media-services-roll-storage-access-keys.md)

