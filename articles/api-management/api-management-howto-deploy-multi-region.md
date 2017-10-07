---
title: "Azure API Management aaaDeploy Hizmetleri toomultiple Azure bölgeleri | Microsoft Docs"
description: "Nasıl toodeploy bir Azure API Management hizmet örneği toomultiple Azure öğrenin bölgeleri."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Nasıl toodeploy bir Azure API Management hizmet örneği toomultiple Azure bölgeleri
API Management istenen Azure bölgeleri herhangi bir sayıda arasında API yayımcılar toodistribute tek bir API management hizmeti sağlayan bölgeli dağıtımını destekler. Bu istek tarafından algılanan gecikme API tüketicileri coğrafi olarak dağıtılmış ve bir bölge çevrimdışı olursa hizmet kullanılabilirliği de geliştirir azaltılmasına yardımcı olur. 

Bir API Management hizmeti başlangıçta oluşturulduğunda, yalnızca bir tane içeriyor [birim] [ unit] ve hangi birincil bölge hello olarak atanmış bir tek Azure bölgesinde, bulunur. Ek bölgeler kolayca hello Azure Portal eklenebilir. Bir API Management ağ geçidi sunucusu dağıtılan tooeach bölgedir ve arama trafiği yönlendirilmiş toohello en yakın ağ geçidi olacaktır. Bir bölge çevrimdışı olması durumunda hello otomatik olarak yeniden yönlendirilmiş toohello sonraki en yakın ağ geçidi trafiğidir. 

> [!IMPORTANT]
> Bölgeli dağıtım kullanılabilir yalnızca hello  **[Premium] [ Premium]**  katmanı.
> 
> 

## <a name="add-region"></a>Bir API Management hizmeti örneği tooa yeni bölge dağıtma
> [!NOTE]
> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Toohello Hello Azure Portal gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası. 

![Ölçek sekmesi][api-management-scale-service]

toodeploy tooa yeni bölge, tıklatıldığında **+ Ekle bölge** hello araç çubuğundan.

![Bölgesi ekleme][api-management-add-region]

Merhaba aşağı açılan listeden Hello konum seçin ve hello kaydırıcı için birimleriyle hello sayısını ayarlayın.

![Birimler belirtin][api-management-select-location-units]

Tıklatın **Ekle** tooplace seçiminizi hello konumları tablosundaki. 

Yapılandırılan tüm konumları elde edene kadar bu işlemi yineleyin ve'ı tıklatın **kaydetmek** hello araç toostart hello dağıtım işlemi.

## <a name="remove-region"></a>Bir konumdan bir API Management hizmeti örneği Sil
Toohello Hello Azure Portal gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası. 

![Ölçek sekmesi][api-management-scale-service]

Gibi hello konumu tooremove hello kullanarak hello bağlam menüsünü açın **...**  düğmesi hello sağ ucunda hello tablo. Select hello **silmek** seçeneği.

![Bölgeyi Kaldır][api-management-remove-region]

Merhaba silmeyi onaylamak ve tıklayın **kaydetmek** tooapply hello değişiklikleri.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

