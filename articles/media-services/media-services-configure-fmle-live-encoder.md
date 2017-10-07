---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello FMLE Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Flash medya Canlı Kodlayıcı (FMLE) Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="2b088-103">Merhaba FMLE Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın</span><span class="sxs-lookup"><span data-stu-id="2b088-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b088-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="2b088-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="2b088-105">Elemental dinamik</span><span class="sxs-lookup"><span data-stu-id="2b088-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="2b088-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="2b088-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="2b088-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="2b088-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="2b088-108">Bu konuda gösterilmektedir nasıl tooconfigure hello [Flash medya Canlı Kodlayıcı](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) Kodlayıcı toosend tek bit hızlı akış gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar.</span><span class="sxs-lookup"><span data-stu-id="2b088-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="2b088-109">Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="2b088-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="2b088-110">Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile.</span><span class="sxs-lookup"><span data-stu-id="2b088-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="2b088-111">Bu araç, yalnızca bir Windows Bilgisayarına çalışır.</span><span class="sxs-lookup"><span data-stu-id="2b088-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="2b088-112">Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="2b088-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="2b088-113">Bu öğretici AAC kullanmayı açıklar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2b088-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="2b088-114">Ancak, FMLE değil destekler AAC varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="2b088-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="2b088-115">Toopurchase AAC kodlama için bir eklenti MainConcept uğradıysa gibi ihtiyacınız: [AAC eklentisi](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="2b088-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b088-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2b088-116">Prerequisites</span></span>
* [<span data-ttu-id="2b088-117">Bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b088-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="2b088-118">Çalıştıran bir akış uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b088-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="2b088-119">Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="2b088-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="2b088-120">Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="2b088-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="2b088-121">Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2b088-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="2b088-122">İpuçları</span><span class="sxs-lookup"><span data-stu-id="2b088-122">Tips</span></span>
* <span data-ttu-id="2b088-123">Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b088-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="2b088-124">Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur.</span><span class="sxs-lookup"><span data-stu-id="2b088-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="2b088-125">Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2b088-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="2b088-126">Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.</span><span class="sxs-lookup"><span data-stu-id="2b088-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="2b088-127">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b088-127">Create a channel</span></span>
1. <span data-ttu-id="2b088-128">Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2b088-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="2b088-129">Seçin **kanal oluştur...**</span><span class="sxs-lookup"><span data-stu-id="2b088-129">Select **Create channel…**</span></span> <span data-ttu-id="2b088-130">Başlangıç menüsünden.</span><span class="sxs-lookup"><span data-stu-id="2b088-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="2b088-132">Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2b088-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="2b088-133">Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="2b088-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="2b088-134">Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b088-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="2b088-135">Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.</span><span class="sxs-lookup"><span data-stu-id="2b088-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="2b088-136">Tıklatın **kanal oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="2b088-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="2b088-138">Merhaba kanal 20 dakika toostart olarak uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2b088-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="2b088-139">Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="2b088-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b088-140">Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2b088-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="2b088-141">Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="2b088-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="2b088-142"><a id=configure_fmle_rtmp></a>Merhaba FMLE Kodlayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2b088-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="2b088-143">Bu öğretici hello aşağıdaki çıkış ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2b088-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="2b088-144">Bu bölümde Hello kalanı daha ayrıntılı yapılandırma adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2b088-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="2b088-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="2b088-145">**Video**:</span></span>

* <span data-ttu-id="2b088-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="2b088-146">Codec: H.264</span></span>
* <span data-ttu-id="2b088-147">Profil: Yüksek (düzeyi 4.0)</span><span class="sxs-lookup"><span data-stu-id="2b088-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="2b088-148">Bit hızı: 5000 KB/sn</span><span class="sxs-lookup"><span data-stu-id="2b088-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="2b088-149">Anahtar kare: 2 saniye (60 saniye)</span><span class="sxs-lookup"><span data-stu-id="2b088-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="2b088-150">Çerçeve oranı: 30</span><span class="sxs-lookup"><span data-stu-id="2b088-150">Frame Rate: 30</span></span>

<span data-ttu-id="2b088-151">**Ses**:</span><span class="sxs-lookup"><span data-stu-id="2b088-151">**Audio**:</span></span>

* <span data-ttu-id="2b088-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="2b088-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="2b088-153">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="2b088-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="2b088-154">Örnek Hızı: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="2b088-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="2b088-155">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="2b088-155">Configuration steps</span></span>
1. <span data-ttu-id="2b088-156">Flash Media Canlı Kodlayıcısı 's (FMLE) kullanılan hello makinede arabirim toohello gidin.</span><span class="sxs-lookup"><span data-stu-id="2b088-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="2b088-157">Merhaba, bir ana sayfa ayarlarını arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="2b088-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="2b088-158">Lütfen hello aşağıda önerilen not edin ayarları tooget FMLE kullanarak akış ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="2b088-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="2b088-159">Biçimi: H.264 kare hızı: 30,00</span><span class="sxs-lookup"><span data-stu-id="2b088-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="2b088-160">Giriş boyutu: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="2b088-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="2b088-161">Bit hızı: 5000 (ağ sınırlamalar göre ayarlanabilir) KB/sn</span><span class="sxs-lookup"><span data-stu-id="2b088-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="2b088-163">Onay işareti hello "Taramasız Hale Getir'i" seçeneğini kullanarak kaynakları aralıklı, lütfen</span><span class="sxs-lookup"><span data-stu-id="2b088-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="2b088-164">Select hello İngiliz anahtarı simgesi sonraki tooFormat, bu ek ayarlar olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="2b088-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="2b088-165">Profil: ana</span><span class="sxs-lookup"><span data-stu-id="2b088-165">Profile: Main</span></span>
   * <span data-ttu-id="2b088-166">Düzeyi: 4.0</span><span class="sxs-lookup"><span data-stu-id="2b088-166">Level: 4.0</span></span>
   * <span data-ttu-id="2b088-167">Ana kare sıklığı: 2 saniye cinsinden</span><span class="sxs-lookup"><span data-stu-id="2b088-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="2b088-169">Önemli ses ayarını aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2b088-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="2b088-170">Biçim: AAC</span><span class="sxs-lookup"><span data-stu-id="2b088-170">Format: AAC</span></span>
   * <span data-ttu-id="2b088-171">Örnek Hızı: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="2b088-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="2b088-172">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="2b088-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="2b088-174">Merhaba kanalın giriş URL sırası tooassign almak, toohello FMLE's **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="2b088-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="2b088-175">Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2b088-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="2b088-176">Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b088-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="2b088-177">Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.</span><span class="sxs-lookup"><span data-stu-id="2b088-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="2b088-179">Bu bilgileri hello yapıştırmak **FMS URL** hello çıkış bölümü ve ata Akış adı alanı.</span><span class="sxs-lookup"><span data-stu-id="2b088-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="2b088-181">Ek artıklık için hello ikincil giriş URL ile bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="2b088-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="2b088-182">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b088-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b088-183">Tıklamadan önce **Bağlan**, size **gerekir** hello kanal hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b088-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="2b088-184">Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.</span><span class="sxs-lookup"><span data-stu-id="2b088-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="2b088-185">Testi kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="2b088-185">Test playback</span></span>

<span data-ttu-id="2b088-186">Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2b088-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="2b088-187">Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="2b088-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="2b088-188">Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.</span><span class="sxs-lookup"><span data-stu-id="2b088-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="2b088-189">Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b088-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="2b088-190">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="2b088-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="2b088-191">Bir program oluşturun</span><span class="sxs-lookup"><span data-stu-id="2b088-191">Create a program</span></span>
1. <span data-ttu-id="2b088-192">Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2b088-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="2b088-193">Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="2b088-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="2b088-195">Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat).</span><span class="sxs-lookup"><span data-stu-id="2b088-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="2b088-196">Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="2b088-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="2b088-197">Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b088-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="2b088-198">Tıklatın **Program oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2b088-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="2b088-199">Program oluşturma kanal oluşturma daha az zaman alır.</span><span class="sxs-lookup"><span data-stu-id="2b088-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="2b088-200">Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="2b088-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="2b088-201">Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).</span><span class="sxs-lookup"><span data-stu-id="2b088-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="2b088-202">Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="2b088-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="2b088-203">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2b088-203">Troubleshooting</span></span>
<span data-ttu-id="2b088-204">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="2b088-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2b088-205">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="2b088-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b088-206">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="2b088-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
