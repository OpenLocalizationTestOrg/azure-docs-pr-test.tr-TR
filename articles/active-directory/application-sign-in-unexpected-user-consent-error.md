---
title: "Bir uygulama onay gerçekleştirirken beklenmeyen bir hata | Microsoft Docs"
description: "Bir uygulamaya ve bunları hakkında neler yapabileceğinizi onaylıyorsunuz işlemi sırasında oluşabilecek hatalar açıklanır"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fd500fdd4c8642bad96dcf71eebcf1fad461a35f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="366c4-103">Bir uygulama onay gerçekleştirirken beklenmeyen bir hata</span><span class="sxs-lookup"><span data-stu-id="366c4-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="366c4-104">Bu makalede, bir uygulamaya onaylıyorsunuz işlemi sırasında oluşabilecek hatalar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="366c4-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="366c4-105">Sorun giderme beklenmeyen varsa, onay ister olmayan herhangi bir hata iletisi içeren bkz [Azure AD için kimlik doğrulama senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="366c4-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="366c4-106">Azure Active Directory ile tümleştirme pek çok uygulama çalışması için diğer kaynaklara erişim izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="366c4-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="366c4-107">Ne zaman bu kaynakları Azure Active Directory ile bunlara erişmek için izinleri de tümleşiktir genellikle ortak izin framework kullanılarak istenir.</span><span class="sxs-lookup"><span data-stu-id="366c4-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="366c4-108">Bu, genellikle bir uygulama kullanılır ancak uygulama üzerinde bir sonraki kullanımı da oluşabilir ilk kez ortaya çıkan görüntülenmesini, bir onay istemi sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="366c4-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="366c4-109">Belirli bir kullanıcının gerektiren bir uygulama izinleri onayı koşulların karşılanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="366c4-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="366c4-110">Bu koşullar karşılanmazsa, çeşitli hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="366c4-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="366c4-111">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="366c4-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="366c4-112">Yetki verilmemiş izinleri hata isteme</span><span class="sxs-lookup"><span data-stu-id="366c4-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="366c4-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; olduğunuz bir veya daha fazla izinler yetkisi vermek istiyor.</span><span class="sxs-lookup"><span data-stu-id="366c4-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="366c4-114">Bu uygulama, sizin adınıza onayı bir yönetici, başvurun.</span><span class="sxs-lookup"><span data-stu-id="366c4-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="366c4-115">Şirket Yöneticisi olmayan bir kullanıcı yalnızca bir yönetici verebilirsiniz izinleri isteyen bir uygulamayı kullanmaya çalıştığında bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="366c4-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="366c4-116">Bu hata, uygulama kendi kuruluş adına erişim verilirken bir yönetici tarafından çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="366c4-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="366c4-117">İlke engeller izin verme hatası</span><span class="sxs-lookup"><span data-stu-id="366c4-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="366c4-118">**AADSTS90093:** yönetici &lt;tenantDisplayName&gt; atamanızı engeller bir ilke ayarladığı &lt;uygulama adını&gt; , istediği izinleri.</span><span class="sxs-lookup"><span data-stu-id="366c4-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="366c4-119">Bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;, kimin sizin adınıza bu uygulama izin verme.</span><span class="sxs-lookup"><span data-stu-id="366c4-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="366c4-120">Bu hata, yönetici olmayan bir kullanıcı onay gerektiren bir uygulama kullanma girişiminde sonra kabul uygulamalara, kullanıcılara şirket Yöneticisi kapatır oluşur.</span><span class="sxs-lookup"><span data-stu-id="366c4-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="366c4-121">Bu hata, uygulama kendi kuruluş adına erişim verilirken bir yönetici tarafından çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="366c4-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="366c4-122">Aralıklı sorun hata</span><span class="sxs-lookup"><span data-stu-id="366c4-122">Intermittent problem error</span></span>
* <span data-ttu-id="366c4-123">**AADSTS90090:** çalıştığınız vermek için izinleri kaydı aralıklı bir sorunla karşılaştık gibi görünüyor &lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="366c4-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="366c4-124">Daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="366c4-124">try again later.</span></span>

<span data-ttu-id="366c4-125">Bu hata, bir aralıklı Hizmet tarafı sorunu oluştuğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="366c4-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="366c4-126">Uygulamayı yeniden kabul deneyerek çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="366c4-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="366c4-127">Kaynak kullanılamaz hatası</span><span class="sxs-lookup"><span data-stu-id="366c4-127">Resource not available error</span></span>
* <span data-ttu-id="366c4-128">**AADSTS65005:** uygulama &lt;clientAppDisplayName&gt; bir kaynağa erişmek için izinleri istenen &lt;resourceAppDisplayName&gt; kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="366c4-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="366c4-129">Uygulama geliştiricisine başvurun.</span><span class="sxs-lookup"><span data-stu-id="366c4-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="366c4-130">Kaynak Kiracı hata mevcut değil</span><span class="sxs-lookup"><span data-stu-id="366c4-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="366c4-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; bir kaynağa erişim isteğinde &lt;resourceAppDisplayName&gt; , kuruluşunuzda mevcut değil &lt; tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="366c4-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="366c4-132">Bu kaynak kullanılabilir olduğundan emin olun veya bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="366c4-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="366c4-133">İzinleri uyuşmazlığı hatası</span><span class="sxs-lookup"><span data-stu-id="366c4-133">Permissions mismatch error</span></span>
* <span data-ttu-id="366c4-134">**AADSTS65005:** uygulama istenen kaynağa erişim izni &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="366c4-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="366c4-135">Uygulama uygulama kaydı sırasında önceden yapılandırılmış nasıl eşleşmediğinden bu isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="366c4-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="366c4-136">Uygulama vendor.* * başvurun</span><span class="sxs-lookup"><span data-stu-id="366c4-136">Contact the app vendor.**</span></span>

<span data-ttu-id="366c4-137">Bir kullanıcı için onay çalışılırken uygulama (Kiracı) kuruluşunuzun dizininde bulunan bir kaynak uygulamaya erişim izni isterken tüm ortaya bu hatalar.</span><span class="sxs-lookup"><span data-stu-id="366c4-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="366c4-138">Bu, çeşitli nedenlerle oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="366c4-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="366c4-139">İstemci uygulama geliştiricisi uygulamasına yanlış, geçersiz bir kaynak için erişim istemek için neden yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="366c4-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="366c4-140">Bu durumda, uygulama geliştiricisi bu sorunu çözmek için istemci uygulaması yapılandırmasını güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="366c4-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="366c4-141">Hedef kaynak uygulama temsil eden bir hizmet sorumlusu kuruluşunuzda mevcut değil veya geçmişte vardı ancak kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="366c4-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="366c4-142">İstemci uygulaması izinlere isteyebilir bu sorunu çözmek için kaynak uygulama için bir hizmet sorumlusu kuruluşta sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="366c4-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="366c4-143">Bir uygulamanın türüne bağlı olarak yol sayısı cinsinden durum olabilir dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="366c4-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="366c4-144">(Microsoft yayımlanan uygulamaları) kaynak uygulama için bir abonelik alınıyor</span><span class="sxs-lookup"><span data-stu-id="366c4-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="366c4-145">Kaynak uygulamaya onaylıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="366c4-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="366c4-146">Azure Portalı aracılığıyla uygulama izin verme</span><span class="sxs-lookup"><span data-stu-id="366c4-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="366c4-147">Azure AD uygulama galerisinden uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="366c4-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="366c4-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="366c4-148">Next steps</span></span> 

[<span data-ttu-id="366c4-149">Uygulamalar, izinler ve onay Azure Active Directory'de (v1 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="366c4-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="366c4-150">Kapsam, izinleri ve onay Azure Active Directory'de (v2.0 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="366c4-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


