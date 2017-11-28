---
title: "aaaDownload Media Services varlıklar tooyour bilgisayar - Azure | Microsoft Docs"
description: "Toodownload varlıklar tooyour bilgisayar hakkında bilgi edinin. Kod örnekleri C# dilinde yazılmıştır ve .NET için Media Services SDK'sı hello kullanın."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="505af-104">Nasıl yapılır: bir varlık indirme tarafından teslim</span><span class="sxs-lookup"><span data-stu-id="505af-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="505af-105">TooMedia Hizmetleri karşıya ortam varlıkları teslim etmek için bu konuda seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="505af-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="505af-106">Medya Hizmetleri içerik çok sayıda uygulama senaryolarında sunabilir.</span><span class="sxs-lookup"><span data-stu-id="505af-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="505af-107">Ortam varlıkları indirin ya da bir Bulucu kullanarak erişim.</span><span class="sxs-lookup"><span data-stu-id="505af-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="505af-108">Medya içerik tooanother uygulama veya tooanother içerik sağlayıcı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="505af-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="505af-109">Bir içerik teslim ağı (CDN) kullanarak, Gelişmiş performans ve ölçeklenebilirlik için içerik sunabilir.</span><span class="sxs-lookup"><span data-stu-id="505af-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="505af-110">Bu örnekte gösterilir nasıl toodownload medya varlıklar Media Services tooyour yerel bilgisayardan.</span><span class="sxs-lookup"><span data-stu-id="505af-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="505af-111">Merhaba kod sorguları hello iş kimliği ve erişim tarafından hello Media Services hesabınızla ilişkili işleri kendi **OutputMediaAssets** (Merhaba bir işin çalışmasını sonuçlanır bir veya daha fazla çıkış ortam varlıkları kümesi olan) koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="505af-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="505af-112">Bu örnek, bir iş, ancak varlıklarından uygulayabilirsiniz toodownload Çıkış medya aynı yaklaşımı toodownload diğer varlıklar nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="505af-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="505af-113">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="505af-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="505af-114">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="505af-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="505af-115">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="505af-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="505af-116">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="505af-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="505af-117">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="505af-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="505af-118">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="505af-118">See Also</span></span>
[<span data-ttu-id="505af-119">Akış içerik dağıtımı</span><span class="sxs-lookup"><span data-stu-id="505af-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

