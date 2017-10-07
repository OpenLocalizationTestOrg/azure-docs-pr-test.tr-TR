---
title: aaaAnalyze hello Azure portal kullanarak medya | Microsoft Docs
description: "Bu konuda ele alınmıştır nasıl medyanızı kullanarak medya analizi medya işlemcileri (Mp'leri) ile Azure portal hello tooprocess."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="8c098-103">Hello Azure portal kullanarak medya Çözümle</span><span class="sxs-lookup"><span data-stu-id="8c098-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="8c098-104">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c098-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8c098-105">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c098-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="8c098-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8c098-106">Overview</span></span>
<span data-ttu-id="8c098-107">Azure Media Services analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler için kendi video dosyalarından kolaylaştıran konuşma ve görme bileşenler (Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma) koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="8c098-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="8c098-108">Daha ayrıntılı Azure Media Services Analytics'e genel bakış için bkz: [bu](media-services-analytics-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="8c098-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="8c098-109">Bu konuda ele alınmıştır nasıl medyanızı kullanarak medya analizi medya işlemcileri (Mp'leri) ile Azure portal hello tooprocess.</span><span class="sxs-lookup"><span data-stu-id="8c098-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="8c098-110">Medya analizi Mp'leri MP4 veya JSON dosyaları üretir.</span><span class="sxs-lookup"><span data-stu-id="8c098-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="8c098-111">Medya işlemcisi bir MP4 dosyası oluşturduysa hello dosyayı aşamalı olarak indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="8c098-112">Medya işlemcisi bir JSON dosyası oluşturduysa hello Azure blob depolama hello dosyayı indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="8c098-113">Bir varlığı seçin tooanalyze istiyor</span><span class="sxs-lookup"><span data-stu-id="8c098-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="8c098-114">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="8c098-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="8c098-115">Merhaba, **ayarları** penceresinde, seçin **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="8c098-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="8c098-116">.</span><span class="sxs-lookup"><span data-stu-id="8c098-116">.</span></span>
    <span data-ttu-id="8c098-117">![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="8c098-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="8c098-118">İstediğiniz select hello varlık tooanalyze ve tuşuna hello **Çözümle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8c098-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="8c098-120">Merhaba, **medya analizi medya varlıkla işlem** penceresinde, select hello işlemci.</span><span class="sxs-lookup"><span data-stu-id="8c098-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="8c098-121">Merhaba makalenin devamında, hello açıklar neden ve nasıl toouse her işlemci.</span><span class="sxs-lookup"><span data-stu-id="8c098-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="8c098-122">Tuşuna **oluşturma** toohello bir proje başlatın.</span><span class="sxs-lookup"><span data-stu-id="8c098-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="8c098-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="8c098-123">Azure Media Indexer</span></span>
<span data-ttu-id="8c098-124">Merhaba **Azure Media Indexer** medya işlemcisi sağlar toomake medya dosyaları ve içerik aranabilir, yanı sıra kapalı açıklamalı alt yazı parçaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c098-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="8c098-125">Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c098-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="8c098-127">Dil</span><span class="sxs-lookup"><span data-stu-id="8c098-127">Language</span></span>
<span data-ttu-id="8c098-128">Merhaba doğal dil toobe Hello multimedya dosyasında tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="8c098-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="8c098-129">Örneğin, İngilizce ve İspanyolca.</span><span class="sxs-lookup"><span data-stu-id="8c098-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="8c098-130">Resim yazıları</span><span class="sxs-lookup"><span data-stu-id="8c098-130">Captions</span></span>
<span data-ttu-id="8c098-131">İçeriğinizi oluşturulan açıklamalı alt yazı biçimi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="8c098-132">Bir dizin oluşturma işi kapalı açıklamalı alt yazı dosyaları biçimleri aşağıdaki hello oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8c098-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="8c098-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="8c098-133">**SAMI**</span></span>
* <span data-ttu-id="8c098-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="8c098-134">**TTML**</span></span>
* <span data-ttu-id="8c098-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="8c098-135">**WebVTT**</span></span>

<span data-ttu-id="8c098-136">Bu biçimler kapalı açıklamalı alt yazı (CC) dosyalarında kullanılan toomake ses olabilir ve erişilebilir toopeople işitme engelli ile video dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8c098-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="8c098-137">AIB dosyası</span><span class="sxs-lookup"><span data-stu-id="8c098-137">AIB file</span></span>
<span data-ttu-id="8c098-138">Özel SQL Server IFilter ile kullanılmak üzere toogenerate hello ses dizin Blob dosya gibi hello, bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8c098-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="8c098-139">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.</span><span class="sxs-lookup"><span data-stu-id="8c098-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="8c098-140">Anahtar sözcükler</span><span class="sxs-lookup"><span data-stu-id="8c098-140">Keywords</span></span>
<span data-ttu-id="8c098-141">Anahtar sözcükler XML dosyası toogenerate istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8c098-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="8c098-142">Bu dosya, sıklığı ve uzaklık bilgileri hello konuşma içerikten ayıklanan anahtar sözcükler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8c098-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="8c098-143">İş adı</span><span class="sxs-lookup"><span data-stu-id="8c098-143">Job name</span></span>
<span data-ttu-id="8c098-144">Hello iş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="8c098-145">[Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8c098-146">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="8c098-146">Output file</span></span>
<span data-ttu-id="8c098-147">Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="8c098-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="8c098-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="8c098-149">Azure medya Hyperlapse ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan bir MP ' dir.</span><span class="sxs-lookup"><span data-stu-id="8c098-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="8c098-150">Daha fazla bilgi için [bu](media-services-hyperlapse-content.md) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="8c098-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="8c098-151">Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c098-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="8c098-153">Hız</span><span class="sxs-lookup"><span data-stu-id="8c098-153">Speed</span></span>
<span data-ttu-id="8c098-154">Hangi toospeed hello giriş video yukarı ile Merhaba hızını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8c098-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="8c098-155">Merhaba çıkışı sabit ve zaman onlara yorumlama hello giriş videonun yapılır.</span><span class="sxs-lookup"><span data-stu-id="8c098-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="8c098-156">İş adı</span><span class="sxs-lookup"><span data-stu-id="8c098-156">Job name</span></span>
<span data-ttu-id="8c098-157">Hello iş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="8c098-158">[Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8c098-159">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="8c098-159">Output file</span></span>
<span data-ttu-id="8c098-160">Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="8c098-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="8c098-161">Azure Media Face Detector</span></span>
<span data-ttu-id="8c098-162">Merhaba **Azure medya yüz algılayıcısı** medya işlemcisi (MP) etkinleştirir, size, toocount, izleme hareketleri ve hatta ölçer İzleyici katılım ve tepki yüz ifadeleri aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="8c098-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="8c098-163">Bu hizmet, iki özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="8c098-163">This service contains two features:</span></span> 

* <span data-ttu-id="8c098-164">**Yüz algılama**</span><span class="sxs-lookup"><span data-stu-id="8c098-164">**Face detection**</span></span>
  
    <span data-ttu-id="8c098-165">Yüz algılama bulur ve video içinde İnsan yüzeyleri izler.</span><span class="sxs-lookup"><span data-stu-id="8c098-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="8c098-166">Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen hello zaman ve yer meta verilerle taşırken sonradan izlenmesi.</span><span class="sxs-lookup"><span data-stu-id="8c098-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="8c098-167">İzleme sırasında toogive obstructed veya kısaca hello çerçeve bırakın olsa bile hello kişi ekranında dolaşma sırada aynı yönde tutarlı bir kimliği toohello dener.</span><span class="sxs-lookup"><span data-stu-id="8c098-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8c098-168">Bu hizmetler, yüz tanıma gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="8c098-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="8c098-169">Merhaba çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.</span><span class="sxs-lookup"><span data-stu-id="8c098-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="8c098-170">**Duygu algılama**</span><span class="sxs-lookup"><span data-stu-id="8c098-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="8c098-171">Duygu algılama hello analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, hello yüzeyleri birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="8c098-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="8c098-173">Algılama modu</span><span class="sxs-lookup"><span data-stu-id="8c098-173">Detection mode</span></span>
<span data-ttu-id="8c098-174">Modları aşağıdaki hello birini hello işlemcisi tarafından kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8c098-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="8c098-175">Yüz algılama</span><span class="sxs-lookup"><span data-stu-id="8c098-175">face detection</span></span>
* <span data-ttu-id="8c098-176">Yüz duygu algılama</span><span class="sxs-lookup"><span data-stu-id="8c098-176">per face emotion detection</span></span>
* <span data-ttu-id="8c098-177">Birleşik duygu algılama</span><span class="sxs-lookup"><span data-stu-id="8c098-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="8c098-178">İş adı</span><span class="sxs-lookup"><span data-stu-id="8c098-178">Job name</span></span>
<span data-ttu-id="8c098-179">Hello iş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="8c098-180">[Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8c098-181">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="8c098-181">Output file</span></span>
<span data-ttu-id="8c098-182">Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="8c098-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="8c098-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="8c098-184">Merhaba **Azure medya hareket algılayıcısı** , tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak medya işlemci (MP) etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8c098-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="8c098-185">Hareket algılama hareket oluştuğu statik kamera görüntülerinin tooidentify bölümlerini hello video üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8c098-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="8c098-186">Zaman damgaları ve bölge hello olayın gerçekleştiği sınırlayıcı hello meta verileri içeren bir JSON dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c098-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="8c098-187">Doğru güvenlik video akışları hedeflenen, bu mümkün toocategorize hareket ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="8c098-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="8c098-188">Bu işlem, sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videolar gelen ilgi mümkün tooextract dakika devam ederken adresinize olmadan kamera akışları toogenerate güvenlik uyarıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c098-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="8c098-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="8c098-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="8c098-191">Bu işlemci otomatik olarak hello kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8c098-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="8c098-192">Tooprovide hangi tooexpect uzun videoda hızlı bir genel bakış istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8c098-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="8c098-193">Ayrıntılı bilgi ve örnekler için bkz: [kullanım Azure medya Video küçük resimleri tooCreate bir Video özeti](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="8c098-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="8c098-195">İş adı</span><span class="sxs-lookup"><span data-stu-id="8c098-195">Job name</span></span>
<span data-ttu-id="8c098-196">Hello iş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="8c098-197">[Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c098-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="8c098-198">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="8c098-198">Output file</span></span>
<span data-ttu-id="8c098-199">Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="8c098-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c098-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c098-200">Next steps</span></span>
<span data-ttu-id="8c098-201">Görünüm Media Services'i öğrenme yolları.</span><span class="sxs-lookup"><span data-stu-id="8c098-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8c098-202">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="8c098-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

