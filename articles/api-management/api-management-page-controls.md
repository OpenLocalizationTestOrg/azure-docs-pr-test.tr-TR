---
title: "Azure API Management sayfası denetimleri | Microsoft Docs"
description: "Azure API Management'ta Geliştirici Portalı şablonlarındaki kullanıma sayfa denetimleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="cce27-103">Azure API Management sayfası denetimleri</span><span class="sxs-lookup"><span data-stu-id="cce27-103">Azure API Management page controls</span></span>
<span data-ttu-id="cce27-104">Azure API Management portal şablonları aşağıdaki denetimleri Geliştirici kullanmak için sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="cce27-105">Bir denetimi kullanmak için Geliştirici Portalı şablonuna istediğiniz konuma yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="cce27-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="cce27-106">Gibi bazı denetimleri [uygulama eylemleri](#app-actions) denetlemek, parametreleri, aşağıdaki örnekte gösterildiği gibi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cce27-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="cce27-107">Parametreler için değerler olarak şablonu için veri modelinin parçası olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="cce27-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="cce27-108">Çoğu durumda, yalnızca düzgün çalışabilmesi için her denetim için sağlanan örnekte yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cce27-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="cce27-109">Parametre değerleri hakkında daha fazla bilgi için denetim kullanılabilir her şablon için veri modeli bölümünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cce27-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="cce27-110">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="cce27-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="cce27-111">Geliştirici Portalı şablonuna sayfa denetimleri</span><span class="sxs-lookup"><span data-stu-id="cce27-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="cce27-112">Uygulama eylemleri</span><span class="sxs-lookup"><span data-stu-id="cce27-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="cce27-113">temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="cce27-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="cce27-114">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="cce27-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="cce27-115">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="cce27-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="cce27-116">arama denetimi</span><span class="sxs-lookup"><span data-stu-id="cce27-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="cce27-117">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="cce27-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="cce27-118">Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="cce27-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="cce27-119">aboneliği iptal etme</span><span class="sxs-lookup"><span data-stu-id="cce27-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="cce27-120"><a name="app-actions"></a>Uygulama eylemleri</span><span class="sxs-lookup"><span data-stu-id="cce27-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="cce27-121">`app-actions` Denetimi Geliştirici Portalı'ndaki kullanıcı profili sayfasında uygulamalarla etkileşim için bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="cce27-122">![uygulamanın &#45; Eylemler denetim](./media/api-management-page-controls/APIM-app-actions-control.png "APIM uygulama eylemleri denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-123">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-124">Parameters</span></span>  
  
|<span data-ttu-id="cce27-125">Parametre</span><span class="sxs-lookup"><span data-stu-id="cce27-125">Parameter</span></span>|<span data-ttu-id="cce27-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cce27-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cce27-127">AppID</span><span class="sxs-lookup"><span data-stu-id="cce27-127">appId</span></span>|<span data-ttu-id="cce27-128">Uygulama kimliği.</span><span class="sxs-lookup"><span data-stu-id="cce27-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-129">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-129">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-130">`app-actions` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-131">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="cce27-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="cce27-132"><a name="basic-signin"></a>temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="cce27-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="cce27-133">`basic-signin` Denetimi, kullanıcı oturum açma oturum açma sayfası Geliştirici Portalı'ndaki bilgileri toplamak için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="cce27-134">![Basic &#45; oturum açma denetimi](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic oturum açma denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-135">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-136">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-136">Parameters</span></span>  
 <span data-ttu-id="cce27-137">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-138">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-138">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-139">`basic-signin` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-140">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="cce27-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cce27-141"><a name="paging-control"></a>disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="cce27-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="cce27-142">`paging-control` Sayfalama işlevselliğinin Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cce27-143">![Denetim disk belleği](./media/api-management-page-controls/APIM-paging-control.png "APIM disk belleği denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-144">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-145">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-145">Parameters</span></span>  
 <span data-ttu-id="cce27-146">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-147">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-147">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-148">`paging-control` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-149">API listesi</span><span class="sxs-lookup"><span data-stu-id="cce27-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cce27-150">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="cce27-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="cce27-151">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="cce27-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cce27-152"><a name="providers"></a>sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="cce27-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="cce27-153">`providers` Denetim, oturum açma sayfasında Geliştirici Portalı'nda kimlik doğrulama sağlayıcıları seçimi için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="cce27-154">![sağlayıcıları Denetim](./media/api-management-page-controls/APIM-providers-control.png "APIM sağlayıcıları denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-155">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-156">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-156">Parameters</span></span>  
 <span data-ttu-id="cce27-157">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-158">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-158">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-159">`providers` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-160">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="cce27-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cce27-161"><a name="search-control"></a>arama denetimi</span><span class="sxs-lookup"><span data-stu-id="cce27-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="cce27-162">`search-control` Arama işlevini Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cce27-163">![Arama denetim](./media/api-management-page-controls/APIM-search-control.png "APIM arama denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-164">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-165">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-165">Parameters</span></span>  
 <span data-ttu-id="cce27-166">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-167">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-167">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-168">`search-control` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-169">API listesi</span><span class="sxs-lookup"><span data-stu-id="cce27-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cce27-170">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="cce27-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cce27-171"><a name="sign-up"></a>Kaydolma</span><span class="sxs-lookup"><span data-stu-id="cce27-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="cce27-172">`sign-up` Denetim kayıt sayfasını Geliştirici Portalı'nda kullanıcı profili bilgilerini toplamak için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="cce27-173">![oturum &#45; yukarı denetim](./media/api-management-page-controls/APIM-sign-up-control.png "APIM kayıt denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-174">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-175">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-175">Parameters</span></span>  
 <span data-ttu-id="cce27-176">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-177">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-177">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-178">`sign-up` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-179">Kaydol</span><span class="sxs-lookup"><span data-stu-id="cce27-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="cce27-180"><a name="subscribe-button"></a>Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="cce27-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="cce27-181">`subscribe-button` Bir kullanıcı bir ürüne abone olmak için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="cce27-182">![Abone &#45; düğme denetimi](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abone düğmesi denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-183">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-184">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-184">Parameters</span></span>  
 <span data-ttu-id="cce27-185">yok.</span><span class="sxs-lookup"><span data-stu-id="cce27-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-186">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-186">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-187">`subscribe-button` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-188">Ürün</span><span class="sxs-lookup"><span data-stu-id="cce27-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="cce27-189"><a name="subscription-cancel"></a>aboneliği iptal etme</span><span class="sxs-lookup"><span data-stu-id="cce27-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="cce27-190">`subscription-cancel` Denetim Geliştirici Portalı'ndaki kullanıcı profili sayfasında ürün aboneliği iptal etmek için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cce27-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="cce27-191">![Abonelik &#45; denetim iptal](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM aboneliği iptal denetimi")</span><span class="sxs-lookup"><span data-stu-id="cce27-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cce27-192">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cce27-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="cce27-193">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cce27-193">Parameters</span></span>  
  
|<span data-ttu-id="cce27-194">Parametre</span><span class="sxs-lookup"><span data-stu-id="cce27-194">Parameter</span></span>|<span data-ttu-id="cce27-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cce27-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cce27-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cce27-196">subscriptionId</span></span>|<span data-ttu-id="cce27-197">İptal etmek için abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="cce27-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="cce27-198">CancelUrl</span><span class="sxs-lookup"><span data-stu-id="cce27-198">cancelUrl</span></span>|<span data-ttu-id="cce27-199">Aboneliği iptal URL'si.</span><span class="sxs-lookup"><span data-stu-id="cce27-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cce27-200">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cce27-200">Developer portal templates</span></span>  
 <span data-ttu-id="cce27-201">`subscription-cancel` Denetimi aşağıdaki Geliştirici Portalı şablonlarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cce27-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cce27-202">Ürün</span><span class="sxs-lookup"><span data-stu-id="cce27-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="cce27-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cce27-203">Next steps</span></span>
<span data-ttu-id="cce27-204">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cce27-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>