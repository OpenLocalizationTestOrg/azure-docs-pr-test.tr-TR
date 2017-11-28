---
title: "hello Azure portal kullanarak şirket içi kodlayıcılarda olan aaaLive akış | Microsoft Docs"
description: "Bu öğretici, doğrudan teslimat için yapılandırılmış bir kanal oluşturulması hello adım adım anlatılmaktadır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="585d9-103">Nasıl tooperform ile canlı akış kodlayıcılar hello Azure portal kullanarak şirket içi</span><span class="sxs-lookup"><span data-stu-id="585d9-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="585d9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="585d9-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="585d9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="585d9-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="585d9-106">REST</span><span class="sxs-lookup"><span data-stu-id="585d9-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="585d9-107">Bu öğreticide Azure portal toocreate hello kullanmanın hello adımlarda size yol gösterir bir **kanal** doğrudan teslimat için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="585d9-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="585d9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="585d9-108">Prerequisites</span></span>
<span data-ttu-id="585d9-109">Merhaba, gerekli toocomplete hello öğretici şunlardır:</span><span class="sxs-lookup"><span data-stu-id="585d9-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="585d9-110">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="585d9-110">An Azure account.</span></span> <span data-ttu-id="585d9-111">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="585d9-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="585d9-112">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="585d9-112">A Media Services account.</span></span> <span data-ttu-id="585d9-113">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="585d9-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="585d9-114">Bir Web kamerası.</span><span class="sxs-lookup"><span data-stu-id="585d9-114">A webcam.</span></span> <span data-ttu-id="585d9-115">Örneğin, [Telestream Wirecast kodlayıcı](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="585d9-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="585d9-116">Aşağıdaki makaleleri tooreview hello önerilir:</span><span class="sxs-lookup"><span data-stu-id="585d9-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="585d9-117">Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar</span><span class="sxs-lookup"><span data-stu-id="585d9-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="585d9-118">Azure Media Services kullanarak Canlı Akış’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="585d9-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="585d9-119">Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış</span><span class="sxs-lookup"><span data-stu-id="585d9-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="585d9-120"><a id="scenario"></a>Ortak canlı akış senaryosu</span><span class="sxs-lookup"><span data-stu-id="585d9-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="585d9-121">Hello aşağıdaki adımlar, doğrudan teslimat için yapılandırılan kanalları kullanan ortak canlı akış uygulamaları oluşturmaya dahil olan görevleri açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="585d9-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="585d9-122">Bu öğreticide gösterilmiştir nasıl toocreate bir geçiş kanalı ve canlı olayları ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="585d9-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="585d9-123">Akış uç noktası toostream içerik istediğiniz hello hello olduğundan emin olun **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="585d9-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="585d9-124">Bir video kamera tooa bilgisayara bağlayın.</span><span class="sxs-lookup"><span data-stu-id="585d9-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="585d9-125">Çoklu bit hızlı RTMP ya da Parçalı MP4 akışı çıktısı veren bir şirket içi gerçek zamanlı kodlayıcı çalıştırın ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="585d9-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="585d9-126">Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="585d9-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="585d9-127">Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="585d9-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="585d9-128">Geçiş Kanalı oluşturun ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="585d9-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="585d9-129">Alma hello kanal URL'sini alma.</span><span class="sxs-lookup"><span data-stu-id="585d9-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="585d9-130">Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="585d9-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="585d9-131">Merhaba kanal Önizleme URL'sini alın.</span><span class="sxs-lookup"><span data-stu-id="585d9-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="585d9-132">Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.</span><span class="sxs-lookup"><span data-stu-id="585d9-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="585d9-133">Canlı olay/program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="585d9-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="585d9-134">Azure portal kullanarak hello zaman canlı bir olay oluşturma bir varlık da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="585d9-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="585d9-135">Akışı ve arşivlemeyi hazır toostart olduğunuzda hello olayı/programı başlatın.</span><span class="sxs-lookup"><span data-stu-id="585d9-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="585d9-136">İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir.</span><span class="sxs-lookup"><span data-stu-id="585d9-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="585d9-137">Merhaba tanıtım hello çıktı akışına eklenir.</span><span class="sxs-lookup"><span data-stu-id="585d9-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="585d9-138">Toostop akış ve arşivleme hello olayı istediğinizde hello olayı/programı durdurun.</span><span class="sxs-lookup"><span data-stu-id="585d9-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="585d9-139">Merhaba olayı/programı silin (ve isteğe bağlı olarak hello varlığını silme).</span><span class="sxs-lookup"><span data-stu-id="585d9-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="585d9-140">Lütfen gözden [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarda canlı akış](media-services-live-streaming-with-onprem-encoders.md) kavramları ve konuları hakkında toolearn ilgili toolive şirket içi kodlayıcılarda ve geçiş kanallarında canlı akış.</span><span class="sxs-lookup"><span data-stu-id="585d9-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="585d9-141">tooview bildirimleri ve hataları</span><span class="sxs-lookup"><span data-stu-id="585d9-141">tooview notifications and errors</span></span>
<span data-ttu-id="585d9-142">Tooview bildirimleri istiyorsanız ve hataları tarafından hello Azure portalında üretilen hello bildirim simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="585d9-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Bildirimler](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="585d9-144">Geçiş kanalları ve olayları oluşturma ve başlatma</span><span class="sxs-lookup"><span data-stu-id="585d9-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="585d9-145">Bir kanal toocontrol hello yayımlama ve canlı akıştaki kesimleri depolanmasını sağlayan olaylar/programlarla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="585d9-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="585d9-146">Kanallar olayları yönetir.</span><span class="sxs-lookup"><span data-stu-id="585d9-146">Channels manage events.</span></span> 

<span data-ttu-id="585d9-147">İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="585d9-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="585d9-148">Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585d9-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="585d9-149">Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler.</span><span class="sxs-lookup"><span data-stu-id="585d9-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="585d9-150">Olayları hello belirtilen sürede çalıştırabilirsiniz ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır.</span><span class="sxs-lookup"><span data-stu-id="585d9-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="585d9-151">Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.</span><span class="sxs-lookup"><span data-stu-id="585d9-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="585d9-152">Her olay bir varlıkla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="585d9-152">Each event is associated with an asset.</span></span> <span data-ttu-id="585d9-153">toopublish hello olay hello ilişkili varlığa yönelik bir OnDemand Bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="585d9-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="585d9-154">Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild sağlar.</span><span class="sxs-lookup"><span data-stu-id="585d9-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="585d9-155">Bir kanal hello birden çok arşivini oluşturabilmesi için olayları eşzamanlı olarak çalışan toothree destekler, aynı gelen akışın.</span><span class="sxs-lookup"><span data-stu-id="585d9-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="585d9-156">Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="585d9-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="585d9-157">Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir program, ancak toobroadcast yalnızca son 10 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="585d9-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="585d9-158">tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="585d9-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="585d9-159">Bir program tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz.</span><span class="sxs-lookup"><span data-stu-id="585d9-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="585d9-160">Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="585d9-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="585d9-161">Mevcut canlı olayları yeniden kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="585d9-161">You should not reuse existing live events.</span></span> <span data-ttu-id="585d9-162">Bunun yerine, her olay için yeni bir olay oluşturun ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="585d9-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="585d9-163">Akışı ve arşivlemeyi hazır toostart olduğunda hello olayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="585d9-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="585d9-164">Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun.</span><span class="sxs-lookup"><span data-stu-id="585d9-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="585d9-165">Arşivlenen toodelete içerik durdurup hello olay silme ve ardından hello ilişkili varlığı silin.</span><span class="sxs-lookup"><span data-stu-id="585d9-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="585d9-166">Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="585d9-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="585d9-167">Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="585d9-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="585d9-168">Arşivlenen tooretain hello içerik istiyor ancak değil bulundurursunuz akış için, Bulucu akış hello silin.</span><span class="sxs-lookup"><span data-stu-id="585d9-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="585d9-169">toouse hello portal toocreate bir kanal</span><span class="sxs-lookup"><span data-stu-id="585d9-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="585d9-170">Bu bölümde gösterilmiştir nasıl toouse hello **hızlı Oluştur** seçeneği toocreate bir geçiş kanalı.</span><span class="sxs-lookup"><span data-stu-id="585d9-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="585d9-171">Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="585d9-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="585d9-172">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="585d9-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="585d9-173">Merhaba, **ayarları** penceresinde tıklatın **canlı akış**.</span><span class="sxs-lookup"><span data-stu-id="585d9-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Başlarken](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="585d9-175">Merhaba **canlı akış** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="585d9-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="585d9-176">Tıklatın **hızlı Oluştur** toocreate bir geçiş kanalı hello RTMP alma protokolüyle.</span><span class="sxs-lookup"><span data-stu-id="585d9-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="585d9-177">Merhaba **Yeni Kanal Oluştur** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="585d9-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="585d9-178">Merhaba yeni kanala bir ad verin ve tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="585d9-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="585d9-179">Bu bir geçiş kanalı ile Merhaba oluşturur RTMP alma protokolüyle.</span><span class="sxs-lookup"><span data-stu-id="585d9-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="585d9-180">Olay oluşturma</span><span class="sxs-lookup"><span data-stu-id="585d9-180">Create events</span></span>
1. <span data-ttu-id="585d9-181">Bir olay tooadd istediğiniz bir kanal toowhich seçin.</span><span class="sxs-lookup"><span data-stu-id="585d9-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="585d9-182">**Canlı Olay** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="585d9-182">Press **Live Event** button.</span></span>

![Olay](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="585d9-184">Alma URL’leri alma</span><span class="sxs-lookup"><span data-stu-id="585d9-184">Get ingest URLs</span></span>
<span data-ttu-id="585d9-185">Merhaba kanal oluşturulduktan sonra alabileceğiniz toohello gerçek zamanlı Kodlayıcı sağlayacak URL'lerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585d9-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="585d9-186">Merhaba Kodlayıcı bu URL'leri tooinput canlı akış kullanır.</span><span class="sxs-lookup"><span data-stu-id="585d9-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="585d9-188">Gözcü hello olay</span><span class="sxs-lookup"><span data-stu-id="585d9-188">Watch hello event</span></span>
<span data-ttu-id="585d9-189">toowatch hello olay tıklatın **izleme** akış URL'si Azure portal ya da kopyalama hello hello ve tercih ettiğiniz bir oynatıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="585d9-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="585d9-191">Canlı olay otomatik olarak durduğunda dönüştürülmüş tooon isteğe bağlı içerik alın.</span><span class="sxs-lookup"><span data-stu-id="585d9-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="585d9-192">Temizleme</span><span class="sxs-lookup"><span data-stu-id="585d9-192">Clean up</span></span>
<span data-ttu-id="585d9-193">Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="585d9-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="585d9-194">Yalnızca tüm olaylar/programlar hello kanalda vermemeye başladığında bir kanal durdurulabilir.</span><span class="sxs-lookup"><span data-stu-id="585d9-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="585d9-195">Merhaba kanal durdurulduktan sonra herhangi bir ücret doğurur değil.</span><span class="sxs-lookup"><span data-stu-id="585d9-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="585d9-196">Toostart gerektiğinde bunu yeniden olacaktır kodlayıcıyı tooreconfigure gerekmeyecek şekilde hello aynı URL alma.</span><span class="sxs-lookup"><span data-stu-id="585d9-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="585d9-197">Bir kanal yalnızca hello kanaldaki tüm Canlı olaylar silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="585d9-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="585d9-198">Arşivlenen içeriği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="585d9-198">View archived content</span></span>
<span data-ttu-id="585d9-199">Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="585d9-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="585d9-200">Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="585d9-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="585d9-201">varlıklarınızı, toomanage seçin **ayarı** tıklatıp **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="585d9-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Varlıklar](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="585d9-203">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="585d9-203">Next step</span></span>
<span data-ttu-id="585d9-204">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="585d9-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="585d9-205">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="585d9-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

