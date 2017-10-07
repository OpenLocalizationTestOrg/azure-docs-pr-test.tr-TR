---
title: "aaaAzure API Management sayfası denetimleri | Microsoft Docs"
description: "Azure API Management'ta Geliştirici Portalı şablonlarındaki kullanıma hello sayfa denetimleri hakkında bilgi edinin."
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="cc0ef-103">Azure API Management sayfası denetimleri</span><span class="sxs-lookup"><span data-stu-id="cc0ef-103">Azure API Management page controls</span></span>
<span data-ttu-id="cc0ef-104">Azure API Management denetimleri şablonlarda hello Geliştirici Portalı aşağıdaki hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="cc0ef-105">toouse bir denetim yerleştirin, istenen hello konumda hello Geliştirici Portalı şablonunda.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="cc0ef-106">Hello gibi bazı denetimler [uygulama eylemleri](#app-actions) denetlemek, parametreleri, hello aşağıdaki örnekte gösterildiği gibi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="cc0ef-107">Merhaba parametrelerin Hello değerleri içinde hello veri modeli hello şablonu için bir parçası olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="cc0ef-108">Çoğu durumda, yalnızca yapıştırabilirsiniz hello sağlanan örnek için her denetim için toowork doğru.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="cc0ef-109">Merhaba parametre değerleri ile ilgili daha fazla bilgi için denetim kullanılabilir her şablon için hello veri modeli bölümünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="cc0ef-110">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="cc0ef-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="cc0ef-111">Geliştirici Portalı şablonuna sayfa denetimleri</span><span class="sxs-lookup"><span data-stu-id="cc0ef-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="cc0ef-112">Uygulama eylemleri</span><span class="sxs-lookup"><span data-stu-id="cc0ef-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="cc0ef-113">temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="cc0ef-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="cc0ef-114">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="cc0ef-115">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="cc0ef-116">arama denetimi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="cc0ef-117">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="cc0ef-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="cc0ef-118">Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="cc0ef-119">aboneliği iptal etme</span><span class="sxs-lookup"><span data-stu-id="cc0ef-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="cc0ef-120"><a name="app-actions"></a>Uygulama eylemleri</span><span class="sxs-lookup"><span data-stu-id="cc0ef-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="cc0ef-121">Merhaba `app-actions` denetim hello kullanıcı profili sayfasında hello Geliştirici Portalı'nda uygulamalarla etkileşim için bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cc0ef-122">![uygulamanın &#45; Eylemler denetim](./media/api-management-page-controls/APIM-app-actions-control.png "APIM uygulama eylemleri denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-123">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-124">Parameters</span></span>  
  
|<span data-ttu-id="cc0ef-125">Parametre</span><span class="sxs-lookup"><span data-stu-id="cc0ef-125">Parameter</span></span>|<span data-ttu-id="cc0ef-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc0ef-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cc0ef-127">AppID</span><span class="sxs-lookup"><span data-stu-id="cc0ef-127">appId</span></span>|<span data-ttu-id="cc0ef-128">Merhaba uygulaması Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-129">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-129">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-130">Merhaba `app-actions` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-131">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="cc0ef-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="cc0ef-132"><a name="basic-signin"></a>temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="cc0ef-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="cc0ef-133">Merhaba `basic-signin` Denetim toplama kullanıcı oturum açma bilgilerini hello içinde hello Geliştirici Portalı'ndaki sayfasında oturum için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cc0ef-134">![Basic &#45; oturum açma denetimi](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic oturum açma denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-135">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-136">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-136">Parameters</span></span>  
 <span data-ttu-id="cc0ef-137">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-138">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-138">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-139">Merhaba `basic-signin` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-140">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="cc0ef-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cc0ef-141"><a name="paging-control"></a>disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="cc0ef-142">Merhaba `paging-control` sayfalama işlevselliğinin Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cc0ef-143">![Denetim disk belleği](./media/api-management-page-controls/APIM-paging-control.png "APIM disk belleği denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-144">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-145">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-145">Parameters</span></span>  
 <span data-ttu-id="cc0ef-146">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-147">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-147">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-148">Merhaba `paging-control` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-149">API listesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cc0ef-150">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="cc0ef-151">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cc0ef-152"><a name="providers"></a>sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="cc0ef-153">Merhaba `providers` denetim hello oturum açma sayfası hello Geliştirici Portalı'nda kimlik doğrulama sağlayıcıları seçimi için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cc0ef-154">![sağlayıcıları Denetim](./media/api-management-page-controls/APIM-providers-control.png "APIM sağlayıcıları denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-155">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-156">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-156">Parameters</span></span>  
 <span data-ttu-id="cc0ef-157">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-158">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-158">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-159">Merhaba `providers` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-160">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="cc0ef-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cc0ef-161"><a name="search-control"></a>arama denetimi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="cc0ef-162">Merhaba `search-control` arama işlevini Geliştirici öğelerinin bir listesini görüntülemek portal sayfalarına sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cc0ef-163">![Arama denetim](./media/api-management-page-controls/APIM-search-control.png "APIM arama denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-164">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-165">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-165">Parameters</span></span>  
 <span data-ttu-id="cc0ef-166">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-167">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-167">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-168">Merhaba `search-control` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-169">API listesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cc0ef-170">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cc0ef-171"><a name="sign-up"></a>Kaydolma</span><span class="sxs-lookup"><span data-stu-id="cc0ef-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="cc0ef-172">Merhaba `sign-up` denetim hello kayıt sayfasını hello Geliştirici Portalı'nda kullanıcı profili bilgilerini toplamak için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cc0ef-173">![oturum &#45; yukarı denetim](./media/api-management-page-controls/APIM-sign-up-control.png "APIM kayıt denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-174">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-175">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-175">Parameters</span></span>  
 <span data-ttu-id="cc0ef-176">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-177">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-177">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-178">Merhaba `sign-up` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-179">Kaydol</span><span class="sxs-lookup"><span data-stu-id="cc0ef-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="cc0ef-180"><a name="subscribe-button"></a>Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="cc0ef-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="cc0ef-181">Merhaba `subscribe-button` bir kullanıcı tooa ürüne abone olmak için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="cc0ef-182">![Abone &#45; düğme denetimi](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abone düğmesi denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-183">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-184">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-184">Parameters</span></span>  
 <span data-ttu-id="cc0ef-185">yok.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-186">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-186">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-187">Merhaba `subscribe-button` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-188">Ürün</span><span class="sxs-lookup"><span data-stu-id="cc0ef-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="cc0ef-189"><a name="subscription-cancel"></a>aboneliği iptal etme</span><span class="sxs-lookup"><span data-stu-id="cc0ef-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="cc0ef-190">Merhaba `subscription-cancel` denetim hello kullanıcı profili sayfasını hello Geliştirici Portalı'nda bir abonelik tooa üründe iptal etmek için bir denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cc0ef-191">![Abonelik &#45; denetim iptal](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM aboneliği iptal denetimi")</span><span class="sxs-lookup"><span data-stu-id="cc0ef-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc0ef-192">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc0ef-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc0ef-193">Parametreler</span><span class="sxs-lookup"><span data-stu-id="cc0ef-193">Parameters</span></span>  
  
|<span data-ttu-id="cc0ef-194">Parametre</span><span class="sxs-lookup"><span data-stu-id="cc0ef-194">Parameter</span></span>|<span data-ttu-id="cc0ef-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc0ef-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cc0ef-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc0ef-196">subscriptionId</span></span>|<span data-ttu-id="cc0ef-197">Merhaba abonelik toocancel Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="cc0ef-198">CancelUrl</span><span class="sxs-lookup"><span data-stu-id="cc0ef-198">cancelUrl</span></span>|<span data-ttu-id="cc0ef-199">Merhaba aboneliği iptal etmeniz URL.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc0ef-200">Geliştirici Portalı şablonları</span><span class="sxs-lookup"><span data-stu-id="cc0ef-200">Developer portal templates</span></span>  
 <span data-ttu-id="cc0ef-201">Merhaba `subscription-cancel` denetlemek Geliştirici Portalı şablonları aşağıdaki hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc0ef-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc0ef-202">Ürün</span><span class="sxs-lookup"><span data-stu-id="cc0ef-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="cc0ef-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc0ef-203">Next steps</span></span>
<span data-ttu-id="cc0ef-204">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cc0ef-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
