---
title: Bir API Azure API Management alma | Microsoft Docs
description: "Bir API ve işlemlerini Azure API Management içeri aktarmayı öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="98e8b-103">Azure API Management işlemleri olan bir API tanımını içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="98e8b-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="98e8b-104">API Management, yeni API'leri oluşturulabilir ve el ile eklenmiş operations veya API işlemlerini tek bir adımda birlikte içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="98e8b-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="98e8b-105">API'ler ve bunların işlemler aşağıdaki biçimlerden kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="98e8b-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="98e8b-106">WADL</span><span class="sxs-lookup"><span data-stu-id="98e8b-106">WADL</span></span>
* <span data-ttu-id="98e8b-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="98e8b-107">Swagger</span></span>

<span data-ttu-id="98e8b-108">Bu kılavuz gösterir yeni bir API oluşturma ve işlemlerini tek bir adımda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="98e8b-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="98e8b-109">El ile bir API oluşturma ve işlemleri ekleme hakkında daha fazla bilgi için bkz: [API oluşturma] [ How to create APIs] ve [API'ye işlem ekleme][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="98e8b-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="98e8b-110"><a name="import-api"> </a>Bir API'yi içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="98e8b-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="98e8b-111">API oluşturulur ve yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="98e8b-112">Yayımcı portalına erişmek için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="98e8b-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="98e8b-113">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="98e8b-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="98e8b-115">Tıklatın **API'leri** gelen **API Management** sol menüsünde ve ardından **API'yi içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="98e8b-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![İçeri aktarma API'si][api-management-import-apis]

<span data-ttu-id="98e8b-117">**İçeri aktarma API'si** penceresinde API belirtimine sağlamak için üç yol karşılık gelen üç sekme bulunur.</span><span class="sxs-lookup"><span data-stu-id="98e8b-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="98e8b-118">**Pano'dan** API belirtimine belirlenen metin kutusuna yapıştırın olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="98e8b-119">**Dosyadan** göz atın ve API belirtimine içeren dosyayı seçin olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="98e8b-120">**URL'den** API belirtimine URL sağlamanız olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![API'yi İçeri Aktar biçimi][api-management-import-api-clipboard]

<span data-ttu-id="98e8b-122">API belirtimine sağladıktan sonra radyo düğmelerinin sağ tarafta belirtimi biçimini belirtmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="98e8b-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="98e8b-123">Aşağıdaki biçimleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98e8b-123">The following formats are supported.</span></span>

* <span data-ttu-id="98e8b-124">WADL</span><span class="sxs-lookup"><span data-stu-id="98e8b-124">WADL</span></span>
* <span data-ttu-id="98e8b-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="98e8b-125">Swagger</span></span>

<span data-ttu-id="98e8b-126">Ardından, girin bir **Web API'si URL soneki**.</span><span class="sxs-lookup"><span data-stu-id="98e8b-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="98e8b-127">Bu API management hizmetiniz için temel URL eklenir.</span><span class="sxs-lookup"><span data-stu-id="98e8b-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="98e8b-128">Temel URL her bir API Management hizmet örneği üzerinde barındırılan tüm API'leri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="98e8b-129">API Management API'leri kendi soneki ayırır ve bu nedenle soneki belirli bir API management hizmet örneğindeki her API için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98e8b-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="98e8b-130">Tüm değerleri girdikten sonra tıklayın **kaydetmek** API ve ilişkili operations oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="98e8b-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="98e8b-131">Swagger biçiminde temel hesaplayıcı API'sini içeri aktarma bir öğretici için bkz: [ilk API'nizi Azure API Management'te yönetme](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="98e8b-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="98e8b-132"><a name="export-api"></a> Bir API dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="98e8b-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="98e8b-133">Yeni API'ları alma yanı sıra Apı'lerinizi tanımlarını yayımcı Portalı'ndan dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98e8b-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="98e8b-134">Bunu yapmak için tıklatın **verme API** gelen **Özet sekmesi** biri, **API**.</span><span class="sxs-lookup"><span data-stu-id="98e8b-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![API dışarı aktarma][api-management-export-api]

<span data-ttu-id="98e8b-136">API WADL veya Swagger kullanılarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="98e8b-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="98e8b-137">İstenen biçim seçin, **kaydetmek**ve dosyanın kaydedileceği konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="98e8b-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Dışa aktarma API biçimi][api-management-export-api-format]

## <span data-ttu-id="98e8b-139"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98e8b-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="98e8b-140">Bir API oluşturulur ve içe işlemleri, gözden geçirin ve yapılandırabilirsiniz sonra herhangi bir ek ayarı bir ürüne API ekleme ve böylece geliştiriciler için kullanılabilir yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="98e8b-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="98e8b-141">Daha fazla bilgi için aşağıdaki kılavuzlara bakın.</span><span class="sxs-lookup"><span data-stu-id="98e8b-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="98e8b-142">[API ayarlarını yapılandırma][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="98e8b-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="98e8b-143">[Oluşturma ve bir ürün yayımlama][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="98e8b-143">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
