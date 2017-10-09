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
# <a name="encoding-error-codes"></a>Kodlama hata kodları

Merhaba aşağıdaki tabloda görev yürütme kodlama hello sırasında bir hatayla karşılaşıldı durumunda döndürülebilen hata kodları listelenmektedir.  .NET kodunuzu tooget hata ayrıntılarında kullanmak hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) sınıfı. REST kodunuzu tooget hata ayrıntılarında kullanmak hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.

| ErrorDetail.Code | Hatanın olası nedenleri |
| --- | --- |
| Bilinmeyen |Merhaba Görev yürütülürken bilinmeyen bir hata oluştu |
| ErrorDownloadingInputAssetMalformedContent |Hatalı dosya adları, yanlış sıfır uzunluk dosyaları gibi giriş varlık indirme hataları kapsayan kategori hata ve benzeri biçimlendirir. |
| ErrorDownloadingInputAssetServiceFailure |Merhaba Hizmet tarafı - indirilirken örnek ağ veya depolama hataları sorunları kapsamaktadır hataları kategorisi. |
| ErrorParsingConfiguration |Kategori hataların nereye görev <see cref="MediaTask.PrivateData"/> (yapılandırma) geçerli değil, örneğin hello yapılandırması geçersiz XML içeriyor ya da geçerli bir sistem hazır değil. |
| ErrorExecutingTaskMalformedContent |Burada sorunları hello içinde medya dosyalarını başarısız olmasına neden giriş hello görevi hello yürütme sırasında hatalar kategorisi. |
| ErrorExecutingTaskUnsupportedFormat |Burada hello medya işlemcisi sağlanan hello dosyaları işleyemiyor - medya biçimlendirilmemesi hataların kategori desteklenen veya hello yapılandırması eşleşmiyor. Örneğin, yalnızca video sahip bir varlık bir salt ses çıkış tooproduce çalışıyor |
| ErrorProcessingTask |Medya işlemcisi hello diğer hataları kategorisini ilgisiz toocontent olan hello görev hello işlenmesi sırasında karşılaşır. |
| ErrorUploadingOutputAsset |Kategori hello çıkış varlığına karşıya yüklenirken hata |
| ErrorCancelingTask |Kategori toocancel hello görev çalışırken hataları toocover hatalar |
| TransientError |Kategori sorunların hatalarını toocover geçici (ör.) Azure Storage ile geçici ağ sorunları) |

Merhaba tooget Yardım **Media Services** takım, açık bir [destek bileti](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>İlgili makaleler
* [Medya Kodlayıcısı standart hazır özelleştirerek gelişmiş kodlama görevleri gerçekleştirme](media-services-custom-mes-presets-with-dotnet.md)
* [Kotalar ve kısıtlamaları](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
