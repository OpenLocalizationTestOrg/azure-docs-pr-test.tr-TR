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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="0277b-103">DASH.js ile HTML5 uygulamada MPEG-DASH Uyarlamalı Akış Video katıştırma</span><span class="sxs-lookup"><span data-stu-id="0277b-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="0277b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0277b-104">Overview</span></span>
<span data-ttu-id="0277b-105">MPEG-DASH bir hello toodeliver yüksek kaliteli, Uyarlamalı video çıkış akışı istediğiniz olanlar için önemli avantajlar sunar video içeriği akışını Uyarlamalı ISO standardıdır.</span><span class="sxs-lookup"><span data-stu-id="0277b-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="0277b-106">Merhaba ağ yoğun hale geldiğinde MPEG-DASH ile Merhaba video akışına otomatik olarak tooa alt tanımı bırakılmasına neden olacak.</span><span class="sxs-lookup"><span data-stu-id="0277b-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="0277b-107">Bu hello player hello sonraki birkaç saniye tooplay (diğer adıyla arabelleğe alma) indirirken "Duraklatıldı" video görmesini hello Görüntüleyicisi hello olasılığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="0277b-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="0277b-108">Ağ Tıkanıklığı azaltır gibi hello video oynatıcı sırayla tooa daha yüksek kaliteli akışı döndürür.</span><span class="sxs-lookup"><span data-stu-id="0277b-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="0277b-109">Gerekli bu yeteneği tooadapt hello bant genişliği de video için daha hızlı bir başlangıç saati ile sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="0277b-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="0277b-110">İlk birkaç saniye hello anlamına gelir hızlı yükleme alt kalite Segmentte çalınabilir ve yeterli içerik arabelleğe sonra tooa daha yüksek kaliteli adım olduğunu.</span><span class="sxs-lookup"><span data-stu-id="0277b-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="0277b-111">Dash.js JavaScript'te yazılmış bir açık kaynak MPEG-DASH video bir oyuncu bulunur.</span><span class="sxs-lookup"><span data-stu-id="0277b-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="0277b-112">Kendi tooprovide video oynatmayı gerektiren uygulamalar ücretsiz olarak yeniden kullanılabilir bir güçlü, platformlar arası oynatıcı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0277b-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="0277b-113">MPEG-DASH kayıttan hello W3C medya kaynağı Uzantıları (MSE) Bugün bu Chrome, Microsoft Edge ve IE11 (diğer tarayıcılarda kendi hedefi toosupport MSE belirttiyseniz) destekleyen herhangi bir tarayıcıda sağlar.</span><span class="sxs-lookup"><span data-stu-id="0277b-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="0277b-114">DASH.js hakkında daha fazla bilgi için js hello GitHub dash.js deposuna bakın.</span><span class="sxs-lookup"><span data-stu-id="0277b-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="0277b-115">Bir tarayıcı tabanlı akış video oynatıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0277b-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="0277b-116">Bu tür bir yürütme, duraklatma, Geri Sar vb. toocreate beklenen hello ile bir video oynatıcı görüntüleyen basit bir web sayfası denetimleri, yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0277b-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="0277b-117">Bir HTML sayfası oluşturun</span><span class="sxs-lookup"><span data-stu-id="0277b-117">Create an HTML page</span></span>
2. <span data-ttu-id="0277b-118">Merhaba video etiket ekleme</span><span class="sxs-lookup"><span data-stu-id="0277b-118">Add hello video tag</span></span>
3. <span data-ttu-id="0277b-119">Merhaba dash.js player ekleme</span><span class="sxs-lookup"><span data-stu-id="0277b-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="0277b-120">Merhaba player başlatma</span><span class="sxs-lookup"><span data-stu-id="0277b-120">Initialize hello player</span></span>
5. <span data-ttu-id="0277b-121">Bazı CSS stil ekleme</span><span class="sxs-lookup"><span data-stu-id="0277b-121">Add some CSS style</span></span>
6. <span data-ttu-id="0277b-122">MSE uygulayan bir tarayıcıda hello sonuçlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="0277b-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="0277b-123">Başlatılırken hello player yalnızca JavaScript kod satırlarını sayıda içinde tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0277b-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="0277b-124">Dash.js'ni kullanarak bu basit tooembed MPEG-DASH video tarayıcı tabanlı uygulamalar gerçekten değildir.</span><span class="sxs-lookup"><span data-stu-id="0277b-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="0277b-125">Merhaba HTML sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0277b-125">Creating hello HTML Page</span></span>
<span data-ttu-id="0277b-126">Merhaba ilk adımdır hello içeren toocreate standart HTML sayfası **video** bu dosyayı aşağıdaki örneğine hello olarak basicPlayer.html Farklı Kaydet öğesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="0277b-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="0277b-127">Ekleme hello DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="0277b-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="0277b-128">tooadd Merhaba dash.js başvuru uygulaması toohello uygulaması, toograb hello dash.all.js hello 1.0 sürümü dash.js proje dosyasından gerekir.</span><span class="sxs-lookup"><span data-stu-id="0277b-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="0277b-129">Bu, uygulamanızın JavaScript klasörüne hello kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0277b-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="0277b-130">Bu dosya birlikte tek bir dosyaya tüm hello gerekli dash.js kodu çeken bir kolaylık dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="0277b-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="0277b-131">Hello dash.js depo bir görünüm varsa, tek tek dosyaların hello bulur, kod ve çok daha fazlasını test ancak tüm toodo istiyorsanız kullanım dash.js olan sonra hello dash.all.js gerekenleri dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="0277b-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="0277b-132">tooadd hello dash.js player tooyour uygulamalar, bir komut dosyası etiketi toohello baş bölümünü basicPlayer.html ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0277b-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="0277b-133">Ardından, Hello sayfa yüklendiğinde işlevi tooinitialize hello player oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0277b-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="0277b-134">Komut dosyası dash.all.js yük hello satırından sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0277b-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

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

<span data-ttu-id="0277b-135">Bu işlev bir DashContext ilk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0277b-135">This function first creates a DashContext.</span></span> <span data-ttu-id="0277b-136">Belirli bir çalışma zamanı ortamı için kullanılan tooconfigure Merhaba uygulaması budur.</span><span class="sxs-lookup"><span data-stu-id="0277b-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="0277b-137">Bir teknik açısından bakıldığında, bağımlılık ekleme framework hello sınıfları Merhaba uygulaması oluştururken kullanması gereken hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0277b-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="0277b-138">Çoğu durumda, Dash.di.DashContext kullanır.</span><span class="sxs-lookup"><span data-stu-id="0277b-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="0277b-139">Ardından, hello dash.js çerçevenin MediaPlayer hello birincil sınıfının örneği.</span><span class="sxs-lookup"><span data-stu-id="0277b-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="0277b-140">Bu sınıf gibi gerekli yöntemleri Yürüt ve duraklatmak, hello video öğesi ile Merhaba ilişkisi yönetir ve hello yorumu hello video toobe oynanan tanımlayan hello medya sunu açıklaması (MPD) dosyası da yönetir hello çekirdek içerir.</span><span class="sxs-lookup"><span data-stu-id="0277b-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="0277b-141">Merhaba startup() hello MediaPlayer sınıfı işlevinin tooensure adlı hello oyuncu hazır tooplay video değil.</span><span class="sxs-lookup"><span data-stu-id="0277b-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="0277b-142">Diğer işlemlerin arasında tüm hello gerekli sınıfları (Merhaba bağlam tarafından tanımlandığı gibi) olarak yüklenmiş olan bu işlev sağlar.</span><span class="sxs-lookup"><span data-stu-id="0277b-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="0277b-143">Merhaba player hazır olduktan sonra hello video öğesi tooit hello attachView() işlevini kullanarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0277b-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="0277b-144">Bu hello MediaPlayer tooinject hello video akışına hello öğesine sağlar ve ayrıca kayıttan yürütme gerektiği gibi denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0277b-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="0277b-145">Böylece olması beklenen hello video hakkında bilir hello MPD dosya toohello MediaPlayer hello URL'sini geçirmek yeni oluşturduğunuz tooplay.hello setupVideo() işlevi hello sayfa tam olarak yüklendikten sonra yürütülen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="0277b-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="0277b-146">Merhaba yüklendiğinde olayı hello gövde öğesinin kullanarak bunu.</span><span class="sxs-lookup"><span data-stu-id="0277b-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="0277b-147">Değişiklik, <body> öğesine:</span><span class="sxs-lookup"><span data-stu-id="0277b-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="0277b-148">Son olarak, CSS kullanarak hello video öğesi hello boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0277b-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="0277b-149">Bir Uyarlamalı akış ortamında kayıttan yürütme toochanging ağ koşulları uyum gibi hello çalınan video hello boyutunu değiştirme çünkü bu özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0277b-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="0277b-150">% 80'hello kullanılabilir tarayıcı penceresinin yalnızca zorla hello video öğesi toobe hello sayfasının CSS toohello baş bölümünde aşağıdaki hello ekleyerek bu basit demo:</span><span class="sxs-lookup"><span data-stu-id="0277b-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="0277b-151">Bir Video oynatma</span><span class="sxs-lookup"><span data-stu-id="0277b-151">Playing a Video</span></span>
<span data-ttu-id="0277b-152">tooplay bir video tarayıcınız hello basicPlayback.html dosyasına gelin ve görüntülenen hello video oynatıcı çalmayı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0277b-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0277b-153">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="0277b-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0277b-154">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="0277b-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0277b-155">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0277b-155">See Also</span></span>
[<span data-ttu-id="0277b-156">Video oynatıcı uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="0277b-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="0277b-157">GitHub dash.js deposu</span><span class="sxs-lookup"><span data-stu-id="0277b-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

