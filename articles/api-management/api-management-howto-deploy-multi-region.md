---
title: "Birden çok Azure bölgeler ile Azure API Management services dağıtma | Microsoft Docs"
description: "Azure API Management hizmet örneği için birden fazla Azure bölgesine dağıtmayı öğrenin."
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
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="52358-103">Azure API Management hizmet örneği birden çok Azure bölgeler ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="52358-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="52358-104">API Management istenen Azure bölgeleri herhangi bir sayıda arasında tek bir API management hizmeti dağıtmak API yayımcılar sağlayan bölgeli dağıtımını destekler.</span><span class="sxs-lookup"><span data-stu-id="52358-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="52358-105">Bu istek tarafından algılanan gecikme API tüketicileri coğrafi olarak dağıtılmış ve bir bölge çevrimdışı olursa hizmet kullanılabilirliği de geliştirir azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="52358-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="52358-106">Bir API Management hizmeti başlangıçta oluşturulduğunda, yalnızca bir tane içeriyor [birim] [ unit] ve birincil bölge belirlenmiş tek bir Azure bölgesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="52358-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="52358-107">Ek bölgeler kolayca Azure Portalı aracılığıyla eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="52358-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="52358-108">Bir API Management ağ geçidi sunucusu her bölgeye dağıtılır ve arama trafiği için en yakın ağ geçidi yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="52358-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="52358-109">Bir bölge çevrimdışı olursa, otomatik olarak sonraki en yakın ağ geçidine yeniden yönlendirilmiş bir trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="52358-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="52358-110">Bölgeli dağıtım bulunan yalnızca  **[Premium] [ Premium]**  katmanı.</span><span class="sxs-lookup"><span data-stu-id="52358-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="52358-111"><a name="add-region"></a>API Management hizmet örneği için yeni bir bölge dağıtma</span><span class="sxs-lookup"><span data-stu-id="52358-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="52358-112">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="52358-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="52358-113">Azure Portalı'nda gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası.</span><span class="sxs-lookup"><span data-stu-id="52358-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Ölçek sekmesi][api-management-scale-service]

<span data-ttu-id="52358-115">Yeni bir bölgeye dağıtmayı tıklayın **+ Ekle bölge** araç çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="52358-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Bölgesi ekleme][api-management-add-region]

<span data-ttu-id="52358-117">Aşağı açılan listeden konumu seçin ve kaydırıcı ile birim sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="52358-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Birimler belirtin][api-management-select-location-units]

<span data-ttu-id="52358-119">Tıklatın **Ekle** konumlar tablosunda seçiminizi yerleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="52358-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="52358-120">Yapılandırılan tüm konumları elde edene kadar bu işlemi yineleyin ve'ı tıklatın **kaydetmek** dağıtım işlemini başlatmak için araç çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="52358-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="52358-121"><a name="remove-region"></a>Bir konumdan bir API Management hizmeti örneği Sil</span><span class="sxs-lookup"><span data-stu-id="52358-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="52358-122">Azure Portalı'nda gidin **ölçek ve fiyatlandırma** , API Management hizmet örneğinizin sayfası.</span><span class="sxs-lookup"><span data-stu-id="52358-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Ölçek sekmesi][api-management-scale-service]

<span data-ttu-id="52358-124">Kaldırmak istediğiniz konumu için bağlam menüsünü kullanarak açın **...**  tablo sağ ucunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="52358-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="52358-125">Seçin **silmek** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="52358-125">Select the **Delete** option.</span></span>

![Bölgeyi Kaldır][api-management-remove-region]

<span data-ttu-id="52358-127">Silme işlemini onaylamak ve tıklayın **kaydetmek** değişiklikleri uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="52358-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

