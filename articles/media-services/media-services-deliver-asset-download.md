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
# <a name="how-to-deliver-an-asset-by-download"></a>Nasıl yapılır: bir varlık indirme tarafından teslim
TooMedia Hizmetleri karşıya ortam varlıkları teslim etmek için bu konuda seçenekleri açıklanmaktadır. Medya Hizmetleri içerik çok sayıda uygulama senaryolarında sunabilir. Ortam varlıkları indirin ya da bir Bulucu kullanarak erişim. Medya içerik tooanother uygulama veya tooanother içerik sağlayıcı gönderebilirsiniz. Bir içerik teslim ağı (CDN) kullanarak, Gelişmiş performans ve ölçeklenebilirlik için içerik sunabilir.

Bu örnekte gösterilir nasıl toodownload medya varlıklar Media Services tooyour yerel bilgisayardan. Merhaba kod sorguları hello iş kimliği ve erişim tarafından hello Media Services hesabınızla ilişkili işleri kendi **OutputMediaAssets** (Merhaba bir işin çalışmasını sonuçlanır bir veya daha fazla çıkış ortam varlıkları kümesi olan) koleksiyon. Bu örnek, bir iş, ancak varlıklarından uygulayabilirsiniz toodownload Çıkış medya aynı yaklaşımı toodownload diğer varlıklar nasıl hello gösterir.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

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



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Akış içerik dağıtımı](media-services-deliver-streaming-content.md)

