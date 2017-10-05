---
title: "Azure portalı kullanarak şirket içi kodlayıcılarda canlı akış | Microsoft Docs"
description: "Bu öğretici, doğrudan teslimat için yapılandırılmış bir Kanal oluşturmaya ilişkin adımları anlatmaktadır."
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
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="a8601-103">Azure portalı kullanarak şirket içi kodlayıcılarda canlı akış gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="a8601-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8601-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a8601-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="a8601-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a8601-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="a8601-106">REST</span><span class="sxs-lookup"><span data-stu-id="a8601-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="a8601-107">Bu öğretici, Azure portal kullanarak doğrudan teslimat için yapılandırılmış bir **Kanal** oluşturmaya ilişkin adımları anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a8601-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8601-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a8601-108">Prerequisites</span></span>
<span data-ttu-id="a8601-109">Öğreticiyi tamamlamak için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a8601-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="a8601-110">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a8601-110">An Azure account.</span></span> <span data-ttu-id="a8601-111">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8601-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a8601-112">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="a8601-112">A Media Services account.</span></span> <span data-ttu-id="a8601-113">Bir Media Services hesabı oluşturmak için bkz. [Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a8601-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a8601-114">Bir Web kamerası.</span><span class="sxs-lookup"><span data-stu-id="a8601-114">A webcam.</span></span> <span data-ttu-id="a8601-115">Örneğin, [Telestream Wirecast kodlayıcı](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="a8601-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="a8601-116">Aşağıdaki makaleleri gözden geçirmeniz için önerilir:</span><span class="sxs-lookup"><span data-stu-id="a8601-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="a8601-117">Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar</span><span class="sxs-lookup"><span data-stu-id="a8601-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="a8601-118">Azure Media Services kullanarak Canlı Akış’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a8601-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="a8601-119">Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış</span><span class="sxs-lookup"><span data-stu-id="a8601-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="a8601-120"><a id="scenario"></a>Ortak canlı akış senaryosu</span><span class="sxs-lookup"><span data-stu-id="a8601-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="a8601-121">Aşağıdaki adımlar, doğrudan teslimat için yapılandırılan kanalları kullanan ortak canlı akış uygulamaları oluşturmaya dahil olan görevleri açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="a8601-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="a8601-122">Bu öğretici, doğrudan geçiş kanalı ve canlı olayları oluşturmayı ve yönetmeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8601-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="a8601-123">İçerik akışı yapmak istediğiniz akış uç noktasının **Çalışıyor** durumunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a8601-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="a8601-124">Bilgisayara bir video kamera bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="a8601-125">Çoklu bit hızlı RTMP ya da Parçalı MP4 akışı çıktısı veren bir şirket içi gerçek zamanlı kodlayıcı çalıştırın ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8601-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="a8601-126">Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="a8601-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="a8601-127">Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="a8601-128">Geçiş Kanalı oluşturun ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8601-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="a8601-129">Kanal alma URL’sini alın.</span><span class="sxs-lookup"><span data-stu-id="a8601-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="a8601-130">Alma URL’si gerçek zamanlı kodlayıcı tarafından akışı Kanala göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8601-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="a8601-131">Kanal önizleme URL’sini alın.</span><span class="sxs-lookup"><span data-stu-id="a8601-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="a8601-132">Kanalınızın canlı akışı düzgün şekilde aldığını doğrulamak için bu URL’yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8601-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="a8601-133">Canlı olay/program oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8601-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="a8601-134">Azure portalı kullanırken, canlı bir olay oluşturma bir varlık da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8601-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="a8601-135">Akışı ve arşivlemeyi başlatmaya hazır olduğunuzda, olayı/programı başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8601-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="a8601-136">İsteğe bağlı olarak, gerçek zamanlı kodlayıcıya bir reklam başlatması bildirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="a8601-137">Reklam, çıktı akışına eklenir.</span><span class="sxs-lookup"><span data-stu-id="a8601-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="a8601-138">Olay akışını ve arşivlemeyi durdurmak istediğinizde, olayı/programı durdurun.</span><span class="sxs-lookup"><span data-stu-id="a8601-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="a8601-139">Olayı/programı silin (ve isteğe bağlı olarak varlığı silin).</span><span class="sxs-lookup"><span data-stu-id="a8601-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="a8601-140">Lütfen şirket içi kodlayıcılarda ve geçiş kanallarında canlı akışlarla ilgili kavramları ve dikkate alınması gereken noktaları öğrenmek için [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md) başlığını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a8601-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="a8601-141">Bildirimleri ve hataları görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="a8601-141">To view notifications and errors</span></span>
<span data-ttu-id="a8601-142">Azure portal tarafından oluşturulan bildirimleri ve hataları görüntülemek istiyorsanız, Bildirim simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Bildirimler](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="a8601-144">Geçiş kanalları ve olayları oluşturma ve başlatma</span><span class="sxs-lookup"><span data-stu-id="a8601-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="a8601-145">Bir kanal, canlı akıştaki kesimleri yayımlamanızı ve depolamanızı denetlemenizi sağlayan olaylar/programlarla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a8601-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="a8601-146">Kanallar olayları yönetir.</span><span class="sxs-lookup"><span data-stu-id="a8601-146">Channels manage events.</span></span> 

<span data-ttu-id="a8601-147">Program için kaydedilen içeriği kaç saat tutmak istediğinizi **Arşiv Penceresi** uzunluğunu ayarlayarak belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8601-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="a8601-148">Bu değer en az 5 dakika, en çok 25 saat olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="a8601-149">Arşiv penceresi uzunluğu, istemcilerin geçerli canlı konumdan zamanda geri gidebilecekleri en uzun süre miktarını da belirler.</span><span class="sxs-lookup"><span data-stu-id="a8601-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="a8601-150">Olaylar belirtilen süre miktarında yürütülür, ancak pencere uzunluğunu aşan içerik sürekli olarak iptal edilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="a8601-151">Bu özelliğin bu değeri, istemci bildiriminin ne kadar uzayabileceğini de belirler.</span><span class="sxs-lookup"><span data-stu-id="a8601-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="a8601-152">Her olay bir varlıkla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a8601-152">Each event is associated with an asset.</span></span> <span data-ttu-id="a8601-153">Olayı yayımlamak için ilişkili varlığa yönelik bir OnDemand bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8601-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="a8601-154">Bu bulucuya sahip olmak istemcilerinize sağlayabileceğiniz bir akış URL’si oluşturmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a8601-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="a8601-155">Bir kanal eşzamanlı çalışan üç olaya kadar destekler, böylece aynı gelen akışta birden fazla arşiv oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8601-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="a8601-156">Bu özellik, gerektiğinde bir olayın farklı kısımlarını yayımlamanıza ve arşivlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a8601-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="a8601-157">Örneğin, iş gereksiniminiz bir programın 6 saatini arşivlemek ancak son 10 dakikasını yayınlamak olabilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="a8601-158">Bunu yapmak için, eşzamanlı olarak çalışan iki program oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8601-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="a8601-159">Bir program olayı 6 saat arşivlemek için ayarlanır ancak program yayımlanmaz.</span><span class="sxs-lookup"><span data-stu-id="a8601-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="a8601-160">Diğer program 10 dakika arşivlenecek şekilde ve bu program yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="a8601-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="a8601-161">Mevcut canlı olayları yeniden kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="a8601-161">You should not reuse existing live events.</span></span> <span data-ttu-id="a8601-162">Bunun yerine, her olay için yeni bir olay oluşturun ve başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8601-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="a8601-163">Akışa ve arşivlemeye hazır olduğunuzda olayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="a8601-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="a8601-164">Olay için akışı ve arşivlemeyi durdurmak istediğinizde programı durdurun.</span><span class="sxs-lookup"><span data-stu-id="a8601-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="a8601-165">Arşivlenen içeriği silmek için, olayı durdurun ve ardından ilişkili varlığı silin.</span><span class="sxs-lookup"><span data-stu-id="a8601-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="a8601-166">Bir olay tarafından kullanılıyorsa varlık silinemez; önce olayın silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8601-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="a8601-167">Olayı durdurduktan ve sildikten sonra dahi, varlığı silmeniz sürece, kullanıcılar arşivlenen içeriğinizin isteğe bağlı içerik olarak akışını gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="a8601-168">Arşivlenen içeriği tutmak istiyor ancak bu içeriğin akış için kullanılmasını istemiyorsanız, akış bulucuyu silin.</span><span class="sxs-lookup"><span data-stu-id="a8601-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="a8601-169">Bir kanal oluşturmak amacıyla portalı kullanmak için</span><span class="sxs-lookup"><span data-stu-id="a8601-169">To use the portal to create a channel</span></span>
<span data-ttu-id="a8601-170">Bu bölüm bir geçiş kanalı oluşturmak için **Hızlı Oluştur** seçeneğinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8601-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="a8601-171">Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a8601-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="a8601-172">[Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="a8601-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a8601-173">**Ayarlar** penceresinde, **Canlı Akış**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Başlarken](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="a8601-175">**Canlı akış** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a8601-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="a8601-176">RTMP alma protokolüyle bir geçiş kanalı oluşturmak için **Hızlı Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="a8601-177">**YENİ KANAL OLUŞTUR** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a8601-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="a8601-178">Yeni kanala bir ad verin ve **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="a8601-179">Bunun yapılması RTMP alma protokolüyle bir geçiş kanalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a8601-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="a8601-180">Olay oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8601-180">Create events</span></span>
1. <span data-ttu-id="a8601-181">Olay eklemek istediğiniz bir kanal seçin.</span><span class="sxs-lookup"><span data-stu-id="a8601-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="a8601-182">**Canlı Olay** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="a8601-182">Press **Live Event** button.</span></span>

![Olay](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="a8601-184">Alma URL’leri alma</span><span class="sxs-lookup"><span data-stu-id="a8601-184">Get ingest URLs</span></span>
<span data-ttu-id="a8601-185">Kanal oluşturulduktan sonra, gerçek zamanlı kodlayıcıya sağlayacağınız alma URL’lerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8601-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="a8601-186">Kodlayıcı bu URL'leri canlı akış girişi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a8601-186">The encoder uses these URLs to input a live stream.</span></span>

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="a8601-188">Olayı izleme</span><span class="sxs-lookup"><span data-stu-id="a8601-188">Watch the event</span></span>
<span data-ttu-id="a8601-189">Olay izlemek için, Azure portalda **İzle**’ye tıklayın veya akış URL'sini kopyalayın ve tercih ettiğiniz bir oynatıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8601-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="a8601-191">Canlı olay durduğunda otomatik olarak isteğe bağlı içeriğe dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="a8601-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a8601-192">Temizleme</span><span class="sxs-lookup"><span data-stu-id="a8601-192">Clean up</span></span>
<span data-ttu-id="a8601-193">Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a8601-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="a8601-194">Bir kanal yalnızca kanaldaki tüm olaylar/programlar durdurulduğunda durdurulabilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="a8601-195">Kanal durdurulduktan sonra herhangi bir ücret uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="a8601-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="a8601-196">Tekrar başlatmanız gerektiğinde, aynı alma URL’sine sahip olacağından kodlayıcıyı yeniden yapılandırmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a8601-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="a8601-197">Bir kanal yalnızca kanaldaki tüm canlı olaylar silindiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="a8601-198">Arşivlenen içeriği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a8601-198">View archived content</span></span>
<span data-ttu-id="a8601-199">Olayı durdurduktan ve sildikten sonra dahi, varlığı silmeniz sürece, kullanıcılar arşivlenen içeriğinizin isteğe bağlı içerik olarak akışını gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="a8601-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="a8601-200">Bir olay tarafından kullanılıyorsa varlık silinemez; önce olayın silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8601-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="a8601-201">Varlıklarınızı yönetmek için, **Ayar**’ı seçin ve **Varlıklar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8601-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Varlıklar](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="a8601-203">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a8601-203">Next step</span></span>
<span data-ttu-id="a8601-204">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a8601-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8601-205">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a8601-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

