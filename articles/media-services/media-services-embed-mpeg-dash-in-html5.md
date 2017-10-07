---
title: "aaaEmbedding MPEG-DASH Uyarlamalı Akış Video DASH.js bir HTML5 uygulaması | Microsoft Docs"
description: "Bu konuda gösterilir nasıl tooembed bir MPEG-DASH Uyarlamalı akış videoda HTML5 uygulamayla DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>DASH.js ile HTML5 uygulamada MPEG-DASH Uyarlamalı Akış Video katıştırma
## <a name="overview"></a>Genel Bakış
MPEG-DASH bir hello toodeliver yüksek kaliteli, Uyarlamalı video çıkış akışı istediğiniz olanlar için önemli avantajlar sunar video içeriği akışını Uyarlamalı ISO standardıdır. Merhaba ağ yoğun hale geldiğinde MPEG-DASH ile Merhaba video akışına otomatik olarak tooa alt tanımı bırakılmasına neden olacak. Bu hello player hello sonraki birkaç saniye tooplay (diğer adıyla arabelleğe alma) indirirken "Duraklatıldı" video görmesini hello Görüntüleyicisi hello olasılığını azaltır. Ağ Tıkanıklığı azaltır gibi hello video oynatıcı sırayla tooa daha yüksek kaliteli akışı döndürür. Gerekli bu yeteneği tooadapt hello bant genişliği de video için daha hızlı bir başlangıç saati ile sonuçlanır. İlk birkaç saniye hello anlamına gelir hızlı yükleme alt kalite Segmentte çalınabilir ve yeterli içerik arabelleğe sonra tooa daha yüksek kaliteli adım olduğunu.

Dash.js JavaScript'te yazılmış bir açık kaynak MPEG-DASH video bir oyuncu bulunur. Kendi tooprovide video oynatmayı gerektiren uygulamalar ücretsiz olarak yeniden kullanılabilir bir güçlü, platformlar arası oynatıcı belirtilir. MPEG-DASH kayıttan hello W3C medya kaynağı Uzantıları (MSE) Bugün bu Chrome, Microsoft Edge ve IE11 (diğer tarayıcılarda kendi hedefi toosupport MSE belirttiyseniz) destekleyen herhangi bir tarayıcıda sağlar. DASH.js hakkında daha fazla bilgi için js hello GitHub dash.js deposuna bakın.

## <a name="creating-a-browser-based-streaming-video-player"></a>Bir tarayıcı tabanlı akış video oynatıcı oluşturma
Bu tür bir yürütme, duraklatma, Geri Sar vb. toocreate beklenen hello ile bir video oynatıcı görüntüleyen basit bir web sayfası denetimleri, yapmanız gerekir:

1. Bir HTML sayfası oluşturun
2. Merhaba video etiket ekleme
3. Merhaba dash.js player ekleme
4. Merhaba player başlatma
5. Bazı CSS stil ekleme
6. MSE uygulayan bir tarayıcıda hello sonuçlarını görüntüleme

Başlatılırken hello player yalnızca JavaScript kod satırlarını sayıda içinde tamamlanabilir. Dash.js'ni kullanarak bu basit tooembed MPEG-DASH video tarayıcı tabanlı uygulamalar gerçekten değildir.

## <a name="creating-hello-html-page"></a>Merhaba HTML sayfası oluşturma
Merhaba ilk adımdır hello içeren toocreate standart HTML sayfası **video** bu dosyayı aşağıdaki örneğine hello olarak basicPlayer.html Farklı Kaydet öğesini gösterir:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Ekleme hello DASH.js Player
tooadd Merhaba dash.js başvuru uygulaması toohello uygulaması, toograb hello dash.all.js hello 1.0 sürümü dash.js proje dosyasından gerekir. Bu, uygulamanızın JavaScript klasörüne hello kaydedilmelidir. Bu dosya birlikte tek bir dosyaya tüm hello gerekli dash.js kodu çeken bir kolaylık dosyasıdır. Hello dash.js depo bir görünüm varsa, tek tek dosyaların hello bulur, kod ve çok daha fazlasını test ancak tüm toodo istiyorsanız kullanım dash.js olan sonra hello dash.all.js gerekenleri dosyasıdır.

tooadd hello dash.js player tooyour uygulamalar, bir komut dosyası etiketi toohello baş bölümünü basicPlayer.html ekleyin:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Ardından, Hello sayfa yüklendiğinde işlevi tooinitialize hello player oluşturun. Komut dosyası dash.all.js yük hello satırından sonra aşağıdaki hello ekleyin:

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

Bu işlev bir DashContext ilk oluşturur. Belirli bir çalışma zamanı ortamı için kullanılan tooconfigure Merhaba uygulaması budur. Bir teknik açısından bakıldığında, bağımlılık ekleme framework hello sınıfları Merhaba uygulaması oluştururken kullanması gereken hello tanımlar. Çoğu durumda, Dash.di.DashContext kullanır.

Ardından, hello dash.js çerçevenin MediaPlayer hello birincil sınıfının örneği. Bu sınıf gibi gerekli yöntemleri Yürüt ve duraklatmak, hello video öğesi ile Merhaba ilişkisi yönetir ve hello yorumu hello video toobe oynanan tanımlayan hello medya sunu açıklaması (MPD) dosyası da yönetir hello çekirdek içerir.

Merhaba startup() hello MediaPlayer sınıfı işlevinin tooensure adlı hello oyuncu hazır tooplay video değil. Diğer işlemlerin arasında tüm hello gerekli sınıfları (Merhaba bağlam tarafından tanımlandığı gibi) olarak yüklenmiş olan bu işlev sağlar. Merhaba player hazır olduktan sonra hello video öğesi tooit hello attachView() işlevini kullanarak ekleyebilirsiniz. Bu hello MediaPlayer tooinject hello video akışına hello öğesine sağlar ve ayrıca kayıttan yürütme gerektiği gibi denetleyebilirsiniz.

Böylece olması beklenen hello video hakkında bilir hello MPD dosya toohello MediaPlayer hello URL'sini geçirmek yeni oluşturduğunuz tooplay.hello setupVideo() işlevi hello sayfa tam olarak yüklendikten sonra yürütülen toobe gerekir. Merhaba yüklendiğinde olayı hello gövde öğesinin kullanarak bunu. Değişiklik, <body> öğesine:

    <body onload="setupVideo()">

Son olarak, CSS kullanarak hello video öğesi hello boyutunu ayarlayın. Bir Uyarlamalı akış ortamında kayıttan yürütme toochanging ağ koşulları uyum gibi hello çalınan video hello boyutunu değiştirme çünkü bu özellikle önemlidir. % 80'hello kullanılabilir tarayıcı penceresinin yalnızca zorla hello video öğesi toobe hello sayfasının CSS toohello baş bölümünde aşağıdaki hello ekleyerek bu basit demo:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Bir Video oynatma
tooplay bir video tarayıcınız hello basicPlayback.html dosyasına gelin ve görüntülenen hello video oynatıcı çalmayı tıklatın.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Video oynatıcı uygulamaları geliştirme](media-services-develop-video-players.md)

[GitHub dash.js deposu](https://github.com/Dash-Industry-Forum/dash.js) 

