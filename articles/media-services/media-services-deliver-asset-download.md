---
title: "Media Services varlıklar - Azure bilgisayarınıza | Microsoft Docs"
description: "Varlıklar bilgisayarınıza karşıdan yüklemek üzere öğrenin. Kod örnekleri, C# dilinde yazılmıştır ve .NET için Media Services SDK'sını kullanın."
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
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a>Nasıl yapılır: bir varlık indirme tarafından teslim
Bu konu, media varlıklar Media Services'e teslim etmek için seçenekleri açıklar. Medya Hizmetleri içerik çok sayıda uygulama senaryolarında sunabilir. Ortam varlıkları indirin ya da bir Bulucu kullanarak erişim. Medya içeriği başka bir uygulamaya veya başka bir içerik sağlayıcısına gönderebilirsiniz. Bir içerik teslim ağı (CDN) kullanarak, Gelişmiş performans ve ölçeklenebilirlik için içerik sunabilir.

Bu örnek, medya varlıklar Media Services'den yerel bilgisayarınıza indirin gösterilmektedir. İş kimliği ve erişim tarafından Media Services hesabınızla ilişkili işleri kodu sorgular kendi **OutputMediaAssets** (bir işi çalışmasını sonuçlanır bir veya daha fazla çıkış ortam varlıkları kümesi olan) koleksiyon. Bu örnek bir işinden çıkış ortam varlıkları indirmek nasıl gösterir, ancak diğer varlıklar indirmek için aynı yaklaşımı uygulayabilirsiniz.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için). Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
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
            // Use the following event handler to check download progress.
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



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Akış içerik dağıtımı](media-services-deliver-streaming-content.md)

