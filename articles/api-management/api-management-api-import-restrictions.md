---
title: aaaRestrictions ve bilinen sorunlar Azure API Management API alma | Microsoft Docs
description: "Bilinen sorunlar ve Azure API Management hello açık API, WSDL veya WADL biçimlerini kullanarak içe kısıtlamalar ayrıntıları."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="f9ced-103">API içeri aktarma kısıtlamaları ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="f9ced-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="f9ced-104">Bu liste hakkında</span><span class="sxs-lookup"><span data-stu-id="f9ced-104">About this list</span></span>
<span data-ttu-id="f9ced-105">Her türlü çabayı tooensure yapılan sırada bu API'nizi Azure API Management alma olarak sorunsuzdur ve sorunsuz mümkün olduğunca biz bazen kısıtlamaları zorunlu tuttukları veya başarıyla içeri aktarmadan önce düzeltilinceye toobe gerektiren sorunları belirlemek.</span><span class="sxs-lookup"><span data-stu-id="f9ced-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="f9ced-106">Bu makalede, bu belgeleri hello alma biçimini hello API tarafından organize.</span><span class="sxs-lookup"><span data-stu-id="f9ced-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="f9ced-107"><a name="open-api"></a>API/Swagger açın</span><span class="sxs-lookup"><span data-stu-id="f9ced-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="f9ced-108">Açık API belgenizi alma hataları alıyorsanız, genel olarak, Lütfen, doğrulandı, - olun hello Tasarımcısını kullanarak, yeni Azure Portalı'nı (Tasarım - ön uç - açık API Belirtimi Düzenleyici) hello veya 3 ile aracı gibi taraf <a href="http://www.swagger.io"> Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="f9ced-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="f9ced-109">**Ana bilgisayar adı** biz bir ana bilgisayar adı özniteliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f9ced-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="f9ced-110">**Temel yolu** biz temel yolu özniteliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f9ced-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="f9ced-111">**Düzenleri** biz bir şema dizisi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f9ced-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="f9ced-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="f9ced-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="f9ced-113">WSDL dosyaları kullanılan toogenerate SOAP doğrudan API'ları, ya bir SOAP ve REST API'si arka hello olarak.</span><span class="sxs-lookup"><span data-stu-id="f9ced-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="f9ced-114">**WSDL: import** şu anda bu özniteliği kullanılarak API'leri desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f9ced-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="f9ced-115">Müşteriler, bir belgeye içe hello öğeleri birleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9ced-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="f9ced-116">**Birden çok bölümü olan iletiler** şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f9ced-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="f9ced-117">**WCF wsHttpBinding** Windows Communication Foundation ile oluşturulan SOAP Hizmetleri basicHttpBinding kullanması gereken - wsHttpBinding desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f9ced-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="f9ced-118">**MTOM** MTOM kullanan hizmetler <em>olabilir</em> çalışır.</span><span class="sxs-lookup"><span data-stu-id="f9ced-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="f9ced-119">Resmi desteği şu anda önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f9ced-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="f9ced-120">**Özyineleme** türlerini tanımlanan yinelemeli olarak (örneğin kendilerini tooan dizisi bakın) desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f9ced-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="f9ced-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="f9ced-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="f9ced-122">Şu anda hiçbir bilinen WADL alma sorunları vardır.</span><span class="sxs-lookup"><span data-stu-id="f9ced-122">There are no known WADL import issues currently.</span></span>


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
