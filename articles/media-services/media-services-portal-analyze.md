---
title: "Azure Portalı'nı kullanarak medya çözümleme | Microsoft Docs"
description: "Bu konuda, Azure Portalı'nı kullanarak medya analizi medya işlemcileri (Mp'leri) medyanızı işlemek nasıl ele alınmıştır."
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
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="d8054-103">Azure portalını kullanarak medyanızı analiz etme</span><span class="sxs-lookup"><span data-stu-id="d8054-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="d8054-104">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8054-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d8054-105">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8054-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="d8054-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d8054-106">Overview</span></span>
<span data-ttu-id="d8054-107">Azure Media Services analizi, kuruluş ve işletmelerin video dosyalarından eyleme dönüştürülebilir Öngörüler türetmesini kolaylaştıran konuşma ve görme bileşenler (Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma) koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="d8054-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="d8054-108">Daha ayrıntılı Azure Media Services Analytics'e genel bakış için bkz: [bu](media-services-analytics-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="d8054-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="d8054-109">Bu konuda, Azure Portalı'nı kullanarak medya analizi medya işlemcileri (Mp'leri) medyanızı işlemek nasıl ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="d8054-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="d8054-110">Medya analizi Mp'leri MP4 veya JSON dosyaları üretir.</span><span class="sxs-lookup"><span data-stu-id="d8054-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="d8054-111">Medya işlemcisi bir MP4 dosyası oluşturduysa dosyayı aşamalı olarak indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="d8054-112">Medya işlemcisi bir JSON dosyası oluşturduysa dosyayı Azure blob depolamadan indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="d8054-113">Analiz etmek istediğiniz bir varlığı seçin</span><span class="sxs-lookup"><span data-stu-id="d8054-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="d8054-114">[Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8054-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d8054-115">**Ayarlar** penceresinde **Varlıklar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8054-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="d8054-116">.</span><span class="sxs-lookup"><span data-stu-id="d8054-116">.</span></span>
    <span data-ttu-id="d8054-117">![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="d8054-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="d8054-118">Çözümleme ve basın istediğiniz varlığı seçin **Çözümle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d8054-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="d8054-120">İçinde **medya analizi medya varlıkla işlem** penceresinde, işlemci seçin.</span><span class="sxs-lookup"><span data-stu-id="d8054-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="d8054-121">Makalenin kalanında nedenini açıklar ve her işlemci kullanma.</span><span class="sxs-lookup"><span data-stu-id="d8054-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="d8054-122">Tuşuna **oluşturma** iş başlatma.</span><span class="sxs-lookup"><span data-stu-id="d8054-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="d8054-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="d8054-123">Azure Media Indexer</span></span>
<span data-ttu-id="d8054-124">**Azure Media Indexer** medya işlemcisi yanı sıra medya dosyaları ve içerik aranabilir yapmanıza kapalı açıklamalı alt yazı parçaları oluşturmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="d8054-125">Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="d8054-127">Dil</span><span class="sxs-lookup"><span data-stu-id="d8054-127">Language</span></span>
<span data-ttu-id="d8054-128">Multimedya dosyasında tanınması için doğal dil.</span><span class="sxs-lookup"><span data-stu-id="d8054-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="d8054-129">Örneğin, İngilizce ve İspanyolca.</span><span class="sxs-lookup"><span data-stu-id="d8054-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="d8054-130">Resim yazıları</span><span class="sxs-lookup"><span data-stu-id="d8054-130">Captions</span></span>
<span data-ttu-id="d8054-131">İçeriğinizi oluşturulan açıklamalı alt yazı biçimi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="d8054-132">Bir dizin oluşturma işi kapalı açıklamalı alt yazı dosyaları aşağıdaki biçimlerde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8054-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="d8054-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="d8054-133">**SAMI**</span></span>
* <span data-ttu-id="d8054-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="d8054-134">**TTML**</span></span>
* <span data-ttu-id="d8054-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="d8054-135">**WebVTT**</span></span>

<span data-ttu-id="d8054-136">Bu biçimler dosyalarında ses ve video dosyaları işitme engelli kişiler için erişilebilir hale getirmek için kullanılan açıklamalı alt yazı (CC) kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="d8054-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="d8054-137">AIB dosyası</span><span class="sxs-lookup"><span data-stu-id="d8054-137">AIB file</span></span>
<span data-ttu-id="d8054-138">Özel SQL Server IFilter ile kullanmak için ses dizin Blob dosyası oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d8054-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="d8054-139">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.</span><span class="sxs-lookup"><span data-stu-id="d8054-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="d8054-140">Anahtar sözcükler</span><span class="sxs-lookup"><span data-stu-id="d8054-140">Keywords</span></span>
<span data-ttu-id="d8054-141">Anahtar sözcükler XML dosyası oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d8054-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="d8054-142">Bu dosya, sıklığı ve uzaklık bilgileri konuşma içerikten ayıklanan anahtar sözcükler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d8054-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="d8054-143">İş adı</span><span class="sxs-lookup"><span data-stu-id="d8054-143">Job name</span></span>
<span data-ttu-id="d8054-144">İş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="d8054-145">[Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="d8054-146">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="d8054-146">Output file</span></span>
<span data-ttu-id="d8054-147">Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="d8054-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d8054-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="d8054-149">Azure medya Hyperlapse ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan bir MP ' dir.</span><span class="sxs-lookup"><span data-stu-id="d8054-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="d8054-150">Daha fazla bilgi için [bu](media-services-hyperlapse-content.md) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="d8054-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="d8054-151">Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="d8054-153">Hız</span><span class="sxs-lookup"><span data-stu-id="d8054-153">Speed</span></span>
<span data-ttu-id="d8054-154">Giriş video hızlandırmak için hızıyla belirtin.</span><span class="sxs-lookup"><span data-stu-id="d8054-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="d8054-155">Çıktı, sabit ve zaman onlara yorumlama video giriş şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="d8054-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="d8054-156">İş adı</span><span class="sxs-lookup"><span data-stu-id="d8054-156">Job name</span></span>
<span data-ttu-id="d8054-157">İş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="d8054-158">[Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="d8054-159">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="d8054-159">Output file</span></span>
<span data-ttu-id="d8054-160">Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="d8054-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="d8054-161">Azure Media Face Detector</span></span>
<span data-ttu-id="d8054-162">**Azure medya yüz algılayıcısı** medya işlemcisi (MP) sayısı, hareketleri izlemek ve İzleyici katılım ve tepki yüz ifadeleri aracılığıyla bile ölçer olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="d8054-163">Bu hizmet, iki özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="d8054-163">This service contains two features:</span></span> 

* <span data-ttu-id="d8054-164">**Yüz algılama**</span><span class="sxs-lookup"><span data-stu-id="d8054-164">**Face detection**</span></span>
  
    <span data-ttu-id="d8054-165">Yüz algılama bulur ve video içinde İnsan yüzeyleri izler.</span><span class="sxs-lookup"><span data-stu-id="d8054-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="d8054-166">Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen zaman ve yer meta verilerle taşırken sonradan izlenmesi.</span><span class="sxs-lookup"><span data-stu-id="d8054-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="d8054-167">İzleme sırasında bunu obstructed veya kısaca çerçeve bırakın olsa bile kişinin ekranında dolaşma sırada tutarlı kimliği aynı yüz vermek dener.</span><span class="sxs-lookup"><span data-stu-id="d8054-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d8054-168">Bu hizmetler, yüz tanıma gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="d8054-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="d8054-169">Çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.</span><span class="sxs-lookup"><span data-stu-id="d8054-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="d8054-170">**Duygu algılama**</span><span class="sxs-lookup"><span data-stu-id="d8054-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="d8054-171">Duygu algılama analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, yüzler birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="d8054-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="d8054-173">Algılama modu</span><span class="sxs-lookup"><span data-stu-id="d8054-173">Detection mode</span></span>
<span data-ttu-id="d8054-174">Aşağıdaki modlarından birini işlemcisi tarafından kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="d8054-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="d8054-175">Yüz algılama</span><span class="sxs-lookup"><span data-stu-id="d8054-175">face detection</span></span>
* <span data-ttu-id="d8054-176">Yüz duygu algılama</span><span class="sxs-lookup"><span data-stu-id="d8054-176">per face emotion detection</span></span>
* <span data-ttu-id="d8054-177">Birleşik duygu algılama</span><span class="sxs-lookup"><span data-stu-id="d8054-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="d8054-178">İş adı</span><span class="sxs-lookup"><span data-stu-id="d8054-178">Job name</span></span>
<span data-ttu-id="d8054-179">İş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="d8054-180">[Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="d8054-181">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="d8054-181">Output file</span></span>
<span data-ttu-id="d8054-182">Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="d8054-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="d8054-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="d8054-184">**Azure medya hareket algılayıcısı** medya işlemcisi (MP), aksi takdirde uzun ve olaysız video içinde ilgi bölümleri verimli bir şekilde tanımlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="d8054-185">Hareket algılama statik kamera görüntülerinin video hareket oluştuğu bölümlerini belirlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d8054-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="d8054-186">Zaman damgaları ve olayın gerçekleştiği sınırlayıcı bölge ile meta verileri içeren bir JSON dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8054-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="d8054-187">Doğru güvenlik video akışları hedeflenen, bu teknolojiyi ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi hareket kategorilere yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="d8054-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="d8054-188">Bu, güvenlik uyarıları sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videoların ilgi dakika ayıklayın kullanabilmeye devam ederken adresinize olmadan kamera Akışları'oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8054-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="d8054-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="d8054-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="d8054-191">Bu işlemci otomatik olarak kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d8054-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="d8054-192">Bu, uzun bir video beklenmesi gerekenler hızlı bir bakış sağlamak istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d8054-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="d8054-193">Ayrıntılı bilgi ve örnekler için bkz: [bir Video özeti oluşturma kullanım Azure medya Video küçük](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="d8054-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="d8054-195">İş adı</span><span class="sxs-lookup"><span data-stu-id="d8054-195">Job name</span></span>
<span data-ttu-id="d8054-196">İş belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="d8054-197">[Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8054-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="d8054-198">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="d8054-198">Output file</span></span>
<span data-ttu-id="d8054-199">Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="d8054-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d8054-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8054-200">Next steps</span></span>
<span data-ttu-id="d8054-201">Görünüm Media Services'i öğrenme yolları.</span><span class="sxs-lookup"><span data-stu-id="d8054-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8054-202">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d8054-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

