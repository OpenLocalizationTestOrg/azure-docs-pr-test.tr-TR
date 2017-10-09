---
title: "aaa\"karşıya yükleme dosyaları hello Azure portal kullanarak bir Media Services hesabına | Microsoft Docs\""
description: "Bu öğretici, hello karşıya yükleme dosyalarının hello Azure portal kullanarak bir Media Services hesabına adımları"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="4a601-103">Dosyaları hello Azure portal kullanarak bir Media Services hesabına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="4a601-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a601-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4a601-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="4a601-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4a601-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="4a601-106">REST</span><span class="sxs-lookup"><span data-stu-id="4a601-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="4a601-107">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a601-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="4a601-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a601-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="4a601-109">Media Services’de dijital dosyalar bir varlığa yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4a601-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="4a601-110">Merhaba varlık, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.) içerebilir. Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="4a601-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="4a601-111">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="4a601-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="4a601-112">Media Services işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="4a601-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="4a601-113">Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.</span><span class="sxs-lookup"><span data-stu-id="4a601-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="4a601-114">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="4a601-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="4a601-115">Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="4a601-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Dosyaları karşıya yükleme](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="4a601-117">Merhaba tıklatın **karşıya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4a601-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="4a601-118">Merhaba **bir varlığı karşıya yükle** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4a601-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4a601-119">Dosya boyutu sınırlaması yoktur.</span><span class="sxs-lookup"><span data-stu-id="4a601-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="4a601-120">Bilgisayarınızda istenen toohello video göz atın, onu seçin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4a601-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="4a601-121">Merhaba karşıya yükleme başlar ve hello dosya adı altında hello ilerleme durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a601-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="4a601-122">Merhaba karşıya yükleme işlemi tamamlandıktan sonra hello yeni varlık hello listelenen görürsünüz **varlıklar** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4a601-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a601-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a601-123">Next steps</span></span>
<span data-ttu-id="4a601-124">Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a601-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="4a601-125">Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="4a601-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="4a601-126">Azure işlevleri tootrigger yapılandırılmış hello kapsayıcısında ulaşan bir dosyayı temel bir kodlama işi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a601-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="4a601-127">Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.</span><span class="sxs-lookup"><span data-stu-id="4a601-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4a601-128">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="4a601-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4a601-129">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="4a601-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

