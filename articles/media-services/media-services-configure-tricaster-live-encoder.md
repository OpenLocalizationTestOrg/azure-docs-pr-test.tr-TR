---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello NewTek TriCaster Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Tricaster Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="a2597-103">Merhaba NewTek TriCaster Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın</span><span class="sxs-lookup"><span data-stu-id="a2597-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2597-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="a2597-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="a2597-105">Elemental dinamik</span><span class="sxs-lookup"><span data-stu-id="a2597-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="a2597-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="a2597-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="a2597-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="a2597-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="a2597-108">Bu konuda gösterilmektedir nasıl tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar Kodlayıcı toosend Canlı.</span><span class="sxs-lookup"><span data-stu-id="a2597-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="a2597-109">Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="a2597-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="a2597-110">Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile.</span><span class="sxs-lookup"><span data-stu-id="a2597-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="a2597-111">Bu araç, yalnızca bir Windows Bilgisayarına çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2597-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="a2597-112">Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="a2597-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a2597-113">Bir katkı göndermek için Tricaster kullanarak gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar akış zaman olabilir video/ses hatalardan Canlı olayınızın hızlı akışları arasında kesme veya grafikten maskeleme görüntülerini değiştirme gibi Tricaster belirli özelliklerini kullanıyorsanız .</span><span class="sxs-lookup"><span data-stu-id="a2597-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="a2597-114">Merhaba AMS takım çalıştığını o zamana kadar bu sorunları düzeltmeye, onu toouse bu özellikleri değil önerilir.</span><span class="sxs-lookup"><span data-stu-id="a2597-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a2597-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2597-115">Prerequisites</span></span>
* [<span data-ttu-id="a2597-116">Bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2597-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="a2597-117">Çalıştıran bir akış uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2597-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="a2597-118">Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="a2597-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="a2597-119">Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="a2597-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="a2597-120">Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2597-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="a2597-121">İpuçları</span><span class="sxs-lookup"><span data-stu-id="a2597-121">Tips</span></span>
* <span data-ttu-id="a2597-122">Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2597-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="a2597-123">Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur.</span><span class="sxs-lookup"><span data-stu-id="a2597-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="a2597-124">Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a2597-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="a2597-125">Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.</span><span class="sxs-lookup"><span data-stu-id="a2597-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="a2597-126">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2597-126">Create a channel</span></span>
1. <span data-ttu-id="a2597-127">Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2597-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="a2597-128">Seçin **kanal oluştur...**</span><span class="sxs-lookup"><span data-stu-id="a2597-128">Select **Create channel…**</span></span> <span data-ttu-id="a2597-129">Başlangıç menüsünden.</span><span class="sxs-lookup"><span data-stu-id="a2597-129">from hello menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="a2597-131">Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a2597-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="a2597-132">Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="a2597-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="a2597-133">Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2597-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="a2597-134">Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.</span><span class="sxs-lookup"><span data-stu-id="a2597-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="a2597-135">Tıklatın **kanal oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="a2597-135">Click **Create Channel**.</span></span>

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="a2597-137">Merhaba kanal 20 dakika toostart olarak uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a2597-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="a2597-138">Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="a2597-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2597-139">Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a2597-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="a2597-140">Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="a2597-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="a2597-141"><a id=configure_tricaster_rtmp></a>Merhaba NewTek TriCaster Kodlayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a2597-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="a2597-142">Bu öğretici hello aşağıdaki çıkış ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a2597-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="a2597-143">Bu bölümde Hello kalanı daha ayrıntılı yapılandırma adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a2597-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="a2597-144">**Video**:</span><span class="sxs-lookup"><span data-stu-id="a2597-144">**Video**:</span></span>

* <span data-ttu-id="a2597-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="a2597-145">Codec: H.264</span></span>
* <span data-ttu-id="a2597-146">Profil: Yüksek (düzeyi 4.0)</span><span class="sxs-lookup"><span data-stu-id="a2597-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="a2597-147">Bit hızı: 5000 KB/sn</span><span class="sxs-lookup"><span data-stu-id="a2597-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="a2597-148">Anahtar kare: 2 saniye (60 saniye)</span><span class="sxs-lookup"><span data-stu-id="a2597-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="a2597-149">Çerçeve oranı: 30</span><span class="sxs-lookup"><span data-stu-id="a2597-149">Frame Rate: 30</span></span>

<span data-ttu-id="a2597-150">**Ses**:</span><span class="sxs-lookup"><span data-stu-id="a2597-150">**Audio**:</span></span>

* <span data-ttu-id="a2597-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="a2597-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="a2597-152">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="a2597-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="a2597-153">Örnek Hızı: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="a2597-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="a2597-154">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="a2597-154">Configuration steps</span></span>
1. <span data-ttu-id="a2597-155">Yeni bir **NewTek TriCaster** hangi video giriş kaynağı kullanılan bağlı olarak proje.</span><span class="sxs-lookup"><span data-stu-id="a2597-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="a2597-156">Bu projede hello kez bulma **akış** düğmesine tıklayın ve hello dişli simgesi sonraki tooit tooaccess hello akışı yapılandırma menüsünü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2597-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="a2597-158">Merhaba menü açtıktan sonra tıklatın **yeni** hello bağlantı başlığı altında.</span><span class="sxs-lookup"><span data-stu-id="a2597-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="a2597-159">Merhaba bağlantı türü için istendiğinde seçin **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="a2597-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="a2597-161">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2597-161">Click **OK**.</span></span>
5. <span data-ttu-id="a2597-162">Bir FMLE profili şimdi hello açılan ok altında tıklayarak içeri aktarılabilir **akış profili** ve çok gezinme**Gözat**.</span><span class="sxs-lookup"><span data-stu-id="a2597-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="a2597-164">Toowhere gidin yapılandırılmış hello FMLE profili kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="a2597-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="a2597-165">Seçin ve basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2597-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="a2597-166">Hello profili yüklendikten sonra toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="a2597-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="a2597-167">Merhaba kanalın giriş URL sırası tooassign almak, toohello Tricaster **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a2597-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="a2597-168">Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a2597-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="a2597-169">Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2597-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="a2597-170">Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.</span><span class="sxs-lookup"><span data-stu-id="a2597-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="a2597-172">Bu bilgileri hello yapıştırmak **konumu** altında **Flash Server** hello Tricaster projede.</span><span class="sxs-lookup"><span data-stu-id="a2597-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="a2597-173">Ayrıca hello bir Akış adı atamak **akış kimliği** alan.</span><span class="sxs-lookup"><span data-stu-id="a2597-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="a2597-174">Akış bilgi toohello FMLE profili eklediyseniz, ayrıca alınabilir toothis bölümünde tıklayarak **ayarları içeri**, kaydedilen toohello FMLE profil gezinme ve tıklatarak **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2597-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="a2597-175">Merhaba ilgili Flash Server alanları FMLE hello bilgileriyle doldurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2597-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="a2597-177">Tamamlandığında tıklatarak **Tamam** Merhaba ekranında hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="a2597-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="a2597-178">Video ve ses girişleri hello Tricaster içine hazır olduğunuzda hello tıklayarak tooAMS akış başlamadan **akış** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a2597-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="a2597-180">Tıklamadan önce **akış**, size **gerekir** hello kanal hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2597-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="a2597-181">Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.</span><span class="sxs-lookup"><span data-stu-id="a2597-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="a2597-182">Testi kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="a2597-182">Test playback</span></span>
<span data-ttu-id="a2597-183">Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2597-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="a2597-184">Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="a2597-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="a2597-185">Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.</span><span class="sxs-lookup"><span data-stu-id="a2597-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="a2597-186">Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2597-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="a2597-187">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="a2597-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="a2597-188">Bir program oluşturun</span><span class="sxs-lookup"><span data-stu-id="a2597-188">Create a program</span></span>
1. <span data-ttu-id="a2597-189">Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2597-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="a2597-190">Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="a2597-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="a2597-192">Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat).</span><span class="sxs-lookup"><span data-stu-id="a2597-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="a2597-193">Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="a2597-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="a2597-194">Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.</span><span class="sxs-lookup"><span data-stu-id="a2597-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="a2597-195">Tıklatın **Program oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a2597-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="a2597-196">Program oluşturma kanal oluşturma daha az zaman alır.</span><span class="sxs-lookup"><span data-stu-id="a2597-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="a2597-197">Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="a2597-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="a2597-198">Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).</span><span class="sxs-lookup"><span data-stu-id="a2597-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="a2597-199">Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="a2597-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="a2597-200">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a2597-200">Troubleshooting</span></span>
<span data-ttu-id="a2597-201">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="a2597-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="a2597-202">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a2597-202">Next step</span></span>
<span data-ttu-id="a2597-203">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a2597-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2597-204">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a2597-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
