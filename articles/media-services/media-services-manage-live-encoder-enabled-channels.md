---
title: "Azure Media Services toocreate Çoklu bit hızı akışları kullanarak aaaLive akış | Microsoft Docs"
description: "Bu konuda, tek bit hızlı alan bir kanalı tooset nasıl bir şirket içi kodlayıcıdan akışı canlı ve Media Services ile kodlama Canlı tooadaptive bit hızlı akış gerçekleştirir açıklanmaktadır. Merhaba akış sonra tooclient kayıttan yürütme uygulamaları aracılığıyla bir veya daha fazla akış uç noktaları, Uyarlamalı akış protokolleri aşağıdaki hello biri kullanılarak alınabilir: HLS, kesintisiz akış, MPEG DASH."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>Canlı akış Azure Media Services toocreate Çoklu bit hızı akışları kullanma
## <a name="overview"></a>Genel Bakış
Azure Media Services (AMS) bir **kanal** canlı akış içeriğinin işlemek için bir işlem hattını temsil eder. A **kanal** Canlı giriş akışları iki yoldan biriyle alır:

* Bir şirket içi gerçek zamanlı Kodlayıcı etkin tooperform toohello kanal Canlı biçimleri aşağıdaki hello birinde Media Services ile kodlama tek bit hızlı akış gönderir: RTP (MPEG-TS), RTMP veya kesintisiz akış (parçalanmış MP4). Merhaba kanal gerçekleştirir gerçek zamanlı kodlama Merhaba gelen tek bit hızlı akış tooa Çoklu bit hızlı (Uyarlamalı) video akışına. İstendiğinde, Media Services hello akış toocustomers sunar.
* Çoklu bit hızlı bir şirket içi gerçek zamanlı Kodlayıcı gönderir **RTMP** veya **kesintisiz akış** değil (parçalanmış MP4) toohello kanal tooperform AMS ile kodlama Canlı etkin. Alınan hello akışları geçirmek aracılığıyla **kanal**herhangi başka bir işleme olmadan s. Bu yöntem çağrılır **doğrudan**. Çoklu bit hızlı kesintisiz akış çıkışı gerçek zamanlı kodlayıcılar aşağıdaki hello kullanabilirsiniz: MediaExcel, Ateme, düşünün iletişimleri, Envivio, Cisco ve Elemental. Merhaba şu gerçek zamanlı kodlayıcılar RTMP çıkışı: Adobe Flash medya Canlı Kodlayıcı (FMLE), Telestream Wirecast, Haivision, Teradek ve Tricaster kodlayıcılar.  Gerçek zamanlı bir kodlayıcı, gerçek zamanlı kodlama için etkin değil, ancak tavsiye edilmez tek bit hızlı akış tooa kanal da gönderebilirsiniz. İstendiğinde, Media Services hello akış toocustomers sunar.
  
  > [!NOTE]
  > Doğrudan geçiş yöntemini kullanarak toodo canlı akış hello en ekonomik yoludur.
  > 
  > 

Bir kanal oluşturduğunuzda hello Media Services 2.10 sürümünden başlayarak, Canlı akışınızı kodlama, kanal tooreceive hello Giriş akışı ve hello kanal tooperform olsun veya olmasın istediğiniz için istediğiniz hangi şekilde belirtebilirsiniz. İki seçeneğiniz vardır:

* **Hiçbiri** – toouse, Çoklu bit hızında akışa (geçiş akışı) çıkış bir şirket içi gerçek zamanlı Kodlayıcı düşünüyorsanız, bu değeri belirtin. Bu durumda, tüm kodlamadan çıktı toohello aracılığıyla hello gelen akış geçirildi. Bir kanal önceki too2.10 sürümünün hello davranış budur.  Bu tür kanallar ile çalışma hakkında daha ayrıntılı bilgi için bkz: [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarda canlı akış](media-services-live-streaming-with-onprem-encoders.md).
* **Standart** – toouse Media Services tooencode düşünüyorsanız, bu değer, tek bit hızlı canlı akış toomulti bit hızında akışa seçin. Gerçek zamanlı kodlama için fatura bir etkisi yoktur ve canlı bir kodlama kanal hello "Çalışır" durumda bırakır fatura ücret uygulanabilir unutmayın unutmayın.  Çalışan kanalların hemen sonra canlı akış olayı durdurmanız önerilir tam tooavoid fazladan saatlik ücretleri olduğu.

> [!NOTE]
> Bu konuda ele alınmıştır etkinleştirilmiş kanallar özniteliklerini tooperform gerçek zamanlı kodlama (**standart** kodlama türü). Tooperform gerçek zamanlı kodlama olmayan kanallar ile çalışma hakkında bilgi etkinleştirilmiş için bkz: [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarda canlı akış](media-services-live-streaming-with-onprem-encoders.md).
> 
> Tooreview hello emin olun [konuları](media-services-manage-live-encoder-enabled-channels.md#Considerations) bölümü.
> 
> 

## <a name="billing-implications"></a>Faturalama etkileri
Canlı bir kodlama kanal çok hello API "çalışır" buna ait durumu geçişleri hemen faturalama başlar.   Merhaba durumu hello Azure portal veya hello Azure Media Services Gezgini aracını (http://aka.ms/amse) de görüntüleyebilirsiniz.

Merhaba aşağıdaki tabloda nasıl kanal durumları hello API toobilling Devletleri'nde ve Azure portalı karşıladığı gösterilmektedir. Merhaba durumları hello API ve Portal UX arasında biraz farklı olduğuna dikkat edin Bir kanal hello "Çalışıyor" Merhaba API aracılığıyla durumda veya hello "Hazır" veya "Akış" durumda hello Azure portal'ın faturalama etkin olarak çalışır.
Daha fazla faturalama gelen toostop hello kanal tooStop hello kanal hello API aracılığıyla veya hello Azure portal sahip.
Merhaba Canlı kodlama kanalıyla bittiğinde, kanalları durdurmak için sorumlu.  Hata toostop kodlama kanal içinde sürekli faturalama neden olur.

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

### <a name="automatic-shut-off-for-unused-channels"></a>Otomatik kapatma kullanılmayan kanallar için kapalı
25 Ocak 2016 ile başlayan Media Services bir kanal (Canlı etkin kodlama ile) otomatik olarak durdurur bir güncelleştirme kullanıma alındı uzun bir süre boyunca kullanılmayan bir durumda yürütüldükten sonra. Bu, etkin program yok olan ve uzun süre akışı bir giriş katkı yapmadığınız tooChannels geçerlidir.

kullanılmayan bir süre için Hello eşik ismen 12 saat, ancak konu toochange.

## <a name="live-encoding-workflow"></a>Canlı kodlama iş akışı
Merhaba Aşağıdaki diyagramda burada bir kanal alır tek bit hızlı akış protokolleri aşağıdaki hello birinde bir canlı akış iş akışı temsil eder: RTMP, kesintisiz akış veya RTP (MPEG-TS); Ardından, hello akış tooa Çoklu bit hızında akışa kodlayan. 

![Canlı iş akışı][live-overview]

## <a id="scenario"></a>Ortak canlı akış senaryosu
Merhaba, ortak canlı akış uygulamaları oluşturmaya dahil genel adımlar verilmiştir.

> [!NOTE]
> Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun. Gerçek zamanlı kodlama için fatura bir etkisi yoktur ve canlı bir kodlama kanal hello "Çalışır" durumda bırakır saatlik faturalandırma ücret uygulanabilir unutmayın unutmayın.  Çalışan kanalların hemen sonra canlı akış olayı durdurmanız önerilir tam tooavoid fazladan saatlik ücretleri olduğu. 
> 
> 

1. Bir video kamera tooa bilgisayara bağlayın. Başlatma ve çıkışı sağlayabilecek bir şirket içi gerçek zamanlı Kodlayıcı yapılandırma bir **tek** bit hızlı akış protokolleri aşağıdaki hello birinde: RTMP, kesintisiz akış veya RTP (MPEG-TS). 
   
    Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.
2. Bir Kanal oluşturup başlatın. 
3. Alma hello kanal URL'sini alma. 
   
    Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.
4. Merhaba kanal Önizleme URL'sini alın. 
   
    Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.
5. Bir program oluşturun. 
   
    Azure portal kullanarak hello olduğunda, bir program oluşturma bir varlık da oluşturur. 
   
    .NET SDK veya REST kullanırken toocreate bir varlık gerekir ve bir programı oluştururken bu varlık toouse belirtin. 
6. Merhaba programla ilişkili hello varlığı yayımlayın.   
   
    >[!NOTE]
    >AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. Akış uç noktası toostream içerik istediğiniz hello sahip toobe hello **çalıştıran** durumu. 
    
7. Akışı ve arşivlemeyi hazır toostart olduğunda hello programını başlatın.
8. İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir. Merhaba tanıtım hello çıktı akışına eklenir.
9. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun.
10. Merhaba programı silin (ve isteğe bağlı olarak hello varlığını silme).   

> [!NOTE]
> Çok önemli olan Canlı kodlama kanal tooforget tooStop değil. Gerçek zamanlı kodlama için etkisi faturalama bir saatlik yoktur ve canlı bir kodlama kanal hello "Çalışır" durumda bırakır fatura ücret uygulanabilir unutmayın unutmayın.  Çalışan kanalların hemen sonra canlı akış olayı durdurmanız önerilir tam tooavoid fazladan saatlik ücretleri olduğu. 
> 
> 

## <a id="channel"></a>Kanal girdisini (alma) yapılandırmaları
### <a id="Ingest_Protocols"></a>Alma Akış Protokolü
Merhaba, **Kodlayıcı türü** çok ayarlanır**standart**, geçerli seçenekler şunlardır:

* **RTP** (MPEG-TS): RTP üzerinden MPEG-2 aktarım akışı.  
* Tek bit hızlı **RTMP**
* Tek bit hızlı **parçalanmış MP4** (kesintisiz akış)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP (MPEG-TS) - RTP üzerinden MPEG-2 aktarım akışı.
Tipik kullanım örneği: 

Profesyonel yayıncıları genellikle yüksek kaliteli şirket içi gerçek zamanlı kodlayıcılar Elemental teknolojileri Ericsson, Ateme Imagine veya Envivio toosend gibi satıcılardan bir akış çalışırlar. Genellikle bir BT departmanının ve özel ağlar ile birlikte kullanılır.

Dikkate alınacak noktalar:

* Giriş bir tek bir program aktarım akışı (SPTS) Hello kullanımını önemle tavsiye edilir. 
* RTP MPEG-2 TS kullanarak too8 ses akışları yukarı girebilirsiniz. 
* Merhaba video akışına ortalama bir bit hızı 15 Mbps aşağıda olmalıdır
* Merhaba toplam ortalama hızı hello ses akışları, 1 MB/sn olmalıdır
* Aşağıdaki desteklenen codec bileşenleri hello:
  
  * MPEG-2 / H.262 Video 
    
    * Ana profili (4:2:0)
    * Yüksek profil (4:2:0, 4:2:2)
    * 422 profil (4:2:0, 4:2:2)
  * MPEG-4 AVC / H.264 Video  
    
    * Taban çizgisi, ana, yüksek profil (8 bit 4:2:0)
    * Yüksek 10 profili (10 bit 4:2:0)
    * Yüksek 422 profili (10 bit 4:2:2)
  * MPEG-2 AAC-LC ses 
    
    * Mono, Stereo, Surround (5.1, 7.1)
    * MPEG-2 stili ADTS paketleme
  * Dolby dijital (AC-3) ses 
    
    * Mono, Stereo, Surround (5.1, 7.1)
  * MPEG Ses (Katman II ve III) 
    
    * Mono, Stereo
* Önerilen yayın kodlayıcılar içerir:
  
  * İletişim Selenio ÇÖZÜCÜ 1 düşünün
  * İletişim Selenio ÇÖZÜCÜ 2 düşünün
  * Elemental dinamik

#### <a id="single_bitrate_RTMP"></a>Tek bit hızlı RTMP
Dikkate alınacak noktalar:

* Merhaba gelen akış Çoklu bit hızlı video içeremez.
* Merhaba video akışına ortalama bir bit hızı 15 Mbps aşağıda olmalıdır
* Merhaba ses akışı aşağıda 1 MB/sn ortalama bir bit hızı olmalıdır
* Aşağıdaki desteklenen codec bileşenleri hello:
* MPEG-4 AVC / H.264 Video
* Taban çizgisi, ana, yüksek profil (8 bit 4:2:0)
* Yüksek 10 profili (10 bit 4:2:0)
* Yüksek 422 profili (10 bit 4:2:2)
* MPEG-2 AAC-LC ses
* Mono, Stereo, Surround (5.1, 7.1)
* 44,1 kHz örnekleme hızı
* MPEG-2 stili ADTS paketleme
* Önerilen kodlayıcılar şunları içerir:
* Telestream Wirecast
* Flash medya gerçek zamanlı kodlayıcı

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>Tek bit hızlı Parçalanmış MP4 (Kesintisiz Akış)
Tipik kullanım örneği:

Şirket içi gerçek zamanlı kodlayıcılar Elemental teknolojileri, Ericsson, Ateme, Envivio toosend hello Giriş akışı hello açık Internet tooa Azure veri merkezine yakındaki üzerinden gibi satıcılardan kullanın.

Dikkate alınacak noktalar:

Aynı olarak [tek bit hızlı RTMP](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP).

#### <a name="other-considerations"></a>Diğer konular
* Merhaba kanal hello giriş protokolünü değiştiremezsiniz veya ilişkili programları çalışmıyor. Farklı protokollere ihtiyacınız varsa her bir giriş protokolü için farklı bir kanal oluşturmalısınız.
* Merhaba gelen video akış için en yüksek çözünürlük 1920 x 1080 olan ve en fazla 60 alanları aralıklı, saniye başına veya 30 Çerçeve/saniye aşamalı durumunda.

### <a name="ingest-urls-endpoints"></a>Alma URL'leri (Bitiş)
Bir giriş uç noktası bir kanal sağlar (URL alma) tooyour kanalları akışları hello Kodlayıcı gönderebilir şekilde hello gerçek zamanlı Kodlayıcı içinde belirtin.

Merhaba alabileceğiniz bir kanalı oluşturduktan sonra URL'lerini alabilirsiniz. tooget bu URL'leri, hello toobe hello kanalı yok **çalıştıran** durumu. Veri kanalı hello dağıtmaya hazır toostart olduğunda hello olmalıdır **çalıştıran** durumu. Veri alma Hello kanal başladıktan sonra akışınızı hello Önizleme URL yoluyla önizleyebilirsiniz.

Parçalanmış MP4 alanını bir seçeneğiniz bir SSL bağlantısı üzerinden canlı akış (kesintisiz akış). SSL üzerinden tooingest URL tooHTTPS alma emin tooupdate hello olun. Şu anda AMS SSL ile özel etki alanlarını, desteklemez.  

### <a name="allowed-ip-addresses"></a>İzin verilen IP adresi
Toopublish video toothis kanalı izin hello IP adreslerini tanımlayabilirsiniz. İzin verilen IP adresleri, tek bir IP adresi (ör. '10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi kullanarak bir IP aralığı (ör. ‘10.0.0.1/22’) veya bir IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı (ör. '10.0.0.1(255.255.252.0)').

Herhangi bir IP adresi belirtilmezse ve bir kural tanımı yoksa hiçbir IP adresine izin verilmez. tooallow herhangi bir IP adresi, bir kural oluşturun ve 0.0.0.0/0 olarak ayarlayın.

## <a name="channel-preview"></a>Kanal Önizleme
### <a name="preview-urls"></a>Önizleme URL'leri
Kanalları toopreview kullanmak ve başka bir işleme ve teslimat önce akışınızı doğrulamak bir önizleme uç noktası (Önizleme URL) sunar.

Merhaba kanal oluşturduğunuzda hello Önizleme URL'sini alabilirsiniz. tooget hello URL hello kanalı yok toobe hello **çalıştıran** durumu.

Veri alma Hello kanal başladıktan sonra akışınızın önizlemesini.

> [!NOTE]
> Şu anda hello Önizleme akış yalnızca parçalanmış MP4 alınabilir (kesintisiz akış) biçiminde hello bakılmaksızın belirtilen giriş türü. Merhaba kullanabilirsiniz [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) player tootest hello kesintisiz akış. Aynı zamanda bir oynatıcı hello Azure portal tooview akışınızı barındırılan.
> 
> 

### <a name="allowed-ip-addresses"></a>İzin verilen IP adreslerini
Tooconnect toohello Önizleme uç noktasını izin verilen hello IP adreslerini tanımlayabilirsiniz. Herhangi bir IP adresine izin herhangi bir IP adresi belirtilmezse. İzin verilen IP adresleri, tek bir IP adresi (ör. '10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi kullanarak bir IP aralığı (ör. ‘10.0.0.1/22’) veya bir IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı (ör. ‘10.0.0.1(255.255.252.0)’) şeklinde belirtilebilir.

## <a name="live-encoding-settings"></a>Canlı kodlama ayarları
Merhaba hello kanal içindeki gerçek zamanlı Kodlayıcı hello ayarlarını nasıl olabilir, bu bölümde açıklanmıştır ayarlanabileceği zaman hello **kodlama türü** bir kanalı çok ayarlamak**standart**.

> [!NOTE]
> Zaman birden çok dil parçaları giriş yapma ve Azure ile gerçek zamanlı kodlama yapılması, yalnızca RTP çok dilli giriş için desteklenir. RTP MPEG-2 TS kullanarak too8 ses akışları yukarı tanımlayabilirsiniz. RTMP veya kesintisiz akış ile birden çok ses izleri alma şu anda desteklenmiyor. Yaparken ile gerçek zamanlı kodlama [şirket içi Canlı kodlar](media-services-live-streaming-with-onprem-encoders.md), ne olursa olsun tooAMS gönderilen bir kanal herhangi başka bir işleme olmadan geçirdiği için böyle bir kısıtlama değil.
> 
> 

### <a name="ad-marker-source"></a>Ad işaret kaynağı
Merhaba reklam işaretçi sinyallerinin kaynağını belirtebilirsiniz. Varsayılan değer **API**, o hello gerçek zamanlı Kodlayıcı hello kanal içinde belirten tooan zaman uyumsuz dinleyecek **reklam işaretçisi API'yi**.

Merhaba diğer geçerli bir seçenek olan **Scte35** (yalnızca hello alma Protokolü akış tooRTP (MPEG-TS) ayarlanmış izin. Scte35 belirtildiğinde, hello gerçek zamanlı Kodlayıcı SCTE-35 sinyalleri hello giriş RTP (MPEG-TS) akışından ayrıştırılamıyor.

### <a name="cea-708-closed-captions"></a>CEA 708 kapalı açıklamalı alt yazıları
Herhangi bir CEA 708 resim yazıları veri hello gerçek zamanlı Kodlayıcı tooignore belirten isteğe bağlı bir bayrak hello gelen videoda katıştırılmış. Merhaba bayrağını toofalse (varsayılan) ayarladığınızda, hello Kodlayıcı algılamak ve CEA 708 veri hello çıkış video akışları yeniden ekleyin.

### <a name="video-stream"></a>Video akışı
İsteğe bağlı. Merhaba giriş video akışı açıklanır. Bu alan belirtilmezse, hello varsayılan değer kullanılır. Bu ayar yalnızca akış protokolüne tooRTP (MPEG-TS) ayarlanmış hello giriş izin verilir.

#### <a name="index"></a>Dizin
Hangi giriş video akışına hello hello kanal içindeki gerçek zamanlı Kodlayıcı tarafından işleneceğini belirtir sıfır tabanlı dizini. Bu ayar yalnızca geçerli alma Protokolü akış RTP (MPEG-TS) kullanılır.

Varsayılan değer sıfır olur. Tek bir program aktarım akışı (SPTS) toosend önerilir. Hello Giriş akışı birden çok program içeriyorsa, hello gerçek zamanlı Kodlayıcı hello Program eşleme tablosu (devresel_ödeme) hello girişte ayrıştırır, akış türü adı MPEG-2 Video veya H.264 sahip hello girişleri tanımlar ve bunları hello ödeme belirtilen hello sırasıyla düzenler Merhaba sıfır tabanlı dizin sonra kullanılan toopick hello n. Bu düzenleme girişi ayarlama.

### <a name="audio-stream"></a>Ses akışı
İsteğe bağlı. Merhaba giriş ses akışları açıklar. Bu alan belirtilmezse, belirtilen hello varsayılan değerleri uygulayın. Bu ayar yalnızca akış protokolüne tooRTP (MPEG-TS) ayarlanmış hello giriş izin verilir.

#### <a name="index"></a>Dizin
Tek bir program aktarım akışı (SPTS) toosend önerilir. Merhaba Giriş akışı birden çok program içeriyorsa, hello hello kanal içindeki gerçek zamanlı Kodlayıcı hello Program eşleme tablosu (devresel_ödeme) hello girişte ayrıştırır, MPEG-2 AAC ADTS veya AC-3 sistem A veya Sistem AC-3-B veya MPEG-2 özel bir akış türü ada sahip hello girişleri tanımlar PES veya MPEG-1 ses veya MPEG-2 ses ve bunları hello ödeme belirtilen hello sırasıyla düzenler Merhaba sıfır tabanlı dizin sonra kullanılan toopick hello n. Bu düzenleme girişi ayarlama.

#### <a name="language"></a>Dil
tooISO 639-2, Müh gibi uyumsuz hello ses akışı dil tanımlayıcısını hello Yoksa, hello (tanımsız) ÇİZİLİ varsayılandır.

Olabilir hello toohello kanal giriş RTP MPEG-2 TS olur kümeleri belirlenen too8 ses akış yukarı. Ancak, hiçbir iki girişleri bulunabilir hello ile aynı dizin değeri.

### <a id="preset"></a>Sistem hazır
Merhaba hello bu kanal içindeki gerçek zamanlı Kodlayıcı tarafından kullanılan toobe önceden belirtir. Şu anda yalnızca değer izin verilen hello **Default720p** (varsayılan).

Özel hazır gerekiyorsa, amslived@Microsoft.com adresine başvurun unutmayın.

**Default720p** hello video 7 Katmanlar izleyerek hello kodlar.

#### <a name="output-video-stream"></a>Çıkış Video akışı
| Bit hızı | Genişlik | Yükseklik | MaxFPS | Profil | Çıkış akış adı |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |Yüksek |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |Ana |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |Ana |Video_704x396_1350kbps |
| 850 |512 |288 |30 |Ana |Video_512x288_850kbps |
| 550 |384 |216 |30 |Ana |Video_384x216_550kbps |
| 350 |340 |192 |30 |Taban çizgisi |Video_340x192_350kbps |
| 200 |340 |192 |30 |Taban çizgisi |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>Çıkış ses akışı
Ses kodlanmış toostereo AAC-LC 44,1 kHz örnekleme 64 Kbps ' dir.

## <a name="signaling-advertisements"></a>Sinyal reklamları
Kanalınızı gerçek zamanlı kodlama etkin olduğunda, işleme video, ardışık düzeninde bir bileşen varsa ve bunu değiştirebilirsiniz. Merhaba kanal tooinsert maskeleme görüntülerini ve/veya hello giden bit hızı Uyarlamalı akışa reklamlar için sinyal. Maskeleme görüntülerini hala toocover hello giriş canlı akış yukarı (örneğin bir ticari sonu sırasında) belirli durumlarla kullanabilirsiniz görüntüleri bağımsızdır. Sinyalleri reklam, eşitlenen zaman sinyalleri eyleme hello giden akış tootell hello video oynatıcı tootake özel – tooswitch tooan tanıtım hello uygun zaman gibi katıştırmak var. Bu bkz [blog](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) hello SCTE-35 sinyal mekanizması bu amaç için kullanılan genel bakış. Aşağıda, Canlı olayınızın uygulamadan tipik bir senaryo yer almaktadır.

1. Merhaba olay başlamadan önce öncesi olay görüntüsünü Al, görüntüleyiciler vardır.
2. Merhaba olay sona erdikten sonra sonrası olay görüntüsünü Al, görüntüleyiciler vardır.
3. Merhaba olayı (örneğin, hello stadyum içinde güç arızası) sırasında bir sorun varsa bir hata OLAYI görüntüsünü Al, görüntüleyiciler vardır.
4. Bir ticari sonu sırasında akışı bir AD-BREAK görüntü toohide hello canlı olay gönderin.

reklamları sinyal zaman ayarlayabileceğiniz hello özellikleri Hello aşağıda verilmiştir. 

### <a name="duration"></a>Süre
saniye cinsinden hello ticari sonuna Hello süresi. Bu toobe sıfır olmayan pozitif bir değer Sipariş toostart hello ticari sonu sahiptir. Bir ticari sonu ilerleme durumunu ve hello süresi içinde olduğunda kümesi toozero hello CueId ile bu sonu iptal sonra hello devam eden ticari sonu eşleşen.

### <a name="cueid"></a>CueId
Merhaba ticari sonu, aşağı akış uygulaması tootake uygun eylemleri tarafından kullanılan toobe için benzersiz bir kimliği. Toobe pozitif bir tamsayı olmalıdır. Bu değer tooany rastgele pozitif tamsayı ayarlayabilir veya Yukarı Akış sistem tootrack hello işaret kimlikleri kullanabilirsiniz. Belirli toonormalize hello API göndermeden önce tüm kimlikleri toopositive tamsayılar olun.

### <a name="show-slate"></a>Göster Kurşun
İsteğe bağlı. Sinyalleri hello gerçek zamanlı Kodlayıcı tooswitch toohello [varsayılan Kurşun](media-services-manage-live-encoder-enabled-channels.md#default_slate) görüntü sırasında ticari sonu ve hello gelen video akışına gizle. Ses sırasında Kurşun de kapalı. Varsayılan değer **false**. 

kullanılan hello görüntüsü hello bir hello slate varsayılan varlık ID özelliği hello hello kanal oluşturma sırasında belirtilen olacaktır. Merhaba Kurşun olacaktır toofit hello görünen görüntü boyutu uzatılabilir. 

## <a name="insert-slate--images"></a>Kurşun görüntüleri ekleme
Merhaba hello kanal içindeki gerçek zamanlı Kodlayıcı iş tooswitch tooa slate görüntü olabilir. Ayrıca, iş tooend devam eden Kurşun de olabilir. 

Merhaba gerçek zamanlı Kodlayıcı yapılandırılmış tooswitch tooa slate görüntüsü olması ve hello gelen video sinyali bazı durumlarda – Örneğin, bir ad sonu sırasında gizleyin. Bu tür bir Kurşun yapılandırılmamışsa, bu ad sonu sırasında giriş video maskelenir değil.

### <a name="duration"></a>Süre
Merhaba Kurşun Hello süresini saniye cinsinden. Bu toobe sıfır olmayan pozitif bir değer Sipariş toostart hello Kurşun sahiptir. Devam eden Kurşun yoktur ve bir süre sıfır belirtilirse, devam eden Kurşun sonlandırılacak.

### <a name="insert-slate-on-ad-marker"></a>Reklam işaretçisine maskeleme görüntüsü ekle
Ne zaman kümesi tootrue, bu ayar bir ad sonu sırasında hello gerçek zamanlı Kodlayıcı tooinsert slate görüntü yapılandırır. Merhaba varsayılan değer true olur. 

### <a id="default_slate"></a>Varsayılan slate varlık kimliği

İsteğe bağlı. Merhaba hello hello slate görüntü içeren Media Services varlık varlık kimliğini belirtir. Varsayılan değer null şeklindedir. 


>[!NOTE] 
>Merhaba kanal oluşturmadan önce hello kısıtlamaları aşağıdaki hello slate görüntüsüyle (diğer bir dosyaları bu varlığı olmalıdır) adanmış bir varlık olarak yüklenmelidir. Bu görüntü, ne zaman hello gerçek zamanlı Kodlayıcı Kurşun tooan ad sonu son ekleme veya açıkça bırakıldı tooinsert bir Kurşun işaret yalnızca kullanılır. Merhaba gerçek zamanlı Kodlayıcı de slate moduna bazı hata koşullarını sırasında – örneğin hello giriş sinyali kayıp olup olmadığını gidebilirsiniz. Var. şu anda hiçbir seçeneği toouse özel bir görüntü hello gerçek zamanlı Kodlayıcı bu tür bir 'giriş sinyali kayıp' durumuna girdiğinde Bu özellik için oy [burada](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel).


* En çok 1920 x 1080 çözünürlük.
* En fazla 3 MB boyutunda.
* Merhaba dosya adı *.jpg uzantısı olmalıdır.
* Merhaba görüntü bir varlığa bu varlığının içinde yalnızca AssetFile ve bu AssetFile hello birincil dosya olarak işaretlenmelidir hello olarak yüklenmelidir. Merhaba varlık şifrelenmiş depolama olamaz.

Merhaba, **varsayılan Kurşun varlık kimliği** belirtilmezse, ve **ad işaret üzerinde Kurşun Ekle** çok ayarlanır**doğru**, varsayılan bir Azure Media Services görüntüsü giriş kullanılan toohide hello olacaktır video akışı. Ses sırasında Kurşun de kapalı. 

## <a name="channels-programs"></a>Kanalın programlar
Bir kanal toocontrol hello yayımlama ve canlı akıştaki kesimleri depolanmasını sağlayan programlarla ilişkilidir. Kanallar, Programları yönetir. Merhaba kanal ve Program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay çok benzer tootraditional medya ilişkidir.

İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz. Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Merhaba belirtilen sürede programları çalıştırabilir, ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her bir program akışı hello içeriği depolayan bir varlıkla ilişkilidir. Eşlenen tooa blok blob kapsayıcısı'hello Azure depolama hesabındaki bir varlıktır ve bu kapsayıcıdaki blobları olarak hello varlık hello dosyalarında depolanır. ilişkili varlık müşterilerinizin hello yönelik bir OnDemand Bulucu oluşturmanız gerekir hello akış görüntüleyebilmeniz toopublish hello program. Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild olanak sağlar.

Bir kanal hello birden çok arşivini oluşturabilmesi için eşzamanlı olarak çalışan programlar toothree destekler, aynı gelen akışın. Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar. Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir program, ancak toobroadcast yalnızca son 10 dakikadır. tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir. Bir program tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz. Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.

Yeni olaylar için mevcut programları yeniden kullanmamalısınız. Bunun yerine, oluşturun ve hello canlı akış uygulamaları programlama bölümde açıklandığı gibi her olay için yeni bir programı başlatın.

Akışı ve arşivlemeyi hazır toostart olduğunda hello programını başlatın. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun. 

Arşivlenen toodelete içerik durdurup hello programı silmek ve ardından hello ilişkili varlığı silin. Bir program tarafından kullanılıyorsa varlık silinemez; Merhaba programın silinmesi gerekir. 

Durdur ve hello programı silmek bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.

Arşivlenen tooretain hello içerik istiyor ancak değil bulundurursunuz akış için, Bulucu akış hello silin.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>Bir canlı akış küçük resim önizlemesini alma
Gerçek zamanlı kodlama etkinleştirildiğinde hello kanal ulaştığında gibi şimdi hello canlı akış önizlemesini alabilirsiniz. Canlı akış gerçekte hello kanal ulaşıyor olup olmadığını bu değerli bir araç toocheck olabilir. 

## <a id="states"></a>Kanal durumları ve nasıl modu faturalama toohello durumları eşleme
bir kanal geçerli durumu Hello. Olası değerler şunlardır:

* **Durdurulmuş**. Bu hello ilk hello kanal oluşturulduktan sonra durumudur. Bu durumda, hello kanal özellikleri güncelleştirildi ancak Akış verilmez.
* **Başlangıç**. Merhaba kanal başlatılıyor. Bu durum süresince güncelleştirmelere veya akışa izin verilmez. Bir hata oluşursa hello kanal toohello durduruldu durumu döndürür.
* **Çalışan**. Merhaba kanal Canlı akışlar işleyebilen ' dir.
* **Durdurma**. Merhaba kanal durduruluyor. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.
* **Silme**. Merhaba kanal siliniyor. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.

Merhaba aşağıdaki tabloda nasıl kanal Haritası toohello fatura modu durumlarını gösterir. 

| Kanal durumu | Portal Arabirimi Göstergeleri | Faturalandırılmış mı? |
| --- | --- | --- |
| Başlangıç |Başlangıç |Hayır (geçici durum) |
| Çalışıyor |Hazır (çalışan program yok)<br/>veya<br/>Akış (en az bir program çalışıyor) |Evet |
| Durduruluyor |Durduruluyor |Hayır (geçici durum) |
| Durduruldu |Durduruldu |Hayır |

> [!NOTE]
> Şu anda hello kanal başlangıç ortalama yaklaşık 2 dakika, ancak bazen too20 + dakika sürebilir. Kanal sıfırlar too5 dakika sürebilir.
> 
> 

## <a id="Considerations"></a>Dikkat edilecek noktalar
* Bir kanalı zaman **standart** kodlama türü giriş kaynağı/katkı akış kaybı karşılaştığında, bunun için bir hata Kurşun ve sessizlik hello kaynak video/ses değiştirerek dengeler. Merhaba giriş/katkı sürdürür akış kadar hello kanal tooemit bir Kurşun devam eder. Canlı kanal böyle bir durumda 2 saatten uzun bırakılması değil, öneririz. Bu noktanın ötesine hello kanal giriş yeniden bağlanmayı üzerinde hello davranışını kesin değildir, yanıt tooa sıfırlama komut içinde kendi davranıştır. Toostop hello kanal sahip, silin ve yeni bir tane oluşturun.
* Merhaba kanal hello giriş protokolünü değiştiremezsiniz veya ilişkili programları çalışmıyor. Farklı protokollere ihtiyacınız varsa her bir giriş protokolü için farklı bir kanal oluşturmalısınız.
* Merhaba gerçek zamanlı Kodlayıcı yeniden her zaman hello çağrısı **sıfırlama** hello kanalda yöntemi. Merhaba kanal sıfırlamadan toostop hello program sahip. Merhaba kanalı sıfırladıktan sonra hello programını yeniden başlatın.
* Bir kanal yalnızca hello çalışıyor durumda olduğunda ve tüm programlar hello kanalda durduruldu durdurulabilir.
* Varsayılan olarak 5 kanalları tooyour Media Services hesabı yalnızca ekleyebilirsiniz. Tüm yeni hesaplarda Esnek kota budur. Daha fazla bilgi için bkz: [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).
* Merhaba kanal hello giriş protokolünü değiştiremezsiniz veya ilişkili programları çalışmıyor. Farklı protokollere ihtiyacınız varsa her bir giriş protokolü için farklı bir kanal oluşturmalısınız.
* Kanalınızı hello olduğunda, yalnızca faturalandırılır **çalıştıran** durumu. Daha fazla bilgi için çok başvurun[bu](media-services-manage-live-encoder-enabled-channels.md#states) bölümü.
* Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.
* Toohave hello hello toostream içeriği istediğiniz akış uç emin olun **çalıştıran** durumu.
* Zaman birden çok dil parçaları giriş yapma ve Azure ile gerçek zamanlı kodlama yapılması, yalnızca RTP çok dilli giriş için desteklenir. RTP MPEG-2 TS kullanarak too8 ses akışları yukarı tanımlayabilirsiniz. RTMP veya kesintisiz akış ile birden çok ses izleri alma şu anda desteklenmiyor. Yaparken ile gerçek zamanlı kodlama [şirket içi Canlı kodlar](media-services-live-streaming-with-onprem-encoders.md), ne olursa olsun tooAMS gönderilen bir kanal herhangi başka bir işleme olmadan geçirdiği için böyle bir kısıtlama değil.
* Merhaba kodlama hazır kullanır 30 fps "max kare hızı" kavramı hello. Merhaba giriş 60 fps ise şekilde / 59.97i, hello giriş çerçeve olan bırakılan/Kaldır-interlaced too30/29.97 fps. Merhaba giriş 50 fps/50i hello giriş çerçeveleri bırakılan/Kaldır-interlaced too25 fps demektir. Merhaba giriş 25 fps ise, çıktı 25 fps ile kalır.
* İşiniz bittiğinde tooSTOP YOUR kanalları unutmayın. Yapmadığınız takdirde, faturalandırma devam eder.

## <a name="known-issues"></a>Bilinen sorunlar
* Kanal başlama süresi geliştirilmiş tooan ortalama 2 dakika ancak bazen artan talebin too20 + dakikada hala sürebilir.
* RTP destek profesyonel yayıncıları catered. Lütfen içinde RTP hello notlarını gözden geçirin. [bu](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) blogu.
* Slate görüntüleri açıklanan toorestrictions uyması [burada](media-services-manage-live-encoder-enabled-channels.md#default_slate). Dener hello istek sonunda olacak 1920 x 1080 büyük slate varsayılan hata bir kanal oluşturun.
* Bir kez daha... İşiniz bittiğinde tooSTOP YOUR kanalları unutmayın akış. Yapmadığınız takdirde, faturalandırma devam eder.

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>İlgili konular
[Azure Media Services ile etkinliklerin canlı akış teslim etme](media-services-overview.md)

[Portal ile singe bit hızı tooadaptive bit hızı akıştan gerçek zamanlı kodlama gerçekleştiren kanallar oluşturmak](media-services-portal-creating-live-encoder-enabled-channel.md)

[.NET SDK'sı singe bit hızı tooadaptive bit hızı akıştan gerçek zamanlı kodlama gerçekleştiren kanallar oluşturmak](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[REST API ile kanalları Yönet](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[Media Services kavramları](media-services-concepts.md)

[Azure Media Services parçalanmış MP4 Canlı belirtimi alma](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

