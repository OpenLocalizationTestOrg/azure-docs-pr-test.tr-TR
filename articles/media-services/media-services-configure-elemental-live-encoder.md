---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello Elemental Canlı Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Elemental Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="c41a1-103">Tek bit hızlı bir canlı akışı Hello Elemental Canlı Kodlayıcı toosend kullanın</span><span class="sxs-lookup"><span data-stu-id="c41a1-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c41a1-104">Elemental dinamik</span><span class="sxs-lookup"><span data-stu-id="c41a1-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="c41a1-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="c41a1-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="c41a1-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="c41a1-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="c41a1-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="c41a1-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="c41a1-108">Bu konuda gösterilmektedir nasıl tooconfigure hello [Elemental canlı](http://www.elementaltechnologies.com/products/elemental-live) Kodlayıcı toosend tek bit hızlı akış gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar.</span><span class="sxs-lookup"><span data-stu-id="c41a1-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="c41a1-109">Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="c41a1-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="c41a1-110">Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile.</span><span class="sxs-lookup"><span data-stu-id="c41a1-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="c41a1-111">Bu araç, yalnızca bir Windows Bilgisayarına çalışır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="c41a1-112">Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="c41a1-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c41a1-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c41a1-113">Prerequisites</span></span>
* <span data-ttu-id="c41a1-114">Web arabirimi toocreate Canlı olayları Elemental Canlı kullanma bilgisine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="c41a1-115">Bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c41a1-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="c41a1-116">Çalıştıran bir akış uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c41a1-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="c41a1-117">Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="c41a1-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="c41a1-118">Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="c41a1-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="c41a1-119">Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="c41a1-120">İpuçları</span><span class="sxs-lookup"><span data-stu-id="c41a1-120">Tips</span></span>
* <span data-ttu-id="c41a1-121">Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="c41a1-122">Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur.</span><span class="sxs-lookup"><span data-stu-id="c41a1-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="c41a1-123">Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c41a1-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="c41a1-124">Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="c41a1-125">RTP ile elemental Canlı alma</span><span class="sxs-lookup"><span data-stu-id="c41a1-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="c41a1-126">Bu bölümde, nasıl tek bit hızlı gönderdiği tooconfigure hello Elemental Canlı gerçek zamanlı kodlayıcıya akış RTP gösterir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="c41a1-127">Daha fazla bilgi için bkz: [RTP üzerinden MPEG-TS akış](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="c41a1-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="c41a1-128">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="c41a1-128">Create a channel</span></span>

1. <span data-ttu-id="c41a1-129">Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="c41a1-130">Seçin **kanal oluştur...**</span><span class="sxs-lookup"><span data-stu-id="c41a1-130">Select **Create channel…**</span></span> <span data-ttu-id="c41a1-131">Başlangıç menüsünden.</span><span class="sxs-lookup"><span data-stu-id="c41a1-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="c41a1-133">Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="c41a1-134">Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="c41a1-135">Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c41a1-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="c41a1-136">Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="c41a1-137">Tıklatın **kanal oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="c41a1-139">Merhaba kanal 20 dakika toostart olarak uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="c41a1-140">Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="c41a1-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c41a1-141">Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="c41a1-142">Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="c41a1-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="c41a1-143"><a id=configure_elemental_rtp></a>Merhaba Elemental Canlı Kodlayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c41a1-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="c41a1-144">Bu öğretici hello aşağıdaki çıkış ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="c41a1-145">Bu bölümde Hello kalanı daha ayrıntılı yapılandırma adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="c41a1-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="c41a1-146">**Video**:</span><span class="sxs-lookup"><span data-stu-id="c41a1-146">**Video**:</span></span>

* <span data-ttu-id="c41a1-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="c41a1-147">Codec: H.264</span></span>
* <span data-ttu-id="c41a1-148">Profil: Yüksek (düzeyi 4.0)</span><span class="sxs-lookup"><span data-stu-id="c41a1-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="c41a1-149">Bit hızı: 5000 KB/sn</span><span class="sxs-lookup"><span data-stu-id="c41a1-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="c41a1-150">Anahtar kare: 2 saniye (60 saniye)</span><span class="sxs-lookup"><span data-stu-id="c41a1-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="c41a1-151">Çerçeve oranı: 30</span><span class="sxs-lookup"><span data-stu-id="c41a1-151">Frame Rate: 30</span></span>

<span data-ttu-id="c41a1-152">**Ses**:</span><span class="sxs-lookup"><span data-stu-id="c41a1-152">**Audio**:</span></span>

* <span data-ttu-id="c41a1-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="c41a1-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="c41a1-154">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="c41a1-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="c41a1-155">Örnek Hızı: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="c41a1-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="c41a1-156">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="c41a1-156">Configuration steps</span></span>
1. <span data-ttu-id="c41a1-157">Toohello gidin **Elemental canlı** web arabirimi ve hello Kodlayıcı için ayarlama **UDP/TS** akış.</span><span class="sxs-lookup"><span data-stu-id="c41a1-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="c41a1-158">Yeni bir olay oluşturulduğunda toohello çıktı grupları kaydırın ve hello ekleyin **UDP/TS** çıktı grubu.</span><span class="sxs-lookup"><span data-stu-id="c41a1-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="c41a1-159">Seçerek yeni bir çıktı oluşturmak **yeni akış** ve ardından **Çıktı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="c41a1-161">Merhaba Elemental olay sahip çok ayarlamak hello zaman kodu önerilir "Sistem saati" toohelp hello Kodlayıcı yeniden akışı hatası hello durumda.</span><span class="sxs-lookup"><span data-stu-id="c41a1-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="c41a1-162">Merhaba çıkış oluşturuldu, tıklatın **akış eklemek**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="c41a1-163">Merhaba çıkış ayarları artık yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="c41a1-164">Kaydırma, yeni oluşturduğunuz toohello "Akış 1", hello tıklatın **Video** sekmesinde hello solda ve hello genişletin **Gelişmiş** Ayarlar bölümünde.</span><span class="sxs-lookup"><span data-stu-id="c41a1-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="c41a1-166">Elemental Canlı kullanılabilir özelleştirme çeşitli sahipken hello aşağıdaki ayarlar tooAMS akış ile çalışmaya başlama için önerilir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="c41a1-167">Çözünürlük: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="c41a1-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="c41a1-168">Kare hızı: 30</span><span class="sxs-lookup"><span data-stu-id="c41a1-168">Framerate: 30</span></span>
   * <span data-ttu-id="c41a1-169">GOP boyutu: 60 çerçeveler</span><span class="sxs-lookup"><span data-stu-id="c41a1-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="c41a1-170">Mod Taramasız hale getirme: aşamalı</span><span class="sxs-lookup"><span data-stu-id="c41a1-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="c41a1-171">Bit hızı: 5000000 bit/sn (Bu ağ sınırlamaları göre ayarlanabilir)</span><span class="sxs-lookup"><span data-stu-id="c41a1-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="c41a1-173">Merhaba kanalın giriş URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="c41a1-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="c41a1-174">Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c41a1-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="c41a1-175">Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c41a1-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="c41a1-176">Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="c41a1-178">Bu bilgileri hello yapıştırmak **birincil hedef** hello Elemental alanı.</span><span class="sxs-lookup"><span data-stu-id="c41a1-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="c41a1-179">Tüm diğer ayarlar hello varsayılan kalabilir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="c41a1-181">Ek artıklık için UDP/TS akış için ayrı bir "Çıktı" sekmesinde oluşturarak hello ikincil giriş URL ile bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="c41a1-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="c41a1-182">Tıklatın **oluşturma** (yeni bir olay oluşturduysanız) veya **güncelleştirme** (önceden var olan bir olay düzenleme varsa) ve toostart hello Kodlayıcı devam edin.</span><span class="sxs-lookup"><span data-stu-id="c41a1-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c41a1-183">Tıklamadan önce **Başlat** hello Elemental canlı web arabiriminde, **gerekir** hello kanal hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c41a1-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="c41a1-184">Ayrıca, emin olun tooleave hello kanal > 15 dakikadan daha uzun bir olay olmadan hazır durumda değil.</span><span class="sxs-lookup"><span data-stu-id="c41a1-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="c41a1-185">Merhaba akış 30 saniye yürütüldükten sonra geri toohello AMSE aracını ve test kayıttan yürütme gidin.</span><span class="sxs-lookup"><span data-stu-id="c41a1-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="c41a1-186">Testi kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="c41a1-186">Test playback</span></span>

<span data-ttu-id="c41a1-187">Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="c41a1-188">Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="c41a1-189">Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.</span><span class="sxs-lookup"><span data-stu-id="c41a1-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="c41a1-190">Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="c41a1-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="c41a1-191">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="c41a1-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="c41a1-192">Bir program oluşturun</span><span class="sxs-lookup"><span data-stu-id="c41a1-192">Create a program</span></span>
1. <span data-ttu-id="c41a1-193">Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c41a1-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="c41a1-194">Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="c41a1-196">Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat).</span><span class="sxs-lookup"><span data-stu-id="c41a1-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="c41a1-197">Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="c41a1-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="c41a1-198">Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c41a1-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="c41a1-199">Tıklatın **Program oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="c41a1-200">Program oluşturma kanal oluşturma daha az zaman alır.</span><span class="sxs-lookup"><span data-stu-id="c41a1-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="c41a1-201">Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="c41a1-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="c41a1-202">Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).</span><span class="sxs-lookup"><span data-stu-id="c41a1-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="c41a1-203">Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="c41a1-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="c41a1-204">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c41a1-204">Troubleshooting</span></span>
<span data-ttu-id="c41a1-205">Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="c41a1-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c41a1-206">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="c41a1-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c41a1-207">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="c41a1-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
