---
title: "aaaGet başlatılan hello Azure portal kullanarak VoD göndermeye | Microsoft Docs"
description: "Bu öğreticide, hello Azure portal kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="bad89-103">Hello Azure portal kullanarak isteğe bağlı içerik göndermeye başlama</span><span class="sxs-lookup"><span data-stu-id="bad89-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="bad89-104">Bu öğreticide, hello Azure portal kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bad89-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bad89-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bad89-105">Prerequisites</span></span>
<span data-ttu-id="bad89-106">Merhaba, gerekli toocomplete hello öğretici şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bad89-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="bad89-107">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="bad89-107">An Azure account.</span></span> <span data-ttu-id="bad89-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bad89-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="bad89-109">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="bad89-109">A Media Services account.</span></span> <span data-ttu-id="bad89-110">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bad89-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="bad89-111">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="bad89-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="bad89-112">Akış uç noktasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="bad89-113">Bir video dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bad89-113">Upload a video file.</span></span>
3. <span data-ttu-id="bad89-114">Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın.</span><span class="sxs-lookup"><span data-stu-id="bad89-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="bad89-115">Merhaba varlık ve get akış ve aşamalı indirme URL'leri yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="bad89-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="bad89-116">İçeriğinizi oynatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="bad89-117">Akış uç noktalarını başlatma</span><span class="sxs-lookup"><span data-stu-id="bad89-117">Start streaming endpoints</span></span> 

<span data-ttu-id="bad89-118">Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="bad89-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="bad89-119">Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.</span><span class="sxs-lookup"><span data-stu-id="bad89-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="bad89-120">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="bad89-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="bad89-121">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="bad89-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="bad89-122">toostart akış uç Merhaba, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bad89-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="bad89-123">Merhaba oturum açma [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bad89-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bad89-124">Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="bad89-125">Merhaba varsayılan akış uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="bad89-126">Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bad89-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="bad89-127">Merhaba başlangıç simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bad89-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="bad89-128">Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="bad89-129">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="bad89-129">Upload files</span></span>
<span data-ttu-id="bad89-130">Azure Media Services kullanarak videoların, tooupload hello kaynak videoları, gereksinim duyduğunuz toostream Çoklu bit hızına kodlamanız ve yayımlama hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="bad89-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="bad89-131">Merhaba ilk adım, bu bölümde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="bad89-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="bad89-132">Merhaba, **ayarı** penceresinde tıklatın **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="bad89-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Dosyaları karşıya yükleme](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="bad89-134">Merhaba tıklatın **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bad89-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="bad89-135">Merhaba **bir varlığı karşıya yükle** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bad89-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bad89-136">Dosya boyutu sınırlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="bad89-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="bad89-137">Bilgisayarınızda istenen toohello video göz atın, onu seçin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bad89-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="bad89-138">Merhaba karşıya yükleme başlar ve hello dosya adı altında hello ilerleme durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bad89-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="bad89-139">Merhaba karşıya yükleme işlemi tamamlandıktan sonra hello yeni varlık hello listelenen bkz **varlıklar** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bad89-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="bad89-140">Varlıkları kodlama</span><span class="sxs-lookup"><span data-stu-id="bad89-140">Encode assets</span></span>

<span data-ttu-id="bad89-141">Merhaba en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı akış tooyour istemcileri iletmektir Azure Media Services ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="bad89-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="bad89-142">Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello destekler: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="bad89-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="bad89-143">tooprepare videolarınızı bit hızı Uyarlamalı akış için tooencode kaynağınız video Çoklu bit hızlı dosyalarıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="bad89-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="bad89-144">Merhaba kullanması gereken **Medya Kodlayıcısı standart** Kodlayıcı tooencode videolarınızı.</span><span class="sxs-lookup"><span data-stu-id="bad89-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="bad89-145">Media Services, Çoklu bit hızlı MP4s akış biçimlerine aşağıdaki hello içinde de toodeliver sağlayan dinamik paketleme sağlar: MPEG DASH, HLS, kesintisiz akış, bu akış biçimlerine toorepackage kalmadan olmadan.</span><span class="sxs-lookup"><span data-stu-id="bad89-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="bad89-146">Dinamik paketleme ile toostore yeterlidir ve ödeme tek bir depolama biçiminde ve Media Services hello dosyaları oluşturur ve istemciden gelen isteklere göre uygun yanıtı hello işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="bad89-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="bad89-147">tootake avantajı dinamik paketleme, tooencode kaynak dosyanızı Çoklu bit hızlı MP4 dosyaları (kodlama adımları hello gösterilmektedir daha sonra bu bölümde) kümesine ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="bad89-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="bad89-148">toouse hello portal tooencode</span><span class="sxs-lookup"><span data-stu-id="bad89-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="bad89-149">Bu bölüm, içeriğinizi Medya Kodlayıcısı standart ile tooencode uygulayabileceğiniz hello adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="bad89-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="bad89-150">Merhaba, **ayarları** penceresinde, seçin **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="bad89-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="bad89-151">Merhaba, **varlıklar** penceresinde, select hello varlık tooencode istersiniz.</span><span class="sxs-lookup"><span data-stu-id="bad89-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="bad89-152">Tuşuna hello **kodla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bad89-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="bad89-153">Merhaba, **bir varlık kodla** penceresi, select hello "Medya Kodlayıcısı standart" işlemcisini ve bir hazır.</span><span class="sxs-lookup"><span data-stu-id="bad89-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="bad89-154">Hazır ayarlar hakkında daha fazla bilgi için bkz. [Bit hızı merdivenini otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md) ve [MES Görev Ön Ayarları](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bad89-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="bad89-155">Hangi kodlama hazır kullanılır toocontrol planlıyorsanız, bunu göz önünde bulundurun: tooselect hello giriş videonuzun için en uygun olan Önayar önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bad89-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="bad89-156">Giriş videonuzun 1920 x 1080 piksel çözünürlüğü sahip biliyorsanız, örneğin, hello kullanabilirsiniz "H264 Çoklu bit hızı 1080p" hazır.</span><span class="sxs-lookup"><span data-stu-id="bad89-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="bad89-157">Düşük çözünürlüklü (640 x 360) bir videonuz olması durumunda "H264 Çoklu Bit hızı 1080p" ön ayarını kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="bad89-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="bad89-158">Daha kolay yönetim için hello hello çıkış varlık adını düzenleme ve hello işinin hello adı bir seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="bad89-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Varlıkları kodlama](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="bad89-160">**Oluştur**’a basın.</span><span class="sxs-lookup"><span data-stu-id="bad89-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="bad89-161">Kodlama işi ilerleme durumunu izleme</span><span class="sxs-lookup"><span data-stu-id="bad89-161">Monitor encoding job progress</span></span>
<span data-ttu-id="bad89-162">İş, kodlama hello toomonitor hello ilerlemesini tıklatın **ayarları** (Merhaba sayfanın en üstündeki hello) ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="bad89-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![İşler](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="bad89-164">İçerik yayımlama</span><span class="sxs-lookup"><span data-stu-id="bad89-164">Publish content</span></span>
<span data-ttu-id="bad89-165">tooprovide kullanılan toostream ya da içeriğinizi indirme URL'si, kullanıcı, önce çok "varlığınız bir Bulucu oluşturarak yayımlamanız".</span><span class="sxs-lookup"><span data-stu-id="bad89-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="bad89-166">Bulucular hello varlıkta bulunan erişim toofiles sağlar.</span><span class="sxs-lookup"><span data-stu-id="bad89-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="bad89-167">Media Services iki tür bulucuyu destekler:</span><span class="sxs-lookup"><span data-stu-id="bad89-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="bad89-168">Akış (OnDemandOrigin) bulucuları, (örneğin, toostream MPEG DASH, HLS veya kesintisiz akış) Uyarlamalı akış için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bad89-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="bad89-169">toocreate akış Bulucusu varlığınız bir .ism dosyası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="bad89-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="bad89-170">Aşamalı indirme aracılığıyla video teslimi için kullanılan aşamalı (SAS) bulucular.</span><span class="sxs-lookup"><span data-stu-id="bad89-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="bad89-171">Bir akış URL'si biçimi aşağıdaki hello sahiptir ve tooplay kesintisiz akış varlıklarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bad89-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="bad89-172">HLS akış URL'si, bir toobuild ekleme (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="bad89-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="bad89-173">bir akış URL'si, MPEG DASH toobuild ekleme (biçim mpd zaman csf =) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="bad89-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="bad89-174">Bir SAS URL'si biçimi aşağıdaki hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bad89-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="bad89-175">Mart 2015 öncesinde hello portal toocreate bulucular kullandıysanız, iki yıllık sona erme tarihi olan bulucular oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="bad89-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="bad89-176">Kullanım Bulucunun sona erme tarihi bir tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) veya [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API'leri.</span><span class="sxs-lookup"><span data-stu-id="bad89-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="bad89-177">Bir SAS Bulucu hello sona erme tarihini güncelleştirdiğinizde hello URL değiştirir.</span><span class="sxs-lookup"><span data-stu-id="bad89-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="bad89-178">toouse hello portal toopublish bir varlığı</span><span class="sxs-lookup"><span data-stu-id="bad89-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="bad89-179">toouse hello portal toopublish bir varlık hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="bad89-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="bad89-180">**Ayarlar** > **Varlıklar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bad89-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="bad89-181">Merhaba varlık toopublish istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="bad89-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="bad89-182">Merhaba tıklatın **Yayımla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bad89-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="bad89-183">Merhaba Bulucu türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="bad89-183">Select hello locator type.</span></span>
5. <span data-ttu-id="bad89-184">**Ekle**’ye basın.</span><span class="sxs-lookup"><span data-stu-id="bad89-184">Press **Add**.</span></span>
   
    ![Yayımlama](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="bad89-186">Merhaba URL toohello listesi eklenen **yayımlanan URL'ler**.</span><span class="sxs-lookup"><span data-stu-id="bad89-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="bad89-187">Merhaba portaldan içerik oynatma</span><span class="sxs-lookup"><span data-stu-id="bad89-187">Play content from hello portal</span></span>
<span data-ttu-id="bad89-188">Hello Azure portalı bir içerik oynatıcı sağlar videonuzu tootest kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bad89-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="bad89-189">İstenen hello videoya tıklayın ve hello ardından **Yürüt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bad89-189">Click hello desired video and then click hello **Play** button.</span></span>

![Yayımlama](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="bad89-191">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="bad89-191">Some considerations apply:</span></span>

* <span data-ttu-id="bad89-192">Akış, toobegin Başlat çalışan hello **varsayılan** akış uç noktası.</span><span class="sxs-lookup"><span data-stu-id="bad89-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="bad89-193">Merhaba video yayımlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="bad89-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="bad89-194">Bu **Media player** hello varsayılan akış uç noktasından oynatır.</span><span class="sxs-lookup"><span data-stu-id="bad89-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="bad89-195">Varsayılan olmayan tooplay istiyorsanız akış uç noktası, toocopy hello URL'yi tıklatın ve başka bir oynatıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bad89-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="bad89-196">Örneğin, [Azure Media Services Oynatıcı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="bad89-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bad89-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bad89-197">Next steps</span></span>
<span data-ttu-id="bad89-198">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="bad89-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bad89-199">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="bad89-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

