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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Nasıl tooUse hello Microsoft kesintisiz akış eklentisi Merhaba Adobe açık kaynak medya çerçeve
## <a name="overview"></a>Genel Bakış
Açık kaynak Media Framework 2.0 (SS OSMF için) hello varsayılan OSMF yeteneklerini genişletir ve Microsoft kesintisiz akış içeriği oynatmayı toonew ve varolan OSMF ekler için Microsoft kesintisiz akış eklentisi hello oynatıcıları. Merhaba eklentisi ayrıca kesintisiz Akış kayıttan yürütme özellikleri tooStrobe medya kayıttan yürütme (SMP) ekler.

OSMF SS eklentisi iki sürümünü içerir:

* OSMF (.swc) için statik kesintisiz akış eklentisi
* OSMF (.swf) için dinamik kesintisiz akış eklentisi

Bu belge hello okuyucu OSMF ve OSMF genel bilgisine sahip olduğunu varsayar eklentileri. OSMF hakkında daha fazla bilgi için hello belge üzerinde hello lütfen bkz. [resmi OSMF sitesi](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>OSMF 2.0 için kesintisiz akış eklentisi
Merhaba eklentisi özellikleri aşağıdaki hello ile yükleme ve isteğe bağlı kesintisiz akış içeriği kayıttan yürütmeyi destekler:

* İsteğe bağlı kesintisiz Akış kayıttan yürütme (yürütme, duraklatma, arama, Dur)
* Canlı kesintisiz Akış kayıttan yürütme (kullan)
* Canlı DVR işlevleri (Duraklat, arama, DVR kayıttan yürütme, Canlı Git)
* Görüntü codec bileşenleri - H.264 desteği
* Ses codec bileşenleri - AAC desteği
* Birden çok ses dil OSMF yerleşik API'leri ile değiştirme
* En fazla kayıttan yürütme kalitesi seçimi OSMF yerleşik API'leri ile
* Resim yazıları OSMF resim yazıları eklentisi ile sepet kapalı
* Adobe&reg; Flash&reg; Player 11.4 ya da daha yüksek.
* Bu sürümü yalnızca OSMF 2.0 destekler.

## <a name="supported-features-and-known-issues"></a>Desteklenen özellikler ve bilinen sorunlar
Desteklenen özellikler, desteklenmeyen özellikler ve bilinen sorunlar tam listesi için çok bakın[bu belgeyi](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Yükleme hello eklentisi
Statik olarak (derleme zamanında) OSMF eklentileri yüklenebilir veya dinamik olarak (çalışma zamanında). Merhaba kesintisiz akış eklentisi OSMF indirmek için dinamik ve statik sürümlerini içerir.

* Statik yükleme: tooload statik olarak, bir statik kitaplık (SWC) dosyası gereklidir. Statik eklentileri bir başvuru olarak eklenen dosya hello derleme zamanında toohello projeleri ve birleştirme hello son çıktı içinde.
* Dinamik yükleme: tooload dinamik olarak derlenmiş bir (SWF) dosyası gereklidir. Dinamik eklenti hello çalışma zamanı yüklendi ve hello proje çıktısına dahil değildir. (Derlenmiş çıktı) Dinamik eklenti, HTTP ve dosya protokolleri kullanılarak yüklenebilir.

Statik ve dinamik yükleme hakkında daha fazla bilgi için bkz: hello resmi [OSMF eklenti sayfası](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>SS OSMF statik yükleme için
Aşağıdaki kod parçacığında Hello nasıl tooload SS eklentisi OSMF için statik olarak hello ve OSMF MediaFactory sınıfını kullanarak bir temel çalmasına gösterir. Merhaba SS OSMF kodu eklemeden önce lütfen hello proje başvurusu hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" statik eklentisi içerdiğinden emin olun.

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


### <a name="ss-for-osmf-dynamic-loading"></a>SS OSMF dinamik yükleme için
Aşağıdaki kod parçacığında Hello nasıl tooload SS eklentisi OSMF için dinamik olarak hello ve hello OSMF MediaFactory sınıfını kullanarak bir temel çalmasına gösterir. Dosya Protokolü kullanarak tooload istediğiniz veya bir web sunucusu HTTP yük altında kopyalarsanız hello SS OSMF kodu eklemeden önce hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" dinamik eklenti toohello proje klasörüne kopyalayın. Merhaba proje başvuruları hiçbir gerek tooinclude "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" dir.

Paket {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Merhaba SS ODMF dinamik eklenti ile flaş ortam çalma
Merhaba kesintisiz akış OSMF dinamik eklenti için uyumlu [flaş medya kayıttan yürütme (SMP)](http://osmf.org/strobe_mediaplayback.html). Merhaba SS OSMF eklentisi tooadd kesintisiz akış içeriği oynatmayı tooSMP için kullanabilirsiniz. toodo "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" bir web sunucusu altında aşağıdaki hello kullanarak HTTP yük için adımları Bu, kopyalama:

1. Merhaba Gözat [flaş Media Çalma Kurulum sayfasında](http://osmf.org/dev/2.0gm/setup.html). 
2. Merhaba src tooa kesintisiz akış kaynak, (örneğin http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) ayarlayın 
3. İstenen hello yapılandırma değişikliklerini yapın ve Önizleme ve güncelleştirme'yi tıklatın.
   
   **Not** içerik web sunucunuzun geçerli crossdomain.xml gerekiyor. 
4. Kopyalama ve yapıştırma hello örnek aşağıdaki gibi sık kullandığınız metin düzenleyiciyi kullanarak hello kod tooa basit HTML sayfası:

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



1. Kesintisiz akış OSMF eklentisi toohello eklemek ekleme kodu edinin ve kaydedin.
   
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
2. HTML sayfası kaydedin ve tooa web sunucusunda yayımlayın. Gözat toohello yayımlanan web sayfasını kullanarak, sık kullanılan Flash&reg; Player etkin Internet tarayıcısı (Internet Explorer, Chrome, Firefox, vb.).
3. Kesintisiz akış içerikten Adobe içinde&reg; Flash&reg; Player.

Merhaba resmi genel OSMF geliştirme hakkında daha fazla bilgi için lütfen bkz [OSMF geliştirme sayfa](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Microsoft eklentisi OSMF güncelleştirmesi Uyarlamalı](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

