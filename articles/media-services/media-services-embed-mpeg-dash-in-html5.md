---
title: "DASH.js ile HTML5 uygulamada MPEG-DASH Uyarlamalı Akış Video katıştırma | Microsoft Docs"
description: "Bu konu, HTML5 uygulamayla DASH.js MPEG-DASH Uyarlamalı Akış Video ekleme gösterilmiştir."
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="ba3d2-103">DASH.js ile HTML5 uygulamada MPEG-DASH Uyarlamalı Akış Video katıştırma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="ba3d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ba3d2-104">Overview</span></span>
<span data-ttu-id="ba3d2-105">MPEG-DASH, çıkış akış yüksek kaliteli, Uyarlamalı video teslim etmek istediğiniz olanlar için önemli avantajlar sunar video içeriği Uyarlamalı akış için bir ISO standardıdır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="ba3d2-106">Ağ yoğun hale geldiğinde MPEG-DASH ile video akışına otomatik olarak bir alt tanımına bırakılmasına neden olacak.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="ba3d2-107">Bu, "Duraklatıldı" bir video oynatıcı (diğer adıyla arabelleğe alma) yürütmek için sonraki birkaç saniye indirirken görmesini Görüntüleyicisi olasılığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="ba3d2-108">Ağ Tıkanıklığı azaltır gibi video oynatıcı sırayla daha yüksek bir kalite akışına döndürür.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="ba3d2-109">İstenen bant genişliği uyarlama olanağı da video için daha hızlı bir başlangıç saati sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="ba3d2-110">İlk birkaç saniye içinde hızlı yükleme alt kalite kesimi çalınabilir ve daha yüksek kaliteli bir kez yeterli içerik kadar adım bir sonra arabelleğe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="ba3d2-111">Dash.js JavaScript'te yazılmış bir açık kaynak MPEG-DASH video bir oyuncu bulunur.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="ba3d2-112">Amacı serbestçe video oynatmayı gerektiren uygulamalar içinde yeniden kullanılabilir bir güçlü, platformlar arası oynatıcı sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="ba3d2-113">MPEG-DASH kayıttan yürütme, Chrome, Microsoft Edge ve (diğer tarayıcılarda MSE desteklemek için kendi hedefi belirttiyseniz) IE11 W3C medya kaynağı Uzantıları (MSE) Bugün destekleyen herhangi bir tarayıcıda sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="ba3d2-114">DASH.js hakkında daha fazla bilgi için GitHub dash.js depo js bakın.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="ba3d2-115">Bir tarayıcı tabanlı akış video oynatıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="ba3d2-116">Bir video oynatıcı beklenen ile görüntüleyen basit bir web sayfası oluşturmak için bu tür bir yürütme, duraklatma, Geri Sar vb. denetimleri, yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="ba3d2-117">Bir HTML sayfası oluşturun</span><span class="sxs-lookup"><span data-stu-id="ba3d2-117">Create an HTML page</span></span>
2. <span data-ttu-id="ba3d2-118">Video etiket ekleme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-118">Add the video tag</span></span>
3. <span data-ttu-id="ba3d2-119">Dash.js player ekleme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-119">Add the dash.js player</span></span>
4. <span data-ttu-id="ba3d2-120">Player başlatma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-120">Initialize the player</span></span>
5. <span data-ttu-id="ba3d2-121">Bazı CSS stil ekleme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-121">Add some CSS style</span></span>
6. <span data-ttu-id="ba3d2-122">MSE uygulayan bir tarayıcıda sonuçları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="ba3d2-123">Player başlatma yalnızca JavaScript kod satırlarını sayıda içinde tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="ba3d2-124">Dash.js kullanarak gerçekten tarayıcı tabanlı uygulamalarınızda MPEG-DASH video ekleme, basit değildir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="ba3d2-125">HTML sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-125">Creating the HTML Page</span></span>
<span data-ttu-id="ba3d2-126">Standart bir HTML sayfası içeren oluşturmak için ilk adımdır **video** bu dosyayı aşağıdaki örnekteki gibi basicPlayer.html Farklı Kaydet öğesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="ba3d2-127">DASH.js Player ekleme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="ba3d2-128">Uygulama dash.js başvuru uygulaması eklemek için dash.js proje 1.0 sürümü dash.all.js dosyasından alın gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="ba3d2-129">Bu, uygulamanızın JavaScript klasöründe kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="ba3d2-130">Bu dosya birlikte tek bir dosyaya tüm gerekli dash.js kodu çeken bir kolaylık dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="ba3d2-131">Dash.js depo bir görünüm varsa, tek tek dosyaları bulmak, kod ve çok daha fazlasını test ancak tüm yapmak istiyorsanız kullanım dash.js olan sonra gerekenler dash.all.js dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="ba3d2-132">Dash.js player uygulamalarınıza eklemek için bir komut dosyası etiketinin basicPlayer.html baş bölümüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="ba3d2-133">Ardından, sayfa yüklendiğinde player başlatmak için bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="ba3d2-134">Aşağıdaki komut dosyası dash.all.js yük satırından sonra ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="ba3d2-135">Bu işlev bir DashContext ilk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-135">This function first creates a DashContext.</span></span> <span data-ttu-id="ba3d2-136">Bu uygulama için belirli çalışma zamanı ortamı yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="ba3d2-137">Bir teknik açısından bakıldığında, bağımlılık ekleme framework uygulama oluştururken kullanması gereken sınıfları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="ba3d2-138">Çoğu durumda, Dash.di.DashContext kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="ba3d2-139">Ardından, MediaPlayer dash.js framework'ün birincil sınıfının örneği.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="ba3d2-140">Bu sınıf gibi gerekli yöntemleri Yürüt ve duraklatmak, video öğesi olan yönetir ve ayrıca çalınacak video tanımlayan medya sunu açıklaması (MPD) dosya yorumu yönetir çekirdek içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="ba3d2-141">MediaPlayer sınıfının startup() işlev player video yürütmek hazır olduğundan emin olmak için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="ba3d2-142">Diğer işlemlerin arasında gerekli tüm sınıflar (bağlam tarafından tanımlandığı gibi) olarak yüklenmiş olan bu işlev sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="ba3d2-143">Player hazır olduktan sonra attachView() işlevi ile video öğesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="ba3d2-144">Bu öğeye video akışına ekleme ve ayrıca gerektiği gibi kayıttan yürütme denetlemek MediaPlayer sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="ba3d2-145">Böylece yürütmek için beklenen ilgili video bilir MPD dosyanın URL'sini MediaPlayer geçirin. Yeni oluşturduğunuz setupVideo() işlevi, sayfa tam olarak yüklendikten sonra yürütülecek gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="ba3d2-146">Gövde öğesinin yüklendiğinde olayı kullanarak bunu.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="ba3d2-147">Değişiklik, <body> öğesine:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="ba3d2-148">Son olarak, CSS kullanarak video öğesi boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="ba3d2-149">Uyarlamalı akış ortamında, değişen ağ koşullarını kayıttan yürütme uyum olarak yürütülen video boyutunu değiştirme çünkü bu özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="ba3d2-150">Bu basit tanıtım sayfası merkez bölümüne aşağıdaki CSS ekleyerek kullanılabilir tarayıcı penceresinin % 80 olarak video öğesi yalnızca zorla:</span><span class="sxs-lookup"><span data-stu-id="ba3d2-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="ba3d2-151">Bir Video oynatma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-151">Playing a Video</span></span>
<span data-ttu-id="ba3d2-152">Bir videoyu yürütmek için tarayıcınızı basicPlayback.html dosyasına işaret ve görüntülenen video oynatıcı çalmayı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ba3d2-153">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ba3d2-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ba3d2-154">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ba3d2-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ba3d2-155">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ba3d2-155">See Also</span></span>
[<span data-ttu-id="ba3d2-156">Video oynatıcı uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="ba3d2-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="ba3d2-157">GitHub dash.js deposu</span><span class="sxs-lookup"><span data-stu-id="ba3d2-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

