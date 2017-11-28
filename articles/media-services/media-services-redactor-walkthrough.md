---
title: "Azure medya analizi kılavuza aaaRedact yüzeyleri | Microsoft Docs"
description: "Bu konu hakkında adım adım yönergeler gösterir toorun Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak bir tam Redaksiyon iş akışı."
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
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="b5fc8-103">Azure medya analizi kılavuza yüzeyleri Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="b5fc8-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="b5fc8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b5fc8-104">Overview</span></span>

<span data-ttu-id="b5fc8-105">**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon hello bulutta sunar.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="b5fc8-106">Yüz Redaksiyon sipariş tooblur yüzeyleri seçilen kişilerin, video, toomodify sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="b5fc8-107">Toouse hello yüz Redaksiyon hizmeti ortak güvenliği ve haber medya senaryolarda isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="b5fc8-108">Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmet hello yüz ile birkaç basit adımla Redaksiyon işlem gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="b5fc8-109">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="b5fc8-110">Hakkındaki ayrıntılar için **Azure medya Redactor**, hello bkz [yüz Redaksiyon genel bakış](media-services-face-redaction.md) konu.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="b5fc8-111">Bu konu hakkında adım adım yönergeler gösterir toorun Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak bir tam Redaksiyon iş akışı.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="b5fc8-112">Merhaba **Azure medya Redactor** MP şu anda önizlemede.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="b5fc8-113">Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="b5fc8-114">Bu önizleme şu anda ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-114">This preview is currently free of charge.</span></span> <span data-ttu-id="b5fc8-115">Merhaba geçerli sürümde, işlenen video uzunluk 10 dakikalık sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="b5fc8-116">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="b5fc8-117">Azure Media Services Gezgini iş akışı</span><span class="sxs-lookup"><span data-stu-id="b5fc8-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="b5fc8-118">Merhaba en kolay yolu tooget kullanmaya Redactor araçtır toouse hello açık kaynak AMSE github'da.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="b5fc8-119">Basitleştirilmiş bir iş akışı aracılığıyla çalıştırabilirsiniz **birleştirilmiş** modu toohello ek açıklama json ya da hello yüz jpg görüntüleri erişim yoktur.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="b5fc8-120">Karşıdan yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="b5fc8-120">Download and setup</span></span>

1. <span data-ttu-id="b5fc8-121">Merhaba AMSE aracını indirin [burada](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="b5fc8-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="b5fc8-122">Tooyour hizmeti anahtarınızı kullanarak Media Services hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="b5fc8-123">hesap adı ve anahtar bilgilerini, Git toohello tooobtain hello [Azure portal](https://portal.azure.com/) ve AMS hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="b5fc8-124">Ardından, ayarları seçin > anahtarları.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="b5fc8-125">Merhaba Yönet anahtarları windows hello hesap adını gösterir ve hello birincil ve ikincil anahtarlar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="b5fc8-126">Merhaba hesap adı ve hello birincil anahtar değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-126">Copy values of hello account name and hello primary key.</span></span>

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="b5fc8-128">İlk geçirmek – modu Çözümle</span><span class="sxs-lookup"><span data-stu-id="b5fc8-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="b5fc8-129">Karşıya yükleme, ortam dosyası aracılığıyla varlığını –> karşıya yükleme, ya da sürükle ve bırak aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="b5fc8-130">Sağ tıklayın ve medya dosyanızı medya analizi kullanarak işlem Azure medya Redactor –> Çözümle modu –>.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="b5fc8-133">Merhaba çıkış jpg algılanan her yazıtipinin yanı sıra, yüz konum verilerini içeren bir ek açıklamaları json dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="b5fc8-135">İkinci geçirmek – modu Redaksiyon</span><span class="sxs-lookup"><span data-stu-id="b5fc8-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="b5fc8-136">Merhaba ilk pass çıkış ve birincil bir varlık ayarlamak, özgün bir varlığı toohello karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="b5fc8-138">(İsteğe bağlı) Merhaba tooredact istediğiniz kimlikleri yeni satır ayrılmış listesini içeren bir 'Dance_idlist.txt' dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="b5fc8-140">(İsteğe bağlı) Sınırlama kutusu sınırlarını hello artırma gibi tüm düzenlemeleri toohello annotations.json dosya olun.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="b5fc8-141">Merhaba ilk geçişi hello çıkış varlığından sağ tıklayın, hello Redactor seçin ve hello ile Çalıştır **Redact** modu.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="b5fc8-143">İndirme veya hello son Redaksiyonu yapılmış çıkış varlığına paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-143">Download or share hello final redacted output asset.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="b5fc8-145">Azure Media Redactor Görselleştirici açık kaynak aracı</span><span class="sxs-lookup"><span data-stu-id="b5fc8-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="b5fc8-146">Bir açık kaynak [Görselleştirici aracı](https://github.com/Microsoft/azure-media-redactor-visualizer) tasarlanmış toohelp geliştiriciler ayrıştırma ve hello çıkış kullanan hello ek açıklama biçimi yalnızca başlayarak olduğunu.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="b5fc8-147">Sipariş toorun hello projesinde hello depoyu kopyalama sonra toodownload FFMPEG gerekir gelen kendi [resmi sitesi](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="b5fc8-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="b5fc8-148">Tooparse hello JSON ek açıklama verilerini çalışırken bir geliştirici iseniz içinde Models.MetaData için örnek kod örnekleri arayın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="b5fc8-149">Merhaba aracı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="b5fc8-149">Set up hello tool</span></span>

1.  <span data-ttu-id="b5fc8-150">Karşıdan yükle ve hello tüm çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-150">Download and build hello entire solution.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="b5fc8-152">Gelen FFMPEG karşıdan [burada](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="b5fc8-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="b5fc8-153">Bu projede statik bağlama ile sürüm be1d324 (2016-10-04) ile ilk olarak geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="b5fc8-154">Ffmpeg.exe ve ffprobe.exe toohello kopyalamak aynı çıkış klasörü AzureMediaRedactor.exe olarak.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="b5fc8-156">AzureMediaRedactor.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="b5fc8-157">Merhaba aracını kullanın</span><span class="sxs-lookup"><span data-stu-id="b5fc8-157">Use hello tool</span></span>

1. <span data-ttu-id="b5fc8-158">Azure Media Services hesabınızla hello Redactor MP Çözümle modunu, videoda işleyin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="b5fc8-159">Merhaba özgün video dosyası ve hello Redaksiyon hello çıktısını yükle - iş analiz edin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="b5fc8-160">Merhaba Görselleştirici uygulamayı çalıştırın ve yukarıdaki hello dosyalar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="b5fc8-162">Dosyanızı önizlemede.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-162">Preview your file.</span></span> <span data-ttu-id="b5fc8-163">Hangi, yüzler seçin hello Kenar çubuğunda hello aracılığıyla tooblur sağ ister.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="b5fc8-165">Merhaba alt metin alanı hello yüz kimlikleri ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="b5fc8-166">"İdlist.txt" adlı bir dosya Bu kimliklerle yeni satır ayrılmış liste olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="b5fc8-167">Merhaba idlist.txt ANSI kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="b5fc8-168">Not Defteri'ni toosave ANSI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="b5fc8-169">Bu dosya toohello çıkış varlık 1. adımdaki karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="b5fc8-170">Merhaba özgün video toothis varlık da karşıya yükleyin ve birincil varlık ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="b5fc8-171">Bu varlık "Redact" modu tooget hello son Redaksiyonu yapılmış video Redaksiyon işi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b5fc8-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b5fc8-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5fc8-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b5fc8-173">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b5fc8-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b5fc8-174">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="b5fc8-174">Related links</span></span>
[<span data-ttu-id="b5fc8-175">Azure Media Services Analytics a genel bakış</span><span class="sxs-lookup"><span data-stu-id="b5fc8-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="b5fc8-176">Azure medya analizi gösterileri</span><span class="sxs-lookup"><span data-stu-id="b5fc8-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="b5fc8-177">Azure medya analizi için yüz Redaksiyon Duyurusu</span><span class="sxs-lookup"><span data-stu-id="b5fc8-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
