---
title: "aaaSmooth hello açık kaynak Media Framework için akış eklentisi"
description: "Nasıl toouse hello hello Adobe açık kaynak Media Framework için Azure Media Services kesintisiz akış eklentisi öğrenin."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="bf246-103">Nasıl tooUse hello Microsoft kesintisiz akış eklentisi Merhaba Adobe açık kaynak medya çerçeve</span><span class="sxs-lookup"><span data-stu-id="bf246-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="bf246-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bf246-104">Overview</span></span>
<span data-ttu-id="bf246-105">Açık kaynak Media Framework 2.0 (SS OSMF için) hello varsayılan OSMF yeteneklerini genişletir ve Microsoft kesintisiz akış içeriği oynatmayı toonew ve varolan OSMF ekler için Microsoft kesintisiz akış eklentisi hello oynatıcıları.</span><span class="sxs-lookup"><span data-stu-id="bf246-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="bf246-106">Merhaba eklentisi ayrıca kesintisiz Akış kayıttan yürütme özellikleri tooStrobe medya kayıttan yürütme (SMP) ekler.</span><span class="sxs-lookup"><span data-stu-id="bf246-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="bf246-107">OSMF SS eklentisi iki sürümünü içerir:</span><span class="sxs-lookup"><span data-stu-id="bf246-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="bf246-108">OSMF (.swc) için statik kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="bf246-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="bf246-109">OSMF (.swf) için dinamik kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="bf246-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="bf246-110">Bu belge hello okuyucu OSMF ve OSMF genel bilgisine sahip olduğunu varsayar eklentileri. OSMF hakkında daha fazla bilgi için hello belge üzerinde hello lütfen bkz. [resmi OSMF sitesi](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="bf246-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="bf246-111">OSMF 2.0 için kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="bf246-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="bf246-112">Merhaba eklentisi özellikleri aşağıdaki hello ile yükleme ve isteğe bağlı kesintisiz akış içeriği kayıttan yürütmeyi destekler:</span><span class="sxs-lookup"><span data-stu-id="bf246-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="bf246-113">İsteğe bağlı kesintisiz Akış kayıttan yürütme (yürütme, duraklatma, arama, Dur)</span><span class="sxs-lookup"><span data-stu-id="bf246-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="bf246-114">Canlı kesintisiz Akış kayıttan yürütme (kullan)</span><span class="sxs-lookup"><span data-stu-id="bf246-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="bf246-115">Canlı DVR işlevleri (Duraklat, arama, DVR kayıttan yürütme, Canlı Git)</span><span class="sxs-lookup"><span data-stu-id="bf246-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="bf246-116">Görüntü codec bileşenleri - H.264 desteği</span><span class="sxs-lookup"><span data-stu-id="bf246-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="bf246-117">Ses codec bileşenleri - AAC desteği</span><span class="sxs-lookup"><span data-stu-id="bf246-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="bf246-118">Birden çok ses dil OSMF yerleşik API'leri ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="bf246-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="bf246-119">En fazla kayıttan yürütme kalitesi seçimi OSMF yerleşik API'leri ile</span><span class="sxs-lookup"><span data-stu-id="bf246-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="bf246-120">Resim yazıları OSMF resim yazıları eklentisi ile sepet kapalı</span><span class="sxs-lookup"><span data-stu-id="bf246-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="bf246-121">Adobe&reg; Flash&reg; Player 11.4 ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="bf246-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="bf246-122">Bu sürümü yalnızca OSMF 2.0 destekler.</span><span class="sxs-lookup"><span data-stu-id="bf246-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="bf246-123">Desteklenen özellikler ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="bf246-123">Supported features and known issues</span></span>
<span data-ttu-id="bf246-124">Desteklenen özellikler, desteklenmeyen özellikler ve bilinen sorunlar tam listesi için çok bakın[bu belgeyi](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="bf246-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="bf246-125">Yükleme hello eklentisi</span><span class="sxs-lookup"><span data-stu-id="bf246-125">Loading hello Plugin</span></span>
<span data-ttu-id="bf246-126">Statik olarak (derleme zamanında) OSMF eklentileri yüklenebilir veya dinamik olarak (çalışma zamanında).</span><span class="sxs-lookup"><span data-stu-id="bf246-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="bf246-127">Merhaba kesintisiz akış eklentisi OSMF indirmek için dinamik ve statik sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="bf246-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="bf246-128">Statik yükleme: tooload statik olarak, bir statik kitaplık (SWC) dosyası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bf246-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="bf246-129">Statik eklentileri bir başvuru olarak eklenen dosya hello derleme zamanında toohello projeleri ve birleştirme hello son çıktı içinde.</span><span class="sxs-lookup"><span data-stu-id="bf246-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="bf246-130">Dinamik yükleme: tooload dinamik olarak derlenmiş bir (SWF) dosyası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bf246-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="bf246-131">Dinamik eklenti hello çalışma zamanı yüklendi ve hello proje çıktısına dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="bf246-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="bf246-132">(Derlenmiş çıktı) Dinamik eklenti, HTTP ve dosya protokolleri kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bf246-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="bf246-133">Statik ve dinamik yükleme hakkında daha fazla bilgi için bkz: hello resmi [OSMF eklenti sayfası](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="bf246-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="bf246-134">SS OSMF statik yükleme için</span><span class="sxs-lookup"><span data-stu-id="bf246-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="bf246-135">Aşağıdaki kod parçacığında Hello nasıl tooload SS eklentisi OSMF için statik olarak hello ve OSMF MediaFactory sınıfını kullanarak bir temel çalmasına gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf246-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="bf246-136">Merhaba SS OSMF kodu eklemeden önce lütfen hello proje başvurusu hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" statik eklentisi içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bf246-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="bf246-137">SS OSMF dinamik yükleme için</span><span class="sxs-lookup"><span data-stu-id="bf246-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="bf246-138">Aşağıdaki kod parçacığında Hello nasıl tooload SS eklentisi OSMF için dinamik olarak hello ve hello OSMF MediaFactory sınıfını kullanarak bir temel çalmasına gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf246-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="bf246-139">Dosya Protokolü kullanarak tooload istediğiniz veya bir web sunucusu HTTP yük altında kopyalarsanız hello SS OSMF kodu eklemeden önce hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" dinamik eklenti toohello proje klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bf246-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="bf246-140">Merhaba proje başvuruları hiçbir gerek tooinclude "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" dir.</span><span class="sxs-lookup"><span data-stu-id="bf246-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="bf246-141">Paket {</span><span class="sxs-lookup"><span data-stu-id="bf246-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="bf246-142">}</span><span class="sxs-lookup"><span data-stu-id="bf246-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="bf246-143">Merhaba SS ODMF dinamik eklenti ile flaş ortam çalma</span><span class="sxs-lookup"><span data-stu-id="bf246-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="bf246-144">Merhaba kesintisiz akış OSMF dinamik eklenti için uyumlu [flaş medya kayıttan yürütme (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="bf246-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="bf246-145">Merhaba SS OSMF eklentisi tooadd kesintisiz akış içeriği oynatmayı tooSMP için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf246-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="bf246-146">toodo "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" bir web sunucusu altında aşağıdaki hello kullanarak HTTP yük için adımları Bu, kopyalama:</span><span class="sxs-lookup"><span data-stu-id="bf246-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="bf246-147">Merhaba Gözat [flaş Media Çalma Kurulum sayfasında](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="bf246-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="bf246-148">Merhaba src tooa kesintisiz akış kaynak, (örneğin http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="bf246-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="bf246-149">İstenen hello yapılandırma değişikliklerini yapın ve Önizleme ve güncelleştirme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bf246-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="bf246-150">**Not** içerik web sunucunuzun geçerli crossdomain.xml gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="bf246-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="bf246-151">Kopyalama ve yapıştırma hello örnek aşağıdaki gibi sık kullandığınız metin düzenleyiciyi kullanarak hello kod tooa basit HTML sayfası:</span><span class="sxs-lookup"><span data-stu-id="bf246-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="bf246-152">Kesintisiz akış OSMF eklentisi toohello eklemek ekleme kodu edinin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bf246-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="bf246-153">HTML sayfası kaydedin ve tooa web sunucusunda yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="bf246-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="bf246-154">Gözat toohello yayımlanan web sayfasını kullanarak, sık kullanılan Flash&reg; Player etkin Internet tarayıcısı (Internet Explorer, Chrome, Firefox, vb.).</span><span class="sxs-lookup"><span data-stu-id="bf246-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="bf246-155">Kesintisiz akış içerikten Adobe içinde&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="bf246-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="bf246-156">Merhaba resmi genel OSMF geliştirme hakkında daha fazla bilgi için lütfen bkz [OSMF geliştirme sayfa](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="bf246-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bf246-157">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="bf246-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf246-158">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="bf246-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="bf246-159">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="bf246-159">See Also</span></span>
[<span data-ttu-id="bf246-160">Microsoft eklentisi OSMF güncelleştirmesi Uyarlamalı</span><span class="sxs-lookup"><span data-stu-id="bf246-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

