---
title: "Tek bit hızlı bir canlı akışı göndermek için FMLE Kodlayıcı yapılandırma | Microsoft Docs"
description: "Bu konuda, tek bit hızlı akış gerçek zamanlı kodlama için etkinleştirilmiş AMS kanallar göndermek için Flash medya Canlı Kodlayıcı (FMLE) Kodlayıcı yapılandırma gösterilmektedir."
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
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="d4b86-103">Tek bit hızlı bir canlı akışı göndermek için FMLE Kodlayıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="d4b86-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4b86-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="d4b86-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="d4b86-105">Elemental dinamik</span><span class="sxs-lookup"><span data-stu-id="d4b86-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="d4b86-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="d4b86-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="d4b86-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="d4b86-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="d4b86-108">Bu konuda nasıl yapılandırılacağını göstermektedir [Flash medya Canlı Kodlayıcı](http://www.adobe.com/products/flash-media-encoder.html) AMS bir tek bit hızlı akışın kanallar göndermek için (FMLE) Kodlayıcı, gerçek zamanlı kodlama için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d4b86-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="d4b86-109">Daha fazla bilgi için bkz. [Azure Media Services ile Gerçek Zamanlı Kodlama Gerçekleştirmek İçin Etkinleştirilmiş Kanallar ile Çalışma](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="d4b86-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="d4b86-110">Bu öğretici, Azure Media Services Gezgini (AMSE) aracı ile Azure Media Services (AMS) yönetmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d4b86-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="d4b86-111">Bu araç, yalnızca bir Windows Bilgisayarına çalışır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="d4b86-112">Mac veya Linux varsa, oluşturmak için Azure portalını kullanın [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="d4b86-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="d4b86-113">Bu öğretici AAC kullanmayı açıklar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="d4b86-114">Ancak, FMLE değil destekler AAC varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="d4b86-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="d4b86-115">AAC uğradıysa MainConcept böyle kodlama için bir eklenti satın almanız gerekir: [AAC eklentisi](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="d4b86-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4b86-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4b86-116">Prerequisites</span></span>
* [<span data-ttu-id="d4b86-117">Bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4b86-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="d4b86-118">Çalıştıran bir akış uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4b86-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="d4b86-119">Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="d4b86-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="d4b86-120">En son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="d4b86-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="d4b86-121">Aracı'nı başlatın ve AMS hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="d4b86-122">İpuçları</span><span class="sxs-lookup"><span data-stu-id="d4b86-122">Tips</span></span>
* <span data-ttu-id="d4b86-123">Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="d4b86-124">Bir iyi bant genişliği gereksinimlerini belirlerken için udur akış bit çift.</span><span class="sxs-lookup"><span data-stu-id="d4b86-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="d4b86-125">Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı etkisini azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d4b86-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="d4b86-126">Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="d4b86-127">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4b86-127">Create a channel</span></span>
1. <span data-ttu-id="d4b86-128">AMSE aracını gidin **canlı** sekmesinde ve içinde kanal alanı sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="d4b86-129">Seçin **kanal oluştur...**</span><span class="sxs-lookup"><span data-stu-id="d4b86-129">Select **Create channel…**</span></span> <span data-ttu-id="d4b86-130">menüden.</span><span class="sxs-lookup"><span data-stu-id="d4b86-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="d4b86-132">Bir kanal adı belirtin açıklama alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="d4b86-133">Kanal ayarları altında seçin **standart** gerçek zamanlı kodlama seçeneğini ayarlamak giriş protokolü için **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="d4b86-134">Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b86-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="d4b86-135">Emin olun **yeni kanal Şimdi Başlat** seçilir.</span><span class="sxs-lookup"><span data-stu-id="d4b86-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="d4b86-136">Tıklatın **kanal oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="d4b86-138">Kanal başlatmak için 20 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d4b86-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="d4b86-139">Kanal başlatılırken yapabilecekleriniz [Kodlayıcı yapılandırma](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="d4b86-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4b86-140">Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="d4b86-141">Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="d4b86-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="d4b86-142"><a id=configure_fmle_rtmp></a>FMLE Kodlayıcı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4b86-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="d4b86-143">Bu öğreticide aşağıdaki çıkış ayarları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="d4b86-144">Bu bölümün geri kalanında daha ayrıntılı yapılandırma adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="d4b86-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="d4b86-145">**Video**:</span><span class="sxs-lookup"><span data-stu-id="d4b86-145">**Video**:</span></span>

* <span data-ttu-id="d4b86-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="d4b86-146">Codec: H.264</span></span>
* <span data-ttu-id="d4b86-147">Profil: Yüksek (düzeyi 4.0)</span><span class="sxs-lookup"><span data-stu-id="d4b86-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="d4b86-148">Bit hızı: 5000 KB/sn</span><span class="sxs-lookup"><span data-stu-id="d4b86-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="d4b86-149">Anahtar kare: 2 saniye (60 saniye)</span><span class="sxs-lookup"><span data-stu-id="d4b86-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="d4b86-150">Çerçeve oranı: 30</span><span class="sxs-lookup"><span data-stu-id="d4b86-150">Frame Rate: 30</span></span>

<span data-ttu-id="d4b86-151">**Ses**:</span><span class="sxs-lookup"><span data-stu-id="d4b86-151">**Audio**:</span></span>

* <span data-ttu-id="d4b86-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="d4b86-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="d4b86-153">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="d4b86-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="d4b86-154">Örnek Hızı: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="d4b86-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="d4b86-155">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="d4b86-155">Configuration steps</span></span>
1. <span data-ttu-id="d4b86-156">Gidin kullanılan makinede Flash medya Canlı Kodlayıcı 's (FMLE) arabirim.</span><span class="sxs-lookup"><span data-stu-id="d4b86-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="d4b86-157">Bir ana sayfa ayarlarını arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="d4b86-157">The interface is one main page of settings.</span></span> <span data-ttu-id="d4b86-158">Lütfen aşağıdaki FMLE kullanarak akış ile kullanmaya başlamak için önerilen ayarları not edin.</span><span class="sxs-lookup"><span data-stu-id="d4b86-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="d4b86-159">Biçimi: H.264 kare hızı: 30,00</span><span class="sxs-lookup"><span data-stu-id="d4b86-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="d4b86-160">Giriş boyutu: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="d4b86-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="d4b86-161">Bit hızı: 5000 (ağ sınırlamalar göre ayarlanabilir) KB/sn</span><span class="sxs-lookup"><span data-stu-id="d4b86-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="d4b86-163">Onay işareti "Taramasız Hale Getir'i" seçeneğini kullanarak kaynakları aralıklı, lütfen</span><span class="sxs-lookup"><span data-stu-id="d4b86-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="d4b86-164">İngiliz anahtarı simgesi biçimi yanındaki seçin, bu ek ayarlar olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4b86-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="d4b86-165">Profil: ana</span><span class="sxs-lookup"><span data-stu-id="d4b86-165">Profile: Main</span></span>
   * <span data-ttu-id="d4b86-166">Düzeyi: 4.0</span><span class="sxs-lookup"><span data-stu-id="d4b86-166">Level: 4.0</span></span>
   * <span data-ttu-id="d4b86-167">Ana kare sıklığı: 2 saniye cinsinden</span><span class="sxs-lookup"><span data-stu-id="d4b86-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="d4b86-169">Aşağıdaki önemli ses ayarını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4b86-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="d4b86-170">Biçim: AAC</span><span class="sxs-lookup"><span data-stu-id="d4b86-170">Format: AAC</span></span>
   * <span data-ttu-id="d4b86-171">Örnek Hızı: 44100 Hz</span><span class="sxs-lookup"><span data-stu-id="d4b86-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="d4b86-172">Bit hızı: 192 Kb/sn</span><span class="sxs-lookup"><span data-stu-id="d4b86-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="d4b86-174">Get kanal girdisini URL FMLE için 's atamak için **RTMP Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="d4b86-175">AMSE aracına gidin ve kanal tamamlanma durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d4b86-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="d4b86-176">Durumu değiştiğinden sonra **başlangıç** için **çalıştıran**, giriş URL'yi elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4b86-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="d4b86-177">Kanal çalıştırırken, kanal adı sağ tıklayın ve ardından aşağıya doğru vurgulu üzerinden gidin **Panoya Kopyala giriş URL** ve ardından **birincil giriş URL**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="d4b86-179">Bu bilgileri **FMS URL** çıkış bölüm ve atama Akış adı alanı.</span><span class="sxs-lookup"><span data-stu-id="d4b86-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="d4b86-181">Ek artıklık için ikincil giriş URL ile bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d4b86-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="d4b86-182">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4b86-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4b86-183">Tıklamadan önce **Bağlan**, size **gerekir** kanal hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4b86-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="d4b86-184">Ayrıca, kanal hazır durumda > 15 dakikadan fazla akış bir giriş katkı olmadan bırakın değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4b86-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="d4b86-185">Testi kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="d4b86-185">Test playback</span></span>

<span data-ttu-id="d4b86-186">AMSE Aracı'na gidin ve sınanacak kanal sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="d4b86-187">Menüden, üzerine gelerek **kayıttan yürütme Önizleme** seçip **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="d4b86-188">Ardından akış player görünürse, kodlayıcı düzgün için AMS bağlanmak için yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="d4b86-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="d4b86-189">Bir hata alırsanız, kanal sıfırlanması gerekir ve Kodlayıcı ayarları ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="d4b86-190">Lütfen bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="d4b86-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="d4b86-191">Bir program oluşturun</span><span class="sxs-lookup"><span data-stu-id="d4b86-191">Create a program</span></span>
1. <span data-ttu-id="d4b86-192">Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4b86-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="d4b86-193">Altında **canlı** sekmesinde AMSE aracının içinde programı alanı sağ tıklatın ve seçin **Yeni Program Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="d4b86-195">Program adı ve gerekirse, ayarlamak **arşiv penceresi uzunluğu** (hangi varsayılan olarak 4 saat olarak).</span><span class="sxs-lookup"><span data-stu-id="d4b86-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="d4b86-196">Ayrıca, bir depolama konumu belirtin veya varsayılan olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="d4b86-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="d4b86-197">Denetleme **Program Şimdi Başlat** kutusu.</span><span class="sxs-lookup"><span data-stu-id="d4b86-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="d4b86-198">Tıklatın **Program oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="d4b86-199">Program oluşturma kanal oluşturma daha az zaman alır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="d4b86-200">Program çalışmaya başladıktan sonra program sağ tıklayarak ve giderek tarafından kayıttan yürütme onaylayın **kayıttan yürütme edinin** seçilerek **Azure Media Player ile**.</span><span class="sxs-lookup"><span data-stu-id="d4b86-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="d4b86-201">Onaylandıktan sonra sağ program yeniden tıklatın ve seçin **çıkış URL'yi Panoya Kopyala** (veya bu bilgileri almak **Program bilgilerine ve ayarlarına** seçeneği menüsünde).</span><span class="sxs-lookup"><span data-stu-id="d4b86-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="d4b86-202">Akış bir oynatıcı katıştırılmış veya dinamik görüntülemek için bir izleyici için Dağıtılmış artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="d4b86-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="d4b86-203">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d4b86-203">Troubleshooting</span></span>
<span data-ttu-id="d4b86-204">Lütfen bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.</span><span class="sxs-lookup"><span data-stu-id="d4b86-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d4b86-205">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="d4b86-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d4b86-206">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d4b86-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
