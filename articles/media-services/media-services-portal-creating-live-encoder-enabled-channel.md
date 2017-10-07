---
title: "aaaHow tooperform Azure Media Services toocreate Çoklu bit hızı akışları hello Azure portal ile kullanarak canlı akış gerçekleştirme | Microsoft Docs"
description: "Bir kanal oluşturulması hello adımlarında, tek bit hızında bir canlı akışı alır ve hello Azure portal kullanarak toomulti bit hızında akışa kodlayan Bu öğretici yetenekte."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a><span data-ttu-id="5c03f-103">Azure Media Services toocreate Çoklu bit hızlı kullanarak tooperform canlı akış hello Azure portal ile nasıl akışları</span><span class="sxs-lookup"><span data-stu-id="5c03f-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c03f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5c03f-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="5c03f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5c03f-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="5c03f-106">REST API</span><span class="sxs-lookup"><span data-stu-id="5c03f-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="5c03f-107">Bu öğretici, oluşturma hello adımlarda size bir **kanal** , tek bit hızında bir canlı akışı alıp toomulti bit hızında akışa kodlayan.</span><span class="sxs-lookup"><span data-stu-id="5c03f-107">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

> [!NOTE]
> <span data-ttu-id="5c03f-108">Daha fazla kavramsal bilgi için bkz: Gerçek zamanlı kodlama için etkinleştirilmiş ilgili tooChannels [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5c03f-108">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
> 
> 

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="5c03f-109">Ortak Canlı Akış Senaryosu</span><span class="sxs-lookup"><span data-stu-id="5c03f-109">Common Live Streaming Scenario</span></span>
<span data-ttu-id="5c03f-110">Merhaba, ortak canlı akış uygulamaları oluşturmaya dahil genel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-110">hello following are general steps involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="5c03f-111">Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-111">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="5c03f-112">Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-112">Please contact  amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="5c03f-113">Bir video kamera tooa bilgisayara bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-113">Connect a video camera tooa computer.</span></span> <span data-ttu-id="5c03f-114">Başlatma ve protokolleri aşağıdaki hello birinde tek bit hızlı akış çıkışı sağlayabilecek bir şirket içi gerçek zamanlı Kodlayıcı yapılandırın: RTMP, kesintisiz akış veya RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="5c03f-114">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="5c03f-115">Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="5c03f-115">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="5c03f-116">Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-116">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="5c03f-117">Bir Kanal oluşturup başlatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-117">Create and start a Channel.</span></span> 
3. <span data-ttu-id="5c03f-118">Alma hello kanal URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="5c03f-118">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="5c03f-119">Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-119">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="5c03f-120">Merhaba kanal Önizleme URL'sini alın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-120">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="5c03f-121">Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-121">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="5c03f-122">Bir olay/program oluşturun (ayrıca bir varlık oluşturur).</span><span class="sxs-lookup"><span data-stu-id="5c03f-122">Create an event/program (that will also create an asset).</span></span> 
6. <span data-ttu-id="5c03f-123">(Merhaba ilişkili varlığa yönelik bir OnDemand Bulucu oluşturulur) hello olayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-123">Publish hello event (that will create an  OnDemand locator for hello associated asset).</span></span>    
7. <span data-ttu-id="5c03f-124">Akışı ve arşivlemeyi hazır toostart olduğunda hello olayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-124">Start hello event when you are ready toostart streaming and archiving.</span></span>
8. <span data-ttu-id="5c03f-125">İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-125">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="5c03f-126">Merhaba tanıtım hello çıktı akışına eklenir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-126">hello advertisement is inserted in hello output stream.</span></span>
9. <span data-ttu-id="5c03f-127">Toostop akış ve arşivleme hello olayı istediğinizde hello olayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-127">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span>
10. <span data-ttu-id="5c03f-128">Merhaba olay silin (ve isteğe bağlı olarak hello varlığını silme).</span><span class="sxs-lookup"><span data-stu-id="5c03f-128">Delete hello event (and optionally delete hello asset).</span></span>   

## <a name="in-this-tutorial"></a><span data-ttu-id="5c03f-129">Bu öğreticide</span><span class="sxs-lookup"><span data-stu-id="5c03f-129">In this tutorial</span></span>
<span data-ttu-id="5c03f-130">Bu öğreticide, hello Azure portal kullanılan tooaccomplish hello görevleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5c03f-130">In this tutorial, hello Azure portal is used tooaccomplish hello following tasks:</span></span> 

1. <span data-ttu-id="5c03f-131">Bir kanal oluşturmak diğer bir deyişle etkin tooperform gerçek zamanlı kodlama.</span><span class="sxs-lookup"><span data-stu-id="5c03f-131">Create a channel that is enabled tooperform live encoding.</span></span>
2. <span data-ttu-id="5c03f-132">Get hello alım URL'sini sipariş toosupply onu toolive Kodlayıcı.</span><span class="sxs-lookup"><span data-stu-id="5c03f-132">Get hello Ingest URL in order toosupply it toolive encoder.</span></span> <span data-ttu-id="5c03f-133">Merhaba gerçek zamanlı Kodlayıcı bu URL tooingest hello akış kanal hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-133">hello live encoder will use this URL tooingest hello stream into hello Channel.</span></span>
3. <span data-ttu-id="5c03f-134">Bir olay/program (ve bir varlık) oluşturma.</span><span class="sxs-lookup"><span data-stu-id="5c03f-134">Create an event/program (and an asset).</span></span>
4. <span data-ttu-id="5c03f-135">Merhaba varlık yayımlama ve akış URL'lerini alma.</span><span class="sxs-lookup"><span data-stu-id="5c03f-135">Publish hello asset and get streaming URLs.</span></span>  
5. <span data-ttu-id="5c03f-136">İçeriğinizi oynatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-136">Play your content.</span></span>
6. <span data-ttu-id="5c03f-137">Temizleme.</span><span class="sxs-lookup"><span data-stu-id="5c03f-137">Cleaning up.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c03f-138">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5c03f-138">Prerequisites</span></span>
<span data-ttu-id="5c03f-139">Merhaba, gerekli toocomplete hello öğretici verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-139">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="5c03f-140">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-140">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5c03f-141">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-141">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> 
  <span data-ttu-id="5c03f-142">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c03f-142">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5c03f-143">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="5c03f-143">A Media Services account.</span></span> <span data-ttu-id="5c03f-144">bir Media Services hesabı toocreate bkz [hesap oluştur](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5c03f-144">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="5c03f-145">Bir web kamerası ve tek bit hızlı bir canlı akış gönderebilen bir kodlayıcı.</span><span class="sxs-lookup"><span data-stu-id="5c03f-145">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="5c03f-146">Kanal oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c03f-146">Create a channel</span></span>
1. <span data-ttu-id="5c03f-147">Merhaba, [Azure portal](https://portal.azure.com/), Media Services seçin ve ardından, Media Services hesap adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-147">In hello [Azure portal](https://portal.azure.com/), select Media Services and then click on your Media Services account name.</span></span>
2. <span data-ttu-id="5c03f-148">**Canlı Akış**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-148">Select **Live Streaming**.</span></span>
3. <span data-ttu-id="5c03f-149">**Özel oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-149">Select **Custom create**.</span></span> <span data-ttu-id="5c03f-150">Bu seçenek canlı kodlama için etkinleştirilmiş bir kanal oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c03f-150">This option will let you create a channel that is enabled for live encoding.</span></span>
   
    ![Kanal oluşturma](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. <span data-ttu-id="5c03f-152">**Ayarlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-152">Click on **Settings**.</span></span>
   
   1. <span data-ttu-id="5c03f-153">Merhaba seçin **gerçek zamanlı kodlama** kanal türü.</span><span class="sxs-lookup"><span data-stu-id="5c03f-153">Choose hello **Live Encoding** channel type.</span></span> <span data-ttu-id="5c03f-154">Bu tür, gerçek zamanlı kodlama için etkinleştirilmiş bir kanal toocreate istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-154">This type specifies that you want toocreate a Channel that is enabled for live encoding.</span></span> <span data-ttu-id="5c03f-155">Anlamına gelen tek bit hızlı hello akış toohello kanal gönderilir ve belirlenmiş gerçek zamanlı Kodlayıcı ayarları kullanılarak Çoklu bit hızında akışa kodlanır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-155">That means hello incoming single bitrate stream is sent toohello Channel and encoded into a multi-bitrate stream using specified live encoder settings.</span></span> <span data-ttu-id="5c03f-156">Daha fazla bilgi için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5c03f-156">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span> <span data-ttu-id="5c03f-157">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-157">Click OK.</span></span>
   2. <span data-ttu-id="5c03f-158">Bir kanalın adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-158">Specify a channel's name.</span></span>
   3. <span data-ttu-id="5c03f-159">Merhaba ekranın hello Tamam düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-159">Click OK at hello bottom of hello screen.</span></span>
5. <span data-ttu-id="5c03f-160">Select hello **alma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5c03f-160">Select hello **Ingest** tab.</span></span>
   
   1. <span data-ttu-id="5c03f-161">Bu sayfada bir akış protokolü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-161">On this page, you can select a streaming protocol.</span></span> <span data-ttu-id="5c03f-162">Hello için **gerçek zamanlı kodlama** kanal türü, geçerli protokol Seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5c03f-162">For hello **Live Encoding** channel type, valid protocol options are:</span></span>
      
      * <span data-ttu-id="5c03f-163">Tek bit hızlı Parçalanmış MP4 (Kesintisiz Akış)</span><span class="sxs-lookup"><span data-stu-id="5c03f-163">Single bitrate Fragmented MP4 (Smooth Streaming)</span></span>
      * <span data-ttu-id="5c03f-164">Tek bit hızlı RTMP</span><span class="sxs-lookup"><span data-stu-id="5c03f-164">Single bitrate RTMP</span></span>
      * <span data-ttu-id="5c03f-165">RTP (MPEG-TS): RTP üzerinden MPEG-2 Aktarım Akışı.</span><span class="sxs-lookup"><span data-stu-id="5c03f-165">RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.</span></span>
        
        <span data-ttu-id="5c03f-166">Her protokolü hakkında ayrıntılı açıklamalar için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5c03f-166">For detailed explanation about each protocol, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
        
        <span data-ttu-id="5c03f-167">Merhaba kanal hatayla hello protokol seçeneği değiştirilemiyor veya ilişkili olaylar/programları çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="5c03f-167">You cannot change hello protocol option while hello Channel or its associated events/programs are running.</span></span> <span data-ttu-id="5c03f-168">Farklı protokollere ihtiyacınız varsa her bir akış protokolü için farklı bir kanal oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="5c03f-168">If you require different protocols, you should create separate channels for each streaming protocol.</span></span>  
   2. <span data-ttu-id="5c03f-169">IP kısıtlama üzerinde hello geçerli alma.</span><span class="sxs-lookup"><span data-stu-id="5c03f-169">You can apply IP restriction on hello ingest.</span></span> 
      
       <span data-ttu-id="5c03f-170">Merhaba IP tanımlayabilirsiniz adreslerinin bir video toothis kanal tooingest izin verilir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-170">You can define hello IP addresses that are allowed tooingest a video toothis channel.</span></span> <span data-ttu-id="5c03f-171">İzin verilen IP adresleri, tek bir IP adresi (ör. '10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi kullanarak bir IP aralığı (ör. ‘10.0.0.1/22’) veya bir IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı (ör. '10.0.0.1(255.255.252.0)').</span><span class="sxs-lookup"><span data-stu-id="5c03f-171">Allowed IP addresses can be specified as either a single IP address (e.g. '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (e.g. '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (e.g. '10.0.0.1(255.255.252.0)').</span></span>
      
       <span data-ttu-id="5c03f-172">Herhangi bir IP adresi belirtilmezse ve bir kural tanımı yoksa hiçbir IP adresine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="5c03f-172">If no IP addresses are specified and there is no rule definition then no IP address will be allowed.</span></span> <span data-ttu-id="5c03f-173">tooallow herhangi bir IP adresi, bir kural oluşturun ve 0.0.0.0/0 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-173">tooallow any IP address, create a rule and set 0.0.0.0/0.</span></span>
6. <span data-ttu-id="5c03f-174">Merhaba üzerinde **Önizleme** sekmesinde, IP kısıtlama hello preview geçerli.</span><span class="sxs-lookup"><span data-stu-id="5c03f-174">On hello **Preview** tab, apply IP restriction on hello preview.</span></span>
7. <span data-ttu-id="5c03f-175">Merhaba üzerinde **kodlama** sekmesinde, hello kodlama hazır belirtin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-175">On hello **Encoding** tab, specify hello encoding preset.</span></span> 
   
    <span data-ttu-id="5c03f-176">Şu anda yalnızca sistem hello seçebileceğiniz hazır **720 p varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="5c03f-176">Currently, hello only system preset you can select is **Default 720p**.</span></span> <span data-ttu-id="5c03f-177">toospecify özel hazır ayarı, Microsoft destek bileti açın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-177">toospecify a custom preset, open a Microsoft support ticket.</span></span> <span data-ttu-id="5c03f-178">Merhaba hello adını enter sizin için oluşturduğu hazır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-178">Then, enter hello name of hello preset created for you.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c03f-179">Şu anda hello kanalın başlaması too30 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-179">Currently, hello Channel start can take up too30 minutes.</span></span> <span data-ttu-id="5c03f-180">Kanal sıfırlanması too5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-180">Channel reset can take up too5 minutes.</span></span>
> 
> 

<span data-ttu-id="5c03f-181">Merhaba kanalı oluşturduktan sonra hello kanalda tıklatın ve seçin **ayarları** kanal yapılandırmalarınızı görüntüleyebileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-181">Once you created hello Channel, you can click on hello channel and select **Settings** where you can view your channels configurations.</span></span> 

<span data-ttu-id="5c03f-182">Daha fazla bilgi için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5c03f-182">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="get-ingest-urls"></a><span data-ttu-id="5c03f-183">Alma URL’leri alma</span><span class="sxs-lookup"><span data-stu-id="5c03f-183">Get ingest URLs</span></span>
<span data-ttu-id="5c03f-184">Merhaba kanal oluşturulduktan sonra alabileceğiniz toohello gerçek zamanlı Kodlayıcı sağlayacak URL'lerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-184">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="5c03f-185">Merhaba Kodlayıcı bu URL'leri tooinput canlı akış kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-185">hello encoder uses these URLs tooinput a live stream.</span></span>

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a><span data-ttu-id="5c03f-187">Olay oluşturma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="5c03f-187">Create and manage events</span></span>
### <a name="overview"></a><span data-ttu-id="5c03f-188">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5c03f-188">Overview</span></span>
<span data-ttu-id="5c03f-189">Bir kanal toocontrol hello yayımlama ve canlı akıştaki kesimleri depolanmasını sağlayan olaylar/programlarla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-189">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="5c03f-190">Olayları/programları kanallar yönetir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-190">Channels manage events/programs.</span></span> <span data-ttu-id="5c03f-191">Merhaba kanal ve Program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay çok benzer tootraditional medya ilişkidir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-191">hello Channel and Program relationship is very similar tootraditional media where a channel has a constant stream of content and a program is scoped toosome timed event on that channel.</span></span>

<span data-ttu-id="5c03f-192">İstediğiniz tooretain kaydedilen hello içerik hello olayı için ayarı hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="5c03f-192">You can specify hello number of hours you want tooretain hello recorded content for hello event by setting hello **Archive Window** length.</span></span> <span data-ttu-id="5c03f-193">Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-193">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="5c03f-194">Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler.</span><span class="sxs-lookup"><span data-stu-id="5c03f-194">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="5c03f-195">Olayları hello belirtilen sürede çalıştırabilirsiniz ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-195">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="5c03f-196">Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.</span><span class="sxs-lookup"><span data-stu-id="5c03f-196">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="5c03f-197">Her olay bir Varlıkla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-197">Each event is associated with an Asset.</span></span> <span data-ttu-id="5c03f-198">Merhaba yönelik bir OnDemand Bulucu oluşturmanız gerekir toopublish hello olay varlık ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="5c03f-198">toopublish hello event you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="5c03f-199">Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c03f-199">Having this locator will enable you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="5c03f-200">Bir kanal hello birden çok arşivini oluşturabilmesi için olayları eşzamanlı olarak çalışan toothree destekler, aynı gelen akışın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-200">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="5c03f-201">Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c03f-201">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="5c03f-202">Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir olay, ancak toobroadcast yalnızca son 10 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-202">For example, your business requirement is tooarchive 6 hours of an event, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="5c03f-203">tooaccomplish Bu, iki eşzamanlı olarak çalışan toocreate gereken olay.</span><span class="sxs-lookup"><span data-stu-id="5c03f-203">tooaccomplish this, you need toocreate two concurrently running event.</span></span> <span data-ttu-id="5c03f-204">Bir olay tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-204">One event is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="5c03f-205">Merhaba diğer olay kümesi tooarchive 10 dakika için ve bu program yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-205">hello other event is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="5c03f-206">Yeni olaylar için mevcut programları yeniden kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="5c03f-206">You should not reuse existing programs for new events.</span></span> <span data-ttu-id="5c03f-207">Bunun yerine, her olay için yeni bir program oluşturup başlatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-207">Instead, create and start a new program for each event.</span></span>

<span data-ttu-id="5c03f-208">Akışı ve arşivlemeyi hazır toostart olduğunuzda olayı/programı başlatın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-208">Start an event/program when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="5c03f-209">Toostop akış ve arşivleme hello olayı istediğinizde hello olayı durdurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-209">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="5c03f-210">Arşivlenen toodelete içerik durdurup hello olay silme ve ardından hello ilişkili varlığı silin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-210">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="5c03f-211">Merhaba olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-211">An asset cannot be deleted if it is used by hello event; hello event must be deleted first.</span></span> 

<span data-ttu-id="5c03f-212">Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-212">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="5c03f-213">Arşivlenen tooretain hello içerik istiyor ancak değil bulundurursunuz akış için, Bulucu akış hello silin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-213">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="createstartstop-events"></a><span data-ttu-id="5c03f-214">Olay oluşturma/başlatma/durdurma</span><span class="sxs-lookup"><span data-stu-id="5c03f-214">Create/start/stop events</span></span>
<span data-ttu-id="5c03f-215">Merhaba kanala akması hello akış olduktan sonra olay bir varlık, Program ve akış Bulucu oluşturarak akış hello başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-215">Once you have hello stream flowing into hello Channel you can begin hello streaming event by creating an Asset, Program, and Streaming Locator.</span></span> <span data-ttu-id="5c03f-216">Merhaba akış arşivlemek ve hello akış uç noktası aracılığıyla kullanılabilir tooviewers yapın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-216">This will archive hello stream and make it available tooviewers through hello Streaming Endpoint.</span></span> 

>[!NOTE]
><span data-ttu-id="5c03f-217">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="5c03f-217">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="5c03f-218">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="5c03f-218">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="5c03f-219">İki yolu toostart olay vardır:</span><span class="sxs-lookup"><span data-stu-id="5c03f-219">There are two ways toostart event:</span></span> 

1. <span data-ttu-id="5c03f-220">Merhaba gelen **kanal** sayfasında, basın **canlı olay** tooadd yeni bir olay.</span><span class="sxs-lookup"><span data-stu-id="5c03f-220">From hello **Channel** page, press **Live Event** tooadd a new event.</span></span>
   
    <span data-ttu-id="5c03f-221">Şunları belirleyin: olay adı, varlık adı, arşiv penceresi ve şifreleme seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5c03f-221">Specify: event name, asset name, archive window, and encryption option.</span></span>
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    <span data-ttu-id="5c03f-223">Bırakılırsa **bu canlı olay Şimdi Yayımla** işaretli hello olay hello yayımlama URL'leri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5c03f-223">If you left **Publish this live event now** checked, hello event hello PUBLISHING URLs will get created.</span></span>
   
    <span data-ttu-id="5c03f-224">Basabilirsiniz **Başlat**, hazır toostream hello olay olduğunda.</span><span class="sxs-lookup"><span data-stu-id="5c03f-224">You can press **Start**, whenever you are ready toostream hello event.</span></span>
   
    <span data-ttu-id="5c03f-225">Merhaba olay başladıktan sonra basabilirsiniz **izleme** hello içeriği oynatmayı toostart.</span><span class="sxs-lookup"><span data-stu-id="5c03f-225">Once you start hello event, you can press **Watch** toostart playing hello content.</span></span>
2. <span data-ttu-id="5c03f-226">Alternatif olarak, bir kısayol ve tuşuna kullanabilirsiniz **Go Live** hello düğmesinde **kanal** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5c03f-226">Alternatively, you can use a shortcut and press **Go Live** button on hello **Channel** page.</span></span> <span data-ttu-id="5c03f-227">Bunun yapılması varsayılan bir Varlık, Program ve Akış Bulucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c03f-227">This will create a default Asset, Program, and Streaming Locator.</span></span>
   
    <span data-ttu-id="5c03f-228">Merhaba olay adlandırılan **varsayılan** ve hello arşiv penceresi ayarlanmış too8 saat.</span><span class="sxs-lookup"><span data-stu-id="5c03f-228">hello event is named **default** and hello archive window is set too8 hours.</span></span>

<span data-ttu-id="5c03f-229">Merhaba yayımlanan hello olayından izleyebilirsiniz **canlı olay** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5c03f-229">You can watch hello published event from hello **Live event** page.</span></span> 

<span data-ttu-id="5c03f-230">**Çevrimdışı** seçeneğine tıklarsanız tüm canlı olaylar durdurulur.</span><span class="sxs-lookup"><span data-stu-id="5c03f-230">If you click **Off Air**, it will stop all live events.</span></span> 

## <a name="watch-hello-event"></a><span data-ttu-id="5c03f-231">Gözcü hello olay</span><span class="sxs-lookup"><span data-stu-id="5c03f-231">Watch hello event</span></span>
<span data-ttu-id="5c03f-232">toowatch hello olay tıklatın **izleme** akış URL'si Azure portal ya da kopyalama hello hello ve tercih ettiğiniz bir oynatıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c03f-232">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Oluşturulan](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

<span data-ttu-id="5c03f-234">Canlı olay otomatik olarak durduğunda olayları tooon isteğe bağlı içerik dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="5c03f-234">Live event automatically converts events tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="5c03f-235">Temizleme</span><span class="sxs-lookup"><span data-stu-id="5c03f-235">Clean up</span></span>
<span data-ttu-id="5c03f-236">Olayların akışla yapılır ve önceden sağlanan hello kaynakları tooclean istiyorsanız hello aşağıdaki yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-236">If you are done streaming events and want tooclean up hello resources provisioned earlier, follow hello following procedure.</span></span>

* <span data-ttu-id="5c03f-237">Merhaba kodlayıcıdan Hello akışı göndermeyi durdurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-237">Stop pushing hello stream from hello encoder.</span></span>
* <span data-ttu-id="5c03f-238">Merhaba kanalı durdurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-238">Stop hello channel.</span></span> <span data-ttu-id="5c03f-239">Merhaba kanal durdurulduktan sonra herhangi bir ücret uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-239">Once hello Channel is stopped, it will not incur any charges.</span></span> <span data-ttu-id="5c03f-240">Toostart gerektiğinde bunu yeniden olacaktır kodlayıcıyı tooreconfigure gerekmeyecek şekilde hello aynı URL alma.</span><span class="sxs-lookup"><span data-stu-id="5c03f-240">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="5c03f-241">Canlı olayınızın bir isteğe bağlı akış olarak toocontinue tooprovide hello arşiv istemiyorsanız akış uç noktanızı durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-241">You can stop your Streaming Endpoint, unless you want toocontinue tooprovide hello archive of your live event as an on-demand stream.</span></span> <span data-ttu-id="5c03f-242">Merhaba kanal durdurulmuş durumda ise, herhangi bir ücret uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="5c03f-242">If hello channel is in stopped state, it will not incur any charges.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="5c03f-243">Arşivlenen içeriği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="5c03f-243">View archived content</span></span>
<span data-ttu-id="5c03f-244">Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5c03f-244">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="5c03f-245">Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-245">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="5c03f-246">varlıklarınızı, toomanage seçin **ayarı** tıklatıp **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="5c03f-246">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Varlıklar](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a><span data-ttu-id="5c03f-248">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="5c03f-248">Considerations</span></span>
* <span data-ttu-id="5c03f-249">Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir.</span><span class="sxs-lookup"><span data-stu-id="5c03f-249">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="5c03f-250">Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.</span><span class="sxs-lookup"><span data-stu-id="5c03f-250">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="5c03f-251">Akış içeriğinizi toostream istediğiniz uç hello hello olduğundan emin olun **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="5c03f-251">Make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

## <a name="next-step"></a><span data-ttu-id="5c03f-252">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="5c03f-252">Next step</span></span>
<span data-ttu-id="5c03f-253">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="5c03f-253">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c03f-254">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="5c03f-254">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

