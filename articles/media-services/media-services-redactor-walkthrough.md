---
title: "Azure medya analizi kılavuza yüzeyleri Redaksiyon | Microsoft Docs"
description: "Bu konu Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak tam Redaksiyon iş akışını çalıştırma hakkında adım adım yönergeler gösterir."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="0478c-103">Azure medya analizi kılavuza yüzeyleri Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="0478c-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="0478c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0478c-104">Overview</span></span>

<span data-ttu-id="0478c-105">**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon bulutta sunar.</span><span class="sxs-lookup"><span data-stu-id="0478c-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="0478c-106">Yüz Redaksiyon seçili kişiler yüzeyleri ölçeklendirilmelidir için videonuzu değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0478c-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="0478c-107">Genel güvenlik ve haber medya senaryolarda yüz Redaksiyon hizmeti kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0478c-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="0478c-108">Birden çok yüzeyleri içeren çekimi birkaç dakika el ile Redaksiyon saat sürebilir, ancak bu hizmet ile birkaç basit adımla yüz Redaksiyon işlem gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0478c-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="0478c-109">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="0478c-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="0478c-110">Hakkındaki ayrıntılar için **Azure medya Redactor**, bkz: [yüz Redaksiyon genel bakış](media-services-face-redaction.md) konu.</span><span class="sxs-lookup"><span data-stu-id="0478c-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="0478c-111">Bu konu Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak tam Redaksiyon iş akışını çalıştırma hakkında adım adım yönergeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="0478c-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="0478c-112">**Azure medya Redactor** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="0478c-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="0478c-113">Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0478c-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="0478c-114">Bu önizleme şu anda ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="0478c-114">This preview is currently free of charge.</span></span> <span data-ttu-id="0478c-115">Geçerli sürümde, işlenen video uzunluk 10 dakikalık sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="0478c-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="0478c-116">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.</span><span class="sxs-lookup"><span data-stu-id="0478c-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="0478c-117">Azure Media Services Gezgini iş akışı</span><span class="sxs-lookup"><span data-stu-id="0478c-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="0478c-118">Redactor ile çalışmaya başlamak için en kolay yolu, github'da açık kaynaklı AMSE aracını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="0478c-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="0478c-119">Basitleştirilmiş bir iş akışı aracılığıyla çalıştırabilirsiniz **birleştirilmiş** ek açıklama json veya yüz jpg görüntüleri erişim gerekmiyorsa modu.</span><span class="sxs-lookup"><span data-stu-id="0478c-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="0478c-120">Karşıdan yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="0478c-120">Download and setup</span></span>

1. <span data-ttu-id="0478c-121">AMSE aracını indirin [burada](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="0478c-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="0478c-122">Media Services hesabınıza hizmet anahtarınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0478c-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="0478c-123">Hesap adını ve anahtar bilgilerini almak için [Azure portalına](https://portal.azure.com/) gidin ve AMS hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="0478c-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="0478c-124">Ardından, ayarları seçin > anahtarları.</span><span class="sxs-lookup"><span data-stu-id="0478c-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="0478c-125">Anahtarları yönet pencerelerinde hesap adı gösterilir ve birincil anahtar ile ikincil anahtar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0478c-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="0478c-126">Hesap adı ve birincil anahtar değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0478c-126">Copy values of the account name and the primary key.</span></span>

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="0478c-128">İlk geçirmek – modu Çözümle</span><span class="sxs-lookup"><span data-stu-id="0478c-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="0478c-129">Karşıya yükleme, ortam dosyası aracılığıyla varlığını –> karşıya yükleme, ya da sürükle ve bırak aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="0478c-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="0478c-130">Sağ tıklayın ve medya dosyanızı medya analizi kullanarak işlem Azure medya Redactor –> Çözümle modu –>.</span><span class="sxs-lookup"><span data-stu-id="0478c-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="0478c-133">Çıktı jpg algılanan her yazıtipinin yanı sıra, yüz konum verilerini içeren bir ek açıklamaları json dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="0478c-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="0478c-135">İkinci geçirmek – modu Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="0478c-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="0478c-136">Özgün video Varlığınızı çıkışı ilk pass karşıya yükleyin ve birincil bir varlık ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0478c-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="0478c-138">(İsteğe bağlı) Redaksiyon istediğiniz kimlikleri yeni satır ayrılmış listesini içeren bir 'Dance_idlist.txt' dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0478c-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="0478c-140">(İsteğe bağlı) Sınırlama kutusu sınırlarını artırma gibi annotations.json dosyaya tüm düzenlemeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="0478c-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="0478c-141">İlk geçişi çıkış varlığından sağ tıklayın, Redactor seçin ve çalıştırmalarına **Redact** modu.</span><span class="sxs-lookup"><span data-stu-id="0478c-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="0478c-143">Karşıdan yükleyin ya da son Redaksiyonu yapılmış çıkış varlığına paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0478c-143">Download or share the final redacted output asset.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="0478c-145">Azure Media Redactor Görselleştirici açık kaynak aracı</span><span class="sxs-lookup"><span data-stu-id="0478c-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="0478c-146">Bir açık kaynak [Görselleştirici aracı](https://github.com/Microsoft/azure-media-redactor-visualizer) ayrıştırma ve çıktı kullanarak ek açıklama biçimi yalnızca başlayarak geliştiricilere yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0478c-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="0478c-147">Projeyi çalıştırmak için depoyu kopyalama sonra gelen FFMPEG indirme gerekir kendi [resmi sitesi](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="0478c-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="0478c-148">JSON ek açıklama verilerini ayrıştırma çalışılırken bir geliştirici iseniz içinde Models.MetaData için örnek kod örnekleri arayın.</span><span class="sxs-lookup"><span data-stu-id="0478c-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="0478c-149">Aracı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0478c-149">Set up the tool</span></span>

1.  <span data-ttu-id="0478c-150">İndirin ve tüm çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0478c-150">Download and build the entire solution.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="0478c-152">Gelen FFMPEG karşıdan [burada](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="0478c-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="0478c-153">Bu projede statik bağlama ile sürüm be1d324 (2016-10-04) ile ilk olarak geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0478c-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="0478c-154">Ffmpeg.exe ve ffprobe.exe AzureMediaRedactor.exe aynı çıktı klasöre kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0478c-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="0478c-156">AzureMediaRedactor.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0478c-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="0478c-157">Aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="0478c-157">Use the tool</span></span>

1. <span data-ttu-id="0478c-158">Azure Media Services hesabınızla Redactor MP Çözümle modunu, videoda işleyin.</span><span class="sxs-lookup"><span data-stu-id="0478c-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="0478c-159">Özgün video dosyası ve Redaksiyon çıktısını yükle - iş analiz edin.</span><span class="sxs-lookup"><span data-stu-id="0478c-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="0478c-160">Görselleştirici uygulamayı çalıştırın ve yukarıdaki dosyaları seçin.</span><span class="sxs-lookup"><span data-stu-id="0478c-160">Run the visualizer application and choose the files above.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="0478c-162">Dosyanızı önizlemede.</span><span class="sxs-lookup"><span data-stu-id="0478c-162">Preview your file.</span></span> <span data-ttu-id="0478c-163">Sağ kenar aracılığıyla ölçeklendirilmelidir istediğiniz hangi yüzeyleri seçin.</span><span class="sxs-lookup"><span data-stu-id="0478c-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="0478c-165">Alt metin alanı kimlikleri yüz ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0478c-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="0478c-166">"İdlist.txt" adlı bir dosya Bu kimliklerle yeni satır ayrılmış liste olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0478c-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="0478c-167">İdlist.txt ANSI kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0478c-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="0478c-168">ANSI kaydetmek için Not Defteri'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0478c-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="0478c-169">Bu dosya, adım 1'den çıkış varlığına karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0478c-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="0478c-170">Bu varlık için özgün video karşıya yükleyin ve birincil varlık ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0478c-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="0478c-171">Redaksiyon işi Redaksiyon son video almak için bu varlık üzerinde "Redact" modu ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0478c-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0478c-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0478c-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0478c-173">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="0478c-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0478c-174">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="0478c-174">Related links</span></span>
[<span data-ttu-id="0478c-175">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="0478c-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="0478c-176">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="0478c-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="0478c-177">Azure medya analizi için yüz Redaksiyon Duyurusu</span><span class="sxs-lookup"><span data-stu-id="0478c-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
