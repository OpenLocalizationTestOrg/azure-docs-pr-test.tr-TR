---
title: "Azure Media Services'i kullanarak canlı akış aaaOverview | Microsoft Docs"
description: "Bu konu Azure Media Services kullanarak canlı akış genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Azure Media Services'i kullanarak canlı akış genel bakış
## <a name="overview"></a>Genel Bakış
Akış olaylarını Azure Media Services ile canlı teslim edilirken bileşenleri aşağıdaki hello sık oynayan:

* Kullanılan toobroadcast bir olay olduğu bir kamera.
* Canlı akış hizmeti tooa gönderilen hello kamera toostreams sinyalleri dönüştürür canlı bir video Kodlayıcısı.

    İsteğe bağlı olarak, birden çok, gerçek zamanlı, zaman eşitlenmiş kodlayıcı. Bazı önemli live olayları isteğe bağlı yüksek kullanılabilirlik ve üstün kaliteli bir deneyim, onu tooemploy aktif-aktif yedekli kodlayıcılar zaman eşitleme tooachieve veri kaybı olmadan sorunsuz yük önerilir.
* Aşağıdaki toodo hello sağlayan bir canlı akış hizmeti:

  * çeşitli canlı akış protokollerini (RTMP veya Kesintisiz Akış gibi) kullanarak canlı içerik alma,
  * (isteğe bağlı olarak) akışınızı, bit hızı uyarlamalı akışa kodlama,
  * canlı akışınızı önizleme,
  * sonraki (isteğe bağlı video) sipariş toobe kaydı ve deposu alınan hello içeriğinde akışı
  * Merhaba içeriği yaygın akış protokolleri (örneğin, MPEG DASH, kesintisiz, HLS) aracılığıyla teslim tooyour müşteriler doğrudan ya da daha fazla dağıtım tooa içerik teslim ağı (CDN).

**Microsoft Azure Media Services** (AMS) yeteneği tooingest Merhaba, kodlama, Önizleme, depolamak ve canlı akış içeriğinizi teslim sağlar.

Amacınız, içerik toocustomers teslim edilirken toodeliver farklı ağ koşulları altında yüksek kaliteli bir video toovarious aygıtları ' dir. tooachieve Bu, kullanım, akış tooa Çoklu bit hızlı (bit hızı Uyarlamalı) video akışına kodlayıcılar tooencode Canlı.  farklı cihazlarda akış Care of tootake kullanmak Media Services [dinamik paketleme](media-services-dynamic-packaging-overview.md) toodynamically yeniden akış toodifferent protokolleri paketini. Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello teslimini destekler: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH.

Azure Media Services'de **kanalları**, **programları**, ve **akış** tüm hello canlı akış işlevlerini biçimlendirme, DVR, alma dahil olmak üzere tanıtıcısı Güvenlik, ölçeklenebilirlik ve yedeklilik.

**Kanal**, canlı akış içeriğinin işleneceği bir işlem hattını temsil eder. Bir kanal canlı bir alabilir girdi şekilde aşağıdaki hello akış:

* Çoklu bit hızlı bir şirket içi gerçek zamanlı Kodlayıcı gönderir **RTMP** veya **kesintisiz akış** (parçalanmış MP4) için yapılandırılmış toohello kanal **doğrudan** teslim. Merhaba **doğrudan** teslim alınan hello akışları geçirir olduğunda **kanal**herhangi başka bir işleme olmadan s. Çoklu bit hızlı kesintisiz akış çıkışı gerçek zamanlı kodlayıcılar aşağıdaki hello kullanabilirsiniz: MediaExcel, Ateme, düşünün iletişimleri, Envivio, Cisco ve Elemental. Merhaba şu gerçek zamanlı kodlayıcılar RTMP çıkışı: Adobe Flash medya Canlı Kodlayıcı (FMLE), Telestream Wirecast, Haivision, Teradek ve Tricaster kod dönüştürücüleri.  Gerçek zamanlı bir kodlayıcı, gerçek zamanlı kodlama için etkin değil, ancak tavsiye edilmez tek bit hızlı akış tooa kanal da gönderebilirsiniz. İstendiğinde, Media Services hello akış toocustomers sunar.

  > [!NOTE]
  > Bir doğrudan geçiş yöntemini kullanmak, uzun bir süre boyunca birden çok olay yapmakta olduğunuz ve zaten şirket içi kodlayıcılara yatırım yaptıysanız toodo akış Canlı hello en ekonomik yoludur. [Fiyatlandırma](https://azure.microsoft.com/pricing/details/media-services/) detaylarına bakın.
  > 
  > 
* Bir şirket içi gerçek zamanlı Kodlayıcı etkin tooperform toohello kanal Canlı biçimleri aşağıdaki hello birinde Media Services ile kodlama tek bit hızlı akış gönderir: RTMP veya kesintisiz akış (parçalanmış MP4). Ayrılmış bağlantı toohello Azure veri merkezi olması koşuluyla RTP (MPEG-TS) de desteklenir. gerçek zamanlı kodlayıcılar RTMP ile aşağıdaki hello çıktı toowork bu tür kanallar ile bilinir: Telestream Wirecast, FMLE. Merhaba kanal gerçekleştirir gerçek zamanlı kodlama Merhaba gelen tek bit hızlı akış tooa Çoklu bit hızlı (Uyarlamalı) video akışına. İstendiğinde, Media Services hello akış toocustomers sunar.

Bir kanal oluşturduğunuzda hello Media Services 2.10 sürümünden başlayarak, Canlı akışınızı kodlama, kanal tooreceive hello Giriş akışı ve hello kanal tooperform olsun veya olmasın istediğiniz için istediğiniz hangi şekilde belirtebilirsiniz. İki seçeneğiniz vardır:

* **Hiçbiri** (doğrudan geçiş) – toouse, Çoklu bit hızında akışa (geçiş akışı) çıkış bir şirket içi gerçek zamanlı Kodlayıcı düşünüyorsanız, bu değeri belirtin. Bu durumda, tüm kodlamadan çıktı toohello aracılığıyla hello gelen akış geçirildi. Bir kanal önceki too2.10 sürümünün hello davranış budur.  
* **Standart** – toouse Media Services tooencode düşünüyorsanız, bu değer, tek bit hızlı canlı akış toomulti bit hızında akışa seçin. Bu yöntem için sık olayları hızla ölçeklendirmeyi için daha ekonomiktir. Gerçek zamanlı kodlama için fatura bir etkisi yoktur ve canlı bir kodlama kanal hello "Çalışır" durumda bırakır fatura ücret uygulanabilir unutmayın unutmayın.  Çalışan kanalların hemen sonra canlı akış olayı durdurmanız önerilir tam tooavoid fazladan saatlik ücretleri olduğu.

## <a name="comparison-of-channel-types"></a>Kanal türleri karşılaştırması
Aşağıdaki tabloda, Media Services ile desteklenen toocomparing hello iki kanal türleri bir kılavuz sağlar

| Özellik | Doğrudan geçiş kanalı | Standart kanal |
| --- | --- | --- |
| Tek bit hızlı giriş hello bulutta Çoklu bit içine kodlanmış |Hayır |Evet |
| Maksimum çözünürlük, Katmanlar sayısı |1080p, 8 Katmanlar 60 + fps |720p, 6 Katmanlar 30 fps |
| Giriş protokolleri |RTMP, kesintisiz akış |RTMP, kesintisiz akış ve RTP |
| Fiyat |Merhaba bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/media-services/) ve "Canlı Video" sekmesini tıklatın |Merhaba bkz [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/media-services/) |
| En fazla çalışma süresi |7 x 24 |8 saat |
| Maskeleme görüntülerini ekleme desteği |Hayır |Evet |
| Ad sinyal desteği |Hayır |Evet |
| Doğrudan CEA 608/708 resim yazıları |Evet |Evet |
| Özelliği toorecover katkı içinde kısa takılması gelen akış |Evet |Hayır (kanal slating giriş verisi olmadan 6 + saniye sonra başlayacak) |
| Tekdüzen olmayan giriş GOPs desteği |Evet |Giriş 2 sn GOPs Hayır – düzeltilmesi gerekir |
| Değişken kare hızı giriş desteği |Evet |Hayır – giriş kare hızı düzeltilmesi gerekir.<br/>İkincil Çeşitlemeler, örneğin, yüksek hareket planda sırasında izin verilir. Ancak Kodlayıcı too10 Çerçeve/sn bırakılamıyor. |
| Otomatik-akış kesici zaman Giriş kanalı kaybolur |Hayır |12 çalışan bir Program yok ise saat sonra |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Şirket içi kodlayıcılardan çoklu bit hızlı canlı akış alan Kanallar ile çalışma (doğrudan geçiş)
Merhaba Aşağıdaki diyagramda hello oynayan başlıca parçaları hello AMS platformunun hello gösterilmektedir **doğrudan** iş akışı.

![Canlı iş akışı](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Daha fazla bilgi için bkz. [Şirket İçi Kodlayıcılardan Çoklu Bit Hızlı Canlı Akış Alan Kanallar ile Çalışma](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Azure Media Services ile kodlama Canlı tooperform olan kanallar ile çalışma etkin
Merhaba Aşağıdaki diyagramda hello önemli bir kanal olduğu canlı akış iş akışında oynayan parçaları hello AMS platformunun tooperform Media Services ile kodlama Canlı etkin gösterir.

![Canlı iş akışı](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Bir kanal ve ilgili bileşenlerini açıklaması
### <a name="channel"></a>Kanal
Media Services [kanal](https://docs.microsoft.com/rest/api/media/operations/channel)s canlı akış içeriğinin işlemekten sorumlu. Bir giriş uç noktası bir kanal sağlar (URL alma) tooa Canlı dönüştürücü ardından sağlayın. Merhaba kanal hello Canlı dönüştürücü Canlı giriş akışları alır ve bir veya daha fazla Akış akış için kullanılabilir hale getirir. Kanal ayrıca toopreview kullanmak ve başka bir işleme ve teslimat önce akışınızı doğrulamak bir önizleme uç noktası (Önizleme URL) sağlar.

Merhaba alabilirsiniz hello kanal oluşturduğunuzda, URL ve hello Önizleme URL'sini alın. tooget bu URL'leri, başlatılan hello durumda toobe hello kanal yok. Veri canlı bir dönüştürücü hello kanal dağıtmaya hazır toostart olduğunda hello kanal başlatılması gerekir. Veri alma Hello Canlı dönüştürücü başladıktan sonra akışınızın önizlemesini.

Her Media Services hesabı birden fazla kanal, birden çok program ve birden çok akış içerebilir. Hello bant genişliği ve güvenlik gereksinimlerine bağlı olarak, ayrılmış tooone veya daha fazla kanalları StreamingEndpoint Hizmetleri olabilir. Tüm StreamingEndpoint herhangi bir kanaldan çeker.

### <a name="program"></a>Program
A [Program](https://docs.microsoft.com/rest/api/media/operations/program) toocontrol hello yayımlama ve canlı akıştaki kesimleri depolama sağlar. Kanallar, Programları yönetir. Merhaba kanal ve Program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay çok benzer tootraditional medya ilişkidir.
İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **ArchiveWindowLength** özelliği. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz.

ArchiveWindowLength hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Merhaba belirtilen sürede programları çalıştırabilir, ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her program bir Varlık ile ilişkilidir. Varlık ilişkili toopublish hello program hello yönelik bir Bulucu oluşturmanız gerekir. Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild olanak sağlar.

Bir kanal hello birden çok arşivini oluşturabilmesi için eşzamanlı olarak çalışan programlar toothree destekler, aynı gelen akışın. Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar. Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir program, ancak toobroadcast yalnızca son 10 dakikadır. tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir. Bir program tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz. Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.

## <a name="billing-implications"></a>Faturalama etkileri
Bir kanal çok hello API "çalışır" buna ait durumu geçişleri hemen faturalama başlar.  

Merhaba aşağıdaki tabloda nasıl kanal durumları hello API toobilling Devletleri'nde ve Azure portalı karşıladığı gösterilmektedir. Merhaba durumları hello API ve Portal UX arasında biraz farklı olduğuna dikkat edin Bir kanal hello "Çalışıyor" Merhaba API aracılığıyla durumda veya hello "Hazır" veya "Akış" durumda hello Azure portal'ın faturalama etkin olarak çalışır.

Daha fazla faturalama gelen toostop hello kanal tooStop hello kanal hello API aracılığıyla veya hello Azure portal sahip.
Merhaba kanalıyla bittiğinde, kanalları durdurmak için sorumlu. Hata toostop hello kanal içinde sürekli faturalama neden olur.

> [!NOTE]
> Standart kanallar ile çalışırken, AMS kesici hala "Çalışır" durumda 12 saat hello Giriş akışı kaybedilir ve çalışan program yok sonra herhangi bir kanal otomatik. Ancak, siz hala kanal "Çalışır" durumda olmadığını hello zaman hello için Fatura edilecek.
>
>

### <a id="states"></a>Kanal durumları ve bunların modu faturalama toohello nasıl eşleneceğine
bir kanal geçerli durumu Hello. Olası değerler şunlardır:

* **Durdurulmuş**. (Autostart hello Portalı'nda seçilmedi. sürece) bu hello ilk hello kanal oluşturulduktan sonra bir durumda Bu durumda hiçbir faturalama oluşur. Bu durumda, hello kanal özellikleri güncelleştirildi ancak Akış verilmez.
* **Başlangıç**. Merhaba kanal başlatılıyor. Bu durumda hiçbir faturalama oluşur. Bu durum süresince güncelleştirmelere veya akışa izin verilmez. Bir hata oluşursa hello kanal toohello durduruldu durumu döndürür.
* **Çalışan**. Merhaba kanal Canlı akışlar işleyebilen ' dir. Şimdi kullanım faturalama. Daha fazla faturalama hello kanal tooprevent durdurmanız gerekir.
* **Durdurma**. Merhaba kanal durduruluyor. Hiçbir faturalama bu geçici durumunda oluşur. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.
* **Silme**. Merhaba kanal siliniyor. Hiçbir faturalama bu geçici durumunda oluşur. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.

Merhaba aşağıdaki tabloda nasıl kanal Haritası toohello fatura modu durumlarını gösterir.

| Kanal durumu | Portal Arabirimi Göstergeleri | Faturalama mi? |
| --- | --- | --- |
| Başlangıç |Başlangıç |Hayır (geçici durum) |
| Çalışıyor |Hazır (çalışan program yok)<br/>veya<br/>Akış (en az bir program çalışıyor) |EVET |
| Durduruluyor |Durduruluyor |Hayır (geçici durum) |
| Durduruldu |Durduruldu |Hayır |

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>İlgili konular
[Azure Media Services parçalanmış MP4 Canlı belirtimi alma](media-services-fmp4-live-ingest-overview.md)

[Etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md)

[Şirket İçi Kodlayıcılardan Çoklu Bit Hızlı Canlı Akış Alan Kanallar ile Çalışma](media-services-live-streaming-with-onprem-encoders.md)

[Kotalar ve kısıtlamaları](media-services-quotas-and-limitations.md).  

[Media Services kavramları](media-services-concepts.md)
