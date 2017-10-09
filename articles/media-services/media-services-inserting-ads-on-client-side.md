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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="752a7-103">Merhaba istemci tarafında reklam ekleme</span><span class="sxs-lookup"><span data-stu-id="752a7-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="752a7-104">Bu konu hakkında bilgi içeren tooinsert hello istemci tarafında ads çeşitli türleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="752a7-105">Canlı akış videoları kapalı açıklamalı alt yazı ve ad desteği hakkında daha fazla bilgi için bkz: [desteklenen alanında Kapalı açıklamalı alt yazı ve Ad ekleme standartları](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="752a7-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="752a7-106">Azure Media Player Ads şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="752a7-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="752a7-107"><a id="insert_ads_into_media"></a>Reklam medyanızı ekleme</span><span class="sxs-lookup"><span data-stu-id="752a7-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="752a7-108">Azure Media Services hello Windows Media platformu aracılığıyla ad ekleme için destek sağlar: oynatıcı çerçevelerine.</span><span class="sxs-lookup"><span data-stu-id="752a7-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="752a7-109">Ad desteğiyle oynatıcı çerçevelerine Windows 8, Silverlight, Windows Phone 8 ve iOS cihazları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="752a7-110">Her player framework nasıl gösteren örnek kod içeren tooimplement oynatıcı uygulaması. Medya: listesine ekleyebilirsiniz ads üç farklı türde vardır.</span><span class="sxs-lookup"><span data-stu-id="752a7-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="752a7-111">**Doğrusal** – tam hello ana video duraklatma çerçevesi ads.</span><span class="sxs-lookup"><span data-stu-id="752a7-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="752a7-112">**Doğrusal** – hello ana video yürütme gibi görüntülenen katmana ads genellikle bir logo veya diğer statik görüntü yerleştirilen hello player içinde.</span><span class="sxs-lookup"><span data-stu-id="752a7-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="752a7-113">**Yardımcı** – hello player dışında görüntülenen ads.</span><span class="sxs-lookup"><span data-stu-id="752a7-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="752a7-114">Reklam hello ana videonun Zaman Çizelgesi herhangi bir noktada yerleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="752a7-115">Ne zaman tooplay hello ad ve hangi hello player söylemelisiniz ads tooplay.</span><span class="sxs-lookup"><span data-stu-id="752a7-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="752a7-116">Bu yapılır bir dizi standart XML tabanlı dosyaları kullanılarak: Video Ad Hizmeti şablonu (VAST), Dijital Video birden çok Ad çalma listesi (VMAP), medya soyut sıralama şablonu (a) ve Dijital Video Oynatıcı Ad arabirim tanımı (VPAID).</span><span class="sxs-lookup"><span data-stu-id="752a7-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="752a7-117">BÜYÜK dosyaları hangi ads toodisplay belirtin.</span><span class="sxs-lookup"><span data-stu-id="752a7-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="752a7-118">VMAP dosyaları belirttiğiniz tooplay çeşitli reklam ve büyük bir XML içeriyor.</span><span class="sxs-lookup"><span data-stu-id="752a7-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="752a7-119">A, büyük XML de içeren başka bir şekilde toosequence ads dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="752a7-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="752a7-120">VPAID dosyaları hello video oynatıcı ve hello ad veya ad sunucusu arasında bir arabirim tanımlar.</span><span class="sxs-lookup"><span data-stu-id="752a7-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="752a7-121">Her player framework farklı şekilde çalışır ve her biri kendi konusunda ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="752a7-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="752a7-122">Bu konuda hello kullanılan temel mekanizmaları tooinsert ads anlatmaktadır. Video oynatıcı uygulamaları ads bir ad sunucusundan isteyin.</span><span class="sxs-lookup"><span data-stu-id="752a7-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="752a7-123">Merhaba ad sunucusu, çeşitli yollarla yanıt verebilir:</span><span class="sxs-lookup"><span data-stu-id="752a7-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="752a7-124">BÜYÜK bir dosya</span><span class="sxs-lookup"><span data-stu-id="752a7-124">Return a VAST file</span></span>
* <span data-ttu-id="752a7-125">İade VMAP dosyası (ile katıştırılmış VAST)</span><span class="sxs-lookup"><span data-stu-id="752a7-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="752a7-126">Bir a dosyasıyla (katıştırılmış VAST) döndürür</span><span class="sxs-lookup"><span data-stu-id="752a7-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="752a7-127">VPAID ads sahip büyük bir dosya Döndür</span><span class="sxs-lookup"><span data-stu-id="752a7-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="752a7-128">Bir Video Ad Hizmeti şablonu (VAST) dosyasını kullanma</span><span class="sxs-lookup"><span data-stu-id="752a7-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="752a7-129">Hangi ad veya reklam toodisplay büyük dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="752a7-130">Merhaba aşağıdaki XML doğrusal ad için büyük bir dosya örneğidir:</span><span class="sxs-lookup"><span data-stu-id="752a7-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="752a7-131">Merhaba doğrusal ad hello tarafından açıklanan <**doğrusal**> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="752a7-132">Merhaba ad hello süreyi belirtir, olayları izleme, izleme'ye tıklayın ve bir dizi aracılığıyla, tıklama **MediaFile** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="752a7-133">İzleme olaylarını hello içinde belirtilen <**TrackingEvents**> öğesi ve bir ad sunucusu tootrack hello ad görüntülerken oluşan çeşitli olayları izin verin.</span><span class="sxs-lookup"><span data-stu-id="752a7-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="752a7-134">Bu durumda hello başlangıç, Orta, tam ve genişletin olayları izlenir.</span><span class="sxs-lookup"><span data-stu-id="752a7-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="752a7-135">Merhaba ad görüntülendiğinde hello başlangıç olayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="752a7-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="752a7-136">Merhaba Orta olayı en az % 50'hello reklamın çizelgesinin görüntülediğinde oluşur.</span><span class="sxs-lookup"><span data-stu-id="752a7-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="752a7-137">Merhaba ad toohello son çalıştırdığınızda hello complete olayını oluşur.</span><span class="sxs-lookup"><span data-stu-id="752a7-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="752a7-138">Merhaba kullanıcı hello video oynatıcı toofull ekran genişletirken hello genişletme olayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="752a7-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="752a7-139">Clickthroughs ile belirtilen bir <**geçişli tıklatma**> öğesinde bir <**VideoClicks**> öğesi ve hello kullanıcı üzerinde hello ad tıkladığında URI tooa kaynak toodisplay belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="752a7-140">ClickTracking belirtilen bir <**ClickTracking**> öğesinde, ayrıca merhaba <**VideoClicks**> öğesi ve hello kullanıcı tıkladığında hello player toorequest için bir izleme kaynağı belirtir Merhaba ad.hello üzerinde <**MediaFile**> öğeleri belirli bir kodlama bir ad ilgili bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="752a7-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="752a7-141">Olduğunda birden fazla <**MediaFile**> öğesi, hello video oynatıcı seçebilirsiniz hello hello platform için en iyi kodlama.</span><span class="sxs-lookup"><span data-stu-id="752a7-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="752a7-142">Doğrusal ads belirli bir sırada görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="752a7-143">toodo Bu, ek eklemek <Ad> öğeleri toohello VAST dosya ve hello sırası özniteliği kullanılarak hello düzenini belirtin.</span><span class="sxs-lookup"><span data-stu-id="752a7-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="752a7-144">Aşağıdaki örnek hello bunu göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="752a7-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="752a7-145">Doğrusal ads belirtilir bir <Creative> de öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="752a7-146">Aşağıdaki örnekte gösterildiği hello bir <Creative> doğrusal ad açıklar öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="752a7-147">Merhaba <**NonLinearAds**> öğesi bir veya daha fazla içerebilir <**NonLinear**> öğeleri, her biri bir doğrusal ad tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="752a7-148">Merhaba <**NonLinear**> öğesi hello kaynak hello doğrusal ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="752a7-149">Merhaba kaynak olabilir bir <**StaticResouce**> e <**IFrameResource**>, veya bir <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="752a7-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="752a7-150"> <**StaticResource**> olarak HTML olmayan kaynak açıklar ve hello kaynak nasıl görüntülendiğini belirten bir creativeType özniteliği tanımlar:</span><span class="sxs-lookup"><span data-stu-id="752a7-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="752a7-151">Görüntü/GIF, görüntü/jpeg resim/png – hello kaynak, bir HTML biçiminde görüntülenir <**img**> etiketi.</span><span class="sxs-lookup"><span data-stu-id="752a7-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="752a7-152">Uygulama/x-javascript – hello kaynak, bir HTML biçiminde görüntülenir <**betik**> etiketi.</span><span class="sxs-lookup"><span data-stu-id="752a7-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="752a7-153">Uygulama/x-shockwave-flash – hello kaynak bir Flash player görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="752a7-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="752a7-154">**IFrameResource** IFRAME içerisinde görüntülenen bir HTML kaynak açıklar.</span><span class="sxs-lookup"><span data-stu-id="752a7-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="752a7-155">**HTMLResource** bir web sayfasına eklenecek HTML kod parçası açıklar.</span><span class="sxs-lookup"><span data-stu-id="752a7-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="752a7-156">**TrackingEvents** hello olay gerçekleştiğinde URI toorequest hello ve izleme olaylarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="752a7-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="752a7-157">Bu örnek hello acceptInvitation ve Daralt olayları izlenir.</span><span class="sxs-lookup"><span data-stu-id="752a7-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="752a7-158">Merhaba hakkında daha fazla bilgi için **NonLinearAds** öğeyi ve alt öğelerini IAB.NET/VAST bakın.</span><span class="sxs-lookup"><span data-stu-id="752a7-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="752a7-159">Bu hello Not **TrackingEvents** öğesi hello içinde bulunduğu **NonLinearAds** hello yerine öğesi **NonLinear** öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="752a7-160">Yardımcı ads içinde tanımlanmış bir <CompanionAds> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="752a7-161">Merhaba <CompanionAds> öğesi bir veya daha fazla içerebilir <Companion> öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="752a7-162">Her <Companion> öğesi Yardımcısı ad açıklar ve içerebilir bir <StaticResource>, <IFrameResource>, veya <HTMLResource> hangi belirtilen içinde hello şekilde AD'de bir doğrusal olarak aynı.</span><span class="sxs-lookup"><span data-stu-id="752a7-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="752a7-163">BÜYÜK bir dosya birden çok yardımcı ads içerebilir ve Merhaba oynatıcı uygulaması hello en uygun ad toodisplay seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="752a7-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="752a7-164">VAST hakkında daha fazla bilgi için bkz: [büyük 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="752a7-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="752a7-165">Birden çok Ad çalma listesi (VMAP) dosyası bir Dijital Video kullanma</span><span class="sxs-lookup"><span data-stu-id="752a7-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="752a7-166">Ad sonları oluştuğunda toospecify, her sonu ne kadar olacağını, kaç ads sonu içinde görüntülenebilir ve ne ads türlerini olabilir sağlar VMAP dosya sonu sırasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="752a7-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="752a7-167">bir tek ad sonu tanımlayan bir örnek VMAP dosyasında aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="752a7-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="752a7-168">VMAP dosya ile başlayan bir <VMAP> içeren bir veya daha fazla öğe <AdBreak> öğeleri, her bir ad sonu tanımlama.</span><span class="sxs-lookup"><span data-stu-id="752a7-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="752a7-169">Her ad sonu sonu türü, kesme kimliği ve saat konumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="752a7-170">Merhaba breakType özniteliği hello sonu sırasında oynatılan ad hello türünü belirtir: Doğrusal, doğrusal, veya görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="752a7-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="752a7-171">Görüntü ads tooVAST Yardımcısı ads eşleyin.</span><span class="sxs-lookup"><span data-stu-id="752a7-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="752a7-172">Birden fazla ad türü (boşluksuz) virgülle ayrılmış liste belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="752a7-173">Merhaba breakID hello ad için isteğe bağlı bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="752a7-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="752a7-174">Merhaba timeOffset hello ad ne zaman görüntüleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="752a7-175">Yolları aşağıdaki hello biri belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="752a7-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="752a7-176">Saat – .mmm milisaniye olduğu ss: dd: veya ss:dd:ss.mmm biçimi.</span><span class="sxs-lookup"><span data-stu-id="752a7-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="752a7-177">Bu özniteliğin değeri Hello hello video zaman çizelgesi toohello hello ad sonu başlangıcını hello başlangıcını hello saati belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="752a7-178">Yüzde – n hello ad yürütmeden önce hello video zaman çizelgesi tooplay hello yüzdesi, %n biçimi</span><span class="sxs-lookup"><span data-stu-id="752a7-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="752a7-179">Başlangıç/bitiş – önce veya sonra hello video görüntülenen bir ad görüntüleneceğini belirtir</span><span class="sxs-lookup"><span data-stu-id="752a7-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="752a7-180">Konum – hello ad sonları hello zamanlamasını bilinmeyen, canlı akış olduğu gibi böyle olduğunda ad sonları hello sırasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="752a7-181">her ad sonu Hello sırasını n 1 veya daha büyük bir tamsayı olduğu hello #n biçiminde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="752a7-182">1 güveninin hello ad yürütülen hello ilk fırsatta hello ad yürütülen hello ikinci fırsatta vb. 2 olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="752a7-183">Merhaba içinde <**AdBreak**> öğesi var. bir olabilir <**AdSource**> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="752a7-184">Merhaba <**AdSource**> öğesi özniteliklerini aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="752a7-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="752a7-185">Kimliği – hello ad kaynağı için bir tanımlayıcı belirtir</span><span class="sxs-lookup"><span data-stu-id="752a7-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="752a7-186">allowMultipleAds – birden çok ads hello ad sonu sırasında görüntülenen olup olmadığını belirten bir Boole değeri</span><span class="sxs-lookup"><span data-stu-id="752a7-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="752a7-187">followRedirects – hello video oynatıcı dikkate belirten isteğe bağlı bir Boole değeri içinde bir ad yanıtı yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="752a7-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="752a7-188">Merhaba <**AdSource**> öğesi, bir satır içi ad yanıt veya bir başvuru tooan ad yanıt hello oynatıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="752a7-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="752a7-189">Öğeleri aşağıdaki hello birini içerebilir:</span><span class="sxs-lookup"><span data-stu-id="752a7-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="752a7-190"><VASTAdData>BÜYÜK ad yanıt hello VMAP dosyanın içinde ekli gösterir</span><span class="sxs-lookup"><span data-stu-id="752a7-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="752a7-191"><AdTagURI>başka bir sistemden bir ad yanıt başvuran bir URI</span><span class="sxs-lookup"><span data-stu-id="752a7-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="752a7-192"><CustomAdData>-bir rastgele bu respresents büyük olmayan bir yanıt dize</span><span class="sxs-lookup"><span data-stu-id="752a7-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="752a7-193">Bu örnekte, bir satır içi ad yanıt ile belirtilen bir <VASTAdData> büyük ad yanıtı içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="752a7-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="752a7-194">Diğer öğeleri hello hakkında daha fazla bilgi için bkz [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="752a7-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="752a7-195">Merhaba <**AdBreak**> öğesi de içerebilir bir <**TrackingEvents**> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="752a7-196">Merhaba <**TrackingEvents**> öğesi sağlar, size, tootrack hello başlangıç veya bitiş bir ad sonu veya olup hello ad sonu sırasında bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="752a7-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="752a7-197">Merhaba <**TrackingEvents**> öğesi içeren bir veya daha fazla <**izleme**> öğeleri, bir izleme olayı ve izleme URI her biri belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="752a7-198">Merhaba olası izleme olaylarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="752a7-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="752a7-199">breakStart – bir ad sonu hello başlangıcını izler</span><span class="sxs-lookup"><span data-stu-id="752a7-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="752a7-200">breakEnd – izleme hello tamamlandığında, bir ad sonu</span><span class="sxs-lookup"><span data-stu-id="752a7-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="752a7-201">hata – hello ad kesme sırasında oluşan hata izler</span><span class="sxs-lookup"><span data-stu-id="752a7-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="752a7-202">İzleme olaylarını belirten bir VMAP dosyası aşağıdaki örneğine hello gösterir</span><span class="sxs-lookup"><span data-stu-id="752a7-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="752a7-203">Merhaba hakkında daha fazla bilgi için <**TrackingEvents**> öğesi ve alt öğelerini http://iab.org/VMAP.pdf bakın</span><span class="sxs-lookup"><span data-stu-id="752a7-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="752a7-204">Şablon (a) dosyası sıralama medya Özet kullanma</span><span class="sxs-lookup"><span data-stu-id="752a7-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="752a7-205">Bir a dosyası, bir ad görüntülendiğinde tanımlamak toospecify Tetikleyiciler sağlar.</span><span class="sxs-lookup"><span data-stu-id="752a7-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="752a7-206">Merhaba, öncesi toplama ad, Orta toplama ad ve sonrası reklam için Tetikleyicileri içeren bir örnek a dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="752a7-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="752a7-207">Bir a dosyası ile başlayan bir **a** içeriyor öğesi **Tetikleyicileri** öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="752a7-208">Merhaba <triggers> öğesi içeren bir veya daha fazla **tetikleyici** bir ad zaman oynanan tanımlayan öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="752a7-209">Merhaba **tetikleyici** öğesi içeren bir **startConditions** bir ad tooplay ne zaman başlaması gerektiğini belirten öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="752a7-210">Merhaba **startConditions** öğesi içeren bir veya daha fazla <condition> öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="752a7-211">Zaman her <condition> tetikleyici başlatılır veya olup olmamasına iptal tootrue değerlendirir hello <condition> kapsamında yer alan bir **startConditions** veya **endConditions** öğesi sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="752a7-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="752a7-212">Zaman birden çok <condition> öğeleri, örtük veya olarak kabul edilir, tootrue değerlendirme herhangi bir koşul hello tetikleyici tooinitiate neden olur.</span><span class="sxs-lookup"><span data-stu-id="752a7-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="752a7-213"><condition>öğeleri içe olamaz.</span><span class="sxs-lookup"><span data-stu-id="752a7-213"><condition> elements can be nested.</span></span> <span data-ttu-id="752a7-214">Zaman alt <condition> öğeleri önceden bir örtük ve kabul edilir, tüm koşulların hello tetikleyici tooinitiate tootrue değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="752a7-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="752a7-215">Merhaba <condition> öğesi hello koşulu tanımla öznitelikleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="752a7-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="752a7-216">**tür** – hello koşul, olay veya özelliğin türünü belirtir</span><span class="sxs-lookup"><span data-stu-id="752a7-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="752a7-217">**ad** – hello değerlendirme sırasında kullanılan hello özelliği veya olayı toobe adı</span><span class="sxs-lookup"><span data-stu-id="752a7-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="752a7-218">**değer** – hello bir özelliğe göre hesaplanan değer</span><span class="sxs-lookup"><span data-stu-id="752a7-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="752a7-219">**İşleç** – işlemi toouse değerlendirme sırasında hello: EQ (eşittir), NEQ (eşit değildir), GTR (büyük), GEQ (büyük veya buna eşit), LT (küçük), LEQ (daha az veya buna eşit) MOD (modül)</span><span class="sxs-lookup"><span data-stu-id="752a7-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="752a7-220">**endConditions** de içeren <condition> öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="752a7-221">Tootrue hello tetikleyici bir koşulu değerlendirir reset.hello olduğunda <trigger> öğesi de içerir bir <sources> içeren bir veya daha fazla öğe <source> öğeleri.</span><span class="sxs-lookup"><span data-stu-id="752a7-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="752a7-222">Merhaba <source> öğelerini tanımlama hello URI toohello ad yanıt ve ad yanıt hello türü.</span><span class="sxs-lookup"><span data-stu-id="752a7-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="752a7-223">Bu örnekte bir URI tooa büyük yanıt verilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="752a7-224">Video oynatıcı Ad arabirim tanımı (VPAID) kullanma</span><span class="sxs-lookup"><span data-stu-id="752a7-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="752a7-225">VPAID, yürütülebilir ad birimleri toocommunicate bir video oynatıcı ile etkinleştirmek için bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="752a7-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="752a7-226">Bu, yüksek oranda etkileşimli ad deneyimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="752a7-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="752a7-227">Merhaba kullanıcı hello ad ile etkileşim kurabilir ve hello ad hello Görüntüleyici tarafından gerçekleştirilen tooactions yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="752a7-228">Örneğin bir ad hello kullanıcı tooview hello ad daha uzun bir sürümü veya daha fazla bilgi ver düğmeleri görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="752a7-229">Merhaba video oynatıcı hello VPAID API desteklemesi ve hello yürütülebilir ad hello API uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="752a7-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="752a7-230">Bir oyuncu bir ad sunucusu hello sunucusundan bir ad isteğinde bulunduğunda VPAID ad içeren büyük bir yanıt ile yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="752a7-231">Yürütülebilir bir ad, bir çalışma zamanı ortamında Adobe Flash™ veya bir web tarayıcısında yürütülebilecek JavaScript gibi yürütülmelidir kod oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="752a7-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="752a7-232">Bir ad sunucusu VPAID ad içeren büyük bir yanıtı geri döndüğünde, hello hello apiFramework özniteliğinin değeri hello <MediaFile> öğesi "VPAID" olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="752a7-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="752a7-233">Bu öznitelik, içerdiği hello ad VPAID yürütülebilir ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="752a7-234">Merhaba türü özniteliği hello toohello MIME türü "application/x-shockwave-flash" veya "uygulama/x-javascript" gibi yürütülebilir ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="752a7-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="752a7-235">Merhaba aşağıdaki XML parçacığını gösterir hello <MediaFile> VPAID yürütülebilir ad içeren büyük bir yanıtı öğesinden.</span><span class="sxs-lookup"><span data-stu-id="752a7-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="752a7-236">Yürütülebilir bir ad hello kullanılarak başlatılabilir <AdParameters> öğesi hello içinde <Linear> veya <NonLinear> öğeleri büyük bir yanıt.</span><span class="sxs-lookup"><span data-stu-id="752a7-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="752a7-237">Merhaba hakkında daha fazla bilgi için <AdParameters> öğesi, bkz: [büyük 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="752a7-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="752a7-238">Merhaba VPAID API'si hakkında daha fazla bilgi için bkz: [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="752a7-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="752a7-239">Bir Windows veya Windows Phone 8 Player Ad desteği ile uygulama</span><span class="sxs-lookup"><span data-stu-id="752a7-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="752a7-240">Merhaba Microsoft ortam platformu: Windows 8 için Player Framework ve Windows Phone 8 nasıl kullanarak bir video oynatıcı uygulaması tooimplement hello framework gösteren örnek uygulamalar koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="752a7-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="752a7-241">Merhaba Player Framework ve hello örneklerini indirin [Player Framework için Windows 8 ve Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="752a7-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="752a7-242">Merhaba Microsoft.PlayerFramework.Xaml.Samples çözümü açtığınızda klasörleri hello proje içindeki bir dizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="752a7-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="752a7-243">Merhaba reklam klasörü hello örnek kodu ilgili toocreating bir video oynatıcı ad desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="752a7-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="752a7-244">İç hello reklam klasördür bir XAML/cs dosyalarının sayısını her hangi Göster nasıl farklı bir şekilde tooinsert reklamları.</span><span class="sxs-lookup"><span data-stu-id="752a7-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="752a7-245">liste aşağıdaki hello açıklar:</span><span class="sxs-lookup"><span data-stu-id="752a7-245">hello following list describes each:</span></span>

* <span data-ttu-id="752a7-246">AdPodPage.xaml nasıl toodisplay bir ad pod gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a7-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="752a7-247">AdSchedulingPage.xaml gösterir nasıl tooschedule ads.</span><span class="sxs-lookup"><span data-stu-id="752a7-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="752a7-248">FreeWheelPage.xaml nasıl toouse hello FreeWheel eklentisi tooschedule ads gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a7-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="752a7-249">MastPage.xaml gösterir nasıl tooschedule ads a dosyası ile.</span><span class="sxs-lookup"><span data-stu-id="752a7-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="752a7-250">ProgrammaticAdPage.xaml nasıl tooprogrammatically zamanlama ads bir video gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a7-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="752a7-251">ScheduleClipPage.xaml gösterir nasıl tooschedule büyük dosyası olmadan bir ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="752a7-252">VastLinearCompanionPage.xaml gösterir nasıl tooinsert bir doğrusal ve yardımcı ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="752a7-253">VastNonLinearPage.xaml gösterir nasıl tooinsert doğrusal olmayan bir ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="752a7-254">VmapPage.xaml gösterir nasıl toospecify ads VMAP dosyası ile.</span><span class="sxs-lookup"><span data-stu-id="752a7-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="752a7-255">Bu örneklerin her hello player çerçevesi tarafından tanımlanan hello MediaPlayer sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="752a7-256">Çoğu örnekleri çeşitli ad yanıt biçimleri için destek eklemek eklentileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="752a7-257">Merhaba ProgrammaticAdPage örnek program aracılığıyla MediaPlayer örneği ile etkileşime girer.</span><span class="sxs-lookup"><span data-stu-id="752a7-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="752a7-258">AdPodPage örnek</span><span class="sxs-lookup"><span data-stu-id="752a7-258">AdPodPage Sample</span></span>
<span data-ttu-id="752a7-259">Bu örnek hello AdSchedulerPlugin toodefine kullandığı zaman toodisplay bir ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="752a7-260">Bu örnekte, bir orta toplama tanıtım 5 saniye sonra yürütülen zamanlanmış toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="752a7-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="752a7-261">Merhaba ad pod (ads toodisplay sırada grup), bir ad sunucusundan döndürülen büyük dosyasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="752a7-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="752a7-262">Merhaba URI toohello büyük dosya hello belirtilen <RemoteAdSource> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="752a7-263">Merhaba AdSchedulerPlugin hakkında daha fazla bilgi için bkz: [hello Player Framework'te Windows 8 ve Windows Phone 8 tanıtma](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="752a7-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="752a7-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="752a7-264">AdSchedulingPage</span></span>
<span data-ttu-id="752a7-265">Bu örnek ayrıca hello AdSchedulerPlugin kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="752a7-266">Üç reklam, yayın öncesi ad, bir orta toplama ad ve sonrası ad zamanlar.</span><span class="sxs-lookup"><span data-stu-id="752a7-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="752a7-267">her ad belirtildiği için URI toohello VAST hello bir <RemoteAdSource> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="752a7-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="752a7-268">FreeWheelPage</span></span>
<span data-ttu-id="752a7-269">Bu örnek hello URI ad zamanlama bilgilerini yanı sıra ad içeriği belirten bu noktaları tooa SmartXML dosyası belirten bir kaynak özniteliği belirten FreeWheelPlugin kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="752a7-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="752a7-270">MastPage</span></span>
<span data-ttu-id="752a7-271">Bu örnek hello toouse a dosya verir MastSchedulerPlugin kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="752a7-272">Merhaba kaynak özniteliği hello hello a dosyasının konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="752a7-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="752a7-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="752a7-274">Bu örnek program aracılığıyla MediaPlayer hello ile etkileşime girer.</span><span class="sxs-lookup"><span data-stu-id="752a7-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="752a7-275">Merhaba ProgrammaticAdPage.xaml dosya hello MediaPlayer başlatır:</span><span class="sxs-lookup"><span data-stu-id="752a7-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="752a7-276">Merhaba ProgrammaticAdPage.xaml.cs dosyasını bir AdHandlerPlugin oluşturur, bir ad görüntülenmesi gerekir ve ardından URI tooa büyük dosya belirtme RemoteAdSource yükler ve sonra çalar hello MarkerReached olay işleyicisi ekler TimelineMarker toospecify ekler Merhaba ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="752a7-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="752a7-277">ScheduleClipPage</span></span>
<span data-ttu-id="752a7-278">Bu örnek, hello ad içeren bir .wmv dosyasını belirterek hello AdSchedulerPlugin tooschedule Orta toplama ad kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="752a7-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="752a7-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="752a7-280">Bu örnek nasıl toouse hello AdSchedulerPlugin tooschedule Orta toplama doğrusal ad Yardımcısı ad ile gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="752a7-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="752a7-281">Merhaba <RemoteAdSource> öğesi hello hello büyük dosyasının konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="752a7-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="752a7-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="752a7-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="752a7-283">Bu örnek, bir doğrusal ve doğrusal olmayan ad hello AdSchedulerPlugin tooschedule kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="752a7-284">Merhaba büyük dosya konumu ile Merhaba belirtilen <RemoteAdSource> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="752a7-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="752a7-285">VMAPPage</span></span>
<span data-ttu-id="752a7-286">Bu örnekler VMAP dosyasını kullanarak hello VmapSchedulerPlugin tooschedule ads kullanır.</span><span class="sxs-lookup"><span data-stu-id="752a7-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="752a7-287">Merhaba URI toohello VMAP dosya hello kaynak özniteliğinde hello belirtilen <VmapSchedulerPlugin> öğesi.</span><span class="sxs-lookup"><span data-stu-id="752a7-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="752a7-288">Video Oynatıcı Ad desteğiyle iOS uygulama</span><span class="sxs-lookup"><span data-stu-id="752a7-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="752a7-289">Merhaba Microsoft ortam platformu: iOS için Player çerçevesi nasıl kullanarak bir video oynatıcı uygulaması tooimplement hello framework gösteren örnek uygulamalar koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="752a7-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="752a7-290">Merhaba Player Framework ve hello örneklerini indirin [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="752a7-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="752a7-291">Merhaba github sayfasına sahip bir bağlantı tooa hello player framework ve bir giriş toohello player örnek hakkında ek bilgi içeren Wiki: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="752a7-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="752a7-292">VMAP birlikte bir reklam planlama</span><span class="sxs-lookup"><span data-stu-id="752a7-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="752a7-293">örnekte gösterildiği nasıl aşağıdaki hello tooschedule ads VMAP dosyasını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="752a7-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="752a7-294">VAST birlikte bir reklam planlama</span><span class="sxs-lookup"><span data-stu-id="752a7-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="752a7-295">Merhaba aşağıdaki örnek gösterir nasıl tooschedule geç bağlama büyük ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="752a7-296">Merhaba aşağıdaki örnek gösterir nasıl tooschedule erken bağlama büyük ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="752a7-297">Örnek: 4 erken bir bağlama büyük ad //Download hello VAST dosya, zamanlama (! [ framework.adResolver downloadManifest: & bildirim withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[kendini logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="752a7-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="752a7-298">Merhaba aşağıdaki örnek gösterir nasıl tooinsert kaba kesme düzenleme (RCE) kullanarak bir ad</span><span class="sxs-lookup"><span data-stu-id="752a7-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="752a7-299">Merhaba aşağıdaki örnekte nasıl tooschedule bir ad pod gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="752a7-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="752a7-300">örnekte gösterildiği nasıl aşağıdaki hello tooschedule Yapışkan olmayan Orta toplama ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="752a7-301">Yapışkan olmayan bir ad, yalnızca bağımsız olarak tüm arama hello Görüntüleyicisi gerçekleştirir sonra oynatılır.</span><span class="sxs-lookup"><span data-stu-id="752a7-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="752a7-302">örnekte gösterildiği nasıl aşağıdaki hello tooschedule Yapışkan Orta toplama ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="752a7-303">Yapışkan ad hello video zaman çizelgesi noktasında ulaşıldığında hello belirtilen her zaman görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="752a7-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="752a7-304">Merhaba aşağıdaki örnek gösterir nasıl tooschedule sonrası ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="752a7-305">Merhaba aşağıdaki örnek gösterir nasıl tooschedule yayın öncesi ad.</span><span class="sxs-lookup"><span data-stu-id="752a7-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="752a7-306">Aşağıdaki örnek hello nasıl tooschedule Orta toplama ad kaplama gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a7-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="752a7-307">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="752a7-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="752a7-308">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="752a7-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="752a7-309">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="752a7-309">See Also</span></span>
[<span data-ttu-id="752a7-310">Video oynatıcı uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="752a7-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

