---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello Telestream Wirecast Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Wirecast Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="4830a-103">Merhaba Wirecast Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın</span><span class="sxs-lookup"><span data-stu-id="4830a-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4830a-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="4830a-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="4830a-105">Elemental dinamik</span><span class="sxs-lookup"><span data-stu-id="4830a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="4830a-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="4830a-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="4830a-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="4830a-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="4830a-108">Bu konuda gösterilmektedir nasıl tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar Kodlayıcı toosend Canlı.</span><span class="sxs-lookup"><span data-stu-id="4830a-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="4830a-109">Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="4830a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="4830a-110">Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile.</span><span class="sxs-lookup"><span data-stu-id="4830a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="4830a-111">Bu araç, yalnızca bir Windows Bilgisayarına çalışır.</span><span class="sxs-lookup"><span data-stu-id="4830a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="4830a-112">Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="4830a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4830a-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4830a-113">Prerequisites</span></span>
* [<span data-ttu-id="4830a-114">Bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4830a-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="4830a-115">Çalıştıran bir akış uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4830a-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="4830a-116">Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="4830a-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="4830a-117">Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="4830a-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="4830a-118">Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.</span><span class="sxs-lookup"><span data-stu-id="4830a-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="4830a-119">İpuçları</span><span class="sxs-lookup"><span data-stu-id="4830a-119">Tips</span></span>
* <span data-ttu-id="4830a-120">Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="4830a-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="4830a-121">Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur.</span><span class="sxs-lookup"><span data-stu-id="4830a-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="4830a-122">Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4830a-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="4830a-123">Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.</span><span class="sxs-lookup"><span data-stu-id="4830a-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="4830a-124">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="4830a-124">Create a channel</span></span>
1. <span data-ttu-id="4830a-125">Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4830a-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="4830a-126">Seçin **kanal oluştur...**</span><span class="sxs-lookup"><span data-stu-id="4830a-126">Select **Create channel…**</span></span> <span data-ttu-id="4830a-127">Başlangıç menüsünden.</span><span class="sxs-lookup"><span data-stu-id="4830a-127">from hello menu.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="4830a-129">Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4830a-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="4830a-130">Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="4830a-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="4830a-131">Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4830a-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="4830a-132">Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.</span><span class="sxs-lookup"><span data-stu-id="4830a-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="4830a-133">Tıklatın **kanal oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="4830a-133">Click **Create Channel**.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="4830a-135">Merhaba kanal 20 dakika toostart olarak uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4830a-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="4830a-136">Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="4830a-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4830a-137">Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4830a-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="4830a-138">Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="4830a-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="4830a-139"><a id=configure_wirecast_rtmp></a>Merhaba Telestream Wirecast Kodlayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4830a-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="4830a-140">Bu öğretici hello aşağıdaki çıkış ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4830a-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="4830a-141">Bu bölümde Hello kalanı daha ayrıntılı yapılandırma adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="4830a-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="4830a-142">**Video**:</span><span class="sxs-lookup"><span data-stu-id="4830a-142">**Video**:</span></span>

* <span data-ttu-id="4830a-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="4830a-143">Codec: H.264</span></span>
* <span data-ttu-id="4830a-144">Profil: Yüksek (düzeyi 4.0)</span><span class="sxs-lookup"><span data-stu-id="4830a-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="4830a-145">Bit hızı: 5000 KB/sn</span><span class="sxs-lookup"><span data-stu-id="4830a-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="4830a-146">Anahtar kare: 2 saniye (60 saniye)</span><span class="sxs-lookup"><span data-stu-id="4830a-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="4830a-147">Çerçeve oranı: 30</span><span class="sxs-lookup"><span data-stu-id="4830a-147">Frame Rate: 30</span></span>

<span data-ttu-id="4830a-148">**Ses**:</span><span class="sxs-lookup"><span data-stu-id="4830a-148">**Audio**:</span></span>

* <span data-ttu-id="4830a-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="4830a-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="4830a-150">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="4830a-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="4830a-151">Örnek Hızı: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="4830a-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="4830a-152">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="4830a-152">Configuration steps</span></span>
1. <span data-ttu-id="4830a-153">Merhaba Telestream Wirecast uygulaması makine hello olan üzerinde kullanılan ve RTMP akış için ayarlanan açın.</span><span class="sxs-lookup"><span data-stu-id="4830a-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="4830a-154">Hello çıktı toohello giderek yapılandırma **çıkış** sekmesi ve seçerek **çıktı ayarları...** .</span><span class="sxs-lookup"><span data-stu-id="4830a-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="4830a-155">Merhaba emin olun **Çıkış hedefini** çok ayarlanır**RTMP sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="4830a-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="4830a-156">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4830a-156">Click **OK**.</span></span>
4. <span data-ttu-id="4830a-157">Merhaba Hello Ayarları sayfasında ayarlamak **hedef** alan toobe **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="4830a-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="4830a-158">Merhaba kodlama profili önceden seçili çok**Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="4830a-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="4830a-159">toocustomize bu ayarlar, select hello dişli simgesi toohello hello sağındaki açılan ve ardından **yeni önceden**.</span><span class="sxs-lookup"><span data-stu-id="4830a-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="4830a-161">Encoder hazır ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4830a-161">Configure encoder presets.</span></span>

    <span data-ttu-id="4830a-162">Ad hello önceden ve için önerilen ayarları hello aşağıdakileri denetleyin:</span><span class="sxs-lookup"><span data-stu-id="4830a-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="4830a-163">**Video**</span><span class="sxs-lookup"><span data-stu-id="4830a-163">**Video**</span></span>

   * <span data-ttu-id="4830a-164">Kodlayıcı: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="4830a-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="4830a-165">Saniyedeki çerçeve sayısı: 30</span><span class="sxs-lookup"><span data-stu-id="4830a-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="4830a-166">Ortalama bit hızı: 5000 kbit/sn (ayarlanabilir ağ sınırlamalar tabanlı)</span><span class="sxs-lookup"><span data-stu-id="4830a-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="4830a-167">Profil: ana</span><span class="sxs-lookup"><span data-stu-id="4830a-167">Profile: Main</span></span>
   * <span data-ttu-id="4830a-168">Anahtar çerçevesi her: 60 çerçeveler</span><span class="sxs-lookup"><span data-stu-id="4830a-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="4830a-169">**Ses**</span><span class="sxs-lookup"><span data-stu-id="4830a-169">**Audio**</span></span>

   * <span data-ttu-id="4830a-170">Hedef bit hızı: 192 kbit/sn</span><span class="sxs-lookup"><span data-stu-id="4830a-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="4830a-171">Örnek Hızı: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="4830a-171">Sample Rate: 44.100 kHz</span></span>

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="4830a-173">Tuşuna **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="4830a-173">Press **Save**.</span></span>

    <span data-ttu-id="4830a-174">Merhaba Encoding alanı artık yeni oluşturulan hello profili seçilebilir sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4830a-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="4830a-175">Merhaba yeni bir profil seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4830a-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="4830a-176">Merhaba kanalın giriş URL sırası tooassign almak, toohello Wirecast **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="4830a-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="4830a-177">Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4830a-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="4830a-178">Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4830a-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="4830a-179">Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.</span><span class="sxs-lookup"><span data-stu-id="4830a-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="4830a-181">Merhaba Wirecast içinde **çıkış ayarları** penceresinde hello bu bilgileri yapıştırmak **adresi** hello çıkış bölümü ve ata Akış adı alanı.</span><span class="sxs-lookup"><span data-stu-id="4830a-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="4830a-183">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4830a-183">Select **OK**.</span></span>
2. <span data-ttu-id="4830a-184">Merhaba ana üzerinde **Wirecast** hazır olduğunuzda, video ve ses giriş kaynağı onaylayın ve ardından isabet **akış** hello üst sol alt köşesindeki.</span><span class="sxs-lookup"><span data-stu-id="4830a-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="4830a-186">Tıklamadan önce **akış**, size **gerekir** hello kanal hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4830a-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="4830a-187">Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.</span><span class="sxs-lookup"><span data-stu-id="4830a-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="4830a-188">Testi kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="4830a-188">Test playback</span></span>

<span data-ttu-id="4830a-189">Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4830a-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="4830a-190">Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="4830a-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="4830a-191">Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.</span><span class="sxs-lookup"><span data-stu-id="4830a-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="4830a-192">Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4830a-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="4830a-193">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="4830a-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="4830a-194">Bir program oluşturun</span><span class="sxs-lookup"><span data-stu-id="4830a-194">Create a program</span></span>
1. <span data-ttu-id="4830a-195">Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4830a-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="4830a-196">Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="4830a-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="4830a-198">Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat).</span><span class="sxs-lookup"><span data-stu-id="4830a-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="4830a-199">Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="4830a-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="4830a-200">Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.</span><span class="sxs-lookup"><span data-stu-id="4830a-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="4830a-201">Tıklatın **Program oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4830a-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="4830a-202">Program oluşturma kanal oluşturma daha az zaman alır.</span><span class="sxs-lookup"><span data-stu-id="4830a-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="4830a-203">Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="4830a-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="4830a-204">Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).</span><span class="sxs-lookup"><span data-stu-id="4830a-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="4830a-205">Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="4830a-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="4830a-206">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4830a-206">Troubleshooting</span></span>
<span data-ttu-id="4830a-207">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="4830a-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4830a-208">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="4830a-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4830a-209">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="4830a-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
