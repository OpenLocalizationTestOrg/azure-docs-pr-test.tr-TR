---
title: "Azure StorSimple Azure Media Services hesabından aaaUpload dosyalarıyla | Microsoft Docs"
description: "Bu makalede Azure StorSimple Veri Yöneticisi'ne ilişkin kısa bir genel bakış sunulmaktadır. Merhaba makale ayrıca şunları nasıl yapacağınızı tootutorials bağlantıları StorSimple tooextract verileri ve varlıklar tooan Azure Media Services hesabı yükleyin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="7777a-104">Azure StorSimple’dan Azure Media Services hesabına dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="7777a-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="7777a-105">Bu makalede Azure StorSimple Veri Yöneticisi'ne ilişkin kısa bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7777a-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="7777a-106">Merhaba makale ayrıca şunları nasıl yapacağınızı tootutorials bağlantıları StorSimple tooextract verileri ve bu verileri varlıklar tooan Azure Media Services (AMS) hesabı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7777a-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="7777a-107">Azure StorSimple Veri Yöneticisi şu anda özel önizleme aşamasındadır.</span><span class="sxs-lookup"><span data-stu-id="7777a-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="7777a-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7777a-108">Overview</span></span>

<span data-ttu-id="7777a-109">Media Services’de dijital dosyalar bir varlığa yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7777a-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="7777a-110">Merhaba varlık, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.) içerebilir. Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="7777a-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="7777a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello uzantısı şirket içi çözüm ve otomatik olarak katmanlarını veri hello şirket içi depolama ve bulut depolama arasında gibi bulut depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="7777a-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="7777a-112">Merhaba StorSimple cihazı dedupes ve verilerinizi büyük dosyalar toohello bulut göndermek için çok verimli hale getirme toohello bulut göndermeden önce sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="7777a-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="7777a-113">Merhaba [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) hizmeti, StorSimple tooextract verileri sağlayan ve AMS varlıklar olarak sunmak API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7777a-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="7777a-114">başlarken</span><span class="sxs-lookup"><span data-stu-id="7777a-114">Get started</span></span>

1. <span data-ttu-id="7777a-115">[Bir Media Services hesabı oluşturma](media-services-portal-create-account.md) tootransfer hello varlıklar istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="7777a-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="7777a-116">Kaydolmak için veri Yöneticisi Önizleme, hello açıklandığı gibi [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7777a-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="7777a-117">Bir StorSimple Veri Yöneticisi hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7777a-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="7777a-118">Çalıştığında bir StorSimple cihazından verileri ayıklayıp varlık olarak AMS hesabına aktaran bir veri dönüşüm işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7777a-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="7777a-119">Merhaba iş çalışmaya başladığında, depolama kuyruğu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7777a-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="7777a-120">Bu kuyruk, hazır olduğunda dönüştürülen bloblar hakkında iletilerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="7777a-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="7777a-121">Bu sıranın Hello adı olduğu hello hello iş tanımı hello adı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="7777a-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="7777a-122">Bu sıra toodetermine kullandığınız zaman varlık olduğu gibi hazır ve üzerinde istenen Media Services işlemi toorun çağırın.</span><span class="sxs-lookup"><span data-stu-id="7777a-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="7777a-123">Örneğin, bu kuyruk tootrigger hello gerekli Media Services kodu içeren bir Azure işlevi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7777a-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="7777a-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7777a-124">See also</span></span>

[<span data-ttu-id="7777a-125">Kullanım .net SDK hello hello Data Manager tootrigger işler</span><span class="sxs-lookup"><span data-stu-id="7777a-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="7777a-126">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="7777a-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7777a-127">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="7777a-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7777a-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7777a-128">Next steps</span></span>

<span data-ttu-id="7777a-129">Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7777a-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="7777a-130">Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="7777a-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
