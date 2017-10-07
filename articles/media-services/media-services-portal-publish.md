---
title: "aaa\"Merhaba Azure portal ile içerik yayımlama | Microsoft Docs\""
description: "Bu öğreticide, içeriğinizi hello Azure portal ile yayımlama hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>İçerik hello Azure portal ile yayımlama
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Genel Bakış
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide kullanılan toostream ya da içeriğinizi indirme URL'si, kullanıcı, önce çok "varlığınız bir Bulucu oluşturarak yayımlamanız". Bulucular hello varlıkta bulunan erişim toofiles sağlar. Media Services iki tür bulucuyu destekler: 

* Akış (OnDemandOrigin) bulucuları, (örneğin, toostream MPEG DASH, HLS veya kesintisiz akış) Uyarlamalı akış için kullanılır. toocreate akış Bulucusu varlığınız bir .ism dosyası içermelidir. 
* Aşamalı indirme aracılığıyla video teslimi için kullanılan aşamalı (SAS) bulucular.

Bir akış URL'si biçimi aşağıdaki hello sahiptir ve tooplay kesintisiz akış varlıklarını kullanın.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS akış URL'si, bir toobuild ekleme (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

bir akış URL'si, MPEG DASH toobuild ekleme (biçim mpd zaman csf =) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Bir SAS URL'si biçimi aşağıdaki hello sahiptir.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Daha fazla bilgi için bkz: [içerik genel bakış sunan](media-services-deliver-content-overview.md).

> [!NOTE]
> Mart 2015 öncesinde hello portal toocreate bulucular kullandıysanız, iki yıl sona erme tarihi olan bulucular oluşturulmuştur.  
> 
> 

Kullanım Bulucunun sona erme tarihi bir tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) veya [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API'leri. Bir SAS Bulucu hello sona erme tarihini güncelleştirdiğinizde hello URL'nin değiştiğini unutmayın.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portal toopublish bir varlığı
toouse hello portal toopublish bir varlık hello aşağıdaki:

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. **Ayarlar** > **Varlıklar**’ı seçin.
3. Merhaba varlık toopublish istediğinizi seçin.
4. Merhaba tıklatın **Yayımla** düğmesi.
5. Merhaba Bulucu türünü seçin.
6. **Ekle**’ye basın.
   
    ![Yayımlama](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Merhaba URL toohello listesi eklenecek **yayımlanan URL'ler**.

## <a name="play-content-from-hello-portal"></a>Merhaba portaldan içerik oynatma
Hello Azure portalı bir içerik oynatıcı sağlar videonuzu tootest kullanabilirsiniz.

İstenen hello videoya tıklayın ve hello ardından **Yürüt** düğmesi.

![Yayımlama](./media/media-services-portal-vod-get-started/media-services-play.png)

Bazı dikkate alınması gereken noktalar vardır:

* Merhaba video yayımlandığından emin olun.
* Bu **Media player** hello varsayılan akış uç noktasından oynatır. Varsayılan olmayan tooplay istiyorsanız akış uç noktası, toocopy hello URL'yi tıklatın ve başka bir oynatıcı kullanın. Örneğin, [Azure Media Services Oynatıcı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Akış uç noktası akış hello çalıştırması gerekir.  

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

