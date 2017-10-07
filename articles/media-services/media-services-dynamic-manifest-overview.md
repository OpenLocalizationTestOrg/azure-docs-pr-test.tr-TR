---
title: aaaFilters ve dinamik bildirimleri | Microsoft Docs
description: "Bu konuda, istemci bir akış belirli bölümlerine toostream kullanabilmeniz için nasıl toocreate filtreler açıklanmaktadır. Media Services, dinamik bildirimleri tooarchive Bu seçmeli akış oluşturur."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtreler ve dinamik bildirimleri
2.11 sürümünden başlayarak, Media Services, varlıklarınızı için toodefine filtreler sağlar. Bu filtreler müşterilerinizin gibi toochoose toodo şeyleri izin veren sunucu tarafı kurallardır: kayıttan yürütme (yerine hello tüm video oynatma), bir video yalnızca bir bölümünü veya yalnızca bir alt kümesini, müşterinizin aygıt işleyebileceğini (ses ve video yorumlama belirtin Tüm hello yorumlama yerine hello varlık ile ilişkili olan). Bu varlıklarınızı filtreleme aracılığıyla arşivlenmiş **dinamik bildirim**müşterinizin isteği toostream bir video oluşturulan s tabanlı üzerinde belirtilen filtreler.

Bu konular açıklanır ortak senaryolarda filtreleri kullanarak nasıl toocreate program aracılığıyla filtreler gösteren çok yararlı tooyour müşteriler ve bağlantıları tootopics olacaktır (şu anda, filtreleri REST API'leri ile oluşturabilmeniz için).

## <a name="overview"></a>Genel Bakış
Amacınız, içerik toocustomers (akış Canlı olayları veya isteğe bağlı video) teslim edilirken toodeliver farklı ağ koşulları altında yüksek kaliteli bir video toovarious aygıtları ' dir. Bu hedef hello aşağıdaki tooachieve:

* Akış toomulti bit hızı kodlayın ([bit hızı Uyarlamalı](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) (Bu ilgilenebilmek kalitesini ve ağ koşullarını) video akışına ve 
* Media Services'i kullanma [dinamik paketleme](media-services-dynamic-packaging-overview.md) toodynamically yeniden paketlemenize akışınızı farklı protokollere (Bu ilgilenebilmek farklı cihazlarda akış). Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello teslimini destekler: HTTP canlı akışı (HLS), kesintisiz akış ve MPEG DASH. 

### <a name="manifest-files"></a>Bildirim dosyası
Bir varlığı, bit hızı Uyarlamalı akış, kodlarken bir **bildirim** (çalma listesi) dosyası oluşturulur (Merhaba dosyasıdır metin veya XML tabanlı). Merhaba **bildirim** dosyası, meta verileri gibi akış içerir: izleme türü (ses, video veya metin), izleme adı, başlangıç ve bitiş zamanı, bit hızı (nitelikleri), izleme diller, sunu penceresini (kayan pencere sabit süresi), video codec (FourCC). Ayrıca, hello player tooretrieve hello sonraki parça'nin hello sonraki oynanabilir video parçaları kullanılabilir ve konumlarını hakkında bilgi sağlayarak bildirir. Parçaları (veya kesimler) hello gerçek "" bir video içeriği öbekleridir.

Burada, bildirim dosyası örneği verilmiştir: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Dinamik bildirimleri
Vardır [senaryoları](media-services-dynamic-manifest-overview.md#scenarios) istemciniz hello varsayılan varlığın bildirim dosyasında açıklanan'den daha fazla esneklik gerektiği zaman. Örneğin:

* Aygıt özel: yalnızca belirtilen yorumlama ve/veya hello belirtilen teslim kullanılan tooplayback olan hello aygıt tarafından desteklenen dil parçaları hello içerik ("yorumlama filtreleme"). 
* Merhaba bildirim tooshow ("alt küçük filtreleme") canlı bir olay alt küçük azaltın.
* ("Kırpma bir video") bir video kırpma hello başlangıcı.
* Sipariş tooprovide hello DVR penceresinde hello player ("ayarlama sunu pencere") sınırlı bir süre içinde sunu penceresi (DVR) ayarlayın.

tooachieve bu esneklik, Media Services teklifleri **dinamik bildirimleri** dayalı üzerinde önceden tanımlanmış [filtreleri](media-services-dynamic-manifest-overview.md#filters).  İstemcilerinizi hello filtreleri tanımladıktan sonra bunları toostream belirli yorumlama veya alt klipleri videonuzun kullanabilirsiniz. Bunlar, akış URL'si hello filtreleri belirtmeniz gerekir. Filtre uygulanmış tooadaptive bit hızı tarafından desteklenen protokolleri akış olabilir [dinamik paketleme](media-services-dynamic-packaging-overview.md): HLS, MPEG DASH ve kesintisiz akış. Örneğin:

MPEG DASH URL filtreli

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

Kesintisiz akış URL'si Filtresi ile

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Hakkında daha fazla bilgi için toodeliver içeriği ve akış URL'lerini, yapı bkz [içerik genel bakış sunan](media-services-deliver-content-overview.md).

> [!NOTE]
> Dinamik bildirimleri değil hello varlık değiştirmek ve bu varlık için varsayılan bildirimi hello unutmayın. İstemci bir akış ile veya olmadan filtreleri toorequest seçebilirsiniz. 
> 
> 

### <a id="filters"></a>Filtreleri
Varlık filtreleri iki tür vardır: 

* Genel filtrelerin (hello Azure Media Services hesabı uygulanan tooany varlığı olması, hello hesap ömürlü) ve 
* Yerel filtreleri (yalnızca uygulanan tooan varlık ile hangi hello filtresi oluşturma sırasında ilişkilendirilmiş olması, yapabilirsiniz hello varlık ömrü vardır). 

Genel ve yerel filtre türleri olan tam olarak hello aynı özellikleri. Merhaba hello ikisi arasındaki temel fark, bir dosya türünü hangi senaryoları için daha uygun olduğunu ' dir. Genel filtrelerin yerel filtreleri kullanılan tootrim belirli bir varlık nerede olabilir (yorumlama filtreleme) cihaz profillerinin genellikle uygundur.

## <a id="scenarios"></a>Yaygın senaryolar
Amacınız, içerik toocustomers (akış Canlı olayları veya isteğe bağlı video) teslim toodeliver yüksek kaliteli video olduğunda toovarious aygıtlar'ın altında farklı koşullar ağ önce belirtildiği gibi. Ayrıca, sizin kaybolabileceğini varlıklarınızı filtreleme ve birini kullanma ile ilgili diğer gereksinimlerin **dinamik bildirim**s. Aşağıdaki bölümlerde hello farklı filtreleme senaryolar kısa bir genel bakış sağlar.

* Yalnızca bir alt kümesini belirli cihazlar (yerine hello varlıkla ilişkilendirilen tüm hello yorumlama) işleyebilir ses ve video yorumlama belirtin. 
* Yalnızca bir bölümünü (Merhaba tüm video oynatma) yerine bir video oynatma.
* DVR Sunu penceresini ayarlayın.

## <a name="rendition-filtering"></a>Yorumlama filtreleme
Varlık toomultiple kodlama profillerinizi (H.264 temel H.264 yüksek, AACL, AACH, Dolby dijital Plus) ve çoklu kalite bit tooencode tercih edebilirsiniz. Ancak, tüm istemci cihazları tüm varlığınızın profilleri ve bit destekleyecektir. Örneğin, eski Android aygıtları yalnızca destekler H.264 temel + AACL. Merhaba avantajları elde edilemiyor daha yüksek bit tooa aygıt gönderme, bant genişliği ve cihaz hesaplama boşa harcar. Böyle bir aygıt çözmelisiniz tüm bilgiler, yalnızca tooscale, aşağı görüntülenmek üzere hello.

Dinamik bildirim aygıtı profilleri oluşturabilirsiniz gibi mobile, konsol, HD/SD, vb. ve hello izler ve istediğiniz nitelikleri dahil toobe her profilinin bir parçası.

![Yorumlama filtreleme örneği][renditions2]

Aşağıdaki örneğine hello kullanılan tooencode yedi ISO MP4s video yorumlama (Başlangıç 180 p too1080p) mezzanine varlığa bir kodlayıcı oluştu. Merhaba kodlanmış varlık dinamik olarak akış protokolleri aşağıdaki hello hiçbirine paketlenmesi: HLS, kesintisiz ve MPEG DASH.  Merhaba diyagramı Hello üstünde HLS bildirim hello varlık için hiçbir filtrelerle hello gösterilir (tüm yedi yorumlama içerir).  Merhaba alt sol HLS "ott" adlı bir filtre uygulandı toowhich bildirim hello gösterilir. Merhaba "ott" filtresini tooremove hangi hello yanıt olarak çıkarılmış hello alt iki kalite düzeyi ile sonuçlandı 1 MB/sn, altındaki tüm bit belirtir.  Merhaba alt sağ hello HLS "mobil" adlı bir filtre uygulandı bildirim toowhich gösterilir. Merhaba "mobil" filtresini hello çözümleme atılmış hello iki 1080 p yorumlama ile sonuçlandı 720 p, daha büyük olduğu tooremove yorumlama belirtir.

![Yorumlama filtreleme][renditions1]

## <a name="removing-language-tracks"></a>Kaldırma dil parçaları
Varlıklarınızı İngilizce, İspanyolca, Fransızca, vb. gibi birden çok ses dilleri içerebilir. Genellikle, ses izleme seçimi hello Player SDK yöneticileri varsayılan ve kullanıcı seçimine göre kullanılabilir ses izler. Bu tür Player SDK'ları toodevelop yapmak zor, cihaza özgü player-çerçeveler arasında farklı uygulamaları gerektirir. Ayrıca, bazı platformlarda Player API'leri sınırlıdır ve burada kullanıcıları seçin veya hello varsayılan ses izleme değiştirmek Ses Seçimi özelliğini içermez. Varlık filtrelerle yalnızca gerekli ses dilleri dahil filtreleri oluşturarak hello davranışını kontrol edebilirsiniz.

![Dil parçaları filtreleme][language_filter]

## <a name="trimming-start-of-an-asset"></a>Bir varlık Kırpma Başlangıcı
Çoğu canlı akış olayları, işleçler hello gerçek olayın önce bazı testleri çalıştırın. Örneğin, şöyle bir Kurşun hello olay hello başlangıcı önce içerebilir: "Programın kısa bir süre içinde başlayacak". Hello program arşivleme, hello test slate veri da arşivlenmiş ve hello sunusunda dahil edilir. Ancak, bu bilgileri toohello istemcileri gösterilmeyecek. Dinamik bildirim başlangıç zaman filtresi oluşturmak ve istenmeyen hello veri hello bildirimden kaldırın.

![Kırpma Başlat][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Canlı arşivinden alt klipleri (görünümler) oluşturma
Birçok Canlı olayları uzun süredir çalışıp ve canlı arşiv birden çok olay içerebilir. Merhaba canlı olay uçları yayıncıları toobreak hello ayarlamak isteyebilirsiniz sonra mantıksal program başlangıç arşiv canlı ve dizileri durdurun. Ardından, sanal bu programların ayrı olarak hello Canlı arşiv işleme ve (Alacak hello varolan önbelleğe alınan parçaları yararı hello CDN'ler değil) ayrı varlıklar oluşturmadığından post olmadan yayımlayın. Merhaba üç aylık dönem futbol veya Basketbol oyun, hello innings Beyzbol içinde ya da bir öğleden sonra Olimpiyatlar programının olayları tek tek sanal programlara (alt klipleri) örnekleridir.

Dinamik bildirim başlangıç/bitiş zamanına kullanarak filtreler oluşturun ve canlı Arşiviniz hello üst sanal görünümleri oluşturun. 

![Filtre subclip][subclip_filter]

Filtrelenmiş varlık:

![Kayak][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Sunu penceresini (DVR) ayarlama
Şu anda Azure Media Services hello süresi yapılandırılabileceği 5 dakika arasında - 25 saat döngüsel arşiv sunar. Bildirim filtreleme kullanılan toocreate çalışırken DVR penceresinde hello üst medya silme olmadan hello arşiv üzerinde olabilir. Edge canlı ve Merhaba aynı anda tutmak daha büyük bir arşivleme penceresi ile Merhaba taşır sınırlı bir DVR penceresi yayıncıları tooprovide istediğiniz yere birçok senaryo vardır. Yayıncı hello DVR penceresi toohighlight klipleri dışında toouse hello veriler isteyebilir veya he\she farklı aygıtlar için tooprovide farklı DVR windows isteyebilirsiniz. Örneğin, çoğu hello mobil aygıtların (Masaüstü istemcileri için 2 dakika DVR penceresi mobil cihazlar için ve 1 saat olabilir) büyük DVR windows işlemek yok.

![DVR penceresi][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>LiveBackoff (dinamik konum) ayarlama
Bildirim filtreleme kullanılan tooremove canlı bir programın hello Canlı kenarından birkaç saniye olabilir. Bu toowatch hello sunu hello Önizleme yayınındaki noktası ve hello görüntüleyiciler (genellikle yedeklenen-30 saniye kapalı) hello akış almadan önce ekleme noktaları Tanıtımı oluşturmak yayıncıları sağlar. Yayıncıları sonra bu reklam tootheir istemci çerçeveleri bunları zamanında hello tanıtım fırsat önce tooreceived ve işlem hello bilgileri gönderebilir.

Ayrıca toohello tanıtım destek, LiveBackoff istemcileri kayma ve hello Canlı kenar isabet bunlar hala parçaları 404 veya 412 HTTP hataları alma yerine sunucudan böylece alabilir istemci Canlı indirme konumu ayarlamak için kullanılabilir.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Tek bir filtre içinde birden çok kural birleştirme
Tek bir filtre birden çok filtre kurallarında birleştirebilirsiniz. Örnek olarak dinamik bir arşiv aralığı kural tooremove sayfadan tanımlayabilir ve ayrıca kullanılabilir bit filtre. Birden çok filtre kuralları hello son sonucu hello (yalnızca kesişim) bu kuralların bileşimdir.

![birden çok kural][multiple-rules]

## <a name="create-filters-programmatically"></a>Filtreler program aracılığıyla oluşturma
konu aşağıdaki hello ilgili toofilters olan Media Services varlıklar açıklanır. Hello konu aynı zamanda tooprogrammatically filtreleri nasıl oluşturacağınızı gösterir.  

[REST API'leri ile filtreleri oluşturma](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Birden çok filtre (filtresi oluşturma) birleştirme
Ayrıca, tek bir URL içinde birden çok filtre birleştirebilirsiniz. 

Merhaba aşağıdaki senaryo toocombine filtreleri neden isteyebileceğinizi gösterir:

1. Android veya (içindeki order toolimit video nitelikleri) iPAD gibi mobil cihazlar için video nitelikleri toofilter gerekir. tooremove Merhaba istenmeyen nitelikleri, cihaz profillerinin uygun olan genel bir filtre oluşturursunuz. Yukarıda belirtildiği gibi genel filtreler tüm varlıklarınızı hello altında kullanılabilir aynı medya Hizmetleri herhangi bir ilişkisi olmayan hesap. 
2. Ayrıca tootrim hello başlangıç istediğiniz ve bitiş saati bir malın. tooachieve Bu, yerel bir filtre oluşturmanız ve hello başlangıç/bitiş saati ayarlayın. 
3. Toocombine hem bu filtrelerin istediğiniz (birleşim olmadan, filtre kullanım zor hale getirir tooadd kalite filtreleme toohello kırpma filtresi gerekir).

toocombine filtreleri, gereksinim duyduğunuz tooset hello filtre adları toohello bildirimi/çalma listesi noktalı virgülle ayrılmış URL. Adlı bir filtre sahip varsayalım *MyMobileDevice* nitelikleri filtreler ve başka adlı sahip *MyStartTime* tooset belirli bir başlangıç saati. Bunları şöyle birleştirebilirsiniz:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Too3 filtreleri birleştirebilirsiniz. 

Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.

## <a name="know-issues-and-limitations"></a>Sorunlar ve sınırlamalar
* Dinamik bildirimi çalışır GOP bu nedenle kırpma sınırları (anahtar çerçeveler) sahip GOP doğruluğu. 
* Yerel ve genel filtrelerin aynı filtre adı kullanabilirsiniz. Bu yerel filtre Not daha yüksek önceliğe sahiptir ve genel filtreleri geçersiz kılar.
* Bir filtre güncelleştirirseniz, Yukarı Akış uç noktası toorefresh hello kuralları too2 dakika sürebilir. Merhaba içerik bazı filtreleri kullanarak sunulduğu (ve proxy'ler ve CDN önbellekleri önbelleğe varsa), bu filtreler güncelleştirme player hatalarına neden olabilir. Bu tooclear hello önbellek hello filtre güncelleştirdikten sonra önerilir. Bu seçenek yoksa, başka bir filtre kullanmayı düşünün.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[İçerik tooCustomers genel bakış teslim etme](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
