---
title: "aaaAvanced Medya Kodlayıcısı Premium iş akışı öğreticileri"
description: "Bu belgeyi nasıl tooperform Gelişmiş Medya Kodlayıcısı Premium akışıyla görevleri göster talimatları içerir ve ayrıca nasıl iş akışı Tasarımcısı ile toocreate karmaşık iş akışları."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="7d480-103">Gelişmiş Medya Kodlayıcısı Premium iş akışı öğreticileri</span><span class="sxs-lookup"><span data-stu-id="7d480-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="7d480-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7d480-104">Overview</span></span>
<span data-ttu-id="7d480-105">Bu belge göster izlenecek yollar içeriyor nasıl toocustomize iş akışlarıyla **iş akışı Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="7d480-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="7d480-106">Gerçek iş akışı dosyalarını hello bulabilirsiniz [burada](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="7d480-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="7d480-107">İÇİNDEKİLER</span><span class="sxs-lookup"><span data-stu-id="7d480-107">TOC</span></span>
<span data-ttu-id="7d480-108">Aşağıdaki konularda hello ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="7d480-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="7d480-109">Tek bit hızlı MP4 MXF kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="7d480-110">Yeni bir iş akışı başlatma</span><span class="sxs-lookup"><span data-stu-id="7d480-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="7d480-111">Merhaba ortam dosyası girişi kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="7d480-112">Medya akışlarının inceleniyor</span><span class="sxs-lookup"><span data-stu-id="7d480-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="7d480-113">Bir video Kodlayıcısı için ekleniyor. MP4 dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d480-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="7d480-114">Kodlama hello ses akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="7d480-115">Ses ve Video akışları bir MP4 kapsayıcıya çoğullama</span><span class="sxs-lookup"><span data-stu-id="7d480-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="7d480-116">Merhaba MP4 dosyası yazılıyor</span><span class="sxs-lookup"><span data-stu-id="7d480-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="7d480-117">Bir Media Services varlık hello çıktı dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d480-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="7d480-118">İş akışı yerel olarak test hello tamamlandı</span><span class="sxs-lookup"><span data-stu-id="7d480-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="7d480-119">MXF MP4s - multibitrate kodlama etkin dinamik paketleme</span><span class="sxs-lookup"><span data-stu-id="7d480-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="7d480-120">Bir veya daha fazla ek MP4 çıktı ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="7d480-121">Yapılandırma hello dosya çıkış adları</span><span class="sxs-lookup"><span data-stu-id="7d480-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="7d480-122">Ayrı bir ses izi ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="7d480-123">Merhaba ekleniyor. ISM SMIL dosyası</span><span class="sxs-lookup"><span data-stu-id="7d480-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="7d480-124">MP4 - Gelişmiş şeması multibitrate MXF kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="7d480-125">İş akışı genel bakış tooenhance</span><span class="sxs-lookup"><span data-stu-id="7d480-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="7d480-126">Dosya adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="7d480-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="7d480-127">Yayımlama hello iş akışı kök üzerine bileşeni özellikleri</span><span class="sxs-lookup"><span data-stu-id="7d480-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="7d480-128">Çıktı dosyası adları yayımlanan özellik değerlerine dayanan oluşturulmasını</span><span class="sxs-lookup"><span data-stu-id="7d480-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="7d480-129">Küçük resimleri toomultibitrate MP4 çıktı ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="7d480-130">İş akışı genel bakış tooadd küçük resim</span><span class="sxs-lookup"><span data-stu-id="7d480-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="7d480-131">JPG kodlama ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="7d480-132">Renk alanını dönüştürme postalarla</span><span class="sxs-lookup"><span data-stu-id="7d480-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="7d480-133">Yazma hello küçük resimleri</span><span class="sxs-lookup"><span data-stu-id="7d480-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="7d480-134">Bir iş akışında hataları algılama</span><span class="sxs-lookup"><span data-stu-id="7d480-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="7d480-135">Tamamlanmış iş akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="7d480-136">Zamana bağlı kırpma multibitrate MP4 çıktı</span><span class="sxs-lookup"><span data-stu-id="7d480-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="7d480-137">İş akışı genel bakış toostart kırpma için ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="7d480-138">Merhaba akış Kırpıcıyı kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="7d480-139">Tamamlanmış iş akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="7d480-140">Merhaba Script bileşeni Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="7d480-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="7d480-141">Bir iş akışı içinde komut dosyası: Merhaba Dünya</span><span class="sxs-lookup"><span data-stu-id="7d480-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="7d480-142">Çerçeve tabanlı kırpma multibitrate MP4 çıktı</span><span class="sxs-lookup"><span data-stu-id="7d480-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="7d480-143">Genel Bakış toostart kırpma için ekleme şeması</span><span class="sxs-lookup"><span data-stu-id="7d480-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="7d480-144">Merhaba küçük liste XML kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="7d480-145">Komut dosyası bir bileşenin Hello küçük listesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="7d480-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="7d480-146">ClippingEnabled kolaylık özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="7d480-147"><a id="MXF_to_MP4"></a>Tek bit hızlı MP4 MXF kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="7d480-148">Bu kılavuzda tek bit hızlı oluşturacağız. MP4 dosyası AAC-HE ile kodlanmış ses öğesinden bir. MXF giriş dosyası.</span><span class="sxs-lookup"><span data-stu-id="7d480-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="7d480-149"><a id="MXF_to_MP4_start_new"></a>Yeni bir iş akışı başlatma</span><span class="sxs-lookup"><span data-stu-id="7d480-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="7d480-150">İş Akışı Tasarımcısı'nı açın ve "Dosyası"-"Yeni çalışma alanı"-"kodlamasını şeması" seçin</span><span class="sxs-lookup"><span data-stu-id="7d480-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="7d480-151">Merhaba yeni iş akışı 3 öğeleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="7d480-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="7d480-152">Birincil kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="7d480-152">Primary Source File</span></span>
* <span data-ttu-id="7d480-153">Küçük resim listesi XML'i</span><span class="sxs-lookup"><span data-stu-id="7d480-153">Clip List XML</span></span>
* <span data-ttu-id="7d480-154">Çıkış dosyası/varlık</span><span class="sxs-lookup"><span data-stu-id="7d480-154">Output File/Asset</span></span>  

![Yeni bir kodlama iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="7d480-156">*Yeni bir kodlama iş akışı*</span><span class="sxs-lookup"><span data-stu-id="7d480-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="7d480-157"><a id="MXF_to_MP4_with_file_input"></a>Merhaba ortam dosyası girişi kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="7d480-158">Sipariş tooaccept bizim giriş medya dosyasını bir medya dosyası giriş bileşeni ekleme ile başlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="7d480-159">tooadd bileşen toohello iş akışı hello deposu arama kutusuna aramanız ve istenen hello girişi hello Tasarımcı bölmesine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="7d480-160">Bunu hello medya dosyası giriş yapmak ve hello birincil kaynak dosya bileşen toohello Filename giriş PIN hello medya dosyası giriş bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7d480-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Bağlı ortam giriş dosyası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="7d480-162">*Bağlı ortam giriş dosyası*</span><span class="sxs-lookup"><span data-stu-id="7d480-162">*Connected Media File Input*</span></span>

<span data-ttu-id="7d480-163">Başka bir çok yapabiliriz önce biz öncelikle tooindicate toohello iş akışı Tasarımcısı hangi örnek dosya gerekir toouse toodesign isteriz bizim iş akışıyla.</span><span class="sxs-lookup"><span data-stu-id="7d480-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="7d480-164">Bu nedenle, toodo hello Tasarımcı bölmesinde arka plan tıklatın ve hello birincil kaynak dosyası özelliği hello sağ özellik bölmesinde için arayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="7d480-165">Merhaba klasör simgesine ve istenen select hello dosya tootest hello akışıyla'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7d480-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="7d480-166">Bu yapılır hemen hello medya dosyası giriş bileşen hello dosyasını inceleyin ve onu Denetlenmekte kendi çıktı PIN'ler tooreflect hello dosyasını doldurun.</span><span class="sxs-lookup"><span data-stu-id="7d480-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Doldurulan ortam giriş dosyası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="7d480-168">*Doldurulan ortam giriş dosyası*</span><span class="sxs-lookup"><span data-stu-id="7d480-168">*Populated Media File Input*</span></span>

<span data-ttu-id="7d480-169">Bu ne ile toowork isteriz giriş ile belirtir, ancak bunu bildirmez henüz kodlanmış hello çıktı için nereye.</span><span class="sxs-lookup"><span data-stu-id="7d480-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="7d480-170">Birincil kaynak dosya yapılandırılan benzer toohow hello şimdi hello hemen altındaki çıkış klasörü değişken özelliğini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Yapılandırılan giriş ve çıkış özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="7d480-172">*Yapılandırılan giriş ve çıkış özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="7d480-173"><a id="MXF_to_MP4_streams"></a>Medya akışlarının inceleniyor</span><span class="sxs-lookup"><span data-stu-id="7d480-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="7d480-174">Genellikle nasıl hello akış gibi göründüğünü tooknow hello iş akışı akar istendiğini.</span><span class="sxs-lookup"><span data-stu-id="7d480-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="7d480-175">tooinspect hello iş akışında, herhangi bir noktada bir akış, bir çıkış veya giriş PIN hello bileşenleri hiçbirinde yalnızca tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7d480-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="7d480-176">Bu durumda, hello sıkıştırılmamış Video Çıkış PIN bizim medya dosyası girişten gelen tıklayarak deneyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="7d480-177">Bir iletişim kutusu tooinspect hello giden video sağlayan açılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![İnceleme hello sıkıştırılmamış Video Çıkış PIN](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="7d480-179">*İnceleme hello sıkıştırılmamış Video Çıkış PIN*</span><span class="sxs-lookup"><span data-stu-id="7d480-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="7d480-180">Örneğimizde, bize örneğin biz 4 saniyede 24 kare konumundaki 1920 x 1080 giriş ile ilgilenen olduğunu söyler: 2:2 örnekleme neredeyse 2 dakikalık video.</span><span class="sxs-lookup"><span data-stu-id="7d480-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="7d480-181"><a id="MXF_to_MP4_file_generation"></a>Bir video Kodlayıcısı için ekleniyor. MP4 dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d480-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="7d480-182">Şimdi unutmayın, sıkıştırılmamış bir Video ve birden çok sıkıştırılmamış ses çıkış PIN bizim ortam dosyası girişi üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="7d480-183">Sipariş tooencode içinde gelen video Merhaba, kodlama bileşeni - bu durumda oluşturmak için ihtiyacımız. Mp4 dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7d480-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="7d480-184">tooencode video akışına tooH.264 Merhaba, hello AVC Video Kodlayıcısı bileşen toohello Tasarımcı yüzeyine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="7d480-185">Bu bileşen uncompress video akışına giriş olarak alır ve bir AVC sıkıştırılmış video akışı kendi çıktı PIN sunar.</span><span class="sxs-lookup"><span data-stu-id="7d480-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Bağlantısız AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="7d480-187">*Bağlantısız AVC kodlayıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="7d480-188">Özelliklerini nasıl hello kodlama tam olarak gerçekleştiğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="7d480-189">Şimdi hello bazıları bakma sahip daha önemli ayarları:</span><span class="sxs-lookup"><span data-stu-id="7d480-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="7d480-190">Çıktı genişlik ve yükseklik çıktı: Bu kodlanmış hello videonun hello çözümü belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="7d480-191">Örneğimizde 640 x 360 ile edelim</span><span class="sxs-lookup"><span data-stu-id="7d480-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="7d480-192">Kare hızı: yalnızca kümesi toopassthrough benimsemeye hello kaynak kare hızı olası toooverride yine de bu olur.</span><span class="sxs-lookup"><span data-stu-id="7d480-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="7d480-193">Böyle kare hızı dönüştürme değil hareket-dengelendi olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="7d480-194">Profil ve düzeyi: Bunlar hello AVC profil ve düzeyini belirler.</span><span class="sxs-lookup"><span data-stu-id="7d480-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="7d480-195">tooconveniently daha fazla bilgi alın hello farklı düzeylerde ve profilleri hakkında hello AVC Video Kodlayıcısı bileşen hello soru işareti simgesine tıklayın ve hello Yardım sayfası, her bir hello düzeyleri hakkında daha fazla ayrıntı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d480-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="7d480-196">Bizim örnek için 3.2 (Merhaba varsayılan) düzeyinde ana profille edelim.</span><span class="sxs-lookup"><span data-stu-id="7d480-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="7d480-197">Denetim modu, bit hızı (kbps) oranı: biz opt Senaryomuzda 1200 KB/sn ile çıkış sabit hızı (CBR) için</span><span class="sxs-lookup"><span data-stu-id="7d480-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="7d480-198">Görüntü biçimi: Bu hello hello H.264 akışa yazılan (Video kullanılabilirlik bilgileri) VUI hakkındadır (bir kod çözücü tooenhance hello görünen ancak temel toocorrectly tarafından kullanılıyor olabilir yan bilgi kod çözme):</span><span class="sxs-lookup"><span data-stu-id="7d480-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="7d480-199">NTSC (ABD veya Japonya, 30 fps kullanma için tipik)</span><span class="sxs-lookup"><span data-stu-id="7d480-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="7d480-200">PAL (25 fps kullanarak Avrupa için tipik)</span><span class="sxs-lookup"><span data-stu-id="7d480-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="7d480-201">GOP boyutu modu: 2 saniye kapalı GOPs ile bir anahtar aralığı ile bizim amacıyla sabit GOP boyutu yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="7d480-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="7d480-202">Bu, dinamik paketleme Azure Media Services sağlar hello ile uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="7d480-203">toofeed bizim AVC Kodlayıcı hello sıkıştırılmamış Video Çıkış PIN hello medya dosyası giriş bileşen toohello sıkıştırılmamış Video giriş PIN hello AVC kodlayıcıdan bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Bağlı AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="7d480-205">*Bağlı AVC ana kodlayıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="7d480-206"><a id="MXF_to_MP4_audio"></a>Kodlama hello ses akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="7d480-207">Bu noktada, biz video kodlanmıştır ancak hello özgün sıkıştırılmamış ses akışı hala sıkıştırılmış toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7d480-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="7d480-208">Bunun için AAC Kodlayıcı (Dolby) bileşeni tarafından hello kodlama AAC ile gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="7d480-209">Toohello iş akışı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-209">Add it toohello workflow.</span></span>

![Bağlantısız AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="7d480-211">*Bağlantısız AAC kodlayıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="7d480-212">Bir uyumsuzluk şimdi: büyük olasılıkla hello medya dosyası giriş iki farklı olacaktır fazlasını ses akışı kullanılabilir sıkıştırılmamış sırasında yalnızca bir tek sıkıştırılmamış ses giriş PIN hello AAC Kodlayıcı gelen olduğu: sol ses kanal ve hello için bir başlangıç için bir tane Sağa.</span><span class="sxs-lookup"><span data-stu-id="7d480-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="7d480-213">(Surround sesle ele alma, 6 kanalları olmasıdır.) Olası değil toodirectly bağlanın hello ses hello medya dosyası giriş kaynağından hello AAC ses Kodlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d480-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="7d480-214">Merhaba AAC bileşen bekliyor sözde "araya eklemeli" ses akışı: her ikisi de sahip tek bir akış hello birbirleri ile araya eklemeli sola ve hello sağ kanallar.</span><span class="sxs-lookup"><span data-stu-id="7d480-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="7d480-215">Bizim kaynak medya dosyasından biliyoruz sonra hangi ses izleri hello kaynağındaki hangi konumuna biz hello olan araya eklemeli gibi ses akış doğru bir şekilde oluşturabilmesi sol ve sağ için Konuşmacı konumlarına atanır.</span><span class="sxs-lookup"><span data-stu-id="7d480-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="7d480-216">Önce bir toogenerated bir araya eklemeli gerekli hello kaynak ses kanalları akıştan isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="7d480-217">Merhaba ses akışı ayırıcı bileşen bu bize işleyecek.</span><span class="sxs-lookup"><span data-stu-id="7d480-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="7d480-218">Toohello iş akışını Ekle ve hello ses çıkış hello ortam dosyası girişi içine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Ses akışı ayırıcı bağlı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="7d480-220">*Ses akışı ayırıcı bağlı*</span><span class="sxs-lookup"><span data-stu-id="7d480-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="7d480-221">Bir araya eklemeli ses akışını sahibiz, hala olduğu için tooassign hello sola veya sağa Konuşmacı konumlandırır belirttiğimiz alamadık.</span><span class="sxs-lookup"><span data-stu-id="7d480-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="7d480-222">Toospecify Bu sipariş, biz hello Konuşmacı konumu Assigner yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Konuşmacı konumu Assigner ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="7d480-224">*Konuşmacı konumu Assigner ekleme*</span><span class="sxs-lookup"><span data-stu-id="7d480-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="7d480-225">Merhaba Konuşmacı konumu Assigner kullanmak için bir kodlayıcı önceden Filtresi "Özel" olan stereo giriş akış yapılandırmak ve "2.0 (M, R)" adlı kanal önceden hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="7d480-226">(Bu hello sol Konuşmacı konumu toochannel 1 ve hello sağ Konuşmacı konumu toochannel 2 atayacaktır.)</span><span class="sxs-lookup"><span data-stu-id="7d480-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="7d480-227">Merhaba Konuşmacı konumu Assigner toohello girişi hello AAC Kodlayıcı Hello çıkışına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="7d480-228">Ardından, bir "2.0 ile (M, R)" Merhaba AAC Kodlayıcı toowork söyleyin kanal stereo ses giriş olarak ile toodeal bilmesi için hazır.</span><span class="sxs-lookup"><span data-stu-id="7d480-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="7d480-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Ses ve Video akışları bir MP4 kapsayıcıya çoğullama</span><span class="sxs-lookup"><span data-stu-id="7d480-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="7d480-230">Bizim AVC belirli bir ses akışını kodlanmış video akışına ve bizim AAC kodlanmış, biz içine yakalamak için bir. MP4 kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="7d480-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="7d480-231">farklı akışları tek bir karıştırma işleminin hello "çoğullama" (veya "muxing") adı verilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="7d480-232">Bu durumda biz hello ses ve video akışları tek bir tutarlı hello Interleaving. MP4 paketi.</span><span class="sxs-lookup"><span data-stu-id="7d480-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="7d480-233">Bu düzenler hello bileşen bir. MP4 kapsayıcı hello ISO MPEG-4 çoğaltıcı adı verilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="7d480-234">Bir toohello Tasarımcı yüzeyine eklemek ve hem hello AVC Video Kodlayıcısı hem de hello AAC Kodlayıcı tooits girişleri bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7d480-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Bağlı MPEG4 çoğaltıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="7d480-236">*Bağlı MPEG4 çoğaltıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="7d480-237"><a id="MXF_to_MP4_writing_mp4"></a>Merhaba MP4 dosyası yazılıyor</span><span class="sxs-lookup"><span data-stu-id="7d480-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="7d480-238">Bir çıkış dosyası yazılırken hello dosya çıktısı bileşeni kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="7d480-239">Böylece çıktısını toodisk yazılmış Biz bu hello ISO MPEG-4 çoğaltıcı toohello çıktısını bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="7d480-240">toodo bunu hello kapsayıcı (MPEG-4) çıkış PIN toohello yazma giriş PIN hello dosya çıktısı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7d480-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Dosya çıktısı bağlı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="7d480-242">*Dosya çıktısı bağlı*</span><span class="sxs-lookup"><span data-stu-id="7d480-242">*Connected File Output*</span></span>

<span data-ttu-id="7d480-243">kullanılacak hello filename hello dosya özelliği tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="7d480-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="7d480-244">Bu özellik sabit kodlanmış tooa değeri verildiğinde olabilirler, ancak büyük olasılıkla bir tooset istediğiniz bir ifade üzerinden yerine.</span><span class="sxs-lookup"><span data-stu-id="7d480-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="7d480-245">toohave hello iş akışı otomatik olarak belirlemek hello çıkış dosya adı bir ifade özelliğinden, hello düğme sonraki toohello dosya adına tıklayın (sonraki toohello klasör simgesine).</span><span class="sxs-lookup"><span data-stu-id="7d480-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="7d480-246">Merhaba gelen açılır menü sonra "İfadesi"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="7d480-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="7d480-247">Bu hello ifade Düzenleyicisi çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7d480-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="7d480-248">Merhaba Düzenleyicisi Merhaba içeriğine ilk temizleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-248">Clear hello contents of hello editor first.</span></span>

![Boş ifade Düzenleyicisi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="7d480-250">*Boş ifade Düzenleyicisi*</span><span class="sxs-lookup"><span data-stu-id="7d480-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="7d480-251">Merhaba ifade Düzenleyicisi tooenter ile bir veya daha fazla değişken karma herhangi bir sabit değere izin verir.</span><span class="sxs-lookup"><span data-stu-id="7d480-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="7d480-252">Değişkenleri dolar işareti başlatın.</span><span class="sxs-lookup"><span data-stu-id="7d480-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="7d480-253">Merhaba $ tuşuna basın, hello Düzenleyicisi açılan kutusundan bir seçenek ile kullanılabilen değişkenlerin gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="7d480-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="7d480-254">Örneğimizde hello çıktı dizini değişken ve hello temel giriş dosyası adı değişkeni bileşimini kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="7d480-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![İfade Düzenleyicisi çıkışı dolu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="7d480-256">*İfade Düzenleyicisi çıkışı dolu*</span><span class="sxs-lookup"><span data-stu-id="7d480-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="7d480-257">Sırayla toosee Azure kodlama işinin bir çıktı dosyasına bakın, hello ifade Düzenleyicisi'nde bir değer sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d480-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="7d480-258">Tamam basarsa tarafından hello ifade onayladığınızda hello özellik penceresi toowhat değeri hello dosya özelliği çözümler bu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="7d480-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Çıktı dizini dosyası ifadesini çözümler](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="7d480-260">*Çıktı dizini dosyası ifadesini çözümler*</span><span class="sxs-lookup"><span data-stu-id="7d480-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="7d480-261"><a id="MXF_to_MP4_asset_from_output"></a>Bir Media Services varlık hello çıktı dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d480-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="7d480-262">Biz bir MP4 çıktı dosyası yazılmış olsa da, hala tooindicate ihtiyacımız bu dosyanın toohello ait çıktı varlık hangi media services, bu iş akışı yürütmenin sonucu olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="7d480-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="7d480-263">toothis son, hello çıktı dosyası/varlık düğümü hello iş akışı tuval üzerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="7d480-264">Bu düğüm tüm gelen dosyalarıyla hello sonuç Azure Media Services varlık parçası hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7d480-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="7d480-265">Merhaba dosya çıktısı bileşen toohello çıktı dosyası/varlık bileşeni toofinish hello iş akışı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="7d480-267">*Tamamlanmış iş akışı*</span><span class="sxs-lookup"><span data-stu-id="7d480-267">*Finished Workflow*</span></span>

### <span data-ttu-id="7d480-268"><a id="MXF_to_MP4_test"></a>İş akışı yerel olarak test hello tamamlandı</span><span class="sxs-lookup"><span data-stu-id="7d480-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="7d480-269">tootest hello iş akışı yerel olarak hello araç çubuğunda hello üstünde hello YÜRÜT düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="7d480-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="7d480-270">Merhaba iş akışı yürütme tamamlandığında, yapılandırılmış hello çıkış klasöründe oluşturulan hello çıkış inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="7d480-271">Merhaba MXF giriş kaynağı dosyasından kodlanan MP4 çıktı dosyası hello tamamlandı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7d480-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="7d480-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Dinamik paketleme etkin MP4 - multibitrate MXF kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="7d480-273">Bu kılavuzda Çoklu bit hızlı MP4 dosyaları kümesini kodlanmış AAC ile tek bir ses oluşturacağız. MXF giriş dosyası.</span><span class="sxs-lookup"><span data-stu-id="7d480-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="7d480-274">Ne zaman Çoklu bit hızlı varlık çıkış birlikte kullanmak için Azure Media Services, birden çok GOP hizalı MP4 dosyaları her farklı bit hızı ve çözüm oluşturulan toobe gerekir tarafından sunulan hello dinamik paketleme özelliklerle istendiğini.</span><span class="sxs-lookup"><span data-stu-id="7d480-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="7d480-275">Bu nedenle, toodo hello [kodlama MXF tek bit hızlı MP4 içine](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) izlenecek bize iyi bir başlangıç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![İş akışı başlatma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="7d480-277">*İş akışı başlatma*</span><span class="sxs-lookup"><span data-stu-id="7d480-277">*Starting Workflow*</span></span>

### <span data-ttu-id="7d480-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Bir veya daha fazla ek MP4 çıktı ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="7d480-279">Sonuçta elde edilen bizim Azure Media Services varlık her MP4 dosyasında farklı bit hızı ve çözüm destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="7d480-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="7d480-280">Bir veya daha fazla MP4 çıktı dosyaları toohello iş akışı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="7d480-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="7d480-281">toomake emin sahibiz bizim video Kodlayıcıları oluşturulan ile tüm Merhaba aynı ayarları, buna ait en kolay tooduplicate zaten mevcut olan AVC Video Kodlayıcısı hello ve çözünürlük ve bit hızı başka bir bileşimini yapılandırın (şimdi 960 x 540 birini sırasında saniye başına 25 çerçeveleri ekleyin 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="7d480-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="7d480-282">tooduplicate hello varolan Kodlayıcı, kopyalama yapıştırın, hello Tasarımcı yüzeyine.</span><span class="sxs-lookup"><span data-stu-id="7d480-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="7d480-283">Merhaba sıkıştırılmamış Video Çıkış PIN hello ortam dosyası girişi bizim yeni AVC bileşen içine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Bağlı ikinci AVC kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="7d480-285">*Bağlı ikinci AVC kodlayıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="7d480-286">Şimdi bizim yeni AVC Kodlayıcı toooutput 960 x 540 2,5 Mbps hızında hello yapılandırmasını uyarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="7d480-287">(Çıktı özellikleri "genişliğini", "Çıktı yükseklik" ve "Bit hızı (kbps)" Bu için kullanın.)</span><span class="sxs-lookup"><span data-stu-id="7d480-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="7d480-288">Verilen Azure Media Services dinamik paketleme ile birlikte toouse hello ortaya çıkan varlık istiyoruz, akış uç noktası hello toobe bu MP4 dosyalarını tam olarak hizalanmış tooeach bir yolla diğer olan HLS/parçalanmış MP4/DASH parçaları oluşturma yeteneği gerekiyor farklı bit arasında geçiş istemcileri tek sorunsuz bir sürekli video ve ses deneyim olduğunu alın.</span><span class="sxs-lookup"><span data-stu-id="7d480-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="7d480-289">durum, her iki AVC kodlayıcılar hello özelliklerinde hello hem MP4 dosyaları için GOP ("grubu") resimlerin boyutu ayarlamak, tooensure ihtiyacımız toomake tarafından yapılan too2 saniye:</span><span class="sxs-lookup"><span data-stu-id="7d480-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="7d480-290">Merhaba GOP boyutu modu tooFixed GOP boyutunu ayarlama ve</span><span class="sxs-lookup"><span data-stu-id="7d480-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="7d480-291">Merhaba anahtar çerçeve aralığı tootwo saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="7d480-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="7d480-292">Ayrıca hello tüm GOP's duran GOP IDR denetim tooClosed GOP tooensure olmadan kendi bağımlılıkları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7d480-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="7d480-293">toomake bizim iş akışı uygun toounderstand hello ilk AVC Kodlayıcı çok yeniden adlandırma "AVC Video Kodlayıcısı 640 x 360 1200kbps" ve ikinci AVC Kodlayıcı hello "AVC Video Kodlayıcısı 960 x 540 2500 kbps".</span><span class="sxs-lookup"><span data-stu-id="7d480-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="7d480-294">İkinci bir ISO MPEG-4 çoğaltıcı ve ikinci bir dosya çıktısı. Şimdi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="7d480-295">Merhaba çoğaltıcı toohello yeni AVC Kodlayıcı bağlanmak ve çıktısını dosya çıktısı hello yönlendirilir emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d480-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="7d480-296">Merhaba AAC ses Kodlayıcı çıkışı toohello yeni da bağlanabilirken çoğaltıcı 's giriş.</span><span class="sxs-lookup"><span data-stu-id="7d480-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="7d480-297">Merhaba dosya çıktısı sırayla sonra olabilir bağlı toohello çıktı dosyası/varlık düğümü tooadd onu toohello oluşturulacak Media Services varlık.</span><span class="sxs-lookup"><span data-stu-id="7d480-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Bağlı ikinci Karıştırıcı ve dosya çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="7d480-299">*Bağlı ikinci Karıştırıcı ve dosya çıktısı*</span><span class="sxs-lookup"><span data-stu-id="7d480-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="7d480-300">Azure Media Services dinamik paketleme ile uyumluluk için hello çoğaltıcı 's öbek modu tooGOP sayısı veya süreyi yapılandırın ve Öbek too1 başına hello GOPs ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="7d480-301">(Bu hello varsayılan olmalıdır.)</span><span class="sxs-lookup"><span data-stu-id="7d480-301">(This should be hello default.)</span></span>

![Karıştırıcı öbek modları](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="7d480-303">*Karıştırıcı öbek modları*</span><span class="sxs-lookup"><span data-stu-id="7d480-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="7d480-304">Not: Bu işlem diğer bit hızı ve toohello varlık çıktı toohave istediğiniz birleşimler eklenen çözümleme için toorepeat isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="7d480-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Yapılandırma hello dosya çıkış adları</span><span class="sxs-lookup"><span data-stu-id="7d480-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="7d480-306">Birden fazla tek dosyalı eklenen toohello çıkış varlığına sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d480-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="7d480-307">Bu, dosya adlarını her hello dosyaları birbirinden farklıdır ve belki de ile ilgilenen hello dosya adından açık olacak şekilde bile dosya adlandırma kuralını uygula çıkış gerek toomake emin bir hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="7d480-308">Çıkış dosya adlandırma hello Tasarımcısı'nda ifadeler ile denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="7d480-309">Merhaba dosya çıktısı bileşenlerden biri için Hello özelliği bölmesini açın ve hello dosya özelliği için hello ifade Düzenleyicisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="7d480-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="7d480-310">Bizim ilk çıkış dosyası ifade aşağıdaki hello yapılandırılmış (gelen gitmek için hello öğretici bkz [MXF tooa tek bit hızlı MP4 çıktı](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="7d480-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="7d480-311">Bu bizim filename iki değişken tarafından belirlenir anlamına gelir: hello çıktı dizini toowrite içinde ve hello kaynak dosya temel adı.</span><span class="sxs-lookup"><span data-stu-id="7d480-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="7d480-312">Merhaba eski hello iş akışı kök bir özellik olarak sunulur ve ikinci hello hello gelen dosyası tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="7d480-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="7d480-313">Yerel test etmek için kullanmak, hello çıktı dizini olduğuna dikkat edin; Azure Media Services hello bulut tabanlı media işlemcisi tarafından Hello iş akışı çalıştırıldığında bu özellik hello iş akışı altyapısı tarafından geçersiz kılınacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="7d480-314">Bizim çıkış adlandırma tutarlı çıktı dosyaları toogive hem, değişiklik hello ilk adlandırma ifade dosya:</span><span class="sxs-lookup"><span data-stu-id="7d480-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7d480-315">ve için ikinci hello:</span><span class="sxs-lookup"><span data-stu-id="7d480-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7d480-316">Her iki MP4 çıktı dosyaları düzgün şekilde oluşturulan emin toomake bir ara testi yürütün.</span><span class="sxs-lookup"><span data-stu-id="7d480-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="7d480-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Ayrı bir ses izi ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="7d480-318">Biz bir .ism dosyası toogo bizim MP4 çıktı dosyalarıyla oluştururken daha sonra anlatıldığı gibi biz de yalnızca ses MP4 dosyası hello ses parçası bizim Uyarlamalı akış için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d480-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="7d480-319">toocreate bu dosya, bir ek Karıştırıcı toohello iş akışı (ISO-MPEG-4 çoğaltıcı) ekleyip hello AAC Kodlayıcı'nın çıkış PIN kendi giriş PIN ile İzle 1 için bağlandığınızda.</span><span class="sxs-lookup"><span data-stu-id="7d480-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Ses karıştırıcı eklendi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="7d480-321">*Ses karıştırıcı eklendi*</span><span class="sxs-lookup"><span data-stu-id="7d480-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="7d480-322">Üçüncü bir dosya çıktısı bileşen toooutput hello giden akış hello Karıştırıcı oluşturun ve hello dosya adlandırma ifade olarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7d480-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Ses karıştırıcı dosya çıktısı oluşturma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="7d480-324">*Ses karıştırıcı dosya çıktısı oluşturma*</span><span class="sxs-lookup"><span data-stu-id="7d480-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="7d480-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Merhaba ekleniyor. ISM SMIL dosyası</span><span class="sxs-lookup"><span data-stu-id="7d480-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="7d480-326">Merhaba dinamik paketleme toowork birlikte her iki MP4 dosyaları (ve yalnızca ses MP4 hello) bizim Media Services varlık da bildirim dosyası ihtiyacımız ("SMIL" dosyası olarak da bilinir: eşitlenmiş multimedya tümleştirme dil).</span><span class="sxs-lookup"><span data-stu-id="7d480-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="7d480-327">Bu dosya, hangi MP4 dosyaları dinamik paketleme ve bu tooconsider hello ses akış için hangisinin kullanılabilir tooAzure Media Services gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d480-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="7d480-328">Kümesiyle tek bir ses akışını MP4'ın için tipik bir bildirim dosyası şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="7d480-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="7d480-329">switch deyimi içinde bir başvuru tooeach hello tek tek MP4 video dosyaları Hello .ism dosyası içerir ve ayrıca toothose ayrıca bir (veya daha fazla) ses dosyası tooan yalnızca hello ses içeren MP4 başvurur.</span><span class="sxs-lookup"><span data-stu-id="7d480-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="7d480-330">Bizim MP4'ın kümesi oluşturma hello bildirim dosyası hello "AMS bildirim Yazan" adında bir bileşen ile yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="7d480-331">toouse, hello yüzeyine sürükleyin ve hello "Yazma tamamlandı" çıktı pini hello üç dosya çıktısı bileşenleri toohello AMS bildirim giriş yazan bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7d480-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="7d480-332">Ardından hello AMS bildirim yazan toohello çıktı dosyası/varlık emin tooconnect hello çıkışını yapın.</span><span class="sxs-lookup"><span data-stu-id="7d480-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="7d480-333">Bizim diğer bileşenlerle dosya çıktı olarak, hello .ism dosyası çıktı adı bir ifade ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7d480-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="7d480-334">Bizim tamamlanmış iş akışı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="7d480-334">Our finished workflow looks like hello below:</span></span>

![Tamamlanmış MXF toomultibitrate MP4 akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="7d480-336">*Tamamlanmış MXF toomultibitrate MP4 akışı*</span><span class="sxs-lookup"><span data-stu-id="7d480-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="7d480-337"><a id="MXF_to__multibitrate_MP4"></a>MP4 - Gelişmiş şeması multibitrate MXF kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="7d480-338">Merhaba, [önceki iş akışı Kılavuzu](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) nasıl tek bir MXF giriş varlık bir çıktı varlığa Çoklu bit hızlı MP4 dosyaları, bir yalnızca ses MP4 dosyası ve Azure medya ile birlikte kullanmak için bir bildirim dosyası ile dönüştürülebilir gördük Dinamik paketleme Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="7d480-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="7d480-339">Bu kılavuzda nasıl bazı hello yönlerinden geliştirilebilen ve daha kullanışlı hale gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d480-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="7d480-340"><a id="MXF_to_multibitrate_MP4_overview"></a>İş akışı genel bakış tooenhance</span><span class="sxs-lookup"><span data-stu-id="7d480-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 akışı tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="7d480-342">*Multibitrate MP4 akışı tooenhance*</span><span class="sxs-lookup"><span data-stu-id="7d480-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="7d480-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Dosya adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="7d480-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="7d480-344">Hello önceki iş akışında hello temel çıktı dosyası adları oluşturmak için basit bir ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="7d480-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="7d480-345">Bazı çoğaltma yine de sunuyoruz: hello hello tek tek çıktı dosyası bileşenlerinin tümünü böyle ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="7d480-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="7d480-346">Örneğin, bizim dosya çıktı bileşen hello ilk video dosyası için bu ifade ile yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="7d480-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7d480-347">Merhaba ikinci çıktı için sırada video, biz gibi bir ifadeye sahip:</span><span class="sxs-lookup"><span data-stu-id="7d480-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7d480-348">Hata daha az yatkın ve biz Bu çoğaltma bazılarını kaldırın ve şeyleri daha yapılandırılabilir yerine yaparsanız daha kullanışlı temizleyici olmaz mıydı?</span><span class="sxs-lookup"><span data-stu-id="7d480-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="7d480-349">Luckily geçebiliriz: hello tasarımcının ifade özellikleri hello özelliği toocreate özel özellikler bizim iş akışı kök ile birlikte, kolaylık eklenen bir katmanı bize verir.</span><span class="sxs-lookup"><span data-stu-id="7d480-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="7d480-350">Biz filename yapılandırma hello tek tek MP4 dosyaları hello bit sürücü varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d480-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="7d480-351">Bir orta tooconfigure hedeflenir bu bit burada erişilen tooconfigure ve sürücü dosya adı oluşturma olacak gelen (Merhaba kökünde bizim grafiği) yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7d480-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="7d480-352">toodo bunu hello AVC kodlayıcılar hem de her iki hello kökünden erişilebilir hale hello bit hızı bizim iş akışı, her iki AVC kodlayıcılar toohello kökündeki özelliğinden yayımlayarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="7d480-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="7d480-353">(İki farklı noktayı kaçırmadığınızdan görüntülenen olsa bile, yalnızca bir temel alınan değer yoktur.)</span><span class="sxs-lookup"><span data-stu-id="7d480-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="7d480-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Yayımlama hello iş akışı kök üzerine bileşeni özellikleri</span><span class="sxs-lookup"><span data-stu-id="7d480-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="7d480-355">Merhaba ilk AVC Kodlayıcı açın, toohello bit hızı (kbps) özelliği gidin ve yayımlama hello aşağı açılır listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="7d480-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Yayımlama hello bit hızı özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="7d480-357">*Yayımlama hello bit hızı özelliği*</span><span class="sxs-lookup"><span data-stu-id="7d480-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="7d480-358">Merhaba yapılandırma Itanium tabanlı sistemler için iletişim toopublish toohello kök bizim iş akışı grafiğinin yayımlanan adını "video1bitrate" ve "Video 1 bit hızı" okunabilir görünen adını ile yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="7d480-359">Özel bir yapılandırma grup adı "Bit akış" olarak adlandırılan ve yayımlama basın.</span><span class="sxs-lookup"><span data-stu-id="7d480-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Yayımlama hello bit hızı özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="7d480-361">*Bit hızı özelliği için yayımlama iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7d480-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="7d480-362">Yineleme hello hello hello bit hızı özelliği için aynı ikinci AVC Kodlayıcı ve "Video 2 bit hızı" ile bir görünen ad "video2bitrate" adı, hello özel aynı "Akış bit" Grup.</span><span class="sxs-lookup"><span data-stu-id="7d480-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="7d480-363">Biz şimdi hello iş akışı kök özelliklerini inceleme, iki yayımlanan özellikleri görünmesini hello özel bizim grubuyla göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="7d480-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="7d480-364">Her ikisi de kendi ilgili AVC Kodlayıcı hızı hello değerini yansıtma.</span><span class="sxs-lookup"><span data-stu-id="7d480-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![İş akışı kök yayımlanan bit hızı özellik](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="7d480-366">Tooaccess bu özellikleri kodu veya bir ifade istediğinizde biz bunu şu şekilde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d480-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="7d480-367">Satır içi kodundan hemen hello kökü altındaki bir bileşenin: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="7d480-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="7d480-368">bir ifade içinde: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="7d480-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="7d480-369">Şimdi de bizim ses izleme hızı üzerindeki yayımlayarak hello "Akış bit" grubu tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="7d480-370">Merhaba AAC Kodlayıcı hello özellikleri içinde hello bit hızı ayarı arayın ve yayımlama hello açılır sonraki tooit seçin.</span><span class="sxs-lookup"><span data-stu-id="7d480-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="7d480-371">Yayımlama hello grafik adı "audio1bitrate" ile toohello kökündeki ve görünen ad "Ses 1 bit hızı" bizim özel gruptaki "Akış bit".</span><span class="sxs-lookup"><span data-stu-id="7d480-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Ses bit hızı için yayımlama iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="7d480-373">*Ses bit hızı için yayımlama iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7d480-373">*Publishing dialog for audio bitrate*</span></span>

![Sonuçta elde edilen video ve ses özellik kök](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="7d480-375">*Sonuçta elde edilen video ve ses özellik kök*</span><span class="sxs-lookup"><span data-stu-id="7d480-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="7d480-376">Bu üç hiçbirini değiştirme değerleri de yeniden yapılandırır ve değişiklikleri hello bunlar bağlı ile Merhaba ilgili bileşenler değerlerine unutmayın (ve bir yayımlandığı yerlerde).</span><span class="sxs-lookup"><span data-stu-id="7d480-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="7d480-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Çıktı dosyası adları yayımlanan özellik değerlerine dayanan oluşturulmasını</span><span class="sxs-lookup"><span data-stu-id="7d480-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="7d480-378">Cmdlet'e kod yerine bizim oluşturulan dosya adları, biz şimdi bizim filename ifade her hello dosya çıktısı bileşenleri toorely biz yalnızca hello grafik kökünde yayımlanan hello bit hızı özellikleri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="7d480-379">Bizim ilk dosya çıktı ile başlayarak, hello dosya özelliğini bulun ve bu gibi hello ifadeyi düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="7d480-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="7d480-380">Bu ifadede Hello farklı parametreler erişilen ve hello dolar işareti penceresinde hello ifade ederken hello klavyede basarsa tarafından girdiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="7d480-381">Merhaba kullanılabilir parametrelerden biri, daha önce yayımlanan bizim video1bitrate özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7d480-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Bir ifade içinde Parametreler erişme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="7d480-383">*Bir ifade içinde Parametreler erişme*</span><span class="sxs-lookup"><span data-stu-id="7d480-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="7d480-384">Bizim ikinci video hello dosyası çıktısı için aynı hello:</span><span class="sxs-lookup"><span data-stu-id="7d480-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="7d480-385">ve hello salt ses dosyası çıktısı için:</span><span class="sxs-lookup"><span data-stu-id="7d480-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="7d480-386">Biz şimdi hello bit hızı herhangi hello video veya ses dosyalarını değiştirirseniz, hello ilgili Kodlayıcı yeniden yapılandırılması ve hello bit hızı tabanlı bir dosya adı kuralı tüm otomatik olarak kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="7d480-387"><a id="thumbnails_to__multibitrate_MP4"></a>Küçük resimleri toomultibitrate MP4 çıktı ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="7d480-388">Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi küçük resimleri toohello çıkış ekleme içine arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="7d480-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>İş akışı genel bakış tooadd küçük resim</span><span class="sxs-lookup"><span data-stu-id="7d480-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Gelen Multibitrate MP4 akışı toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="7d480-391">*Gelen Multibitrate MP4 akışı toostart*</span><span class="sxs-lookup"><span data-stu-id="7d480-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="7d480-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>JPG kodlama ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="7d480-393">Bizim küçük resim oluşturma Hello Kalp hello JPG Kodlayıcı bileşeni mümkün toooutput JPG dosyaları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![JPG kodlayıcı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="7d480-395">*JPG kodlayıcı*</span><span class="sxs-lookup"><span data-stu-id="7d480-395">*JPG Encoder*</span></span>

<span data-ttu-id="7d480-396">Ancak doğrudan sunduğumuz sıkıştırılmamış Video akışı hello ortam dosyası girişi hello JPG Kodlayıcı içine gelen bağlanamıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d480-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="7d480-397">Bunun yerine, tek tek çerçeveler toobe karmalayan bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7d480-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="7d480-398">Bu, hello Video çerçeve kapısı bileşen ile yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="7d480-398">This, we can do through hello Video Frame Gate component.</span></span>

![Bir çerçeve kapısı toohello JPG Kodlayıcısı bağlanma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="7d480-400">*Bir çerçeve kapısı toohello JPG Kodlayıcısı bağlanma*</span><span class="sxs-lookup"><span data-stu-id="7d480-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="7d480-401">Her çok fazla sayıda saniye veya çerçeveler olanak sağlayan bir kez video çerçeve toopass hello çerçeve kapısı.</span><span class="sxs-lookup"><span data-stu-id="7d480-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="7d480-402">hangi böyle ile uzaklığı hello aralığı ve hello hello özelliklerinde yapılandırılabilir saattir.</span><span class="sxs-lookup"><span data-stu-id="7d480-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Video çerçeve kapısı özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="7d480-404">*Video çerçeve kapısı özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="7d480-405">Şimdi hello modu tooTime (saniye) ayarlayarak dakikada küçük resim oluşturma ve aralığı too60 hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="7d480-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Renk alanını dönüştürme postalarla</span><span class="sxs-lookup"><span data-stu-id="7d480-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="7d480-407">Mantıksal göründüğü sırada hem sıkıştırılmamış Video PIN'ler hello çerçeve kapısı ve hello ortam dosyası girişi şimdi bağlanabilir, biz bunu yapmayı tercih ediyorsanız bir uyarı almak.</span><span class="sxs-lookup"><span data-stu-id="7d480-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Giriş rengi alan hatası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="7d480-409">*Giriş rengi alan hatası*</span><span class="sxs-lookup"><span data-stu-id="7d480-409">*Input color space error*</span></span>

<span data-ttu-id="7d480-410">Hangi renkli bilgileri bizim özgün ham sıkıştırılmamış video akışında, bizim MXF gelen temsil edilen hello şekilde JPG Kodlayıcı bekleniyor hangi hello farklı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="7d480-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="7d480-411">Özellikle, bir sözde "renk aralığı" "RGB" veya "Gri" olduğundan daha fazla beklenen tooflow içinde.</span><span class="sxs-lookup"><span data-stu-id="7d480-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="7d480-412">Başka bir deyişle, bu hello Video çerçeve ağ geçidi'nin gelen video akışına toohave kendi renk alanını önce uygulanan bir dönüştürme gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d480-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="7d480-413">Merhaba iş akışı hello renk alanı Dönüştürücüsü - Intel sürükleyin ve tooour çerçeve kapısı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Bir renk alanı Dönüştürücüsü bağlanma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="7d480-415">*Bir renk alanı Dönüştürücüsü bağlanma*</span><span class="sxs-lookup"><span data-stu-id="7d480-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="7d480-416">Merhaba Özellikler penceresinde hello BGR 24 girişi hello hazır listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="7d480-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="7d480-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Yazma hello küçük resimleri</span><span class="sxs-lookup"><span data-stu-id="7d480-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="7d480-418">Bizim MP4 video farklıdır, bir dosyada birden çok JPG bileşen çıkış Kodlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="7d480-419">Bu sipariş toodeal içinde Sahne arama JPG dosya yazıcısı bileşeni kullanılabilir: hello gelen JPG küçük resimleri ele ve bunları çıkışı, farklı bir sayı sonekine her dosya yazar.</span><span class="sxs-lookup"><span data-stu-id="7d480-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="7d480-420">(genellikle hello sayısını saniye/birimleri gelen hangi hello küçük çizilmiş hello akışında belirten hello sayı.)</span><span class="sxs-lookup"><span data-stu-id="7d480-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Merhaba Sahne arama JPG dosyası yazan Tanıtımı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="7d480-422">*Merhaba Sahne arama JPG dosyası yazan Tanıtımı*</span><span class="sxs-lookup"><span data-stu-id="7d480-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="7d480-423">Merhaba ifadesiyle Hello çıkış klasörü yolu özelliğini yapılandırın: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="7d480-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="7d480-424">ve dosya adı önekini özelliğiyle hello:</span><span class="sxs-lookup"><span data-stu-id="7d480-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="7d480-425">Merhaba önek hello küçük resim dosyaları nasıl adlı belirler.</span><span class="sxs-lookup"><span data-stu-id="7d480-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="7d480-426">Bunlar bir numara belirten hello parmak uzakta konum hello akışında sonekine.</span><span class="sxs-lookup"><span data-stu-id="7d480-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Sahne arama JPG dosya yazıcı özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="7d480-428">*Sahne arama JPG dosya yazıcı özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="7d480-429">Merhaba Sahne arama JPG dosyası yazan toohello çıktı dosyası/varlık düğüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="7d480-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Bir iş akışında hataları algılama</span><span class="sxs-lookup"><span data-stu-id="7d480-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="7d480-431">Hello girişi hello renk alanı dönüştürücü toohello ham sıkıştırılmamış video çıkışına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="7d480-432">Şimdi hello iş akışı için yerel testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7d480-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="7d480-433">Olasılığı hello iş akışı aniden yürütme durdurmak ve kırmızı bir hatayla karşılaştı hello bileşen çerçevesinde ile belirtin:</span><span class="sxs-lookup"><span data-stu-id="7d480-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Renk alanı dönüştürücü hatası](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="7d480-435">*Renk alanı dönüştürücü hatası*</span><span class="sxs-lookup"><span data-stu-id="7d480-435">*Color Space Converter error*</span></span>

<span data-ttu-id="7d480-436">Merhaba kodlama girişimi başarısız oldu hello nedeni nedir hello sağ üst köşesinde hello renk alanı dönüştürücü bileşen toosee Hello biraz kırmızı "E" simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Renk alanı dönüştürücü hata iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="7d480-438">*Renk alanı dönüştürücü hata iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7d480-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="7d480-439">Gördüğünüz gibi hello gelen renk alanını hello renk alanı dönüştürücü için standart toobe rec601 YUV tooRGB istenen bizim dönüştürülmesi için sahip olduğundan, etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="7d480-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="7d480-440">Görünüşe göre bizim akışı onun rec601 göstermez.</span><span class="sxs-lookup"><span data-stu-id="7d480-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="7d480-441">(Rec 601 aralıklı analog video sinyalleri dijital video formunda kodlama standardıdır.</span><span class="sxs-lookup"><span data-stu-id="7d480-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="7d480-442">720 aydınlatma örnekleri ve her satırda 360 chrominance örnekleri kapsayan etkin bir bölge belirtir.</span><span class="sxs-lookup"><span data-stu-id="7d480-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="7d480-443">Sistem kodlama hello renk YCbCr 4 bilinir: 2:2.)</span><span class="sxs-lookup"><span data-stu-id="7d480-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="7d480-444">toofix Bu, biz rec601 içerikle ilgilenme bizim akış hello meta verileri üzerinde belirtmek.</span><span class="sxs-lookup"><span data-stu-id="7d480-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="7d480-445">Biz bizim ham kaynak ve hello renk alanı dönüştürme bileşeni Between gireceğiniz bir Video veri türü güncelleştirici bileşeni kullanacağız şekilde toodo.</span><span class="sxs-lookup"><span data-stu-id="7d480-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="7d480-446">Bu veri türü güncelleştirici hello el ile belirli bir video verileri güncelleştirmesi türü özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="7d480-447">Bir renk alanı standart "Rec 601", tooindicate yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="7d480-448">Henüz tanımlanmış hiçbir renk alanını ise bu hello "Rec 601" renk alanını ile Merhaba Video veri türü güncelleştirici tootag hello akış neden olur.</span><span class="sxs-lookup"><span data-stu-id="7d480-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="7d480-449">(Merhaba geçersiz kılma onay kutusu işaretli değilse, var olan tüm meta veriler geçersiz kılmaz.)</span><span class="sxs-lookup"><span data-stu-id="7d480-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Renk alanı standart veri türü güncelleştirici hello üzerinde güncelleştirme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="7d480-451">*Renk alanı standart veri türü güncelleştirici hello üzerinde güncelleştirme*</span><span class="sxs-lookup"><span data-stu-id="7d480-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="7d480-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Tamamlanmış iş akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="7d480-453">Şimdi bizim bizim iş akışı tamamlandı, onu başka bir test çalışması toosee yapın.</span><span class="sxs-lookup"><span data-stu-id="7d480-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Küçük resimler ile çoklu mp4 çıktı için tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="7d480-455">*Küçük resimler ile çoklu mp4 çıktı için tamamlanmış iş akışı*</span><span class="sxs-lookup"><span data-stu-id="7d480-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="7d480-456"><a id="time_based_trim"></a>Zamana bağlı kırpma multibitrate MP4 çıktı</span><span class="sxs-lookup"><span data-stu-id="7d480-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7d480-457">Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi zaman damgalarını temel hello kaynak görüntü kırpma içine arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="7d480-458"><a id="time_based_trim_start"></a>İş akışı genel bakış toostart kırpma için ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Başlangıç iş akışı tooadd kırpma](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="7d480-460">*Başlangıç iş akışı tooadd kırpma*</span><span class="sxs-lookup"><span data-stu-id="7d480-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="7d480-461"><a id="time_based_trim_use_stream_trimmer"></a>Merhaba akış Kırpıcıyı kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="7d480-462">Merhaba akış Kırpıcıyı bileşeni tootrim hello başlangıç ve bitiş Giriş akışı, zamanlama bilgileri (saniye, dakika,...) temel sağlar. Merhaba Kırpıcıyı tabanlı çerçeve kırpma desteklemez.</span><span class="sxs-lookup"><span data-stu-id="7d480-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Akış Ayarlayıcısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="7d480-464">*Akış Ayarlayıcısı*</span><span class="sxs-lookup"><span data-stu-id="7d480-464">*Stream Trimmer*</span></span>

<span data-ttu-id="7d480-465">Merhaba AVC Kodlayıcıları ve Konuşmacı konumu assigner toohello ortam dosyası girişi doğrudan bağlama yerine, bu hello akış Kırpıcıyı Between gireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="7d480-466">(Bir hello video sinyali ve bir araya eklemeli ses sinyal hello.)</span><span class="sxs-lookup"><span data-stu-id="7d480-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Akış Kırpıcıyı arasında yerleştirme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="7d480-468">*Akış Kırpıcıyı arasında yerleştirme*</span><span class="sxs-lookup"><span data-stu-id="7d480-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="7d480-469">Şimdi biz yalnızca video ve ses 15 saniye ile Merhaba videoda 60 saniye arasında işleyecek şekilde hello Kırpıcıyı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="7d480-470">Merhaba Video akışı Kırpıcıyı toohello özelliklerine gidin ve başlangıç saati (15 sn) ve bitiş zamanı (60s) özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="7d480-471">hem bizim ses ve video Kırpıcıyı her zaman aynı başlangıç ve değerleri bitiş yapılandırılmış toohello emin toomake, biz bu toohello kök hello iş akışının yayımlar.</span><span class="sxs-lookup"><span data-stu-id="7d480-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Başlangıç saati akış Kırpıcıyı özelliğinden yayımlama](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="7d480-473">*Başlangıç saati akış Kırpıcıyı özelliğinden yayımlama*</span><span class="sxs-lookup"><span data-stu-id="7d480-473">*Publish start time property from Stream Trimmer*</span></span>

![Yayımlama özelliği iletişim kutusu için başlangıç saati](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="7d480-475">*Yayımlama özelliği iletişim kutusu için başlangıç saati*</span><span class="sxs-lookup"><span data-stu-id="7d480-475">*Publish property dialog for start time*</span></span>

![Bitiş saati Yayımlama özelliği iletişim kutusu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="7d480-477">*Bitiş saati Yayımlama özelliği iletişim kutusu*</span><span class="sxs-lookup"><span data-stu-id="7d480-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="7d480-478">Biz hello kökü verdiğimiz bir iş akışı şimdi inceleyin, her iki özellik düzgün görüntülenen ve yapılandırılabilir buradan olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Kök kullanılabilen yayımlanan Özellikler](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="7d480-480">*Kök kullanılabilen yayımlanan Özellikler*</span><span class="sxs-lookup"><span data-stu-id="7d480-480">*Published properties available on root*</span></span>

<span data-ttu-id="7d480-481">Şimdi hello ses Kırpıcıyı hello kırpma özelliklerini açın ve toohello başvuran bir ifadeyle başlangıç ve bitiş zamanları yapılandırın hello kökü verdiğimiz bir iş akışı özellikleri yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="7d480-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="7d480-482">Merhaba ses kırpma başlangıç zamanı:</span><span class="sxs-lookup"><span data-stu-id="7d480-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="7d480-483">ve bitiş saati:</span><span class="sxs-lookup"><span data-stu-id="7d480-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="7d480-484"><a id="time_based_trim_finish"></a>Tamamlanmış iş akışı</span><span class="sxs-lookup"><span data-stu-id="7d480-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Tamamlanmış iş akışı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="7d480-486">*Tamamlanmış iş akışı*</span><span class="sxs-lookup"><span data-stu-id="7d480-486">*Finished Workflow*</span></span>

## <span data-ttu-id="7d480-487"><a id="scripting"></a>Merhaba Script bileşeni Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="7d480-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="7d480-488">Komut dosyası bileşenleri hello yürütme aşamaları bizim iş akışı sırasında rastgele komut dosyaları yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="7d480-489">Çalıştırılabilir, dört farklı betikleri vardır her birinin belirli özelliklere ve kendi yerinde hello iş akışı yaşam döngüsü:</span><span class="sxs-lookup"><span data-stu-id="7d480-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="7d480-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="7d480-490">**commandScript**</span></span>
* <span data-ttu-id="7d480-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="7d480-491">**realizeScript**</span></span>
* <span data-ttu-id="7d480-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="7d480-492">**processInputScript**</span></span>
* <span data-ttu-id="7d480-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="7d480-493">**lifeCycleScript**</span></span>

<span data-ttu-id="7d480-494">Merhaba Hello belgelerine komut dosyasıyla bileşen daha ayrıntılı olarak her hello yukarıdaki gider.</span><span class="sxs-lookup"><span data-stu-id="7d480-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="7d480-495">İçinde [hello bölümde](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** komut dosyası bileşenidir hello iş akışı başlatıldığında kullanılan tooconstruct cliplist xml hello kolay bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="7d480-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="7d480-496">Bu komut, yalnızca bir kez kaydının çevriminin olur hello Bileşen Kurulumu sırasında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="7d480-497"><a id="scripting_hello_world"></a>Bir iş akışı içinde komut dosyası: Merhaba Dünya</span><span class="sxs-lookup"><span data-stu-id="7d480-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="7d480-498">Bir komut dosyasıyla bileşenini hello Tasarımcı yüzeyine sürükleyin ve bunu (örneğin, "SetClipListXML") yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Bir komut dosyası bileşeni ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7d480-500">*Bir komut dosyası bileşeni ekleme*</span><span class="sxs-lookup"><span data-stu-id="7d480-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7d480-501">Merhaba özelliklerini incelediğinizde, komut dosyasıyla bileşen, dört farklı komut türlerine gösterilen Merhaba, her yapılandırılabilir tooa farklı komut dosyası hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Komut dosyası bileşeni özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7d480-503">*Komut dosyası bileşeni özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-503">*Scripted Component properties*</span></span>

<span data-ttu-id="7d480-504">Temizle processInputScript hello ve hello realizeScript için hello Düzenleyicisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="7d480-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="7d480-505">Şimdi biz kurduktan ve toostart scripting hazır.</span><span class="sxs-lookup"><span data-stu-id="7d480-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="7d480-506">Komut dosyaları Groovy, Java ile uyumluluk korur hello Java platform için dinamik olarak derlenmiş bir komut dosyası dili yazılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="7d480-507">Aslında, çoğu Java kodu geçerli Modaya uygun koddur.</span><span class="sxs-lookup"><span data-stu-id="7d480-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="7d480-508">Basit hello world Modaya uygun betik hello bizim realizeScript bağlamında yazalım.</span><span class="sxs-lookup"><span data-stu-id="7d480-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="7d480-509">Merhaba Düzenleyicisi'nde Hello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="7d480-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="7d480-510">Şimdi yerel test çalışması yürütün.</span><span class="sxs-lookup"><span data-stu-id="7d480-510">Now execute a local test run.</span></span> <span data-ttu-id="7d480-511">Bu çalışma sonrasında inceleyin (Merhaba Sistem sekmesinde aracılığıyla Script bileşeni hello) günlükleri özelliği hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Hello world günlük çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="7d480-513">*Hello world günlük çıktısı*</span><span class="sxs-lookup"><span data-stu-id="7d480-513">*Hello world log output*</span></span>

<span data-ttu-id="7d480-514">Merhaba günlük yöntemi, diyoruz hello düğüm nesnesi tooour geçerli "düğümü" ya da hello bileşen biz içindeki komut dosyası anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="7d480-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="7d480-515">Her bileşen şekilde hello özelliği toooutput günlük verileri hello sistem sekmesi kullanılabilir sahiptir. Bu durumda, hello dize sabit değeri "hello world" çıktı.</span><span class="sxs-lookup"><span data-stu-id="7d480-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="7d480-516">Bu, hangi hello komut gerçekte yapmakta olduğu hakkında bilgi sağlayan çok hata ayıklama aracı toobe kanıtlayabilirsiniz burada önemli toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="7d480-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="7d480-517">Komut dosyası ortamımızda içinde biz de erişim tooproperties diğer bileşenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="7d480-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="7d480-518">Şunu deneyin:</span><span class="sxs-lookup"><span data-stu-id="7d480-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="7d480-519">Bizim günlük penceresinde bize aşağıdaki hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="7d480-519">Our log window will show us hello following:</span></span>

![Düğüm yollarını erişmek için bir günlük çıktısı](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="7d480-521">*Düğüm yollarını erişmek için bir günlük çıktısı*</span><span class="sxs-lookup"><span data-stu-id="7d480-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="7d480-522"><a id="frame_based_trim"></a>Çerçeve tabanlı kırpma multibitrate MP4 çıktı</span><span class="sxs-lookup"><span data-stu-id="7d480-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7d480-523">Üreten bir iş akışından başlangıç [giriş MXF multibitrate MP4 çıktısını](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), biz şimdi çerçeve sayar dayalı hello kaynak görüntü kırpma içine arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d480-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="7d480-524"><a id="frame_based_trim_start"></a>Genel Bakış toostart kırpma için ekleme şeması</span><span class="sxs-lookup"><span data-stu-id="7d480-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![İş akışı toostart kırpma için ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="7d480-526">*İş akışı toostart kırpma için ekleme*</span><span class="sxs-lookup"><span data-stu-id="7d480-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="7d480-527"><a id="frame_based_trim_clip_list"></a>Merhaba küçük liste XML kullanma</span><span class="sxs-lookup"><span data-stu-id="7d480-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="7d480-528">Tüm önceki iş akışı eğitimlerine bizim video giriş kaynağı olarak hello medya dosyası giriş bileşen kullandık.</span><span class="sxs-lookup"><span data-stu-id="7d480-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="7d480-529">Bu belirli bir senaryo için yine de biz hello küçük listesi kaynak bileşen yerine kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7d480-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="7d480-530">Bu çalışma tercih edilen hello yolu olmamalıdır unutmayın; olduğunda gerçek neden toodo şekilde hello küçük kaynak listesi yalnızca kullanın (burada yapmadan talebi aşağıda hello de olduğu gibi hello küçük listesi kırpma özelliklerinin kullanılmasına).</span><span class="sxs-lookup"><span data-stu-id="7d480-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="7d480-531">Bizim ortam dosyası girişi toohello küçük listesi kaynak gelen tooswitch hello küçük listesi kaynak bileşen hello tasarım yüzeyine sürükleyin ve hello küçük listesi XML PIN toohello küçük liste XML düğümü hello iş akışı Tasarımcısı'nın bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="7d480-532">Bu hello küçük listesi kaynak tooour giriş video göre çıkış PIN ile doldurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d480-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="7d480-533">Şimdi hello sıkıştırılmamış Video ve sıkıştırılmamış ses PIN'ler hello hello küçük listesi kaynak toohello Bağlan ilgili AVC Kodlayıcıları ve ses akışı ayırıcı.</span><span class="sxs-lookup"><span data-stu-id="7d480-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="7d480-534">Şimdi hello ortam dosyası girişi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7d480-534">Now remove hello Media File Input.</span></span>

![Merhaba ortam dosyası girişi hello küçük kaynak listesi ile değiştirilir](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="7d480-536">*Merhaba ortam dosyası girişi hello küçük kaynak listesi ile değiştirilir*</span><span class="sxs-lookup"><span data-stu-id="7d480-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="7d480-537">Merhaba küçük listesi kaynak bileşen "Küçük listesi XML" kendi giriş olarak alır.</span><span class="sxs-lookup"><span data-stu-id="7d480-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="7d480-538">Merhaba kaynak dosya tootest ile yerel olarak seçerken bu küçük resim listesi xml otomatik-sizin için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="7d480-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Otomatik olarak doldurulmuş küçük listesi XML özelliği](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="7d480-540">*Otomatik olarak doldurulmuş küçük listesi XML özelliği*</span><span class="sxs-lookup"><span data-stu-id="7d480-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="7d480-541">Biraz daha yakından toohello xml baktığınızda, bu nasıl gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="7d480-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Küçük resim listesi iletişim kutusunda Düzenle](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="7d480-543">*Küçük resim listesi iletişim kutusunda Düzenle*</span><span class="sxs-lookup"><span data-stu-id="7d480-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="7d480-544">Bu hello küçük liste xml hello yeteneklerini ancak yansıtmaz.</span><span class="sxs-lookup"><span data-stu-id="7d480-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="7d480-545">Bir seçenek sahibiz tooadd "Kırpma" öğesinin hello video ve ses kaynağı, böyle altında verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7d480-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Kırpma öğe toohello küçük listesi ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="7d480-547">*Kırpma öğe toohello küçük listesi ekleme*</span><span class="sxs-lookup"><span data-stu-id="7d480-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="7d480-548">Merhaba küçük liste xml bu gibi değiştirin ve yerel testi gerçekleştirmek, hello video görürsünüz doğru edilmiş hello videoda 10 ile 20 saniye arasında kırpılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="7d480-549">Bu çok aynı cliplist xml, aynı Azure Media Services çalıştıran bir iş akışında uygulandığında efekt hello sahip değil de, yerel çalıştırma yaptığınızda bulmadýðýný toowhat olur.</span><span class="sxs-lookup"><span data-stu-id="7d480-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="7d480-550">Azure Premium Kodlayıcı başlatır, hello cliplist xml oluşturulduğu zaman yeniden hello giriş dosyası hello kodlama dayalı her zaman iş verildi.</span><span class="sxs-lookup"><span data-stu-id="7d480-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="7d480-551">Bu, biz hello xml yapmak herhangi bir değişiklik ne yazık ki geçersiz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d480-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="7d480-552">bir kodlama iş başlatıldığında silmeden toocounter hello cliplist xml biz bunu hello anında yalnızca bizim iş akışının hello başladıktan sonra yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="7d480-553">Bu tür özel eylemler bir "komut dosyası Component" adlı aracılığıyla alınabilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="7d480-554">Daha fazla bilgi için bkz: [Introducing hello Script bileşeni](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="7d480-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="7d480-555">Bir komut dosyasıyla bileşenini hello Tasarımcı yüzeyine sürükleyin ve çok yeniden adlandırma "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="7d480-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Bir komut dosyası bileşeni ekleme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7d480-557">*Bir komut dosyası bileşeni ekleme*</span><span class="sxs-lookup"><span data-stu-id="7d480-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7d480-558">Merhaba özelliklerini incelediğinizde, komut dosyasıyla bileşen, dört farklı komut türlerine gösterilen Merhaba, her yapılandırılabilir tooa farklı komut dosyası hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Komut dosyası bileşeni özellikleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7d480-560">*Komut dosyası bileşeni özellikleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="7d480-561"><a id="frame_based_trim_modify_clip_list"></a>Komut dosyası bir bileşenin Hello küçük listesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="7d480-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="7d480-562">İş akışı başlatma sırasında oluşturulan hello cliplist xml yeniden yazma önce biz toohave erişim toohello cliplist xml özellik ve içeriğini gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d480-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="7d480-563">Biz bunu şu şekilde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d480-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Günlüğe kaydedilmesini gelen küçük resim listesi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="7d480-565">*Günlüğe kaydedilmesini gelen küçük resim listesi*</span><span class="sxs-lookup"><span data-stu-id="7d480-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="7d480-566">Bir şekilde toodetermine ilk ihtiyacımız olan noktasını istiyoruz tootrim hangi noktasından video hello.</span><span class="sxs-lookup"><span data-stu-id="7d480-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="7d480-567">Bu kullanışlı toohello daha az teknik kullanıcı hello akışının toomake yayımlama hello grafiğinin iki özellik toohello kök.</span><span class="sxs-lookup"><span data-stu-id="7d480-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="7d480-568">toodo bunu hello Tasarımcı yüzeyine sağ tıklatın ve "Özellik Ekle" seçin:</span><span class="sxs-lookup"><span data-stu-id="7d480-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="7d480-569">İlk özellik: türü "ClippingTimeStart": "zaman kodu"</span><span class="sxs-lookup"><span data-stu-id="7d480-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="7d480-570">İkinci özelliği: türü "ClippingTimeEnd": "zaman kodu"</span><span class="sxs-lookup"><span data-stu-id="7d480-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Özellik iletişim için kırpma başlangıç saati ekleyin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="7d480-572">*Özellik iletişim için kırpma başlangıç saati ekleyin*</span><span class="sxs-lookup"><span data-stu-id="7d480-572">*Add Property dialog for clipping start time*</span></span>

![İş akışı kökünde zaman özellik kırpma yayımlanan](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="7d480-574">*İş akışı kökünde zaman özellik kırpma yayımlanan*</span><span class="sxs-lookup"><span data-stu-id="7d480-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="7d480-575">Her iki özellikleri tooa uygun değeri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7d480-575">Configure both properties tooa suitable value:</span></span>

![Başlangıç ve bitiş özellikleri kırpma hello yapılandırın](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="7d480-577">*Başlangıç ve bitiş özellikleri kırpma hello yapılandırın*</span><span class="sxs-lookup"><span data-stu-id="7d480-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="7d480-578">Şimdi, bizim komut dosyası içinden Biz bu gibi her iki özellik erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d480-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Başlangıç ve bitiş kırpma, gösteren Günlüğü penceresi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="7d480-580">*Başlangıç ve bitiş kırpma, gösteren Günlüğü penceresi*</span><span class="sxs-lookup"><span data-stu-id="7d480-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="7d480-581">Şimdi hello zaman kodu dizeleri basit bir normal ifade kullanarak daha kullanışlı toouse forma, ayrıştırılamıyor:</span><span class="sxs-lookup"><span data-stu-id="7d480-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Ayrıştırılmış zaman kodu çıkış Günlüğü penceresi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="7d480-583">*Ayrıştırılmış zaman kodu çıkış Günlüğü penceresi*</span><span class="sxs-lookup"><span data-stu-id="7d480-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="7d480-584">Bu bilgilerle elinizdeki, biz şimdi hello cliplist xml tooreflect hello başlangıç değiştirebilir ve bitiş zamanları hello için çerçeve doğru kırpma hello film, istenen.</span><span class="sxs-lookup"><span data-stu-id="7d480-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Komut dosyası kod tooadd kırpma öğeleri](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="7d480-586">*Komut dosyası kod tooadd kırpma öğeleri*</span><span class="sxs-lookup"><span data-stu-id="7d480-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="7d480-587">Bu normal dize düzenleme işlemleri gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7d480-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="7d480-588">Merhaba elde edilen değiştirilmiş küçük liste xml geri toohello clipListXML özelliği hello iş akışı kökünde hello "setProperty" yöntemi ile yazılır.</span><span class="sxs-lookup"><span data-stu-id="7d480-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="7d480-589">başka bir test çalıştırdıktan sonra hello Günlüğü penceresi bize aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="7d480-589">hello log window after another test run would show us hello following:</span></span>

![Merhaba küçük listesinde günlüğe kaydetme](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="7d480-591">*Merhaba küçük listesinde günlüğe kaydetme*</span><span class="sxs-lookup"><span data-stu-id="7d480-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="7d480-592">Nasıl hello video ve ses akışları kırpılmış bir test çalıştırması toosee yapın.</span><span class="sxs-lookup"><span data-stu-id="7d480-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="7d480-593">Merhaba kesme noktaları için farklı değerlere sahip birden fazla test çalıştırması gerçekleştirirsiniz gibi bu hesaba ancak alınmayacak olduğunu fark edeceksiniz!</span><span class="sxs-lookup"><span data-stu-id="7d480-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="7d480-594">Bunun nedeni Hello hello Azure çalışma zamanı aksine bu hello Tasarımcısı, her çalıştırma değil geçersiz kılma hello cliplist xml yapar.</span><span class="sxs-lookup"><span data-stu-id="7d480-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="7d480-595">Bu yalnızca hello hello ayarlamış çok ilk kez giriş ve çıkış noktaları, neden olur, hello xml tootransform anlamına gelir, tüm diğer bizim koruma yan tümcesi kez hello (varsa (clipListXML.indexOf ("<trim>") -1 ==)) hello iş akışı kırpma başka ekleme engeller olduğunda zaten mevcut bir öğe.</span><span class="sxs-lookup"><span data-stu-id="7d480-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="7d480-596">Bizim iş akışı uygun tootest yerel olarak en iyi biz toomake kırpma öğesi zaten mevcut olmadığını inceler bazı ev tutma kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d480-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="7d480-597">Bu durumda, biz hello xml hello yeni değerlerle değiştirerek devam etmeden önce kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="7d480-598">Düz dize işlemeleri kullanmak yerine, bu gerçek xml nesnesi aracılığıyla model ayrıştırma büyük olasılıkla daha güvenli toodo değil.</span><span class="sxs-lookup"><span data-stu-id="7d480-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="7d480-599">Bu tür kodu ancak ekleyebilmeniz için önce biz bizim komut dosyasının ilk olarak başlatma hello içeri aktarma deyimlerini sayısı tooadd gerekir:</span><span class="sxs-lookup"><span data-stu-id="7d480-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="7d480-600">Bundan sonra kodu temizleme gerekli hello ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d480-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="7d480-601">Bu kod yalnızca hello kırpma öğeleri toohello cliplist xml eklediğimiz hello noktası gider.</span><span class="sxs-lookup"><span data-stu-id="7d480-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="7d480-602">Bu noktada, biz çalıştırabilir ve her zamankinden uygulanan hello değişiklikler yaparken istediğiniz kadar süresi gibi bizim iş akışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="7d480-603"><a id="frame_based_trim_clippingenabled_prop"></a>ClippingEnabled kolaylık özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="7d480-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="7d480-604">Kırpma toohappen her zaman istemeyebilirsiniz, şimdi bizim iş akışı belirten uygun bir boolean bayrak ekleyerek bitiş kırpma / kırpma tooenable olsun veya olmasın istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d480-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="7d480-605">Gibi daha önce "ClippingEnabled" adlı bizim iş akışının yeni bir özellik toohello kökü "BOOLEAN" türü yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d480-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Kırpma etkinleştirmek için bir özellik yayımlanan](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="7d480-607">*Kırpma etkinleştirmek için bir özellik yayımlanan*</span><span class="sxs-lookup"><span data-stu-id="7d480-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="7d480-608">Basit koruma yan tümcesi aşağıda Hello ile biz kırpma gerekli olup olmadığını denetleyin ve bizim küçük listesi şekilde değiştirilmiş veya değil toobe gerekmediğine karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d480-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="7d480-609"><a id="code"></a>Tam kod</span><span class="sxs-lookup"><span data-stu-id="7d480-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="7d480-610">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7d480-610">Also see</span></span>
[<span data-ttu-id="7d480-611">Premium Azure Media Services kodlama Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="7d480-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7d480-612">Nasıl tooUse Premium Azure Media Services kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7d480-613">Azure medya hizmeti ile isteğe bağlı içerik kodlama</span><span class="sxs-lookup"><span data-stu-id="7d480-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="7d480-614">Media Encoder Premium İş Akışı Biçimleri ve Kod Çözücüleri</span><span class="sxs-lookup"><span data-stu-id="7d480-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="7d480-615">Örnek iş akışı dosyaları</span><span class="sxs-lookup"><span data-stu-id="7d480-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="7d480-616">Azure Media Services Gezgini aracı</span><span class="sxs-lookup"><span data-stu-id="7d480-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="7d480-617">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="7d480-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7d480-618">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="7d480-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
