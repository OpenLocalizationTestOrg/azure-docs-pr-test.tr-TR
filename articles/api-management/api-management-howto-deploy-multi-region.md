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
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="523f6-103">Nasıl toodeploy bir Azure API Management hizmet örneği toomultiple Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="523f6-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="523f6-104">API Management istenen Azure bölgeleri herhangi bir sayıda arasında API yayımcılar toodistribute tek bir API management hizmeti sağlayan bölgeli dağıtımını destekler.</span><span class="sxs-lookup"><span data-stu-id="523f6-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="523f6-105">Bu istek tarafından algılanan gecikme API tüketicileri coğrafi olarak dağıtılmış ve bir bölge çevrimdışı olursa hizmet kullanılabilirliği de geliştirir azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="523f6-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="523f6-106">Bir API Management hizmeti başlangıçta oluşturulduğunda, yalnızca bir tane içeriyor [birim] [ unit] ve hangi birincil bölge hello olarak atanmış bir tek Azure bölgesinde, bulunur.</span><span class="sxs-lookup"><span data-stu-id="523f6-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="523f6-107">Ek bölgeler kolayca hello Azure Portal eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="523f6-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="523f6-108">Bir API Management ağ geçidi sunucusu dağıtılan tooeach bölgedir ve arama trafiği yönlendirilmiş toohello en yakın ağ geçidi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="523f6-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="523f6-109">Bir bölge çevrimdışı olması durumunda hello otomatik olarak yeniden yönlendirilmiş toohello sonraki en yakın ağ geçidi trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="523f6-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="523f6-110">Bölgeli dağıtım kullanılabilir yalnızca hello  **[Premium] [ Premium]**  katmanı.</span><span class="sxs-lookup"><span data-stu-id="523f6-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="523f6-111"><a name="add-region"></a>Bir API Management hizmeti örneği tooa yeni bölge dağıtma</span><span class="sxs-lookup"><span data-stu-id="523f6-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="523f6-112">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="523f6-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="523f6-113">Toohello Hello Azure Portal gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası.</span><span class="sxs-lookup"><span data-stu-id="523f6-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Ölçek sekmesi][api-management-scale-service]

<span data-ttu-id="523f6-115">toodeploy tooa yeni bölge, tıklatıldığında **+ Ekle bölge** hello araç çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="523f6-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Bölgesi ekleme][api-management-add-region]

<span data-ttu-id="523f6-117">Merhaba aşağı açılan listeden Hello konum seçin ve hello kaydırıcı için birimleriyle hello sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="523f6-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Birimler belirtin][api-management-select-location-units]

<span data-ttu-id="523f6-119">Tıklatın **Ekle** tooplace seçiminizi hello konumları tablosundaki.</span><span class="sxs-lookup"><span data-stu-id="523f6-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="523f6-120">Yapılandırılan tüm konumları elde edene kadar bu işlemi yineleyin ve'ı tıklatın **kaydetmek** hello araç toostart hello dağıtım işlemi.</span><span class="sxs-lookup"><span data-stu-id="523f6-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="523f6-121"><a name="remove-region"></a>Bir konumdan bir API Management hizmeti örneği Sil</span><span class="sxs-lookup"><span data-stu-id="523f6-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="523f6-122">Toohello Hello Azure Portal gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası.</span><span class="sxs-lookup"><span data-stu-id="523f6-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Ölçek sekmesi][api-management-scale-service]

<span data-ttu-id="523f6-124">Gibi hello konumu tooremove hello kullanarak hello bağlam menüsünü açın **...**  düğmesi hello sağ ucunda hello tablo.</span><span class="sxs-lookup"><span data-stu-id="523f6-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="523f6-125">Select hello **silmek** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="523f6-125">Select hello **Delete** option.</span></span>

![Bölgeyi Kaldır][api-management-remove-region]

<span data-ttu-id="523f6-127">Merhaba silmeyi onaylamak ve tıklayın **kaydetmek** tooapply hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="523f6-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

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

