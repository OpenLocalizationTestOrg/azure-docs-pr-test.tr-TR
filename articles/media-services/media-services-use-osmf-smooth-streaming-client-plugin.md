---
title: "Açık kaynak Media Framework için kesintisiz akış eklentisi"
description: "Adobe açık kaynak Media Framework için Azure Media Services kesintisiz akış eklentisi kullanmayı öğrenin."
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="21357-103">Microsoft Adobe açık kaynak Media Framework eklentisi akış kesintisiz kullanma</span><span class="sxs-lookup"><span data-stu-id="21357-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="21357-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="21357-104">Overview</span></span>
<span data-ttu-id="21357-105">Açık kaynak Media Framework 2.0 (SS OSMF için) için Microsoft kesintisiz akış eklentisi OSMF varsayılan yeteneklerini genişletir ve yeni ve mevcut OSMF oynatıcıları Microsoft kesintisiz akış içeriği oynatmayı ekler.</span><span class="sxs-lookup"><span data-stu-id="21357-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="21357-106">Eklenti kesintisiz Akış kayıttan yürütme özellikleri flaş medya kayıttan yürütme (SMP) da ekler.</span><span class="sxs-lookup"><span data-stu-id="21357-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="21357-107">OSMF SS eklentisi iki sürümünü içerir:</span><span class="sxs-lookup"><span data-stu-id="21357-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="21357-108">OSMF (.swc) için statik kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="21357-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="21357-109">OSMF (.swf) için dinamik kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="21357-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="21357-110">Bu belge okuyucunun OSMF ve OSMF genel bilgilere sahip olduğunu varsayar eklentileri. OSMF hakkında daha fazla bilgi için lütfen belgelere bakın [resmi OSMF sitesi](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="21357-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="21357-111">OSMF 2.0 için kesintisiz akış eklentisi</span><span class="sxs-lookup"><span data-stu-id="21357-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="21357-112">Eklenti yükleme ve isteğe bağlı kesintisiz akış içeriği aşağıdaki özelliklerle kayıttan yürütmeyi destekler:</span><span class="sxs-lookup"><span data-stu-id="21357-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="21357-113">İsteğe bağlı kesintisiz Akış kayıttan yürütme (yürütme, duraklatma, arama, Dur)</span><span class="sxs-lookup"><span data-stu-id="21357-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="21357-114">Canlı kesintisiz Akış kayıttan yürütme (kullan)</span><span class="sxs-lookup"><span data-stu-id="21357-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="21357-115">Canlı DVR işlevleri (Duraklat, arama, DVR kayıttan yürütme, Canlı Git)</span><span class="sxs-lookup"><span data-stu-id="21357-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="21357-116">Görüntü codec bileşenleri - H.264 desteği</span><span class="sxs-lookup"><span data-stu-id="21357-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="21357-117">Ses codec bileşenleri - AAC desteği</span><span class="sxs-lookup"><span data-stu-id="21357-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="21357-118">Birden çok ses dil OSMF yerleşik API'leri ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="21357-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="21357-119">En fazla kayıttan yürütme kalitesi seçimi OSMF yerleşik API'leri ile</span><span class="sxs-lookup"><span data-stu-id="21357-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="21357-120">Resim yazıları OSMF resim yazıları eklentisi ile sepet kapalı</span><span class="sxs-lookup"><span data-stu-id="21357-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="21357-121">Adobe&reg; Flash&reg; Player 11.4 ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="21357-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="21357-122">Bu sürümü yalnızca OSMF 2.0 destekler.</span><span class="sxs-lookup"><span data-stu-id="21357-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="21357-123">Desteklenen özellikler ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="21357-123">Supported features and known issues</span></span>
<span data-ttu-id="21357-124">Desteklenen özellikler, desteklenmeyen özellikler ve bilinen sorunlar tam bir listesi için bkz [bu belgeyi](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="21357-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="21357-125">Eklentisi yükleniyor</span><span class="sxs-lookup"><span data-stu-id="21357-125">Loading the Plugin</span></span>
<span data-ttu-id="21357-126">Statik olarak (derleme zamanında) OSMF eklentileri yüklenebilir veya dinamik olarak (çalışma zamanında).</span><span class="sxs-lookup"><span data-stu-id="21357-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="21357-127">Kesintisiz akış eklentisi OSMF indirmek için dinamik ve statik sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="21357-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="21357-128">Statik yükleme: statik olarak yüklemek için bir statik kitaplık (SWC) dosyası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21357-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="21357-129">Statik eklentileri varsayılan olarak, derleme zamanında son çıktı dosyası içinde birleştirme ve projeler başvuru olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="21357-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="21357-130">Dinamik yükleme: dinamik olarak yüklemek için önceden derlenmiş (SWF) dosyası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21357-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="21357-131">Dinamik eklenti çalışma zamanı'nda yüklü ve proje çıktısına dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="21357-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="21357-132">(Derlenmiş çıktı) Dinamik eklenti, HTTP ve dosya protokolleri kullanılarak yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="21357-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="21357-133">Resmi statik ve dinamik yükleme hakkında daha fazla bilgi için bkz: [OSMF eklenti sayfası](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="21357-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="21357-134">SS OSMF statik yükleme için</span><span class="sxs-lookup"><span data-stu-id="21357-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="21357-135">Aşağıdaki kod parçacığında, SS eklentisi OSMF için statik olarak yüklemek ve OSMF MediaFactory sınıfını kullanarak bir temel çalmasına gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="21357-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="21357-136">OSMF kod SS eklemeden önce lütfen proje başvurusu "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" statik eklentisi içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="21357-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="21357-137">SS OSMF dinamik yükleme için</span><span class="sxs-lookup"><span data-stu-id="21357-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="21357-138">Aşağıdaki kod parçacığında SS eklentisi OSMF için dinamik olarak yükleme ve temel bir Yürüt OSMF MediaFactory sınıfını kullanarak video gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="21357-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="21357-139">OSMF kod SS dahil olmak üzere önce dosya protokolü kullanarak yüklemek istiyorsanız, "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" dinamik eklenti proje klasörüne kopyalayın veya bir web sunucusu HTTP yük altında kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="21357-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="21357-140">Proje başvurularını "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" eklemenize gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="21357-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="21357-141">Paket {</span><span class="sxs-lookup"><span data-stu-id="21357-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="21357-142">}</span><span class="sxs-lookup"><span data-stu-id="21357-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="21357-143">SS ODMF dinamik eklenti ile flaş ortam çalma</span><span class="sxs-lookup"><span data-stu-id="21357-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="21357-144">Kesintisiz akış OSMF dinamik eklenti için uyumlu [flaş medya kayıttan yürütme (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="21357-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="21357-145">OSMF eklentisi SS SMP için kesintisiz akış içeriği oynatmayı eklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21357-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="21357-146">Bunu yapmak için bir web sunucusu için aşağıdaki adımları kullanarak HTTP yük altında "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="21357-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="21357-147">Gözat [flaş Media Çalma Kurulum sayfasında](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="21357-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="21357-148">Src kesintisiz akış için kaynak (örneğin http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="21357-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="21357-149">İstenen yapılandırma değişiklikleri yapın ve Önizleme ve güncelleştirme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="21357-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="21357-150">**Not** içerik web sunucunuzun geçerli crossdomain.xml gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21357-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="21357-151">Kodu kopyalayıp aşağıdaki örnekte olduğu gibi sık kullandığınız metin düzenleyiciyi kullanarak basit bir HTML sayfasına yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="21357-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="21357-152">Kesintisiz akış OSMF eklenti ekleme kodu ekleme ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21357-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="21357-153">HTML sayfası kaydedin ve bir web sunucusunda yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="21357-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="21357-154">Sık kullanılan Flash kullanarak yayımlanan web sayfasına göz atın&reg; Player etkin Internet tarayıcısı (Internet Explorer, Chrome, Firefox, vb.).</span><span class="sxs-lookup"><span data-stu-id="21357-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="21357-155">Kesintisiz akış içerikten Adobe içinde&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="21357-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="21357-156">Resmi genel OSMF geliştirme hakkında daha fazla bilgi için lütfen bkz [OSMF geliştirme sayfa](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="21357-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="21357-157">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="21357-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21357-158">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="21357-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="21357-159">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="21357-159">See Also</span></span>
[<span data-ttu-id="21357-160">Microsoft eklentisi OSMF güncelleştirmesi Uyarlamalı</span><span class="sxs-lookup"><span data-stu-id="21357-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

