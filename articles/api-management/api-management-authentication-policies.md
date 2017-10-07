---
title: "aaaAzure API Management kimlik doğrulama ilkeleri | Microsoft Docs"
description: "Azure API Management'te kullanıma hello kimlik doğrulama ilkeleri hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="314ea-103">API Management kimlik doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="314ea-103">API Management authentication policies</span></span>
<span data-ttu-id="314ea-104">Bu konuda API Management ilkelere hello için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="314ea-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="314ea-105">Ekleme ve ilkeleri yapılandırma hakkında daha fazla bilgi için bkz: [API Management ilkeleri](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="314ea-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="314ea-106"><a name="AuthenticationPolicies"></a>Kimlik doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="314ea-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="314ea-107">[Basic ile kimlik doğrulaması](api-management-authentication-policies.md#Basic) -temel kimlik doğrulaması kullanarak arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="314ea-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="314ea-108">[İstemci sertifikası ile kimlik doğrulaması](api-management-authentication-policies.md#ClientCertificate) -istemci sertifikalarını kullanan bir arka uç hizmeti ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="314ea-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="314ea-109"><a name="Basic"></a>Basic ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="314ea-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="314ea-110">Kullanım hello `authentication-basic` temel kimlik doğrulaması kullanarak arka uç hizmeti ile ilke tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="314ea-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="314ea-111">Bu ilke etkili bir şekilde hello HTTP yetkilendirme üstbilgisi toohello hello belirtilen değeri karşılık gelen toohello kimlik bilgilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="314ea-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="314ea-112">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="314ea-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="314ea-113">Örnek</span><span class="sxs-lookup"><span data-stu-id="314ea-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="314ea-114">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="314ea-114">Elements</span></span>  
  
|<span data-ttu-id="314ea-115">Ad</span><span class="sxs-lookup"><span data-stu-id="314ea-115">Name</span></span>|<span data-ttu-id="314ea-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="314ea-116">Description</span></span>|<span data-ttu-id="314ea-117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="314ea-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="314ea-118">kimlik doğrulama-temel</span><span class="sxs-lookup"><span data-stu-id="314ea-118">authentication-basic</span></span>|<span data-ttu-id="314ea-119">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="314ea-119">Root element.</span></span>|<span data-ttu-id="314ea-120">Evet</span><span class="sxs-lookup"><span data-stu-id="314ea-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="314ea-121">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="314ea-121">Attributes</span></span>  
  
|<span data-ttu-id="314ea-122">Ad</span><span class="sxs-lookup"><span data-stu-id="314ea-122">Name</span></span>|<span data-ttu-id="314ea-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="314ea-123">Description</span></span>|<span data-ttu-id="314ea-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="314ea-124">Required</span></span>|<span data-ttu-id="314ea-125">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="314ea-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="314ea-126">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="314ea-126">username</span></span>|<span data-ttu-id="314ea-127">Merhaba kullanıcı hello temel kimlik bilgisi adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="314ea-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="314ea-128">Evet</span><span class="sxs-lookup"><span data-stu-id="314ea-128">Yes</span></span>|<span data-ttu-id="314ea-129">Yok</span><span class="sxs-lookup"><span data-stu-id="314ea-129">N/A</span></span>|  
|<span data-ttu-id="314ea-130">password</span><span class="sxs-lookup"><span data-stu-id="314ea-130">password</span></span>|<span data-ttu-id="314ea-131">Merhaba temel kimlik bilgisi Hello parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="314ea-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="314ea-132">Evet</span><span class="sxs-lookup"><span data-stu-id="314ea-132">Yes</span></span>|<span data-ttu-id="314ea-133">Yok</span><span class="sxs-lookup"><span data-stu-id="314ea-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="314ea-134">Kullanım</span><span class="sxs-lookup"><span data-stu-id="314ea-134">Usage</span></span>  
 <span data-ttu-id="314ea-135">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="314ea-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="314ea-136">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="314ea-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="314ea-137">**İlke kapsamları:** API</span><span class="sxs-lookup"><span data-stu-id="314ea-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="314ea-138"><a name="ClientCertificate"></a>İstemci sertifikası ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="314ea-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="314ea-139">Kullanım hello `authentication-certificate` istemci sertifikasını kullanarak bir arka uç hizmeti ile ilke tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="314ea-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="314ea-140">Merhaba sertifikanın gerekir toobe [API yönetime yüklü](http://go.microsoft.com/fwlink/?LinkID=511599) ilk ve kendi parmak izi tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="314ea-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="314ea-141">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="314ea-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="314ea-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="314ea-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="314ea-143">Öğeleri</span><span class="sxs-lookup"><span data-stu-id="314ea-143">Elements</span></span>  
  
|<span data-ttu-id="314ea-144">Ad</span><span class="sxs-lookup"><span data-stu-id="314ea-144">Name</span></span>|<span data-ttu-id="314ea-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="314ea-145">Description</span></span>|<span data-ttu-id="314ea-146">Gerekli</span><span class="sxs-lookup"><span data-stu-id="314ea-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="314ea-147">kimlik doğrulama sertifikası</span><span class="sxs-lookup"><span data-stu-id="314ea-147">authentication-certificate</span></span>|<span data-ttu-id="314ea-148">Kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="314ea-148">Root element.</span></span>|<span data-ttu-id="314ea-149">Evet</span><span class="sxs-lookup"><span data-stu-id="314ea-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="314ea-150">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="314ea-150">Attributes</span></span>  
  
|<span data-ttu-id="314ea-151">Ad</span><span class="sxs-lookup"><span data-stu-id="314ea-151">Name</span></span>|<span data-ttu-id="314ea-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="314ea-152">Description</span></span>|<span data-ttu-id="314ea-153">Gerekli</span><span class="sxs-lookup"><span data-stu-id="314ea-153">Required</span></span>|<span data-ttu-id="314ea-154">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="314ea-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="314ea-155">parmak izi</span><span class="sxs-lookup"><span data-stu-id="314ea-155">thumbprint</span></span>|<span data-ttu-id="314ea-156">Merhaba istemci sertifikası parmak izi hello.</span><span class="sxs-lookup"><span data-stu-id="314ea-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="314ea-157">Evet</span><span class="sxs-lookup"><span data-stu-id="314ea-157">Yes</span></span>|<span data-ttu-id="314ea-158">Yok</span><span class="sxs-lookup"><span data-stu-id="314ea-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="314ea-159">Kullanım</span><span class="sxs-lookup"><span data-stu-id="314ea-159">Usage</span></span>  
 <span data-ttu-id="314ea-160">Bu ilkeyi ilke aşağıdaki hello kullanılabilir [bölümleri](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) ve [kapsamları](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="314ea-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="314ea-161">**İlke bölümleri:** gelen</span><span class="sxs-lookup"><span data-stu-id="314ea-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="314ea-162">**İlke kapsamları:** API</span><span class="sxs-lookup"><span data-stu-id="314ea-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="314ea-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="314ea-163">Next steps</span></span>
<span data-ttu-id="314ea-164">İlkeleriyle çalışma daha fazla bilgi için bkz: [API Management ilkeleri](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="314ea-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  