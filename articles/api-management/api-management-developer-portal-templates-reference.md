---
title: "Azure API Management Geliştirici Portalı şablonları | Microsoft Docs"
description: "Azure API Management'te şablonları kümesi kullanılarak Geliştirici portal sayfalarına içeriğini özelleştirmeyi öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 5189f3d8-2a4c-4dc8-ab19-11c7df0114d4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dc3f32a3cff2e66a798bd8f6c19c6b56a47643ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-developer-portal-templates"></a><span data-ttu-id="0c86a-103">Azure API Management Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="0c86a-103">Azure API Management Developer Portal Templates</span></span>
<span data-ttu-id="0c86a-104">Azure API Management Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriği özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c86a-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="0c86a-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve düzenleyiciyi, gibi [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfa denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde sayfaların yapılandırmak için büyük esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="0c86a-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="0c86a-106">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0c86a-106">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  



  
##  <span data-ttu-id="0c86a-107"><a name="DeveloperPortalTemplates"></a>Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="0c86a-107"><a name="DeveloperPortalTemplates"></a> Developer portal templates</span></span>  
  
-   [<span data-ttu-id="0c86a-108">API'ler</span><span class="sxs-lookup"><span data-stu-id="0c86a-108">APIs</span></span>](api-management-api-templates.md)  
    -   [<span data-ttu-id="0c86a-109">API listesi</span><span class="sxs-lookup"><span data-stu-id="0c86a-109">API list</span></span>](api-management-api-templates.md#APIList)  
    -   [<span data-ttu-id="0c86a-110">İşlem</span><span class="sxs-lookup"><span data-stu-id="0c86a-110">Operation</span></span>](api-management-api-templates.md#Product)  
    -   [<span data-ttu-id="0c86a-111">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="0c86a-111">Code samples</span></span>](api-management-api-templates.md#CodeSamples)  
        -   [<span data-ttu-id="0c86a-112">Curl</span><span class="sxs-lookup"><span data-stu-id="0c86a-112">Curl</span></span>](api-management-api-templates.md#Curl)  
        -   [<span data-ttu-id="0c86a-113">C#</span><span class="sxs-lookup"><span data-stu-id="0c86a-113">C#</span></span>](api-management-api-templates.md#CSharp)  
        -   [<span data-ttu-id="0c86a-114">Java</span><span class="sxs-lookup"><span data-stu-id="0c86a-114">Java</span></span>](api-management-api-templates.md#Stub)  
        -   [<span data-ttu-id="0c86a-115">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0c86a-115">JavaScript</span></span>](api-management-api-templates.md#JavaScript)  
        -   [<span data-ttu-id="0c86a-116">Objective C</span><span class="sxs-lookup"><span data-stu-id="0c86a-116">Objective C</span></span>](api-management-api-templates.md#ObjectiveC)  
        -   [<span data-ttu-id="0c86a-117">PHP</span><span class="sxs-lookup"><span data-stu-id="0c86a-117">PHP</span></span>](api-management-api-templates.md#PHP)  
        -   [<span data-ttu-id="0c86a-118">Python</span><span class="sxs-lookup"><span data-stu-id="0c86a-118">Python</span></span>](api-management-api-templates.md#Python)  
        -   [<span data-ttu-id="0c86a-119">Ruby</span><span class="sxs-lookup"><span data-stu-id="0c86a-119">Ruby</span></span>](api-management-api-templates.md#Ruby)  
-   [<span data-ttu-id="0c86a-120">Ürünler</span><span class="sxs-lookup"><span data-stu-id="0c86a-120">Products</span></span>](api-management-product-templates.md)  
    -   [<span data-ttu-id="0c86a-121">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="0c86a-121">Product list</span></span>](api-management-product-templates.md#ProductList)  
    -   [<span data-ttu-id="0c86a-122">Ürün</span><span class="sxs-lookup"><span data-stu-id="0c86a-122">Product</span></span>](api-management-product-templates.md#Product)  
-   [<span data-ttu-id="0c86a-123">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="0c86a-123">Applications</span></span>](api-management-application-templates.md)  
    -   [<span data-ttu-id="0c86a-124">Uygulama listesi</span><span class="sxs-lookup"><span data-stu-id="0c86a-124">Application list</span></span>](api-management-application-templates.md#ProductList)  
    -   [<span data-ttu-id="0c86a-125">Uygulama</span><span class="sxs-lookup"><span data-stu-id="0c86a-125">Application</span></span>](api-management-application-templates.md#Application)  
-   [<span data-ttu-id="0c86a-126">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="0c86a-126">Issues</span></span>](api-management-issue-templates.md)  
    -   [<span data-ttu-id="0c86a-127">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="0c86a-127">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
-   [<span data-ttu-id="0c86a-128">Kullanıcı profili</span><span class="sxs-lookup"><span data-stu-id="0c86a-128">User Profile</span></span>](api-management-user-profile-templates.md)  
    -   [<span data-ttu-id="0c86a-129">Profili</span><span class="sxs-lookup"><span data-stu-id="0c86a-129">Profile</span></span>](api-management-user-profile-templates.md#Profile)  
    -   [<span data-ttu-id="0c86a-130">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="0c86a-130">Subscriptions</span></span>](api-management-user-profile-templates.md#Subscriptions)  
    -   [<span data-ttu-id="0c86a-131">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="0c86a-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
    -   [<span data-ttu-id="0c86a-132">Hesap bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="0c86a-132">Update account info</span></span>](api-management-user-profile-templates.md#UpdateAccountInfo)  
-   [<span data-ttu-id="0c86a-133">Sayfalar</span><span class="sxs-lookup"><span data-stu-id="0c86a-133">Pages</span></span>](api-management-page-templates.md)  
    -   [<span data-ttu-id="0c86a-134">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="0c86a-134">Sign in</span></span>](api-management-page-templates.md#SignIn)  
    -   [<span data-ttu-id="0c86a-135">Kaydol</span><span class="sxs-lookup"><span data-stu-id="0c86a-135">Sign up</span></span>](api-management-page-templates.md#SignUp)  
    -   [<span data-ttu-id="0c86a-136">Sayfa bulunamadı</span><span class="sxs-lookup"><span data-stu-id="0c86a-136">Page not found</span></span>](api-management-page-templates.md#PageNotFound)


## <a name="next-steps"></a><span data-ttu-id="0c86a-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c86a-137">Next steps</span></span>  
-   [<span data-ttu-id="0c86a-138">Şablon başvurusu</span><span class="sxs-lookup"><span data-stu-id="0c86a-138">Template reference</span></span>](api-management-developer-portal-templates-reference.md)  
-   [<span data-ttu-id="0c86a-139">Veri modeli başvurusu</span><span class="sxs-lookup"><span data-stu-id="0c86a-139">Data model reference</span></span>](api-management-template-data-model-reference.md)  
-   [<span data-ttu-id="0c86a-140">Sayfa denetimleri</span><span class="sxs-lookup"><span data-stu-id="0c86a-140">Page controls</span></span>](api-management-page-controls.md)  
-   [<span data-ttu-id="0c86a-141">Şablon kaynakları</span><span class="sxs-lookup"><span data-stu-id="0c86a-141">Template resources</span></span>](api-management-template-resources.md)