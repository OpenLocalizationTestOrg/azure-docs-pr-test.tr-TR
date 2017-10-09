---
title: "Azure Media Services aaaMicrosoft senaryolar ve veri merkezleri arasında özelliklerin kullanılabilirliği | Microsoft Docs"
description: "Bu konu başlığı altında, Microsoft Azure Media Services senaryolarına ve özelliklerle hizmetlerin veri merkezleri arasında kullanılabilirliğine genel bir bakış sağlanır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>Senaryolar ve Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği

Microsoft Azure Media Services (AMS) toosecurely karşıya yükleme sağlar, depolama, kodlamak ve hem isteğe bağlı ve canlı akış teslimi toovarious istemcileri için (örneğin, TV, PC ve mobil aygıtlar) video ve ses içeriklerini paketini.

Birden çok veri merkezlerinde Merhaba Dünya AMS çalışır. Bu veri merkezlerinde nereye koyacağınızı seçmek esneklik vermiş toogeographic bölgelerdeki gruplandırılır toobuild uygulamalarınızı. Merhaba gözden geçirebilirsiniz [bölgeler ve konumlarını listesi](https://azure.microsoft.com/regions/). 

Bu konu başlığı altında, içeriğinizin [canlı](#live_scenarios) veya [isteğe bağlı](#vod_scenarios) teslimiyle ilgili yaygın senaryolar gösterilmektedir. Merhaba konu aynı zamanda veri merkezleri arasında ortam özellikleri ve hizmetlerin kullanılabilirliğini hakkında ayrıntılar sağlar.

## <a name="overview"></a>Genel Bakış

### <a name="prerequisites"></a>Ön koşullar

Azure Media Services'i kullanarak toostart hello şunlara sahip olmanız:

* Bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com).
* Bir Azure Media Services hesabı. Daha fazla bilgi için bkz. [Hesap Oluşturma](media-services-portal-create-account.md).
* Akış uç noktası toostream içerik istediğiniz hello sahip toobe hello **çalıştıran** durumu.

    AMS hesabınızı oluştururken bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme, akış uç noktası hello akış toostart sahip toobe hello **çalıştıran** durumu.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>AMS OData modeli hello karşı geliştirirken yaygın olarak kullanılan nesneleri

Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modeline göre geliştirirken gösterir.

Merhaba görüntü tooview boyutu tam'ı tıklatın.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Merhaba tüm model görüntüleyebilirsiniz [burada](https://media.windows.net/API/$metadata?api-version=2.15).  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>Depolama alanında içeriği koruma ve (şifrelenmemiş) teslim akan medyayı hello temizleyin

![VoD iş akışı](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.

    İçeriğinizi sırasında karşıya yükleme ve deposunda kalan while sipariş tooprotect tooapply depolama şifreleme seçeneği tooyour varlığı önerilir.
2. Bit hızı Uyarlamalı MP4 dosyaları tooa kodlayın.

    İçeriğinizi beklerken sipariş tooprotect varlığı tooapply depolama şifreleme seçeneği toohello çıkış önerilir.
3. Varlık teslim ilkesini (dinamik paketleme tarafından kullanılır) yapılandırın.

    Varlığınıza depolama şifrelemesi uygulanmışsa varlık teslim ilkesini yapılandırmanız **gerekir**.
4. Bir OnDemand Bulucu oluşturarak Hello varlığı yayımlayın.
5. Yayımlanan içeriği akışla aktarın.

Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>Depolama alanında içeriği koruma, dinamik olarak şifrelenmiş akan medya teslim etme

![PlayReady ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin. Depolama şifrelemesi seçeneğini toohello varlık uygulayın.
2. Bit hızı Uyarlamalı MP4 dosyaları tooa kodlayın. Depolama şifrelemesi seçeneğini toohello çıkış varlığına uygulayın.
3. Kayıttan yürütme sırasında dinamik olarak şifrelenmiş toobe istediğiniz hello varlık için şifreleme içerik anahtarı oluşturun.
4. İçerik anahtarı yetkilendirme ilkesini yapılandırın.
5. Varlık teslim ilkesini (dinamik paketleme ve dinamik şifreleme tarafından kullanılır) yapılandırın.
6. Bir OnDemand Bulucu oluşturarak Hello varlığı yayımlayın.
7. Yayımlanan içeriği akışla aktarın.

Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>Medya analizi tooderive eyleme dönüştürülebilir Öngörüler videolarınızı gelen kullanın

Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırmak için konuşma ve görme bileşenleri koleksiyonudur. Daha fazla bilgi için bkz. [Azure Media Services Analizi’ne Genel Bakış](media-services-analytics-overview.md).

1. Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.
2. İle hello açıklanan hello medya analizi hizmetlerinden birini kullanarak videolarınızı işleyin [medya analizi genel bakış](media-services-analytics-overview.md) bölümü.
3. Medya Analizi medya işlemcileri MP4 veya JSON dosyaları üretir. Medya işlemcisi bir MP4 dosyası oluşturduysa hello dosyayı aşamalı olarak indirebilirsiniz. Medya işlemcisi bir JSON dosyası oluşturduysa hello Azure blob depolama hello dosyayı indirebilirsiniz.

Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.

## <a name="deliver-progressive-download"></a>Aşamalı indirme teslimi

1. Yüksek kaliteli bir medya dosyasını bir varlığa yükleyin.
2. Tooa tek MP4 dosyasına kodlayın.
3. Bir OnDemand veya SAS Bulucu oluşturarak Hello varlığı yayımlayın.

    SAS Bulucu kullanıyorsanız hello içerik hello Azure blob depolama indirilir. Bu durumda, akış uç noktaları başlatılmış durumda toohave gerekmez.
4. Aşamalı olarak içerik indirin.

## <a id="live_scenarios"></a>Canlı akış olayları teslimi 

1. Çeşitli canlı akış protokollerini (RTMP veya Kesintisiz Akış gibi) kullanarak canlı içerik alın.
2. (isteğe bağlı) Akışınızı, bit hızı uyarlamalı akışa kodlayın.
3. Canlı akışınızın önizlemesini görüntüleyin.
4. Merhaba içeriği yaygın akış protokolleri (örneğin, MPEG DASH, kesintisiz, HLS) aracılığıyla teslim tooyour müşteriler doğrudan ya da daha fazla dağıtım tooa içerik teslim ağı (CDN).

    -veya-

    Sipariş toobe kaydı ve deposu hello alınan içeriği daha sonra (isteğe bağlı video) akışı.

Canlı akış yaparken yönlendirir hello aşağıdakilerden birini seçebilirsiniz:

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Şirket içi kodlayıcılardan çoklu bit hızlı canlı akış alan kanallar ile çalışma (doğrudan geçiş)

Merhaba Aşağıdaki diyagramda hello oynayan başlıca parçaları hello AMS platformunun hello gösterilmektedir **doğrudan** iş akışı.

![Canlı iş akışı](./media/scenarios-and-availability/media-services-live-streaming-current.png)

Daha fazla bilgi için bkz. [Şirket İçi Kodlayıcılardan Çoklu Bit Hızlı Canlı Akış Alan Kanallar ile Çalışma](media-services-live-streaming-with-onprem-encoders.md).

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Azure Media Services ile kodlama Canlı tooperform olan kanallar ile çalışma etkin

Merhaba Aşağıdaki diyagramda hello önemli bir kanal olduğu canlı akış iş akışında oynayan parçaları hello AMS platformunun tooperform Media Services ile kodlama Canlı etkin gösterir.

![Canlı iş akışı](./media/scenarios-and-availability/media-services-live-streaming-new.png)

Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [kullanılabilirlik](#availability) bölümü.

## <a name="consuming-content"></a>İçerik kullanma

Azure Media Services sağlar hello araçları toocreate zengin gereksinim dinamik istemci oynatıcı uygulamaları dahil olmak üzere çoğu Platform: iOS cihazları, Android cihazları, Windows, Windows Phone, Xbox ve alıcı kutuları. konu aşağıdaki hello bağlantılar tooSDKs ve oynatıcı çerçevelerine Media Services akış medyadan tüketebileceği kendi istemci uygulamalarınızı toodevelop kullanabilirsiniz sağlar. Daha fazla bilgi için bkz. [Video oynatma uygulamaları geliştirme](media-services-develop-video-players.md)

## <a name="enabling-azure-cdn"></a>Azure CDN'yi etkinleştirme

Media Services, Azure CDN ile tümleştirmeyi destekler. Hakkında bilgi için bkz tooenable Azure CDN [nasıl tooManage akış uç noktalarını Media Services hesabı](media-services-portal-manage-streaming-endpoints.md).

## <a id="scaling"></a>Media Services hesabını ölçeklendirme

AMS müşterileri akış uç noktalarını, medya işleme ve depolamayı kendi AMS hesaplarında ölçeklendirebilir.

* Media Services müşterileri **Standart** akış uç noktası veya **Premium** akış uç noktası seçebilir. **Standart** akış uç noktası çoğu akış iş yükü için uygundur. Aynı özellikleri olarak hello içeren bir **Premium** uç noktaları ve ölçekler giden bant genişliği otomatik olarak akış. 

    **Premium** akış uç noktaları, adanmış ve ölçeklenebilir bant genişliği kapasitesi sağlar; dolayısıyla gelişmiş iş yükleri için uygundur. **Premium** akış uç noktası olan müşteriler, varsayılan olarak bir akış birimi (SU) alır. Akış uç noktası hello SUs eklenerek genişletilebilir. Her SU ek bant genişliği kapasitesi toohello uygulama sağlar. Ölçeklendirme hakkında daha fazla bilgi için **Premium** akış uç noktaları, hello bkz [akış uç noktalarını ölçeklendirme](media-services-portal-scale-streaming-endpoints.md) konu.

* Bir Media Services hesabı bir ayrılmış birim görevleri işleme medyanızı işlenme hello hızı belirleyen türü ile ilişkilidir. Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**. Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü.

    Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler** (RUs). sağlanan RUs Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.

    >[!NOTE]
    >RU, tüm medya işlemesini paralel hale getirmek için çalışır ve Azure Media Indexer’ın kullanıldığı dizin oluşturma işleri de buna dahildir. Bununla birlikte kodlamadan farklı olarak, dizin oluşturma işleri daha hızlı ayrılmış birimlerde daha hızlı işlenmez.

    Daha fazla bilgi için bkz. [Medya işlemeyi ölçeklendirme](media-services-portal-scale-media-processing.md).
* Media Services hesabınızı depolama hesapları tooit ekleyerek de ölçeklendirebilirsiniz. Her Depolama hesabı sınırlı too500 TB'tır. tooexpand deponuzda hello varsayılan sınırlamaların ötesine birden çok depolama hesapları tooa tek Media Services hesabı tooattach seçebilirsiniz. Daha fazla bilgi için bkz. [Depolama hesaplarını yönetme](meda-services-managing-multiple-storage-accounts.md).

##<a id="availability"></a> Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği

Bu bölümde, Media Services özelliklerinin veri merkezleri arasında kullanılabilirliği hakkındaki ayrıntılar sağlanır.

### <a name="ams-accounts"></a>AMS hesapları

#### <a name="availability"></a>Kullanılabilirlik

Bölgeler şu hello Media Services hesapları oluşturabilirsiniz: Kuzey Avrupa, Batı Avrupa, Batı ABD, Doğu ABD, Güneydoğu Asya, Doğu Asya, Japonya Batı, Japonya Doğu, Brezilya Güney, Hindistan Batı, Hindistan Güney ve Hindistan orta. 

### <a name="streaming-endpoints"></a>Akış uç noktaları 

Media Services müşterileri **Standart** akış uç noktası veya **Premium** akış uç noktası seçebilir. Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.

#### <a name="availability"></a>Kullanılabilirlik

|Ad|Durum|Veri merkezleri
|---|---|---|
|Standart|GA|Tümü|
|Premium|GA|Tümü|

### <a name="live-encoding"></a>Live encoding

#### <a name="availability"></a>Kullanılabilirlik

Şu bölgeler hariç tüm veri merkezlerinde kullanılabilir: Almanya, Brezilya Güney, Hindistan Batı, Hindistan Güney ve Hindistan Orta. 

### <a name="encoding-media-processors"></a>Kodlama medya işleyicileri

AMS, isteğe bağlı iki kodlayıcı sunar: **Media Encoder Standard** ve **Media Encoder Premium İş Akışı**. Daha fazla bilgi için bkz. [Azure isteğe bağlı medya kodlayıcılarına genel bakış ve karşılaştırma](media-services-encode-asset.md). 

#### <a name="availability"></a>Kullanılabilirlik

|Medya işlemci adı|Durum|Veri merkezleri
|---|---|---|
|Media Encoder Standard|GA|Tümü|
|Media Encoder Premium İş Akışı|GA|Çin dışında tümü|

### <a name="analytics-media-processors"></a>Analiz medya işlemcileri

Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırır konuşma ve görme bileşenidir koleksiyonudur. Daha fazla bilgi için bkz. [Azure Media Services Analizi’ne Genel Bakış](media-services-analytics-overview.md).

#### <a name="availability"></a>Kullanılabilirlik

|Medya işlemci adı|Durum|Veri merkezleri
|---|---|---|
|Azure Media Face Detector|Önizleme|Tümü|
|Azure Media Hyperlapse|Önizleme|Tümü|
|Azure Media Indexer|GA|Tümü|
|Azure Media Motion Detector|Önizleme|Tümü|
|Azure Media OCR|Önizleme|Tümü|
|Azure Media Redactor|Önizleme|Tümü|
|Azure Media Stabilizer|Önizleme|Tümü|
|Azure Media Video Thumbnails|Önizleme|Tümü|
|Azure Media Indexer 2|Önizleme|Çin ve Federal Devlet bölgesi dışında tümü|

### <a name="protection"></a>Koruma

Microsoft Azure Media Services, toosecure, depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan sağlar. Daha fazla bilgi için bkz. [AMS içeriğini koruma](media-services-content-protection-overview.md).

#### <a name="availability"></a>Kullanılabilirlik

|Şifreleme|Durum|Veri merkezleri|
|---|---|---| 
|Depolama|GA|Tümü|
|AES-128 anahtarları|GA|Tümü|
|Fairplay|GA|Tümü|
|PlayReady|GA|Tümü|
|Widevine|GA|Almanya, Federal Devlet ve Çin dışında tümü.

### <a name="reserved-units-rus"></a>Ayrılmış birimler (RU)

sağlanan ayrılmış birim Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler. 

Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.

#### <a name="availability"></a>Kullanılabilirlik

Tüm veri merkezlerinde kullanılabilir.

### <a name="reserved-unit-ru-type"></a>Ayrılmış birim (RU) türü

Bir Media Services hesabı görevleri işleme medyanızı işlenme hello hızını belirler ve ayrılmış birim türü ile ilişkilidir. Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: S1, S2 ve S3.

Daha fazla bilgi için bkz: Merhaba [ölçeklendirme](#scaling) bölümü.

#### <a name="availability"></a>Kullanılabilirlik

|RU türü adı|Durum|Veri merkezleri
|---|---|---|
|S1|GA|Tümü|
|S2|GA|Brezilya Güney ve Hindistan Batı dışında tümü|
|S3|GA|Hindistan Batı dışında tümü|

## <a name="next-steps"></a>Sonraki adımlar

Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

