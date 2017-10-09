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
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Azure StorSimple’dan Azure Media Services hesabına dosya yükleme

Bu makalede Azure StorSimple Veri Yöneticisi'ne ilişkin kısa bir genel bakış sunulmaktadır. Merhaba makale ayrıca şunları nasıl yapacağınızı tootutorials bağlantıları StorSimple tooextract verileri ve bu verileri varlıklar tooan Azure Media Services (AMS) hesabı yükleyin.

> 
> [!NOTE]
> Azure StorSimple Veri Yöneticisi şu anda özel önizleme aşamasındadır. 
> 

## <a name="overview"></a>Genel Bakış

Media Services’de dijital dosyalar bir varlığa yüklenir. Merhaba varlık, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.) içerebilir. Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello uzantısı şirket içi çözüm ve otomatik olarak katmanlarını veri hello şirket içi depolama ve bulut depolama arasında gibi bulut depolama kullanır. Merhaba StorSimple cihazı dedupes ve verilerinizi büyük dosyalar toohello bulut göndermek için çok verimli hale getirme toohello bulut göndermeden önce sıkıştırır. Merhaba [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) hizmeti, StorSimple tooextract verileri sağlayan ve AMS varlıklar olarak sunmak API'ler sağlar.

## <a name="get-started"></a>başlarken

1. [Bir Media Services hesabı oluşturma](media-services-portal-create-account.md) tootransfer hello varlıklar istediğiniz.
2. Kaydolmak için veri Yöneticisi Önizleme, hello açıklandığı gibi [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) makalesi.
3. Bir StorSimple Veri Yöneticisi hesabı oluşturun.
4. Çalıştığında bir StorSimple cihazından verileri ayıklayıp varlık olarak AMS hesabına aktaran bir veri dönüşüm işi oluşturun. 

    Merhaba iş çalışmaya başladığında, depolama kuyruğu oluşturulur. Bu kuyruk, hazır olduğunda dönüştürülen bloblar hakkında iletilerle doldurulur. Bu sıranın Hello adı olduğu hello hello iş tanımı hello adı ile aynı. Bu sıra toodetermine kullandığınız zaman varlık olduğu gibi hazır ve üzerinde istenen Media Services işlemi toorun çağırın. Örneğin, bu kuyruk tootrigger hello gerekli Media Services kodu içeren bir Azure işlevi kullanabilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.

[Kullanım .net SDK hello hello Data Manager tootrigger işler](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz. Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).
