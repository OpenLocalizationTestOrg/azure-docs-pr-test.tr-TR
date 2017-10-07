---
title: "aaaStream Azure - Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla Canlı | Microsoft Docs"
description: "Bu konuda nasıl tooset Çoklu bit hızlı alan bir kanalı canlı bir şirket içi kodlayıcıdan akışı açıklanır. Merhaba akış sonra tooclient kayıttan yürütme uygulamalar Uyarlamalı akış protokolleri aşağıdaki hello birini kullanarak bir veya daha fazla akış uç noktalarını, aracılığıyla teslim edilebilir: HLS, kesintisiz akış, tire."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış
## <a name="overview"></a>Genel Bakış
Azure Media Services, bir *kanal* canlı akış içeriği işlemek için bir işlem hattını temsil eder. Bir kanal Canlı giriş akışları iki yoldan biriyle alır:

* Bir şirket içi gerçek zamanlı Kodlayıcı Çoklu bit hızlı RTMP gönderir veya etkin tooperform olmayan kesintisiz akış (parçalanmış MP4) akış toohello kanal Canlı görüntü Media Services ile kodlama. Merhaba herhangi başka bir işleme olmadan akışları geçişi kanalları üzerinden alınan. Bu yöntem çağrılır *doğrudan*. Çoklu bit hızlı kesintisiz akış çıktı olarak sahip gerçek zamanlı kodlayıcılar aşağıdaki hello kullanabilirsiniz: Media Excel, Ateme, düşünün iletişimleri, Envivio, Cisco ve Elemental. gerçek zamanlı kodlayıcılar aşağıdaki hello RTMP çıktı olarak vardır: dinamik Adobe Flash medya Kodlayıcı, Telestream Wirecast, Haivision, Teradek ve TriCaster. Gerçek zamanlı bir kodlayıcı, gerçek zamanlı kodlama için etkinleştirilmemiş bir tek bit hızında akışa tooa kanal da gönderebilir, ancak bunu önermiyoruz. Media Services, bunu isteyen hello akış toocustomers sunar.

  > [!NOTE]
  > Doğrudan geçiş yöntemini kullanarak toodo canlı akış hello en ekonomik yoludur.


* Bir şirket içi gerçek zamanlı Kodlayıcı tek bit hızında akışa toohello kanal etkin tooperform biçimleri aşağıdaki hello birinde Media Services ile kodlama Canlı gönderir: RTP (MPEG-TS), RTMP veya kesintisiz akış (parçalanmış MP4). Merhaba kanal hello gelen tek bit hızlı akış tooa Çoklu bit hızlı (Uyarlamalı) video akışına gerçek zamanlı kodlama gerçekleştirir. Media Services, bunu isteyen hello akış toocustomers sunar.

Bir kanal oluşturduğunuzda hello Media Services 2.10 sürümünden başlayarak, nasıl, kanal tooreceive hello Giriş akışı istediğinizi belirtebilirsiniz. Merhaba kanal tooperform Canlı akışınızı kodlama isteyip istemediğinizi de belirtebilirsiniz. İki seçeneğiniz vardır:

* **Geçir**: toouse Çoklu bit hızında akışa (geçiş akışı) çıkış olarak sahip olan bir şirket içi gerçek zamanlı Kodlayıcı düşünüyorsanız, bu değeri belirtin. Bu durumda, tüm kodlamadan çıktı toohello aracılığıyla hello gelen akış geçirir. Kanal hello 2.10 serbest bırakmadan önce hello davranış budur. Bu konuda bu tür kanallar ile çalışma hakkında ayrıntılar sağlar.
* **Kodlama canlı**: Bu değer, tek bit hızında bir canlı akışı tooa Çoklu bit hızında akışa toouse Media Services tooencode düşünüyorsanız seçin. Gerçek zamanlı kodlama bırakarak kanal unutmayın bir **çalıştıran** durumu fatura ücretleri erişimliye. Çalışan kanalların hemen sonra canlı akış olayınızın durdurma öneririz tam tooavoid fazladan saatlik ücretleri olduğu. Media Services, bunu isteyen hello akış toocustomers sunar.

> [!NOTE]
> Bu konuda ele alınmıştır etkin olmayan kanalları özniteliklerini tooperform gerçek zamanlı kodlama. Tooperform gerçek zamanlı kodlama olan kanallar ile çalışma hakkında bilgi etkinleştirilmiş için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).
>
>

Aşağıdaki diyagramda hello bir şirket içi gerçek zamanlı Kodlayıcı toohave Çoklu bit hızlı RTMP ya da parçalanmış MP4 (kesintisiz akış) akışları çıkış olarak kullanan bir canlı akış iş akışı temsil eder.

![Canlı iş akışı][live-overview]

## <a id="scenario"></a>Ortak canlı akış senaryosu
Merhaba aşağıdaki adımlar ortak canlı akış uygulamaları oluşturmaya dahil olan görevleri açıklamaktadır.

1. Bir video kamera tooa bilgisayara bağlayın. Başlangıç ve Çoklu bit hızlı RTMP veya parçalanmış MP4 sahip bir şirket içi gerçek zamanlı Kodlayıcı yapılandırın (kesintisiz akış) akış çıktı olarak. Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).

    Bu adım, kanalınızı oluşturduktan sonra de gerçekleştirebilirsiniz.
2. Bir kanal oluşturup başlatın.

3. Alma hello kanal URL'sini alma.

    Merhaba gerçek zamanlı Kodlayıcı kullanır hello alma URL toosend hello akış toohello kanal.
4. Merhaba kanal Önizleme URL'sini alın.

    Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.
5. Bir program oluşturun.

    Hello Azure portalını kullandığınızda, bir program oluşturma bir varlık da oluşturur.

    Merhaba .NET SDK veya REST kullandığınızda, toocreate bir varlık gerekir ve bir programı oluştururken bu varlık toouse belirtin.
6. Merhaba programla ilişkili hello varlığı yayımlayın.   

    >[!NOTE]
    >Azure Media Services hesabınızı oluştururken bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. Akış uç noktası toostream içerik istediğiniz hello sahip toobe hello **çalıştıran** durumu.

7. Akışı ve arşivlemeyi hazır toostart olduğunuzda hello programını başlatın.

8. İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir. Merhaba tanıtım hello çıktı akışına eklenir.

9. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun.

10. Merhaba programı silin (ve isteğe bağlı olarak hello varlığını silme).     

## <a id="channel"></a>Bir kanal ve ilgili bileşenlerini açıklaması
### <a id="channel_input"></a>Kanal giriş (alma) yapılandırmaları
#### <a id="ingest_protocols"></a>Alma Akış Protokolü
Media Services, Çoklu bit hızlı parçalanmış MP4 ve Çoklu bit hızlı RTMP olarak akış protokolleri kullanarak canlı akışlar alanını destekler. Merhaba RTMP alma Protokolü akış seçildiğinde, iki alma (giriş) uç noktaları için hello kanalı oluşturulur:

* **Birincil URL**: hello belirtir hello kanalın birincil RTMP tam URL'sini alma uç noktası.
* **İkincil URL** (isteğe bağlı): hello belirtir hello kanalın ikincil RTMP tam URL'sini alma uç noktası.

Tooimprove hello dayanıklılık ve hataya dayanıklılık, alma akış (yanı sıra Kodlayıcı yük devretme ve hataya dayanıklılık), isterseniz hello ikincil URL özellikle senaryoları aşağıdaki hello için kullanın:

- Tooboth birincil ve ikincil URL'leri çift Ftp'den tek Kodlayıcı:

    Merhaba ana amacı bu senaryo, daha fazla esneklik toonetwork dalgalanmaları ve sinyal tooprovide değil. Bazı RTMP kodlayıcılar işlemek olmayan ağ iyi bağlantısını keser. Bir ağ bağlantısının gerçekleştiğinde bir kodlayıcı kodlamayı durdurmak ve bir reconnect gerçekleştiğinde sonra hello arabelleğe alınan verileri göndermek. Bu discontinuities ve veri kaybına neden olabilir. Ağ bağlantısını keser hello Azure yan üzerinde hatalı ağ veya bakım nedeniyle oluşabilir. Birincil/ikincil URL'leri hello ağ sorunlarını azaltmak ve denetlenen bir yükseltme işlemi sağlar. Bir zamanlanmış ağ bağlantısının olduğunda, Media Services yönetir hello birincil ve ikincil bağlantısını keser ve bir Gecikmeli sağlayan her zaman iki hello arasında bağlantısını kesin. Kodlayıcılar sonra verileri gönderme zamanı tookeep sahip ve tekrar yeniden bağlayın. Merhaba Hello sırasını keser rastgele olabilir, ancak her zaman olacaktır bir gecikme birincil/ikincil ya da ikincil/birincil URL'ler arasında. Bu senaryoda, hello Kodlayıcı hello tek hata noktası hala işliyor.

- Tooa Ftp'den her Kodlayıcı ile birden çok kodlayıcılar noktası ayrılmış:

    Bu senaryoda, her iki Kodlayıcı sunar ve artıklık alma. Bu senaryoda, encoder1 toohello birincil URL iter ve encoder2 toohello ikincil URL iter. Bir kodlayıcı başarısız olduğunda, hello diğer Kodlayıcı veri göndermeye devam. Media Services hello birincil ve ikincil URL'lere kesmez olduğundan veri artıklığı korunabilir aynı anda. Bu senaryo Kodlayıcıları eşitlenen zamanı ve tam olarak sağlamak varsayar hello aynı veri.  

- Birden çok kodlayıcılar tooboth birincil ve ikincil URL'leri çift Ftp'den:

    Bu senaryoda, her iki kodlayıcılar veri tooboth birincil ve ikincil URL'leri iletin. Bu, veri artıklığı yanı sıra hello en iyi güvenilirlik ve hataya dayanıklılık sağlar. Bu senaryo iki Kodlayıcı hatalarına dayanabilir ve bir kodlayıcı çalışmayı durdurursa bile, bağlantısını keser. Kodlayıcılar eşitlenen zamanı ve tam olarak sağlamak varsayar hello aynı veri.  

Gerçek zamanlı kodlayıcılar RTMP hakkında daha fazla bilgi için bkz: [Azure Media Services RTMP desteği ve gerçek zamanlı kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).

#### <a name="ingest-urls-endpoints"></a>Alma URL'leri (Bitiş)
Bir giriş uç noktası bir kanal sağlar (URL alma) tooyour kanalları akışları hello Kodlayıcı gönderebilir şekilde hello gerçek zamanlı Kodlayıcı içinde belirtin.   

Merhaba alabilirsiniz hello kanal oluşturduğunuzda URL'lerini alabilirsiniz. Tooget bu URL'leri hello kanal toobe hello yok **çalıştıran** durumu. Veri toohello kanalı dağıtmaya hazır toostart olduğunuzda hello kanal hello olmalıdır **çalıştıran** durumu. Veri alma Hello kanal başladıktan sonra akışınızı hello Önizleme URL yoluyla önizleyebilirsiniz.

Parçalanmış MP4 alanını bir seçeneğiniz bir SSL bağlantısı üzerinden canlı akış (kesintisiz akış). SSL üzerinden tooingest URL tooHTTPS alma emin tooupdate hello olun. Şu anda, SSL üzerinden RTMP alma olamaz.

#### <a id="keyframe_interval"></a>Ana kare aralığı
Bir şirket içi gerçek zamanlı Kodlayıcı toogenerate Çoklu bit hızında akışa kullanırken hello ana kare aralığı olarak bu dış Kodlayıcı tarafından kullanılan resimleri (GOP) hello grubunun hello süresini belirtir. Gelen bu akış Hello kanal aldıktan sonra canlı akışınızı tooclient kayıttan yürütme uygulamaları herhangi bir biçimleri aşağıdaki hello sunabilir: kesintisiz akış, dinamik Uyarlamalı akış HTTP (DASH) ve HTTP canlı akışı (HLS) üzerinden. Canlı akış yaparken HLS her zaman dinamik olarak paketlenir. Varsayılan olarak, Media Services hello Canlı kodlayıcıdan alınan hello ana kare aralığı göre hello HLS segment paketleme oranı (kesim başına parça) otomatik olarak hesaplar.

Aşağıdaki tablonun hello hello kesim süresinin nasıl hesaplandığını gösterir:

| Ana kare aralığı | HLS segment paketleme oranı (FragmentsPerSegment) | Örnek |
| --- | --- | --- |
| Küçüktür veya eşittir too3 saniye |3:1 |KeyFrameInterval (veya GOP) 2 saniye ise, hello varsayılan HLS segment paketleme 3 too1 orandır. Bu, 6-ikinci HLS segment oluşturur. |
| 3 too5 saniye |2:1 |KeyFrameInterval (veya GOP) 4 saniye ise, hello varsayılan HLS segment paketleme 2 too1 orandır. Bu 8 saniyelik HLS segment oluşturur. |
| 5 saniyeden büyük |1:1 |KeyFrameInterval (veya GOP) 6 saniye ise, hello varsayılan HLS segment paketleme 1 too1 orandır. Bu, 6-ikinci HLS segment oluşturur. |

Merhaba kesim başına parçaları oranı yapılandırma hello kanalın çıkış ve ayarı ChannelOutputHls üzerinde FragmentsPerSegment değiştirebilirsiniz.

Ayrıca, üzerinde ChanneInput hello KeyFrameInterval özelliği ayarlanarak hello ana kare aralığı değeri değiştirebilirsiniz. Açıkça KeyFrameInterval ayarlarsanız, HLS segment paketleme oranı FragmentsPerSegment daha önce açıklanan hello kuralları hesaplanır hello.  

Açıkça KeyFrameInterval ve FragmentsPerSegment ayarlarsanız, Media Services ayarladığınız hello değerleri kullanır.

#### <a name="allowed-ip-addresses"></a>İzin verilen IP adresi
Toopublish video toothis kanalı izin hello IP adreslerini tanımlayabilirsiniz. İzin verilen IP adresi hello aşağıdakilerden biri olarak belirtilebilir:

* Tek bir IP adresi (örneğin, 10.0.0.1)
* Bir IP adresi ve CIDR alt ağ maskesi (örneğin, 10.0.0.1/22) kullanan bir IP aralığı
* Bir IP adresi ve noktalı ondalık alt ağ maskesine (örneğin, 10.0.0.1(255.255.252.0)) kullanan bir IP aralığı

Herhangi bir IP adresi belirtilir ve hiçbir kural tanımı yoksa hiçbir IP adresi izin verilir. tooallow herhangi bir IP adresi, bir kural oluşturun ve 0.0.0.0/0 olarak ayarlayın.

### <a name="channel-preview"></a>Kanal Önizleme
#### <a name="preview-urls"></a>Önizleme URL'leri
Kanalları toopreview kullanmak ve başka bir işleme ve teslimat önce akışınızı doğrulamak bir önizleme uç noktası (Önizleme URL) sunar.

Merhaba kanal oluşturduğunuzda hello Önizleme URL'sini alabilirsiniz. Tooget hello URL'si için hello toobe hello kanalı yok **çalıştıran** durumu. Veri alma Hello kanal başladıktan sonra akışınızın önizlemesini.

Şu anda hello Önizleme akış yalnızca parçalanmış MP4 içinde teslim edilebilir hello bakılmaksızın (kesintisiz akış) biçimi belirtilen giriş türü. Merhaba kullanabilirsiniz [kesintisiz akış sistem durumu İzleyicisi](http://smf.cloudapp.net/healthmonitor) player tootest hello kesintisiz akış. Hello Azure portal tooview akışınızı ayarına sahip bir oynatıcı de kullanabilirsiniz.

#### <a name="allowed-ip-addresses"></a>İzin verilen IP adresi
Tooconnect toohello Önizleme uç noktasını izin verilen hello IP adreslerini tanımlayabilirsiniz. Herhangi bir IP adresi belirtilmezse, herhangi bir IP adresine izin verilir. İzin verilen IP adresi hello aşağıdakilerden biri olarak belirtilebilir:

* Tek bir IP adresi (örneğin, 10.0.0.1)
* Bir IP adresi ve CIDR alt ağ maskesi (örneğin, 10.0.0.1/22) kullanan bir IP aralığı
* Bir IP adresi ve noktalı ondalık alt ağ maskesine (örneğin, 10.0.0.1(255.255.252.0)) kullanan bir IP aralığı

### <a name="channel-output"></a>Kanal çıktı
Merhaba kanallı çıkışı hakkında daha fazla bilgi için bkz [ana kare aralığı](#keyframe_interval) bölümü.

### <a name="channel-managed-programs"></a>Kanal yönetilen programlar
Bir kanal bir canlı akış toocontrol hello yayımlama ve depolama kesimleri kullanabilirsiniz programlarla ilişkilidir. Kanallar, programları yönetir. Merhaba kanal ve program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay çok benzer tootraditional medya ilişkidir.

İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz. Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Merhaba belirtilen sürede programları çalıştırabilir, ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her bir program akışı hello içeriği depolayan bir varlıkla ilişkilidir. Eşlenen tooa blok blob kapsayıcısında hello Azure depolama hesabı bir varlıktır ve bu kapsayıcıdaki blobları olarak hello varlık hello dosyalarında depolanır. toopublish hello program müşterilerinizin hello akış görebilecek şekilde hello ilişkili varlığa yönelik bir OnDemand Bulucu oluşturmanız gerekir. Bu konum belirleyicisi toobuild tooyour istemcileri sağlayabilen bir akış URL'si kullanabilirsiniz.

Bir kanal hello birden çok arşivini oluşturabilmesi için eşzamanlı olarak çalışan programlar, toothree destekler, aynı gelen akışın. Yayımlama ve gerektiğinde bir olayın farklı kısımlarını arşivleyin. Örneğin, iş gereksiniminiz bir programın, ancak toobroadcast yalnızca hello 6 saatlik tooarchive son 10 dakika olduğunu düşünün. tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir. Bir program tooarchive hello olay 6 saatlik ayarlanmış, ancak hello program yayımlanamaz. Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.

Yeni olaylar için mevcut programları yeniden kullanmamalısınız. Bunun yerine, her olay için yeni bir program oluşturun. Akışı ve arşivlemeyi hazır toostart olduğunuzda hello programını başlatın. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun.

Arşivlenen toodelete içerik durdurun ve hello programı silmek ve hello ilişkili varlığı silin. Bir program kullanıyorsa, bir varlık silinemiyor. Merhaba programın silinmesi gerekir.

Durdur ve hello programı silmek bile sonra hello varlık silene kadar kullanıcılar arşivlenen içeriğinizi, isteğe bağlı video olarak akışını sağlayabilirsiniz. Tooretain hello arşivlenen içeriği istiyor, ancak değil bulundurursunuz akış için Bulucu akış hello silin.

## <a id="states"></a>Kanal durumları ve faturalama
Bir kanal hello geçerli durumu için olası değerler şunlardır:

* **Durdurulmuş**: Bu hello ilk hello kanal oluşturulduktan sonra bir durumda. Bu durumda, hello kanal özellikleri güncelleştirildi ancak Akış verilmez.
* **Başlangıç**: hello kanal başladığını. Bu durum süresince güncelleştirmelere veya akışa izin verilmez. Bir hata oluşursa hello kanal toohello döndürür **durduruldu** durumu.
* **Çalışan**: hello kanal, Canlı akışlar işleyebilir.
* **Durdurma**: hello kanalı durduruldu. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.
* **Silme**: hello kanal siliniyor. Bu durum süresince güncelleştirmelere veya akışa izin verilmez.

Merhaba aşağıdaki tabloda nasıl kanal Haritası toohello fatura modu durumlarını gösterir.

| Kanal durumu | Portal UI göstergeleri | Faturalandırılmış mı? |
| --- | --- | --- | --- |
| **Başlatma** |**Başlatma** |Hayır (geçici durum) |
| **Çalışan** |**Hazır** (çalışan program yok)<p><p>or<p>**Akış** (en az bir çalışan program) |Evet |
| **Durdurma** |**Durdurma** |Hayır (geçici durum) |
| **Durduruldu** |**Durduruldu** |Hayır |

## <a id="cc_and_ads"></a>Kapalı açıklamalı alt yazı ve ad ekleme
Aşağıdaki tablonun hello desteklenen standartlar kapalı açıklamalı alt yazı ve reklam eklemeyi gösterir.

| Standart | Notlar |
| --- | --- |
| CEA 708 ve EIA 608 (708/608) |CEA 708 ve EIA 608 kapalı-açıklamalı alt yazı hello ABD ve Kanada için standartları.<p><p>Şu anda, açıklamalı alt yazı yalnızca hello kodlanmış Giriş akışı taşınan durumunda desteklenir. Toouse 608 veya 708 resim yazıları tooMedia Hizmetleri gönderildiğini hello kodlanmış akışında ekleyebilirsiniz bir canlı Medya Kodlayıcısı gerekir. Medya Hizmetleri eklenen resim yazıları tooyour görüntüleyiciler hello içerikle sunar. |
| TTML .ismt (metin parçaları kesintisiz akış) içinde |Media Services dinamik paketleme sağlar istemcileri toostream içeriğinizi biçimleri aşağıdaki hello hiçbirinde: DASH, HLS veya kesintisiz akış. Alma, ancak parçalanmış MP4 (kesintisiz akış) .ismt (metin parçaları kesintisiz akış) içinde resim yazıları ile kesintisiz akış istemcileri hello akış tooonly sunabilir. |
| SCTE-35 |SCTE-35 toocue reklam ekleme kullanılan dijital bir sinyal sistemidir. Aşağı Akış alıcıları hello sinyal toosplice reklam hello akışa zaman ayrılan hello için kullanın. SCTE-35 hello Giriş akışı formatta seyrek bir parçası olarak gönderilmelidir.<p><p>Şu anda ad sinyalleri taşıyan yalnızca desteklenen hello Giriş akışı biçimi parçalanmış MP4 (kesintisiz akış). yalnızca desteklenen hello çıktı da kesintisiz akış biçimidir. |

## <a id="considerations"></a>Dikkat edilecek noktalar
Bir şirket içi gerçek zamanlı Kodlayıcı toosend Çoklu bit hızlı akış tooa kanal kullanırken aşağıdaki kısıtlamalar hello Uygula:

* Noktaları alma yeterli boş Internet bağlantısı toosend veri toohello olduğundan emin olun.
* Alma URL'si ikincil kullanarak ek bant genişliği gerektirir.
* Merhaba gelen Çoklu bit hızında akışa en fazla 10 video kalitesini düzeyleri (katman) ve en fazla 5 ses izleri olabilir.
* Hello en yüksek ortalama hızı herhangi hello video kalitesini düzeylerinin 10 MB/sn olmalıdır.
* Merhaba hello tüm hello video ve ses akışları için ortalama bit hızları toplamını 25 MB/sn olmalıdır.
* Merhaba kanal hello giriş protokolünü değiştiremezsiniz veya ilişkili programları çalışmıyor. Farklı protokollere ihtiyacınız varsa her bir giriş protokolü için farklı bir kanal oluşturmalısınız.
* Tek bit hızlı, kanalda işleyebilen. Ancak hello kanal hello akış işlemez çünkü hello istemci uygulamaları tek bit hızlı akış de alırsınız. (Bu seçenek öneririz yoktur.)

Diğer konular ilgili tooworking kanalları ve ilgili bileşenler şunlardır:

* Merhaba gerçek zamanlı Kodlayıcı yeniden her zaman hello çağrısı **sıfırlama** hello kanalda yöntemi. Merhaba kanal sıfırlamadan toostop hello program sahip. Merhaba kanalı sıfırladıktan sonra hello programını yeniden başlatın.
* Bir kanal yalnızca hello olduğunda durdurulabilir **çalıştıran** durumunu ve tüm programlar hello kanalda durduruldu.
* Varsayılan olarak, yalnızca 5 kanalları tooyour Media Services hesabı ekleyebilirsiniz. Daha fazla bilgi için bkz: [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).
* Yalnızca, kanal hello olduğunda faturalandırılır **çalıştıran** durumu. Daha fazla bilgi için toohello başvuran [kanal durumları ve faturalama](media-services-live-streaming-with-onprem-encoders.md#states) bölümü.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>Geri Bildirim
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>İlgili konular
[Azure Media Services parçalanmış MP4 Canlı belirtimi alma](media-services-fmp4-live-ingest-overview.md)

[Azure Media Services genel bakış ve yaygın senaryolar](media-services-overview.md)

[Media Services kavramları](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
