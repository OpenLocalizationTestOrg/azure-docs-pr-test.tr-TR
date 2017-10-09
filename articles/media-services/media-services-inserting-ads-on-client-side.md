---
title: "Merhaba istemci tarafında aaaInserting ads | Microsoft Docs"
description: "Bu konu, üzerinde tooinsert ads istemci tarafı nasıl hello gösterir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Merhaba istemci tarafında reklam ekleme
Bu konu hakkında bilgi içeren tooinsert hello istemci tarafında ads çeşitli türleri.

Canlı akış videoları kapalı açıklamalı alt yazı ve ad desteği hakkında daha fazla bilgi için bkz: [desteklenen alanında Kapalı açıklamalı alt yazı ve Ad ekleme standartları](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Azure Media Player Ads şu anda desteklemiyor.
> 
> 

## <a id="insert_ads_into_media"></a>Reklam medyanızı ekleme
Azure Media Services hello Windows Media platformu aracılığıyla ad ekleme için destek sağlar: oynatıcı çerçevelerine. Ad desteğiyle oynatıcı çerçevelerine Windows 8, Silverlight, Windows Phone 8 ve iOS cihazları için kullanılabilir. Her player framework nasıl gösteren örnek kod içeren tooimplement oynatıcı uygulaması. Medya: listesine ekleyebilirsiniz ads üç farklı türde vardır.

* **Doğrusal** – tam hello ana video duraklatma çerçevesi ads.
* **Doğrusal** – hello ana video yürütme gibi görüntülenen katmana ads genellikle bir logo veya diğer statik görüntü yerleştirilen hello player içinde.
* **Yardımcı** – hello player dışında görüntülenen ads.

Reklam hello ana videonun Zaman Çizelgesi herhangi bir noktada yerleştirilebilir. Ne zaman tooplay hello ad ve hangi hello player söylemelisiniz ads tooplay. Bu yapılır bir dizi standart XML tabanlı dosyaları kullanılarak: Video Ad Hizmeti şablonu (VAST), Dijital Video birden çok Ad çalma listesi (VMAP), medya soyut sıralama şablonu (a) ve Dijital Video Oynatıcı Ad arabirim tanımı (VPAID). BÜYÜK dosyaları hangi ads toodisplay belirtin. VMAP dosyaları belirttiğiniz tooplay çeşitli reklam ve büyük bir XML içeriyor. A, büyük XML de içeren başka bir şekilde toosequence ads dosyalarıdır. VPAID dosyaları hello video oynatıcı ve hello ad veya ad sunucusu arasında bir arabirim tanımlar.

Her player framework farklı şekilde çalışır ve her biri kendi konusunda ele alınacaktır. Bu konuda hello kullanılan temel mekanizmaları tooinsert ads anlatmaktadır. Video oynatıcı uygulamaları ads bir ad sunucusundan isteyin. Merhaba ad sunucusu, çeşitli yollarla yanıt verebilir:

* BÜYÜK bir dosya
* İade VMAP dosyası (ile katıştırılmış VAST)
* Bir a dosyasıyla (katıştırılmış VAST) döndürür
* VPAID ads sahip büyük bir dosya Döndür

### <a name="using-a-video-ad-service-template-vast-file"></a>Bir Video Ad Hizmeti şablonu (VAST) dosyasını kullanma
Hangi ad veya reklam toodisplay büyük dosyayı belirtir. Merhaba aşağıdaki XML doğrusal ad için büyük bir dosya örneğidir:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

Merhaba doğrusal ad hello tarafından açıklanan <**doğrusal**> öğesi. Merhaba ad hello süreyi belirtir, olayları izleme, izleme'ye tıklayın ve bir dizi aracılığıyla, tıklama **MediaFile** öğeleri. İzleme olaylarını hello içinde belirtilen <**TrackingEvents**> öğesi ve bir ad sunucusu tootrack hello ad görüntülerken oluşan çeşitli olayları izin verin. Bu durumda hello başlangıç, Orta, tam ve genişletin olayları izlenir. Merhaba ad görüntülendiğinde hello başlangıç olayı oluşur. Merhaba Orta olayı en az % 50'hello reklamın çizelgesinin görüntülediğinde oluşur. Merhaba ad toohello son çalıştırdığınızda hello complete olayını oluşur. Merhaba kullanıcı hello video oynatıcı toofull ekran genişletirken hello genişletme olayı oluşur. Clickthroughs ile belirtilen bir <**geçişli tıklatma**> öğesinde bir <**VideoClicks**> öğesi ve hello kullanıcı üzerinde hello ad tıkladığında URI tooa kaynak toodisplay belirtir. ClickTracking belirtilen bir <**ClickTracking**> öğesinde, ayrıca merhaba <**VideoClicks**> öğesi ve hello kullanıcı tıkladığında hello player toorequest için bir izleme kaynağı belirtir Merhaba ad.hello üzerinde <**MediaFile**> öğeleri belirli bir kodlama bir ad ilgili bilgileri belirtin. Olduğunda birden fazla <**MediaFile**> öğesi, hello video oynatıcı seçebilirsiniz hello hello platform için en iyi kodlama. 

Doğrusal ads belirli bir sırada görüntülenebilir. toodo Bu, ek eklemek <Ad> öğeleri toohello VAST dosya ve hello sırası özniteliği kullanılarak hello düzenini belirtin. Aşağıdaki örnek hello bunu göstermektedir:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Doğrusal ads belirtilir bir <Creative> de öğesi. Aşağıdaki örnekte gösterildiği hello bir <Creative> doğrusal ad açıklar öğesi.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Merhaba <**NonLinearAds**> öğesi bir veya daha fazla içerebilir <**NonLinear**> öğeleri, her biri bir doğrusal ad tanımlayabilir. Merhaba <**NonLinear**> öğesi hello kaynak hello doğrusal ad belirtir. Merhaba kaynak olabilir bir <**StaticResouce**> e <**IFrameResource**>, veya bir <**HTMLResouce**>. <**StaticResource**> olarak HTML olmayan kaynak açıklar ve hello kaynak nasıl görüntülendiğini belirten bir creativeType özniteliği tanımlar:

Görüntü/GIF, görüntü/jpeg resim/png – hello kaynak, bir HTML biçiminde görüntülenir <**img**> etiketi.

Uygulama/x-javascript – hello kaynak, bir HTML biçiminde görüntülenir <**betik**> etiketi.

Uygulama/x-shockwave-flash – hello kaynak bir Flash player görüntülenir.

**IFrameResource** IFRAME içerisinde görüntülenen bir HTML kaynak açıklar. **HTMLResource** bir web sayfasına eklenecek HTML kod parçası açıklar. **TrackingEvents** hello olay gerçekleştiğinde URI toorequest hello ve izleme olaylarını belirtin. Bu örnek hello acceptInvitation ve Daralt olayları izlenir. Merhaba hakkında daha fazla bilgi için **NonLinearAds** öğeyi ve alt öğelerini IAB.NET/VAST bakın. Bu hello Not **TrackingEvents** öğesi hello içinde bulunduğu **NonLinearAds** hello yerine öğesi **NonLinear** öğesi.

Yardımcı ads içinde tanımlanmış bir <CompanionAds> öğesi. Merhaba <CompanionAds> öğesi bir veya daha fazla içerebilir <Companion> öğeleri. Her <Companion> öğesi Yardımcısı ad açıklar ve içerebilir bir <StaticResource>, <IFrameResource>, veya <HTMLResource> hangi belirtilen içinde hello şekilde AD'de bir doğrusal olarak aynı. BÜYÜK bir dosya birden çok yardımcı ads içerebilir ve Merhaba oynatıcı uygulaması hello en uygun ad toodisplay seçebilirsiniz. VAST hakkında daha fazla bilgi için bkz: [büyük 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Birden çok Ad çalma listesi (VMAP) dosyası bir Dijital Video kullanma
Ad sonları oluştuğunda toospecify, her sonu ne kadar olacağını, kaç ads sonu içinde görüntülenebilir ve ne ads türlerini olabilir sağlar VMAP dosya sonu sırasında görüntülenir. bir tek ad sonu tanımlayan bir örnek VMAP dosyasında aşağıdaki hello:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

VMAP dosya ile başlayan bir <VMAP> içeren bir veya daha fazla öğe <AdBreak> öğeleri, her bir ad sonu tanımlama. Her ad sonu sonu türü, kesme kimliği ve saat konumu belirtir. Merhaba breakType özniteliği hello sonu sırasında oynatılan ad hello türünü belirtir: Doğrusal, doğrusal, veya görüntüleme. Görüntü ads tooVAST Yardımcısı ads eşleyin. Birden fazla ad türü (boşluksuz) virgülle ayrılmış liste belirtilebilir. Merhaba breakID hello ad için isteğe bağlı bir tanımlayıcıdır. Merhaba timeOffset hello ad ne zaman görüntüleneceğini belirtir. Yolları aşağıdaki hello biri belirtilebilir:

1. Saat – .mmm milisaniye olduğu ss: dd: veya ss:dd:ss.mmm biçimi. Bu özniteliğin değeri Hello hello video zaman çizelgesi toohello hello ad sonu başlangıcını hello başlangıcını hello saati belirtir.
2. Yüzde – n hello ad yürütmeden önce hello video zaman çizelgesi tooplay hello yüzdesi, %n biçimi
3. Başlangıç/bitiş – önce veya sonra hello video görüntülenen bir ad görüntüleneceğini belirtir
4. Konum – hello ad sonları hello zamanlamasını bilinmeyen, canlı akış olduğu gibi böyle olduğunda ad sonları hello sırasını belirtir. her ad sonu Hello sırasını n 1 veya daha büyük bir tamsayı olduğu hello #n biçiminde belirtilir. 1 güveninin hello ad yürütülen hello ilk fırsatta hello ad yürütülen hello ikinci fırsatta vb. 2 olduğunu belirtir.

Merhaba içinde <**AdBreak**> öğesi var. bir olabilir <**AdSource**> öğesi. Merhaba <**AdSource**> öğesi özniteliklerini aşağıdaki hello içerir:

1. Kimliği – hello ad kaynağı için bir tanımlayıcı belirtir
2. allowMultipleAds – birden çok ads hello ad sonu sırasında görüntülenen olup olmadığını belirten bir Boole değeri
3. followRedirects – hello video oynatıcı dikkate belirten isteğe bağlı bir Boole değeri içinde bir ad yanıtı yeniden yönlendirir.

Merhaba <**AdSource**> öğesi, bir satır içi ad yanıt veya bir başvuru tooan ad yanıt hello oynatıcı sağlar. Öğeleri aşağıdaki hello birini içerebilir:

* <VASTAdData>BÜYÜK ad yanıt hello VMAP dosyanın içinde ekli gösterir
* <AdTagURI>başka bir sistemden bir ad yanıt başvuran bir URI
* <CustomAdData>-bir rastgele bu respresents büyük olmayan bir yanıt dize

Bu örnekte, bir satır içi ad yanıt ile belirtilen bir <VASTAdData> büyük ad yanıtı içeren öğe. Diğer öğeleri hello hakkında daha fazla bilgi için bkz [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Merhaba <**AdBreak**> öğesi de içerebilir bir <**TrackingEvents**> öğesi. Merhaba <**TrackingEvents**> öğesi sağlar, size, tootrack hello başlangıç veya bitiş bir ad sonu veya olup hello ad sonu sırasında bir hata oluştu. Merhaba <**TrackingEvents**> öğesi içeren bir veya daha fazla <**izleme**> öğeleri, bir izleme olayı ve izleme URI her biri belirtir. Merhaba olası izleme olaylarını şunlardır:

1. breakStart – bir ad sonu hello başlangıcını izler
2. breakEnd – izleme hello tamamlandığında, bir ad sonu
3. hata – hello ad kesme sırasında oluşan hata izler

İzleme olaylarını belirten bir VMAP dosyası aşağıdaki örneğine hello gösterir

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Merhaba hakkında daha fazla bilgi için <**TrackingEvents**> öğesi ve alt öğelerini http://iab.org/VMAP.pdf bakın

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Şablon (a) dosyası sıralama medya Özet kullanma
Bir a dosyası, bir ad görüntülendiğinde tanımlamak toospecify Tetikleyiciler sağlar. Merhaba, öncesi toplama ad, Orta toplama ad ve sonrası reklam için Tetikleyicileri içeren bir örnek a dosyası aşağıdadır.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



Bir a dosyası ile başlayan bir **a** içeriyor öğesi **Tetikleyicileri** öğesi. Merhaba <triggers> öğesi içeren bir veya daha fazla **tetikleyici** bir ad zaman oynanan tanımlayan öğeleri. 

Merhaba **tetikleyici** öğesi içeren bir **startConditions** bir ad tooplay ne zaman başlaması gerektiğini belirten öğesi. Merhaba **startConditions** öğesi içeren bir veya daha fazla <condition> öğeleri. Zaman her <condition> tetikleyici başlatılır veya olup olmamasına iptal tootrue değerlendirir hello <condition> kapsamında yer alan bir **startConditions** veya **endConditions** öğesi sırasıyla. Zaman birden çok <condition> öğeleri, örtük veya olarak kabul edilir, tootrue değerlendirme herhangi bir koşul hello tetikleyici tooinitiate neden olur. <condition>öğeleri içe olamaz. Zaman alt <condition> öğeleri önceden bir örtük ve kabul edilir, tüm koşulların hello tetikleyici tooinitiate tootrue değerlendirmeniz gerekir. Merhaba <condition> öğesi hello koşulu tanımla öznitelikleri aşağıdaki hello içerir: 

1. **tür** – hello koşul, olay veya özelliğin türünü belirtir
2. **ad** – hello değerlendirme sırasında kullanılan hello özelliği veya olayı toobe adı
3. **değer** – hello bir özelliğe göre hesaplanan değer
4. **İşleç** – işlemi toouse değerlendirme sırasında hello: EQ (eşittir), NEQ (eşit değildir), GTR (büyük), GEQ (büyük veya buna eşit), LT (küçük), LEQ (daha az veya buna eşit) MOD (modül)

**endConditions** de içeren <condition> öğeleri. Tootrue hello tetikleyici bir koşulu değerlendirir reset.hello olduğunda <trigger> öğesi de içerir bir <sources> içeren bir veya daha fazla öğe <source> öğeleri. Merhaba <source> öğelerini tanımlama hello URI toohello ad yanıt ve ad yanıt hello türü. Bu örnekte bir URI tooa büyük yanıt verilir. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Video oynatıcı Ad arabirim tanımı (VPAID) kullanma
VPAID, yürütülebilir ad birimleri toocommunicate bir video oynatıcı ile etkinleştirmek için bir API'dir. Bu, yüksek oranda etkileşimli ad deneyimleri sağlar. Merhaba kullanıcı hello ad ile etkileşim kurabilir ve hello ad hello Görüntüleyici tarafından gerçekleştirilen tooactions yanıt verebilir. Örneğin bir ad hello kullanıcı tooview hello ad daha uzun bir sürümü veya daha fazla bilgi ver düğmeleri görüntüleyebilir. Merhaba video oynatıcı hello VPAID API desteklemesi ve hello yürütülebilir ad hello API uygulamanız gerekir. Bir oyuncu bir ad sunucusu hello sunucusundan bir ad isteğinde bulunduğunda VPAID ad içeren büyük bir yanıt ile yanıt verebilir.

Yürütülebilir bir ad, bir çalışma zamanı ortamında Adobe Flash™ veya bir web tarayıcısında yürütülebilecek JavaScript gibi yürütülmelidir kod oluşturulur. Bir ad sunucusu VPAID ad içeren büyük bir yanıtı geri döndüğünde, hello hello apiFramework özniteliğinin değeri hello <MediaFile> öğesi "VPAID" olması gerekir. Bu öznitelik, içerdiği hello ad VPAID yürütülebilir ad belirtir. Merhaba türü özniteliği hello toohello MIME türü "application/x-shockwave-flash" veya "uygulama/x-javascript" gibi yürütülebilir ayarlanmalıdır. Merhaba aşağıdaki XML parçacığını gösterir hello <MediaFile> VPAID yürütülebilir ad içeren büyük bir yanıtı öğesinden. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Yürütülebilir bir ad hello kullanılarak başlatılabilir <AdParameters> öğesi hello içinde <Linear> veya <NonLinear> öğeleri büyük bir yanıt. Merhaba hakkında daha fazla bilgi için <AdParameters> öğesi, bkz: [büyük 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Merhaba VPAID API'si hakkında daha fazla bilgi için bkz: [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Bir Windows veya Windows Phone 8 Player Ad desteği ile uygulama
Merhaba Microsoft ortam platformu: Windows 8 için Player Framework ve Windows Phone 8 nasıl kullanarak bir video oynatıcı uygulaması tooimplement hello framework gösteren örnek uygulamalar koleksiyonunu içerir. Merhaba Player Framework ve hello örneklerini indirin [Player Framework için Windows 8 ve Windows Phone 8](https://playerframework.codeplex.com).

Merhaba Microsoft.PlayerFramework.Xaml.Samples çözümü açtığınızda klasörleri hello proje içindeki bir dizi görürsünüz. Merhaba reklam klasörü hello örnek kodu ilgili toocreating bir video oynatıcı ad desteği içerir. İç hello reklam klasördür bir XAML/cs dosyalarının sayısını her hangi Göster nasıl farklı bir şekilde tooinsert reklamları. liste aşağıdaki hello açıklar:

* AdPodPage.xaml nasıl toodisplay bir ad pod gösterir.
* AdSchedulingPage.xaml gösterir nasıl tooschedule ads.
* FreeWheelPage.xaml nasıl toouse hello FreeWheel eklentisi tooschedule ads gösterir.
* MastPage.xaml gösterir nasıl tooschedule ads a dosyası ile.
* ProgrammaticAdPage.xaml nasıl tooprogrammatically zamanlama ads bir video gösterir.
* ScheduleClipPage.xaml gösterir nasıl tooschedule büyük dosyası olmadan bir ad.
* VastLinearCompanionPage.xaml gösterir nasıl tooinsert bir doğrusal ve yardımcı ad.
* VastNonLinearPage.xaml gösterir nasıl tooinsert doğrusal olmayan bir ad.
* VmapPage.xaml gösterir nasıl toospecify ads VMAP dosyası ile.

Bu örneklerin her hello player çerçevesi tarafından tanımlanan hello MediaPlayer sınıfını kullanır. Çoğu örnekleri çeşitli ad yanıt biçimleri için destek eklemek eklentileri kullanır. Merhaba ProgrammaticAdPage örnek program aracılığıyla MediaPlayer örneği ile etkileşime girer.

### <a name="adpodpage-sample"></a>AdPodPage örnek
Bu örnek hello AdSchedulerPlugin toodefine kullandığı zaman toodisplay bir ad. Bu örnekte, bir orta toplama tanıtım 5 saniye sonra yürütülen zamanlanmış toobe ' dir. Merhaba ad pod (ads toodisplay sırada grup), bir ad sunucusundan döndürülen büyük dosyasında belirtilir. Merhaba URI toohello büyük dosya hello belirtilen <RemoteAdSource> öğesi.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Merhaba AdSchedulerPlugin hakkında daha fazla bilgi için bkz: [hello Player Framework'te Windows 8 ve Windows Phone 8 tanıtma](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
Bu örnek ayrıca hello AdSchedulerPlugin kullanır. Üç reklam, yayın öncesi ad, bir orta toplama ad ve sonrası ad zamanlar. her ad belirtildiği için URI toohello VAST hello bir <RemoteAdSource> öğesi.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
Bu örnek hello URI ad zamanlama bilgilerini yanı sıra ad içeriği belirten bu noktaları tooa SmartXML dosyası belirten bir kaynak özniteliği belirten FreeWheelPlugin kullanır.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Bu örnek hello toouse a dosya verir MastSchedulerPlugin kullanır. Merhaba kaynak özniteliği hello hello a dosyasının konumunu belirtir.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
Bu örnek program aracılığıyla MediaPlayer hello ile etkileşime girer. Merhaba ProgrammaticAdPage.xaml dosya hello MediaPlayer başlatır:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

Merhaba ProgrammaticAdPage.xaml.cs dosyasını bir AdHandlerPlugin oluşturur, bir ad görüntülenmesi gerekir ve ardından URI tooa büyük dosya belirtme RemoteAdSource yükler ve sonra çalar hello MarkerReached olay işleyicisi ekler TimelineMarker toospecify ekler Merhaba ad.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
Bu örnek, hello ad içeren bir .wmv dosyasını belirterek hello AdSchedulerPlugin tooschedule Orta toplama ad kullanır.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
Bu örnek nasıl toouse hello AdSchedulerPlugin tooschedule Orta toplama doğrusal ad Yardımcısı ad ile gösterilmektedir. Merhaba <RemoteAdSource> öğesi hello hello büyük dosyasının konumunu belirtir.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Bu örnek, bir doğrusal ve doğrusal olmayan ad hello AdSchedulerPlugin tooschedule kullanır. Merhaba büyük dosya konumu ile Merhaba belirtilen <RemoteAdSource> öğesi.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
Bu örnekler VMAP dosyasını kullanarak hello VmapSchedulerPlugin tooschedule ads kullanır. Merhaba URI toohello VMAP dosya hello kaynak özniteliğinde hello belirtilen <VmapSchedulerPlugin> öğesi.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Video Oynatıcı Ad desteğiyle iOS uygulama
Merhaba Microsoft ortam platformu: iOS için Player çerçevesi nasıl kullanarak bir video oynatıcı uygulaması tooimplement hello framework gösteren örnek uygulamalar koleksiyonunu içerir. Merhaba Player Framework ve hello örneklerini indirin [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). Merhaba github sayfasına sahip bir bağlantı tooa hello player framework ve bir giriş toohello player örnek hakkında ek bilgi içeren Wiki: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>VMAP birlikte bir reklam planlama
örnekte gösterildiği nasıl aşağıdaki hello tooschedule ads VMAP dosyasını kullanarak.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>VAST birlikte bir reklam planlama
Merhaba aşağıdaki örnek gösterir nasıl tooschedule geç bağlama büyük ad.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   Merhaba aşağıdaki örnek gösterir nasıl tooschedule erken bağlama büyük ad.
Örnek: 4 erken bir bağlama büyük ad //Download hello VAST dosya, zamanlama (! [ framework.adResolver downloadManifest: & bildirim withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[kendini logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

Merhaba aşağıdaki örnek gösterir nasıl tooinsert kaba kesme düzenleme (RCE) kullanarak bir ad

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Merhaba aşağıdaki örnekte nasıl tooschedule bir ad pod gösterilmektedir.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

örnekte gösterildiği nasıl aşağıdaki hello tooschedule Yapışkan olmayan Orta toplama ad. Yapışkan olmayan bir ad, yalnızca bağımsız olarak tüm arama hello Görüntüleyicisi gerçekleştirir sonra oynatılır.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

örnekte gösterildiği nasıl aşağıdaki hello tooschedule Yapışkan Orta toplama ad. Yapışkan ad hello video zaman çizelgesi noktasında ulaşıldığında hello belirtilen her zaman görüntülenir.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


Merhaba aşağıdaki örnek gösterir nasıl tooschedule sonrası ad.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Merhaba aşağıdaki örnek gösterir nasıl tooschedule yayın öncesi ad.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Aşağıdaki örnek hello nasıl tooschedule Orta toplama ad kaplama gösterir.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Video oynatıcı uygulamaları geliştirme](media-services-develop-video-players.md)

