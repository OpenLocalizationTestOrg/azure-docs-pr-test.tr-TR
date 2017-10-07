---
title: "aaaScale medya kodlama birimleri - Azure ekleyerek işleme |  Microsoft Docs"
description: "Bilgi nasıl toohow tooadd kodlama birimleri .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Nasıl tooscale .NET SDK'sı ile kodlama
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> Tooreview hello emin olun [genel bakış](media-services-scale-media-processing-overview.md) konu tooget konu işleme medya ölçeklendirme hakkında daha fazla bilgi.
> 
> 

.NET SDK kullanarak ayrılan birimler kodlama toochange hello ayrılmış birim türü ve hello sayısı hello aşağıdaki:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Bir destek bileti açmadan
Varsayılan olarak her Media Services hesabı tooup too25 ölçeklendirebilirsiniz kodlama ve 5 isteğe bağlı akışa ayrılan birimler. Bir destek bileti açılarak daha yüksek bir sınır isteyebilir.

### <a name="open-a-support-ticket"></a>Bir destek bileti açın
tooopen bir destek bileti hello aşağıdaki:

1. Tıklatın [alma desteği](https://manage.windowsazure.com/?getsupport=true). Açmadınız ederseniz kimlik bilgileriniz istendiğinde tooenter olabilir.
2. Aboneliğinizi seçin.
3. Destek türü'nün altında "Teknik" seçin.
4. "Bilet oluştur" seçeneğini tıklatın.
5. "Azure medya hello sonraki sayfada sunulan hizmetler" Merhaba ürün listesinde seçin.
6. "Sorun türü" seçin sorununuz için uygun olan.
7. Devam Et'i tıklatın.
8. Sonraki sayfasındaki yönergeleri izleyin ve sorunu ayrıntılarını girin.
9. Tooopen hello bilet Gönder'e tıklayın.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

