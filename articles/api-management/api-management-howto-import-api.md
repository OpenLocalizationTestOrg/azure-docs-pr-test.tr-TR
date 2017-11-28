---
title: "aaaImport bir API uygulamasına Azure API Management | Microsoft Docs"
description: "Bilgi nasıl tooimport bir API ve Azure API Management içine işlemlerini."
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
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="6a195-103">Nasıl tooimport hello Azure API Management işlemleri olan bir API tanımı</span><span class="sxs-lookup"><span data-stu-id="6a195-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="6a195-104">API Management, yeni API'leri oluşturulabilir ve hello işlemleri el ile eklenmiş veya hello API hello işlemlerini tek bir adımda birlikte içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="6a195-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="6a195-105">API'ler ve bunların işlemler biçimleri aşağıdaki hello kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="6a195-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="6a195-106">WADL</span><span class="sxs-lookup"><span data-stu-id="6a195-106">WADL</span></span>
* <span data-ttu-id="6a195-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="6a195-107">Swagger</span></span>

<span data-ttu-id="6a195-108">Bu kılavuz gösterir yeni bir API oluşturma ve işlemlerini tek bir adımda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="6a195-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="6a195-109">El ile bir API oluşturma ve işlemleri ekleme hakkında daha fazla bilgi için bkz: [nasıl toocreate API'leri] [ How toocreate APIs] ve [nasıl tooadd işlemleri tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="6a195-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="6a195-110"><a name="import-api"> </a>Bir API'yi içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="6a195-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="6a195-111">API oluşturulur ve hello yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="6a195-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="6a195-112">tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="6a195-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="6a195-113">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="6a195-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="6a195-115">Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API'yi içeri aktarma**.</span><span class="sxs-lookup"><span data-stu-id="6a195-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![İçeri aktarma API'si][api-management-import-apis]

<span data-ttu-id="6a195-117">Merhaba **içeri aktarma API'si** penceresinde toohello üç yolu tooprovide hello API Belirtimi karşılık gelen üç sekme bulunur.</span><span class="sxs-lookup"><span data-stu-id="6a195-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="6a195-118">**Pano'dan** hello belirlenen metin kutusuna toopaste hello API belirtimine izin verir.</span><span class="sxs-lookup"><span data-stu-id="6a195-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="6a195-119">**Dosyadan** hello API belirtimi içeren toobrowse tooand select hello dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a195-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="6a195-120">**URL'den** toosupply hello URL toohello belirtimi hello API sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a195-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![API'yi İçeri Aktar biçimi][api-management-import-api-clipboard]

<span data-ttu-id="6a195-122">Merhaba API Belirtimi sağladıktan sonra hello radyo düğmeleri hello sağ tooindicate hello belirtimi biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a195-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="6a195-123">biçimler aşağıdaki hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6a195-123">hello following formats are supported.</span></span>

* <span data-ttu-id="6a195-124">WADL</span><span class="sxs-lookup"><span data-stu-id="6a195-124">WADL</span></span>
* <span data-ttu-id="6a195-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="6a195-125">Swagger</span></span>

<span data-ttu-id="6a195-126">Ardından, girin bir **Web API'si URL soneki**.</span><span class="sxs-lookup"><span data-stu-id="6a195-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="6a195-127">API management hizmetiniz için temel URL eklenmiş toohello budur.</span><span class="sxs-lookup"><span data-stu-id="6a195-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="6a195-128">Her bir API Management hizmet örneği üzerinde barındırılan tüm API'leri Hello temel URL yaygındır.</span><span class="sxs-lookup"><span data-stu-id="6a195-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="6a195-129">API Management API'leri kendi soneki ayırır ve bu nedenle hello soneki belirli bir API management hizmet örneğindeki her API için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6a195-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="6a195-130">Tüm değerleri girdikten sonra tıklayın **kaydetmek** toocreate hello API ve hello ilişkili işlemleri.</span><span class="sxs-lookup"><span data-stu-id="6a195-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a195-131">Swagger biçiminde temel hesaplayıcı API'sini içeri aktarma bir öğretici için bkz: [ilk API'nizi Azure API Management'te yönetme](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a195-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="6a195-132"><a name="export-api"></a> Bir API dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="6a195-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="6a195-133">Ayrıca tooimporting, yeni API'leri, Apı'lerinizi hello tanımlarını hello yayımcı Portalı'ndan verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a195-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="6a195-134">Bu nedenle, toodo'ı tıklatın **verme API** hello gelen **Özet sekmesi** , **API**.</span><span class="sxs-lookup"><span data-stu-id="6a195-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![API dışarı aktarma][api-management-export-api]

<span data-ttu-id="6a195-136">API WADL veya Swagger kullanılarak verilebilir.</span><span class="sxs-lookup"><span data-stu-id="6a195-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="6a195-137">Merhaba istediğiniz biçimi seçin, **kaydetmek**ve hangi toosave hello dosyasında hello konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="6a195-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Dışa aktarma API biçimi][api-management-export-api-format]

## <span data-ttu-id="6a195-139"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a195-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="6a195-140">Bir API oluşturulur ve içe hello işlemleri, gözden geçirin ve yapılandırabilirsiniz sonra herhangi bir ek ayarı hello API tooa ürün ekleyin ve böylece geliştiriciler için kullanılabilir yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6a195-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="6a195-141">Daha fazla bilgi için aşağıdaki kılavuzları hello bakın.</span><span class="sxs-lookup"><span data-stu-id="6a195-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="6a195-142">[Nasıl tooconfigure API ayarları][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="6a195-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="6a195-143">[Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="6a195-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
