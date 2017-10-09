---
title: "hata kodları kodlama aaaAzure Media Services | Microsoft Docs"
description: "Bu konuda görev yürütme kodlama hello sırasında bir hatayla karşılaşıldı durumunda döndürülebilen hata kodları listelenmektedir..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="07b5b-103">Kodlama hata kodları</span><span class="sxs-lookup"><span data-stu-id="07b5b-103">Encoding error codes</span></span>

<span data-ttu-id="07b5b-104">Merhaba aşağıdaki tabloda görev yürütme kodlama hello sırasında bir hatayla karşılaşıldı durumunda döndürülebilen hata kodları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="07b5b-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="07b5b-105">.NET kodunuzu tooget hata ayrıntılarında kullanmak hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="07b5b-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="07b5b-106">REST kodunuzu tooget hata ayrıntılarında kullanmak hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="07b5b-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="07b5b-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="07b5b-107">ErrorDetail.Code</span></span> | <span data-ttu-id="07b5b-108">Hatanın olası nedenleri</span><span class="sxs-lookup"><span data-stu-id="07b5b-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="07b5b-109">Bilinmeyen</span><span class="sxs-lookup"><span data-stu-id="07b5b-109">Unknown</span></span> |<span data-ttu-id="07b5b-110">Merhaba Görev yürütülürken bilinmeyen bir hata oluştu</span><span class="sxs-lookup"><span data-stu-id="07b5b-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="07b5b-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="07b5b-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="07b5b-112">Hatalı dosya adları, yanlış sıfır uzunluk dosyaları gibi giriş varlık indirme hataları kapsayan kategori hata ve benzeri biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="07b5b-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="07b5b-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="07b5b-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="07b5b-114">Merhaba Hizmet tarafı - indirilirken örnek ağ veya depolama hataları sorunları kapsamaktadır hataları kategorisi.</span><span class="sxs-lookup"><span data-stu-id="07b5b-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="07b5b-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07b5b-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="07b5b-116">Kategori hataların nereye görev <see cref="MediaTask.PrivateData"/> (yapılandırma) geçerli değil, örneğin hello yapılandırması geçersiz XML içeriyor ya da geçerli bir sistem hazır değil.</span><span class="sxs-lookup"><span data-stu-id="07b5b-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="07b5b-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="07b5b-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="07b5b-118">Burada sorunları hello içinde medya dosyalarını başarısız olmasına neden giriş hello görevi hello yürütme sırasında hatalar kategorisi.</span><span class="sxs-lookup"><span data-stu-id="07b5b-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="07b5b-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="07b5b-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="07b5b-120">Burada hello medya işlemcisi sağlanan hello dosyaları işleyemiyor - medya biçimlendirilmemesi hataların kategori desteklenen veya hello yapılandırması eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="07b5b-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="07b5b-121">Örneğin, yalnızca video sahip bir varlık bir salt ses çıkış tooproduce çalışıyor</span><span class="sxs-lookup"><span data-stu-id="07b5b-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="07b5b-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="07b5b-122">ErrorProcessingTask</span></span> |<span data-ttu-id="07b5b-123">Medya işlemcisi hello diğer hataları kategorisini ilgisiz toocontent olan hello görev hello işlenmesi sırasında karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="07b5b-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="07b5b-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="07b5b-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="07b5b-125">Kategori hello çıkış varlığına karşıya yüklenirken hata</span><span class="sxs-lookup"><span data-stu-id="07b5b-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="07b5b-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="07b5b-126">ErrorCancelingTask</span></span> |<span data-ttu-id="07b5b-127">Kategori toocancel hello görev çalışırken hataları toocover hatalar</span><span class="sxs-lookup"><span data-stu-id="07b5b-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="07b5b-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="07b5b-128">TransientError</span></span> |<span data-ttu-id="07b5b-129">Kategori sorunların hatalarını toocover geçici (ör.)</span><span class="sxs-lookup"><span data-stu-id="07b5b-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="07b5b-130">Azure Storage ile geçici ağ sorunları)</span><span class="sxs-lookup"><span data-stu-id="07b5b-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="07b5b-131">Merhaba tooget Yardım **Media Services** takım, açık bir [destek bileti](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="07b5b-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="07b5b-132">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="07b5b-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="07b5b-133">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="07b5b-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="07b5b-134">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="07b5b-134">Related articles</span></span>
* [<span data-ttu-id="07b5b-135">Medya Kodlayıcısı standart hazır özelleştirerek gelişmiş kodlama görevleri gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="07b5b-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="07b5b-136">Kotalar ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="07b5b-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
