---
title: "aaaAvanced Medya Kodlayıcısı Premium iş akışı öğreticileri"
description: "Bu belgeyi nasıl tooperform Gelişmiş Medya Kodlayıcısı Premium akışıyla görevleri göster talimatları içerir ve ayrıca nasıl iş akışı Tasarımcısı ile toocreate karmaşık iş akışları."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Gelişmiş Medya Kodlayıcısı Premium iş akışı öğreticileri
## <a name="overview"></a>Genel Bakış
Bu belge göster izlenecek yollar içeriyor nasıl toocustomize iş akışlarıyla **iş akışı Tasarımcısı**. Gerçek iş akışı dosyalarını hello bulabilirsiniz [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>İÇİNDEKİLER
Aşağıdaki konularda hello ele alınmaktadır:

* [Tek bit hızlı MP4 MXF kodlama](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Yeni bir iş akışı başlatma](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Merhaba ortam dosyası girişi kullanma](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Medya akışlarının inceleniyor](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Bir video Kodlayıcısı için ekleniyor. MP4 dosyası oluşturma](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Kodlama hello ses akışı](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Ses ve Video akışları bir MP4 kapsayıcıya çoğullama](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Merhaba MP4 dosyası yazılıyor](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Bir Media Services varlık hello çıktı dosyası oluşturma](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [İş akışı yerel olarak test hello tamamlandı](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [MXF MP4s - multibitrate kodlama etkin dinamik paketleme](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Bir veya daha fazla ek MP4 çıktı ekleme](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Yapılandırma hello dosya çıkış adları](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Ayrı bir ses izi ekleme](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Merhaba ekleniyor. ISM SMIL dosyası](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [MP4 - Gelişmiş şeması multibitrate MXF kodlama](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [İş akışı genel bakış tooenhance](#workflow-overview-to-enhance)
  * [Dosya adlandırma kuralları](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Yayımlama hello iş akışı kök üzerine bileşeni özellikleri](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Çıktı dosyası adları yayımlanan özellik değerlerine dayanan oluşturulmasını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Küçük resimleri toomultibitrate MP4 çıktı ekleme](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [İş akışı genel bakış tooadd küçük resim](#workflow-overview-to-add-thumbnails-to)
  * [JPG kodlama ekleme](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Renk alanını dönüştürme postalarla](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Yazma hello küçük resimleri](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Bir iş akışında hataları algılama](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Tamamlanmış iş akışı](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Zamana bağlı kırpma multibitrate MP4 çıktı](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [İş akışı genel bakış toostart kırpma için ekleme](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Merhaba akış Kırpıcıyı kullanma](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Tamamlanmış iş akışı](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Merhaba Script bileşeni Tanıtımı](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Bir iş akışı içinde komut dosyası: Merhaba Dünya](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Çerçeve tabanlı kırpma multibitrate MP4 çıktı](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Genel Bakış toostart kırpma için ekleme şeması](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Merhaba küçük liste XML kullanma](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Komut dosyası bir bileşenin Hello küçük listesini değiştirme](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [ClippingEnabled kolaylık özellik ekleme](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Tek bit hızlı MP4 MXF kodlama
Bu kılavuzda tek bit hızlı oluşturacağız. MP4 dosyası AAC-HE ile kodlanmış ses öğesinden bir. MXF giriş dosyası.

### <a id="MXF_to_MP4_start_new"></a>Yeni bir iş akışı başlatma
İş Akışı Tasarımcısı'nı açın ve "Dosyası"-"Yeni çalışma alanı"-"kodlamasını şeması" seçin

Merhaba yeni iş akışı 3 öğeleri gösterir:

* Birincil kaynak dosyası
* Küçük resim listesi XML'i
* Çıkış dosyası/varlık  

![Yeni bir kodlama iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Yeni bir kodlama iş akışı*

### <a id="MXF_to_MP4_with_file_input"></a>Merhaba ortam dosyası girişi kullanma
Sipariş tooaccept bizim giriş medya dosyasını bir medya dosyası giriş bileşeni ekleme ile başlar. tooadd bileşen toohello iş akışı hello deposu arama kutusuna aramanız ve istenen hello girişi hello Tasarımcı bölmesine sürükleyin. Bunu hello medya dosyası giriş yapmak ve hello birincil kaynak dosya bileşen toohello Filename giriş PIN hello medya dosyası giriş bağlanın.

![Bağlı ortam giriş dosyası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Bağlı ortam giriş dosyası*

Başka bir çok yapabiliriz önce biz öncelikle tooindicate toohello iş akışı Tasarımcısı hangi örnek dosya gerekir toouse toodesign isteriz bizim iş akışıyla. Bu nedenle, toodo hello Tasarımcı bölmesinde arka plan tıklatın ve hello birincil kaynak dosyası özelliği hello sağ özellik bölmesinde için arayın. Merhaba klasör simgesine ve istenen select hello dosya tootest hello akışıyla'ı tıklatın. Bu yapılır hemen hello medya dosyası giriş bileşen hello dosyasını inceleyin ve onu Denetlenmekte kendi çıktı PIN'ler tooreflect hello dosyasını doldurun.

![Doldurulan ortam giriş dosyası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Doldurulan ortam giriş dosyası*

Bu ne ile toowork isteriz giriş ile belirtir, ancak bunu bildirmez henüz kodlanmış hello çıktı için nereye. Birincil kaynak dosya yapılandırılan benzer toohow hello şimdi hello hemen altındaki çıkış klasörü değişken özelliğini yapılandırın.

![Yapılandırılan giriş ve çıkış özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Yapılandırılan giriş ve çıkış özellikleri*

### <a id="MXF_to_MP4_streams"></a>Medya akışlarının inceleniyor
Genellikle nasıl hello akış gibi göründüğünü tooknow hello iş akışı akar istendiğini. tooinspect hello iş akışında, herhangi bir noktada bir akış, bir çıkış veya giriş PIN hello bileşenleri hiçbirinde yalnızca tıklatın. Bu durumda, hello sıkıştırılmamış Video Çıkış PIN bizim medya dosyası girişten gelen tıklayarak deneyin. Bir iletişim kutusu tooinspect hello giden video sağlayan açılır.

![İnceleme hello sıkıştırılmamış Video Çıkış PIN](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*İnceleme hello sıkıştırılmamış Video Çıkış PIN*

Örneğimizde, bize örneğin biz 4 saniyede 24 kare konumundaki 1920 x 1080 giriş ile ilgilenen olduğunu söyler: 2:2 örnekleme neredeyse 2 dakikalık video.

### <a id="MXF_to_MP4_file_generation"></a>Bir video Kodlayıcısı için ekleniyor. MP4 dosyası oluşturma
Şimdi unutmayın, sıkıştırılmamış bir Video ve birden çok sıkıştırılmamış ses çıkış PIN bizim ortam dosyası girişi üzerinde kullanılabilir. Sipariş tooencode içinde gelen video Merhaba, kodlama bileşeni - bu durumda oluşturmak için ihtiyacımız. Mp4 dosyaları.

tooencode video akışına tooH.264 Merhaba, hello AVC Video Kodlayıcısı bileşen toohello Tasarımcı yüzeyine ekleyin. Bu bileşen uncompress video akışına giriş olarak alır ve bir AVC sıkıştırılmış video akışı kendi çıktı PIN sunar.

![Bağlantısız AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Bağlantısız AVC kodlayıcı*

Özelliklerini nasıl hello kodlama tam olarak gerçekleştiğini belirleyin. Şimdi hello bazıları bakma sahip daha önemli ayarları:

* Çıktı genişlik ve yükseklik çıktı: Bu kodlanmış hello videonun hello çözümü belirleyebilirsiniz. Örneğimizde 640 x 360 ile edelim
* Kare hızı: yalnızca kümesi toopassthrough benimsemeye hello kaynak kare hızı olası toooverride yine de bu olur. Böyle kare hızı dönüştürme değil hareket-dengelendi olduğunu unutmayın.
* Profil ve düzeyi: Bunlar hello AVC profil ve düzeyini belirler. tooconveniently daha fazla bilgi alın hello farklı düzeylerde ve profilleri hakkında hello AVC Video Kodlayıcısı bileşen hello soru işareti simgesine tıklayın ve hello Yardım sayfası, her bir hello düzeyleri hakkında daha fazla ayrıntı gösterir. Bizim örnek için 3.2 (Merhaba varsayılan) düzeyinde ana profille edelim.
* Denetim modu, bit hızı (kbps) oranı: biz opt Senaryomuzda 1200 KB/sn ile çıkış sabit hızı (CBR) için
* Görüntü biçimi: Bu hello hello H.264 akışa yazılan (Video kullanılabilirlik bilgileri) VUI hakkındadır (bir kod çözücü tooenhance hello görünen ancak temel toocorrectly tarafından kullanılıyor olabilir yan bilgi kod çözme):
* NTSC (ABD veya Japonya, 30 fps kullanma için tipik)
* PAL (25 fps kullanarak Avrupa için tipik)
* GOP boyutu modu: 2 saniye kapalı GOPs ile bir anahtar aralığı ile bizim amacıyla sabit GOP boyutu yapılandıracağız. Bu, dinamik paketleme Azure Media Services sağlar hello ile uyumluluk sağlar.

toofeed bizim AVC Kodlayıcı hello sıkıştırılmamış Video Çıkış PIN hello medya dosyası giriş bileşen toohello sıkıştırılmamış Video giriş PIN hello AVC kodlayıcıdan bağlayın.

![Bağlı AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Bağlı AVC ana kodlayıcı*

### <a id="MXF_to_MP4_audio"></a>Kodlama hello ses akışı
Bu noktada, biz video kodlanmıştır ancak hello özgün sıkıştırılmamış ses akışı hala sıkıştırılmış toobe gerekiyor. Bunun için AAC Kodlayıcı (Dolby) bileşeni tarafından hello kodlama AAC ile gidersiniz. Toohello iş akışı ekleyin.

![Bağlantısız AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Bağlantısız AAC kodlayıcı*

Bir uyumsuzluk şimdi: büyük olasılıkla hello medya dosyası giriş iki farklı olacaktır fazlasını ses akışı kullanılabilir sıkıştırılmamış sırasında yalnızca bir tek sıkıştırılmamış ses giriş PIN hello AAC Kodlayıcı gelen olduğu: sol ses kanal ve hello için bir başlangıç için bir tane Sağa. (Surround sesle ele alma, 6 kanalları olmasıdır.) Olası değil toodirectly bağlanın hello ses hello medya dosyası giriş kaynağından hello AAC ses Kodlayıcı. Merhaba AAC bileşen bekliyor sözde "araya eklemeli" ses akışı: her ikisi de sahip tek bir akış hello birbirleri ile araya eklemeli sola ve hello sağ kanallar. Bizim kaynak medya dosyasından biliyoruz sonra hangi ses izleri hello kaynağındaki hangi konumuna biz hello olan araya eklemeli gibi ses akış doğru bir şekilde oluşturabilmesi sol ve sağ için Konuşmacı konumlarına atanır.

Önce bir toogenerated bir araya eklemeli gerekli hello kaynak ses kanalları akıştan isteyeceksiniz. Merhaba ses akışı ayırıcı bileşen bu bize işleyecek. Toohello iş akışını Ekle ve hello ses çıkış hello ortam dosyası girişi içine bağlayın.

![Ses akışı ayırıcı bağlı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Ses akışı ayırıcı bağlı*

Bir araya eklemeli ses akışını sahibiz, hala olduğu için tooassign hello sola veya sağa Konuşmacı konumlandırır belirttiğimiz alamadık. Toospecify Bu sipariş, biz hello Konuşmacı konumu Assigner yararlanabilirsiniz.

![Konuşmacı konumu Assigner ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Konuşmacı konumu Assigner ekleme*

Merhaba Konuşmacı konumu Assigner kullanmak için bir kodlayıcı önceden Filtresi "Özel" olan stereo giriş akış yapılandırmak ve "2.0 (M, R)" adlı kanal önceden hello. (Bu hello sol Konuşmacı konumu toochannel 1 ve hello sağ Konuşmacı konumu toochannel 2 atayacaktır.)

Merhaba Konuşmacı konumu Assigner toohello girişi hello AAC Kodlayıcı Hello çıkışına bağlayın. Ardından, bir "2.0 ile (M, R)" Merhaba AAC Kodlayıcı toowork söyleyin kanal stereo ses giriş olarak ile toodeal bilmesi için hazır.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Ses ve Video akışları bir MP4 kapsayıcıya çoğullama
Bizim AVC belirli bir ses akışını kodlanmış video akışına ve bizim AAC kodlanmış, biz içine yakalamak için bir. MP4 kapsayıcı. farklı akışları tek bir karıştırma işleminin hello "çoğullama" (veya "muxing") adı verilir. Bu durumda biz hello ses ve video akışları tek bir tutarlı hello Interleaving. MP4 paketi. Bu düzenler hello bileşen bir. MP4 kapsayıcı hello ISO MPEG-4 çoğaltıcı adı verilir. Bir toohello Tasarımcı yüzeyine eklemek ve hem hello AVC Video Kodlayıcısı hem de hello AAC Kodlayıcı tooits girişleri bağlanın.

![Bağlı MPEG4 çoğaltıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Bağlı MPEG4 çoğaltıcı*

### <a id="MXF_to_MP4_writing_mp4"></a>Merhaba MP4 dosyası yazılıyor
Bir çıkış dosyası yazılırken hello dosya çıktısı bileşeni kullanılır. Böylece çıktısını toodisk yazılmış Biz bu hello ISO MPEG-4 çoğaltıcı toohello çıktısını bağlanabilir. toodo bunu hello kapsayıcı (MPEG-4) çıkış PIN toohello yazma giriş PIN hello dosya çıktısı bağlanın.

![Dosya çıktısı bağlı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Dosya çıktısı bağlı*

kullanılacak hello filename hello dosya özelliği tarafından belirlenir. Bu özellik sabit kodlanmış tooa değeri verildiğinde olabilirler, ancak büyük olasılıkla bir tooset istediğiniz bir ifade üzerinden yerine.

toohave hello iş akışı otomatik olarak belirlemek hello çıkış dosya adı bir ifade özelliğinden, hello düğme sonraki toohello dosya adına tıklayın (sonraki toohello klasör simgesine). Merhaba gelen açılır menü sonra "İfadesi"'i seçin. Bu hello ifade Düzenleyicisi çıkarır. Merhaba Düzenleyicisi Merhaba içeriğine ilk temizleyin.

![Boş ifade Düzenleyicisi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Boş ifade Düzenleyicisi*

Merhaba ifade Düzenleyicisi tooenter ile bir veya daha fazla değişken karma herhangi bir sabit değere izin verir. Değişkenleri dolar işareti başlatın. Merhaba $ tuşuna basın, hello Düzenleyicisi açılan kutusundan bir seçenek ile kullanılabilen değişkenlerin gösterecektir. Örneğimizde hello çıktı dizini değişken ve hello temel giriş dosyası adı değişkeni bileşimini kullanacağız:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![İfade Düzenleyicisi çıkışı dolu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*İfade Düzenleyicisi çıkışı dolu*

> [!NOTE]
> Sırayla toosee Azure kodlama işinin bir çıktı dosyasına bakın, hello ifade Düzenleyicisi'nde bir değer sağlamanız gerekir.
>
>

Tamam basarsa tarafından hello ifade onayladığınızda hello özellik penceresi toowhat değeri hello dosya özelliği çözümler bu anda önizlemede.

![Çıktı dizini dosyası ifadesini çözümler](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Çıktı dizini dosyası ifadesini çözümler*

### <a id="MXF_to_MP4_asset_from_output"></a>Bir Media Services varlık hello çıktı dosyası oluşturma
Biz bir MP4 çıktı dosyası yazılmış olsa da, hala tooindicate ihtiyacımız bu dosyanın toohello ait çıktı varlık hangi media services, bu iş akışı yürütmenin sonucu olarak üretir. toothis son, hello çıktı dosyası/varlık düğümü hello iş akışı tuval üzerinde kullanılır. Bu düğüm tüm gelen dosyalarıyla hello sonuç Azure Media Services varlık parçası hale getirir.

Merhaba dosya çıktısı bileşen toohello çıktı dosyası/varlık bileşeni toofinish hello iş akışı bağlayın.

![Tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Tamamlanmış iş akışı*

### <a id="MXF_to_MP4_test"></a>İş akışı yerel olarak test hello tamamlandı
tootest hello iş akışı yerel olarak hello araç çubuğunda hello üstünde hello YÜRÜT düğmesine basın. Merhaba iş akışı yürütme tamamlandığında, yapılandırılmış hello çıkış klasöründe oluşturulan hello çıkış inceleyin. Merhaba MXF giriş kaynağı dosyasından kodlanan MP4 çıktı dosyası hello tamamlandı görürsünüz.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Dinamik paketleme etkin MP4 - multibitrate MXF kodlama
Bu kılavuzda Çoklu bit hızlı MP4 dosyaları kümesini kodlanmış AAC ile tek bir ses oluşturacağız. MXF giriş dosyası.

Ne zaman Çoklu bit hızlı varlık çıkış birlikte kullanmak için Azure Media Services, birden çok GOP hizalı MP4 dosyaları her farklı bit hızı ve çözüm oluşturulan toobe gerekir tarafından sunulan hello dinamik paketleme özelliklerle istendiğini. Bu nedenle, toodo hello [kodlama MXF tek bit hızlı MP4 içine](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) izlenecek bize iyi bir başlangıç noktası sağlar.

![İş akışı başlatma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*İş akışı başlatma*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Bir veya daha fazla ek MP4 çıktı ekleme
Sonuçta elde edilen bizim Azure Media Services varlık her MP4 dosyasında farklı bit hızı ve çözüm destekleyecektir. Bir veya daha fazla MP4 çıktı dosyaları toohello iş akışı ekleyelim.

toomake emin sahibiz bizim video Kodlayıcıları oluşturulan ile tüm Merhaba aynı ayarları, buna ait en kolay tooduplicate zaten mevcut olan AVC Video Kodlayıcısı hello ve çözünürlük ve bit hızı başka bir bileşimini yapılandırın (şimdi 960 x 540 birini sırasında saniye başına 25 çerçeveleri ekleyin 2,5 Mbps). tooduplicate hello varolan Kodlayıcı, kopyalama yapıştırın, hello Tasarımcı yüzeyine.

Merhaba sıkıştırılmamış Video Çıkış PIN hello ortam dosyası girişi bizim yeni AVC bileşen içine bağlayın.

![Bağlı ikinci AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Bağlı ikinci AVC kodlayıcı*

Şimdi bizim yeni AVC Kodlayıcı toooutput 960 x 540 2,5 Mbps hızında hello yapılandırmasını uyarlayın. (Çıktı özellikleri "genişliğini", "Çıktı yükseklik" ve "Bit hızı (kbps)" Bu için kullanın.)

Verilen Azure Media Services dinamik paketleme ile birlikte toouse hello ortaya çıkan varlık istiyoruz, akış uç noktası hello toobe bu MP4 dosyalarını tam olarak hizalanmış tooeach bir yolla diğer olan HLS/parçalanmış MP4/DASH parçaları oluşturma yeteneği gerekiyor farklı bit arasında geçiş istemcileri tek sorunsuz bir sürekli video ve ses deneyim olduğunu alın. durum, her iki AVC kodlayıcılar hello özelliklerinde hello hem MP4 dosyaları için GOP ("grubu") resimlerin boyutu ayarlamak, tooensure ihtiyacımız toomake tarafından yapılan too2 saniye:

* Merhaba GOP boyutu modu tooFixed GOP boyutunu ayarlama ve
* Merhaba anahtar çerçeve aralığı tootwo saniye sayısı.
* Ayrıca hello tüm GOP's duran GOP IDR denetim tooClosed GOP tooensure olmadan kendi bağımlılıkları ayarlayın

toomake bizim iş akışı uygun toounderstand hello ilk AVC Kodlayıcı çok yeniden adlandırma "AVC Video Kodlayıcısı 640 x 360 1200kbps" ve ikinci AVC Kodlayıcı hello "AVC Video Kodlayıcısı 960 x 540 2500 kbps".

İkinci bir ISO MPEG-4 çoğaltıcı ve ikinci bir dosya çıktısı. Şimdi ekleyin. Merhaba çoğaltıcı toohello yeni AVC Kodlayıcı bağlanmak ve çıktısını dosya çıktısı hello yönlendirilir emin olun. Merhaba AAC ses Kodlayıcı çıkışı toohello yeni da bağlanabilirken çoğaltıcı 's giriş. Merhaba dosya çıktısı sırayla sonra olabilir bağlı toohello çıktı dosyası/varlık düğümü tooadd onu toohello oluşturulacak Media Services varlık.

![Bağlı ikinci Karıştırıcı ve dosya çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Bağlı ikinci Karıştırıcı ve dosya çıktısı*

Azure Media Services dinamik paketleme ile uyumluluk için hello çoğaltıcı 's öbek modu tooGOP sayısı veya süreyi yapılandırın ve Öbek too1 başına hello GOPs ayarlayın. (Bu hello varsayılan olmalıdır.)

![Karıştırıcı öbek modları](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Karıştırıcı öbek modları*

Not: Bu işlem diğer bit hızı ve toohello varlık çıktı toohave istediğiniz birleşimler eklenen çözümleme için toorepeat isteyebilirsiniz.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Yapılandırma hello dosya çıkış adları
Birden fazla tek dosyalı eklenen toohello çıkış varlığına sunuyoruz. Bu, dosya adlarını her hello dosyaları birbirinden farklıdır ve belki de ile ilgilenen hello dosya adından açık olacak şekilde bile dosya adlandırma kuralını uygula çıkış gerek toomake emin bir hello sağlar.

Çıkış dosya adlandırma hello Tasarımcısı'nda ifadeler ile denetlenebilir. Merhaba dosya çıktısı bileşenlerden biri için Hello özelliği bölmesini açın ve hello dosya özelliği için hello ifade Düzenleyicisi'ni açın. Bizim ilk çıkış dosyası ifade aşağıdaki hello yapılandırılmış (gelen gitmek için hello öğretici bkz [MXF tooa tek bit hızlı MP4 çıktı](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Bu bizim filename iki değişken tarafından belirlenir anlamına gelir: hello çıktı dizini toowrite içinde ve hello kaynak dosya temel adı. Merhaba eski hello iş akışı kök bir özellik olarak sunulur ve ikinci hello hello gelen dosyası tarafından belirlenir. Yerel test etmek için kullanmak, hello çıktı dizini olduğuna dikkat edin; Azure Media Services hello bulut tabanlı media işlemcisi tarafından Hello iş akışı çalıştırıldığında bu özellik hello iş akışı altyapısı tarafından geçersiz kılınacaktır.
Bizim çıkış adlandırma tutarlı çıktı dosyaları toogive hem, değişiklik hello ilk adlandırma ifade dosya:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

ve için ikinci hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Her iki MP4 çıktı dosyaları düzgün şekilde oluşturulan emin toomake bir ara testi yürütün.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Ayrı bir ses izi ekleme
Biz bir .ism dosyası toogo bizim MP4 çıktı dosyalarıyla oluştururken daha sonra anlatıldığı gibi biz de yalnızca ses MP4 dosyası hello ses parçası bizim Uyarlamalı akış için gerektirir. toocreate bu dosya, bir ek Karıştırıcı toohello iş akışı (ISO-MPEG-4 çoğaltıcı) ekleyip hello AAC Kodlayıcı'nın çıkış PIN kendi giriş PIN ile İzle 1 için bağlandığınızda.

![Ses karıştırıcı eklendi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Ses karıştırıcı eklendi*

Üçüncü bir dosya çıktısı bileşen toooutput hello giden akış hello Karıştırıcı oluşturun ve hello dosya adlandırma ifade olarak yapılandırın:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Ses karıştırıcı dosya çıktısı oluşturma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Ses karıştırıcı dosya çıktısı oluşturma*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Merhaba ekleniyor. ISM SMIL dosyası
Merhaba dinamik paketleme toowork birlikte her iki MP4 dosyaları (ve yalnızca ses MP4 hello) bizim Media Services varlık da bildirim dosyası ihtiyacımız ("SMIL" dosyası olarak da bilinir: eşitlenmiş multimedya tümleştirme dil). Bu dosya, hangi MP4 dosyaları dinamik paketleme ve bu tooconsider hello ses akış için hangisinin kullanılabilir tooAzure Media Services gösterir. Kümesiyle tek bir ses akışını MP4'ın için tipik bir bildirim dosyası şuna benzer:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

switch deyimi içinde bir başvuru tooeach hello tek tek MP4 video dosyaları Hello .ism dosyası içerir ve ayrıca toothose ayrıca bir (veya daha fazla) ses dosyası tooan yalnızca hello ses içeren MP4 başvurur.

Bizim MP4'ın kümesi oluşturma hello bildirim dosyası hello "AMS bildirim Yazan" adında bir bileşen ile yapılabilir. toouse, hello yüzeyine sürükleyin ve hello "Yazma tamamlandı" çıktı pini hello üç dosya çıktısı bileşenleri toohello AMS bildirim giriş yazan bağlanın. Ardından hello AMS bildirim yazan toohello çıktı dosyası/varlık emin tooconnect hello çıkışını yapın.

Bizim diğer bileşenlerle dosya çıktı olarak, hello .ism dosyası çıktı adı bir ifade ile yapılandırın:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Bizim tamamlanmış iş akışı hello aşağıdaki gibi görünür:

![Tamamlanmış MXF toomultibitrate MP4 akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Tamamlanmış MXF toomultibitrate MP4 akışı*

## <a id="MXF_to__multibitrate_MP4"></a>MP4 - Gelişmiş şeması multibitrate MXF kodlama
Merhaba, [önceki iş akışı Kılavuzu](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) nasıl tek bir MXF giriş varlık bir çıktı varlığa Çoklu bit hızlı MP4 dosyaları, bir yalnızca ses MP4 dosyası ve Azure medya ile birlikte kullanmak için bir bildirim dosyası ile dönüştürülebilir gördük Dinamik paketleme Hizmetleri.

Bu kılavuzda nasıl bazı hello yönlerinden geliştirilebilen ve daha kullanışlı hale gösterir.

### <a id="MXF_to_multibitrate_MP4_overview"></a>İş akışı genel bakış tooenhance
![Multibitrate MP4 akışı tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 akışı tooenhance*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Dosya adlandırma kuralları
Hello önceki iş akışında hello temel çıktı dosyası adları oluşturmak için basit bir ifade belirtildi. Bazı çoğaltma yine de sunuyoruz: hello hello tek tek çıktı dosyası bileşenlerinin tümünü böyle ifade belirtildi.

Örneğin, bizim dosya çıktı bileşen hello ilk video dosyası için bu ifade ile yapılandırılır:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Merhaba ikinci çıktı için sırada video, biz gibi bir ifadeye sahip:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Hata daha az yatkın ve biz Bu çoğaltma bazılarını kaldırın ve şeyleri daha yapılandırılabilir yerine yaparsanız daha kullanışlı temizleyici olmaz mıydı? Luckily geçebiliriz: hello tasarımcının ifade özellikleri hello özelliği toocreate özel özellikler bizim iş akışı kök ile birlikte, kolaylık eklenen bir katmanı bize verir.

Biz filename yapılandırma hello tek tek MP4 dosyaları hello bit sürücü varsayalım. Bir orta tooconfigure hedeflenir bu bit burada erişilen tooconfigure ve sürücü dosya adı oluşturma olacak gelen (Merhaba kökünde bizim grafiği) yerleştirin. toodo bunu hello AVC kodlayıcılar hem de her iki hello kökünden erişilebilir hale hello bit hızı bizim iş akışı, her iki AVC kodlayıcılar toohello kökündeki özelliğinden yayımlayarak başlatın. (İki farklı noktayı kaçırmadığınızdan görüntülenen olsa bile, yalnızca bir temel alınan değer yoktur.)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Yayımlama hello iş akışı kök üzerine bileşeni özellikleri
Merhaba ilk AVC Kodlayıcı açın, toohello bit hızı (kbps) özelliği gidin ve yayımlama hello aşağı açılır listeden seçin.

![Yayımlama hello bit hızı özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Yayımlama hello bit hızı özelliği*

Merhaba yapılandırma Itanium tabanlı sistemler için iletişim toopublish toohello kök bizim iş akışı grafiğinin yayımlanan adını "video1bitrate" ve "Video 1 bit hızı" okunabilir görünen adını ile yayımlayın. Özel bir yapılandırma grup adı "Bit akış" olarak adlandırılan ve yayımlama basın.

![Yayımlama hello bit hızı özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Bit hızı özelliği için yayımlama iletişim kutusu*

Yineleme hello hello hello bit hızı özelliği için aynı ikinci AVC Kodlayıcı ve "Video 2 bit hızı" ile bir görünen ad "video2bitrate" adı, hello özel aynı "Akış bit" Grup.

Biz şimdi hello iş akışı kök özelliklerini inceleme, iki yayımlanan özellikleri görünmesini hello özel bizim grubuyla göreceğiz. Her ikisi de kendi ilgili AVC Kodlayıcı hızı hello değerini yansıtma.

![İş akışı kök yayımlanan bit hızı özellik](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Tooaccess bu özellikleri kodu veya bir ifade istediğinizde biz bunu şu şekilde yapabilirsiniz:

* Satır içi kodundan hemen hello kökü altındaki bir bileşenin: node.getPropertyAsString('.. / video1bitrate', null)
* bir ifade içinde: ${ROOT_video1bitrate}

Şimdi de bizim ses izleme hızı üzerindeki yayımlayarak hello "Akış bit" grubu tamamlayın. Merhaba AAC Kodlayıcı hello özellikleri içinde hello bit hızı ayarı arayın ve yayımlama hello açılır sonraki tooit seçin. Yayımlama hello grafik adı "audio1bitrate" ile toohello kökündeki ve görünen ad "Ses 1 bit hızı" bizim özel gruptaki "Akış bit".

![Ses bit hızı için yayımlama iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Ses bit hızı için yayımlama iletişim kutusu*

![Sonuçta elde edilen video ve ses özellik kök](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Sonuçta elde edilen video ve ses özellik kök*

Bu üç hiçbirini değiştirme değerleri de yeniden yapılandırır ve değişiklikleri hello bunlar bağlı ile Merhaba ilgili bileşenler değerlerine unutmayın (ve bir yayımlandığı yerlerde).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Çıktı dosyası adları yayımlanan özellik değerlerine dayanan oluşturulmasını
Cmdlet'e kod yerine bizim oluşturulan dosya adları, biz şimdi bizim filename ifade her hello dosya çıktısı bileşenleri toorely biz yalnızca hello grafik kökünde yayımlanan hello bit hızı özellikleri değiştirebilirsiniz. Bizim ilk dosya çıktı ile başlayarak, hello dosya özelliğini bulun ve bu gibi hello ifadeyi düzenleyin:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

Bu ifadede Hello farklı parametreler erişilen ve hello dolar işareti penceresinde hello ifade ederken hello klavyede basarsa tarafından girdiniz. Merhaba kullanılabilir parametrelerden biri, daha önce yayımlanan bizim video1bitrate özelliğidir.

![Bir ifade içinde Parametreler erişme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Bir ifade içinde Parametreler erişme*

Bizim ikinci video hello dosyası çıktısı için aynı hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

ve hello salt ses dosyası çıktısı için:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Biz şimdi hello bit hızı herhangi hello video veya ses dosyalarını değiştirirseniz, hello ilgili Kodlayıcı yeniden yapılandırılması ve hello bit hızı tabanlı bir dosya adı kuralı tüm otomatik olarak kullanılacaktır.

## <a id="thumbnails_to__multibitrate_MP4"></a>Küçük resimleri toomultibitrate MP4 çıktı ekleme
Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi küçük resimleri toohello çıkış ekleme içine arayacaktır.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>İş akışı genel bakış tooadd küçük resim
![Gelen Multibitrate MP4 akışı toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Gelen Multibitrate MP4 akışı toostart*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>JPG kodlama ekleme
Bizim küçük resim oluşturma Hello Kalp hello JPG Kodlayıcı bileşeni mümkün toooutput JPG dosyaları olacaktır.

![JPG kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*JPG kodlayıcı*

Ancak doğrudan sunduğumuz sıkıştırılmamış Video akışı hello ortam dosyası girişi hello JPG Kodlayıcı içine gelen bağlanamıyoruz. Bunun yerine, tek tek çerçeveler toobe karmalayan bekliyor. Bu, hello Video çerçeve kapısı bileşen ile yapabiliriz.

![Bir çerçeve kapısı toohello JPG Kodlayıcısı bağlanma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Bir çerçeve kapısı toohello JPG Kodlayıcısı bağlanma*

Her çok fazla sayıda saniye veya çerçeveler olanak sağlayan bir kez video çerçeve toopass hello çerçeve kapısı. hangi böyle ile uzaklığı hello aralığı ve hello hello özelliklerinde yapılandırılabilir saattir.

![Video çerçeve kapısı özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Video çerçeve kapısı özellikleri*

Şimdi hello modu tooTime (saniye) ayarlayarak dakikada küçük resim oluşturma ve aralığı too60 hello.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Renk alanını dönüştürme postalarla
Mantıksal göründüğü sırada hem sıkıştırılmamış Video PIN'ler hello çerçeve kapısı ve hello ortam dosyası girişi şimdi bağlanabilir, biz bunu yapmayı tercih ediyorsanız bir uyarı almak.

![Giriş rengi alan hatası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Giriş rengi alan hatası*

Hangi renkli bilgileri bizim özgün ham sıkıştırılmamış video akışında, bizim MXF gelen temsil edilen hello şekilde JPG Kodlayıcı bekleniyor hangi hello farklı olmasıdır. Özellikle, bir sözde "renk aralığı" "RGB" veya "Gri" olduğundan daha fazla beklenen tooflow içinde. Başka bir deyişle, bu hello Video çerçeve ağ geçidi'nin gelen video akışına toohave kendi renk alanını önce uygulanan bir dönüştürme gerekir.

Merhaba iş akışı hello renk alanı Dönüştürücüsü - Intel sürükleyin ve tooour çerçeve kapısı bağlayın.

![Bir renk alanı Dönüştürücüsü bağlanma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Bir renk alanı Dönüştürücüsü bağlanma*

Merhaba Özellikler penceresinde hello BGR 24 girişi hello hazır listeden seçin.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Yazma hello küçük resimleri
Bizim MP4 video farklıdır, bir dosyada birden çok JPG bileşen çıkış Kodlayıcı hello. Bu sipariş toodeal içinde Sahne arama JPG dosya yazıcısı bileşeni kullanılabilir: hello gelen JPG küçük resimleri ele ve bunları çıkışı, farklı bir sayı sonekine her dosya yazar. (genellikle hello sayısını saniye/birimleri gelen hangi hello küçük çizilmiş hello akışında belirten hello sayı.)

![Merhaba Sahne arama JPG dosyası yazan Tanıtımı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Merhaba Sahne arama JPG dosyası yazan Tanıtımı*

Merhaba ifadesiyle Hello çıkış klasörü yolu özelliğini yapılandırın: ${ROOT_outputWriteDirectory}

ve dosya adı önekini özelliğiyle hello:

    ${ROOT_sourceFileBaseName}_thumb_

Merhaba önek hello küçük resim dosyaları nasıl adlı belirler. Bunlar bir numara belirten hello parmak uzakta konum hello akışında sonekine.

![Sahne arama JPG dosya yazıcı özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Sahne arama JPG dosya yazıcı özellikleri*

Merhaba Sahne arama JPG dosyası yazan toohello çıktı dosyası/varlık düğüm bağlayın.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Bir iş akışında hataları algılama
Hello girişi hello renk alanı dönüştürücü toohello ham sıkıştırılmamış video çıkışına bağlayın. Şimdi hello iş akışı için yerel testi gerçekleştirin. Olasılığı hello iş akışı aniden yürütme durdurmak ve kırmızı bir hatayla karşılaştı hello bileşen çerçevesinde ile belirtin:

![Renk alanı dönüştürücü hatası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Renk alanı dönüştürücü hatası*

Merhaba kodlama girişimi başarısız oldu hello nedeni nedir hello sağ üst köşesinde hello renk alanı dönüştürücü bileşen toosee Hello biraz kırmızı "E" simgesine tıklayın.

![Renk alanı dönüştürücü hata iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Renk alanı dönüştürücü hata iletişim kutusu*

Gördüğünüz gibi hello gelen renk alanını hello renk alanı dönüştürücü için standart toobe rec601 YUV tooRGB istenen bizim dönüştürülmesi için sahip olduğundan, etkinleştirir. Görünüşe göre bizim akışı onun rec601 göstermez. (Rec 601 aralıklı analog video sinyalleri dijital video formunda kodlama standardıdır. 720 aydınlatma örnekleri ve her satırda 360 chrominance örnekleri kapsayan etkin bir bölge belirtir. Sistem kodlama hello renk YCbCr 4 bilinir: 2:2.)

toofix Bu, biz rec601 içerikle ilgilenme bizim akış hello meta verileri üzerinde belirtmek. Biz bizim ham kaynak ve hello renk alanı dönüştürme bileşeni Between gireceğiniz bir Video veri türü güncelleştirici bileşeni kullanacağız şekilde toodo. Bu veri türü güncelleştirici hello el ile belirli bir video verileri güncelleştirmesi türü özellikleri sağlar. Bir renk alanı standart "Rec 601", tooindicate yapılandırın. Henüz tanımlanmış hiçbir renk alanını ise bu hello "Rec 601" renk alanını ile Merhaba Video veri türü güncelleştirici tootag hello akış neden olur. (Merhaba geçersiz kılma onay kutusu işaretli değilse, var olan tüm meta veriler geçersiz kılmaz.)

![Renk alanı standart veri türü güncelleştirici hello üzerinde güncelleştirme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Renk alanı standart veri türü güncelleştirici hello üzerinde güncelleştirme*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Tamamlanmış iş akışı
Şimdi bizim bizim iş akışı tamamlandı, onu başka bir test çalışması toosee yapın.

![Küçük resimler ile çoklu mp4 çıktı için tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Küçük resimler ile çoklu mp4 çıktı için tamamlanmış iş akışı*

## <a id="time_based_trim"></a>Zamana bağlı kırpma multibitrate MP4 çıktı
Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi zaman damgalarını temel hello kaynak görüntü kırpma içine arayacaktır.

### <a id="time_based_trim_start"></a>İş akışı genel bakış toostart kırpma için ekleme
![Başlangıç iş akışı tooadd kırpma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Başlangıç iş akışı tooadd kırpma*

### <a id="time_based_trim_use_stream_trimmer"></a>Merhaba akış Kırpıcıyı kullanma
Merhaba akış Kırpıcıyı bileşeni tootrim hello başlangıç ve bitiş Giriş akışı, zamanlama bilgileri (saniye, dakika,...) temel sağlar. Merhaba Kırpıcıyı tabanlı çerçeve kırpma desteklemez.

![Akış Ayarlayıcısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Akış Ayarlayıcısı*

Merhaba AVC Kodlayıcıları ve Konuşmacı konumu assigner toohello ortam dosyası girişi doğrudan bağlama yerine, bu hello akış Kırpıcıyı Between gireceğiniz. (Bir hello video sinyali ve bir araya eklemeli ses sinyal hello.)

![Akış Kırpıcıyı arasında yerleştirme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Akış Kırpıcıyı arasında yerleştirme*

Şimdi biz yalnızca video ve ses 15 saniye ile Merhaba videoda 60 saniye arasında işleyecek şekilde hello Kırpıcıyı yapılandırın.

Merhaba Video akışı Kırpıcıyı toohello özelliklerine gidin ve başlangıç saati (15 sn) ve bitiş zamanı (60s) özelliklerini yapılandırın. hem bizim ses ve video Kırpıcıyı her zaman aynı başlangıç ve değerleri bitiş yapılandırılmış toohello emin toomake, biz bu toohello kök hello iş akışının yayımlar.

![Başlangıç saati akış Kırpıcıyı özelliğinden yayımlama](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Başlangıç saati akış Kırpıcıyı özelliğinden yayımlama*

![Yayımlama özelliği iletişim kutusu için başlangıç saati](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Yayımlama özelliği iletişim kutusu için başlangıç saati*

![Bitiş saati Yayımlama özelliği iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Bitiş saati Yayımlama özelliği iletişim kutusu*

Biz hello kökü verdiğimiz bir iş akışı şimdi inceleyin, her iki özellik düzgün görüntülenen ve yapılandırılabilir buradan olacaktır.

![Kök kullanılabilen yayımlanan Özellikler](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Kök kullanılabilen yayımlanan Özellikler*

Şimdi hello ses Kırpıcıyı hello kırpma özelliklerini açın ve toohello başvuran bir ifadeyle başlangıç ve bitiş zamanları yapılandırın hello kökü verdiğimiz bir iş akışı özellikleri yayımlanan.

Merhaba ses kırpma başlangıç zamanı:

    ${ROOT_TrimmingStartTime}

ve bitiş saati:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Tamamlanmış iş akışı
![Tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Tamamlanmış iş akışı*

## <a id="scripting"></a>Merhaba Script bileşeni Tanıtımı
Komut dosyası bileşenleri hello yürütme aşamaları bizim iş akışı sırasında rastgele komut dosyaları yürütebilir. Çalıştırılabilir, dört farklı betikleri vardır her birinin belirli özelliklere ve kendi yerinde hello iş akışı yaşam döngüsü:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

Merhaba Hello belgelerine komut dosyasıyla bileşen daha ayrıntılı olarak her hello yukarıdaki gider. İçinde [hello bölümde](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** komut dosyası bileşenidir hello iş akışı başlatıldığında kullanılan tooconstruct cliplist xml hello kolay bir şekilde. Bu komut, yalnızca bir kez kaydının çevriminin olur hello Bileşen Kurulumu sırasında çağrılır.

### <a id="scripting_hello_world"></a>Bir iş akışı içinde komut dosyası: Merhaba Dünya
Bir komut dosyasıyla bileşenini hello Tasarımcı yüzeyine sürükleyin ve bunu (örneğin, "SetClipListXML") yeniden adlandırın.

![Bir komut dosyası bileşeni ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Bir komut dosyası bileşeni ekleme*

Merhaba özelliklerini incelediğinizde, komut dosyasıyla bileşen, dört farklı komut türlerine gösterilen Merhaba, her yapılandırılabilir tooa farklı komut dosyası hello.

![Komut dosyası bileşeni özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Komut dosyası bileşeni özellikleri*

Temizle processInputScript hello ve hello realizeScript için hello Düzenleyicisi'ni açın. Şimdi biz kurduktan ve toostart scripting hazır.

Komut dosyaları Groovy, Java ile uyumluluk korur hello Java platform için dinamik olarak derlenmiş bir komut dosyası dili yazılır. Aslında, çoğu Java kodu geçerli Modaya uygun koddur.

Basit hello world Modaya uygun betik hello bizim realizeScript bağlamında yazalım. Merhaba Düzenleyicisi'nde Hello aşağıdakileri girin:

    node.log("hello world");

Şimdi yerel test çalışması yürütün. Bu çalışma sonrasında inceleyin (Merhaba Sistem sekmesinde aracılığıyla Script bileşeni hello) günlükleri özelliği hello.

![Hello world günlük çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Hello world günlük çıktısı*

Merhaba günlük yöntemi, diyoruz hello düğüm nesnesi tooour geçerli "düğümü" ya da hello bileşen biz içindeki komut dosyası anlamına gelmektedir. Her bileşen şekilde hello özelliği toooutput günlük verileri hello sistem sekmesi kullanılabilir sahiptir. Bu durumda, hello dize sabit değeri "hello world" çıktı. Bu, hangi hello komut gerçekte yapmakta olduğu hakkında bilgi sağlayan çok hata ayıklama aracı toobe kanıtlayabilirsiniz burada önemli toounderstand olur.

Komut dosyası ortamımızda içinde biz de erişim tooproperties diğer bileşenleri vardır. Şunu deneyin:

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

Bizim günlük penceresinde bize aşağıdaki hello gösterilir:

![Düğüm yollarını erişmek için bir günlük çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Düğüm yollarını erişmek için bir günlük çıktısı*

## <a id="frame_based_trim"></a>Çerçeve tabanlı kırpma multibitrate MP4 çıktı
Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi çerçeve sayar dayalı hello kaynak görüntü kırpma içine arayacaktır.

### <a id="frame_based_trim_start"></a>Genel Bakış toostart kırpma için ekleme şeması
![İş akışı toostart kırpma için ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*İş akışı toostart kırpma için ekleme*

### <a id="frame_based_trim_clip_list"></a>Merhaba küçük liste XML kullanma
Tüm önceki iş akışı eğitimlerine bizim video giriş kaynağı olarak hello medya dosyası giriş bileşen kullandık. Bu belirli bir senaryo için yine de biz hello küçük listesi kaynak bileşen yerine kullanırsınız. Bu çalışma tercih edilen hello yolu olmamalıdır unutmayın; olduğunda gerçek neden toodo şekilde hello küçük kaynak listesi yalnızca kullanın (burada yapmadan talebi aşağıda hello de olduğu gibi hello küçük listesi kırpma özelliklerinin kullanılmasına).

Bizim ortam dosyası girişi toohello küçük listesi kaynak gelen tooswitch hello küçük listesi kaynak bileşen hello tasarım yüzeyine sürükleyin ve hello küçük listesi XML PIN toohello küçük liste XML düğümü hello iş akışı Tasarımcısı'nın bağlayın. Bu hello küçük listesi kaynak tooour giriş video göre çıkış PIN ile doldurmanız gerekir. Şimdi hello sıkıştırılmamış Video ve sıkıştırılmamış ses PIN'ler hello hello küçük listesi kaynak toohello Bağlan ilgili AVC Kodlayıcıları ve ses akışı ayırıcı. Şimdi hello ortam dosyası girişi kaldırın.

![Merhaba ortam dosyası girişi hello küçük kaynak listesi ile değiştirilir](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Merhaba ortam dosyası girişi hello küçük kaynak listesi ile değiştirilir*

Merhaba küçük listesi kaynak bileşen "Küçük listesi XML" kendi giriş olarak alır. Merhaba kaynak dosya tootest ile yerel olarak seçerken bu küçük resim listesi xml otomatik-sizin için doldurulur.

![Otomatik olarak doldurulmuş küçük listesi XML özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Otomatik olarak doldurulmuş küçük listesi XML özelliği*

Biraz daha yakından toohello xml baktığınızda, bu nasıl gibi görünüyor.

![Küçük resim listesi iletişim kutusunda Düzenle](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Küçük resim listesi iletişim kutusunda Düzenle*

Bu hello küçük liste xml hello yeteneklerini ancak yansıtmaz. Bir seçenek sahibiz tooadd "Kırpma" öğesinin hello video ve ses kaynağı, böyle altında verilmiştir:

![Kırpma öğe toohello küçük listesi ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Kırpma öğe toohello küçük listesi ekleme*

Merhaba küçük liste xml bu gibi değiştirin ve yerel testi gerçekleştirmek, hello video görürsünüz doğru edilmiş hello videoda 10 ile 20 saniye arasında kırpılır.

Bu çok aynı cliplist xml, aynı Azure Media Services çalıştıran bir iş akışında uygulandığında efekt hello sahip değil de, yerel çalıştırma yaptığınızda bulmadýðýný toowhat olur. Azure Premium Kodlayıcı başlatır, hello cliplist xml oluşturulduğu zaman yeniden hello giriş dosyası hello kodlama dayalı her zaman iş verildi. Bu, biz hello xml yapmak herhangi bir değişiklik ne yazık ki geçersiz anlamına gelir.

bir kodlama iş başlatıldığında silmeden toocounter hello cliplist xml biz bunu hello anında yalnızca bizim iş akışının hello başladıktan sonra yeniden oluşturabilirsiniz. Bu tür özel eylemler bir "komut dosyası Component" adlı aracılığıyla alınabilir. Daha fazla bilgi için bkz: [Introducing hello Script bileşeni](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Bir komut dosyasıyla bileşenini hello Tasarımcı yüzeyine sürükleyin ve çok yeniden adlandırma "SetClipListXML".

![Bir komut dosyası bileşeni ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Bir komut dosyası bileşeni ekleme*

Merhaba özelliklerini incelediğinizde, komut dosyasıyla bileşen, dört farklı komut türlerine gösterilen Merhaba, her yapılandırılabilir tooa farklı komut dosyası hello.

![Komut dosyası bileşeni özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Komut dosyası bileşeni özellikleri*

### <a id="frame_based_trim_modify_clip_list"></a>Komut dosyası bir bileşenin Hello küçük listesini değiştirme
İş akışı başlatma sırasında oluşturulan hello cliplist xml yeniden yazma önce biz toohave erişim toohello cliplist xml özellik ve içeriğini gerekir. Biz bunu şu şekilde yapabilirsiniz:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Günlüğe kaydedilmesini gelen küçük resim listesi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Günlüğe kaydedilmesini gelen küçük resim listesi*

Bir şekilde toodetermine ilk ihtiyacımız olan noktasını istiyoruz tootrim hangi noktasından video hello. Bu kullanışlı toohello daha az teknik kullanıcı hello akışının toomake yayımlama hello grafiğinin iki özellik toohello kök. toodo bunu hello Tasarımcı yüzeyine sağ tıklatın ve "Özellik Ekle" seçin:

* İlk özellik: türü "ClippingTimeStart": "zaman kodu"
* İkinci özelliği: türü "ClippingTimeEnd": "zaman kodu"

![Özellik iletişim için kırpma başlangıç saati ekleyin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Özellik iletişim için kırpma başlangıç saati ekleyin*

![İş akışı kökünde zaman özellik kırpma yayımlanan](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*İş akışı kökünde zaman özellik kırpma yayımlanan*

Her iki özellikleri tooa uygun değeri yapılandırın:

![Başlangıç ve bitiş özellikleri kırpma hello yapılandırın](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Başlangıç ve bitiş özellikleri kırpma hello yapılandırın*

Şimdi, bizim komut dosyası içinden Biz bu gibi her iki özellik erişebilirsiniz:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Başlangıç ve bitiş kırpma, gösteren Günlüğü penceresi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Başlangıç ve bitiş kırpma, gösteren Günlüğü penceresi*

Şimdi hello zaman kodu dizeleri basit bir normal ifade kullanarak daha kullanışlı toouse forma, ayrıştırılamıyor:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Ayrıştırılmış zaman kodu çıkış Günlüğü penceresi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Ayrıştırılmış zaman kodu çıkış Günlüğü penceresi*

Bu bilgilerle elinizdeki, biz şimdi hello cliplist xml tooreflect hello başlangıç değiştirebilir ve bitiş zamanları hello için çerçeve doğru kırpma hello film, istenen.

![Komut dosyası kod tooadd kırpma öğeleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Komut dosyası kod tooadd kırpma öğeleri*

Bu normal dize düzenleme işlemleri gerçekleştirilir. Merhaba elde edilen değiştirilmiş küçük liste xml geri toohello clipListXML özelliği hello iş akışı kökünde hello "setProperty" yöntemi ile yazılır. başka bir test çalıştırdıktan sonra hello Günlüğü penceresi bize aşağıdaki hello gösterir:

![Merhaba küçük listesinde günlüğe kaydetme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Merhaba küçük listesinde günlüğe kaydetme*

Nasıl hello video ve ses akışları kırpılmış bir test çalıştırması toosee yapın. Merhaba kesme noktaları için farklı değerlere sahip birden fazla test çalıştırması gerçekleştirirsiniz gibi bu hesaba ancak alınmayacak olduğunu fark edeceksiniz! Bunun nedeni Hello hello Azure çalışma zamanı aksine bu hello Tasarımcısı, her çalıştırma değil geçersiz kılma hello cliplist xml yapar. Bu yalnızca hello hello ayarlamış çok ilk kez giriş ve çıkış noktaları, neden olur, hello xml tootransform anlamına gelir, tüm diğer bizim koruma yan tümcesi kez hello (varsa (clipListXML.indexOf ("<trim>") -1 ==)) hello iş akışı kırpma başka ekleme engeller olduğunda zaten mevcut bir öğe.

Bizim iş akışı uygun tootest yerel olarak en iyi biz toomake kırpma öğesi zaten mevcut olmadığını inceler bazı ev tutma kodu ekleyin. Bu durumda, biz hello xml hello yeni değerlerle değiştirerek devam etmeden önce kaldırabilirsiniz. Düz dize işlemeleri kullanmak yerine, bu gerçek xml nesnesi aracılığıyla model ayrıştırma büyük olasılıkla daha güvenli toodo değil.

Bu tür kodu ancak ekleyebilmeniz için önce biz bizim komut dosyasının ilk olarak başlatma hello içeri aktarma deyimlerini sayısı tooadd gerekir:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Bundan sonra kodu temizleme gerekli hello ekleyebilirsiniz:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Bu kod yalnızca hello kırpma öğeleri toohello cliplist xml eklediğimiz hello noktası gider.

Bu noktada, biz çalıştırabilir ve her zamankinden uygulanan hello değişiklikler yaparken istediğiniz kadar süresi gibi bizim iş akışı değiştirebilirsiniz.    

### <a id="frame_based_trim_clippingenabled_prop"></a>ClippingEnabled kolaylık özellik ekleme
Kırpma toohappen her zaman istemeyebilirsiniz, şimdi bizim iş akışı belirten uygun bir boolean bayrak ekleyerek bitiş kırpma / kırpma tooenable olsun veya olmasın istiyoruz.

Gibi daha önce "ClippingEnabled" adlı bizim iş akışının yeni bir özellik toohello kökü "BOOLEAN" türü yayımlayın.

![Kırpma etkinleştirmek için bir özellik yayımlanan](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Kırpma etkinleştirmek için bir özellik yayımlanan*

Basit koruma yan tümcesi aşağıda Hello ile biz kırpma gerekli olup olmadığını denetleyin ve bizim küçük listesi şekilde değiştirilmiş veya değil toobe gerekmediğine karar verebilirsiniz.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Tam kod
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Ayrıca bkz.
[Premium Azure Media Services kodlama Tanıtımı](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Nasıl tooUse Premium Azure Media Services kodlama](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Azure medya hizmeti ile isteğe bağlı içerik kodlama](media-services-encode-asset.md#media-encoder-premium-workflow)

[Media Encoder Premium İş Akışı Biçimleri ve Kod Çözücüleri](media-services-premium-workflow-encoder-formats.md)

[Örnek iş akışı dosyaları](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Azure Media Services Gezgini aracı](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
