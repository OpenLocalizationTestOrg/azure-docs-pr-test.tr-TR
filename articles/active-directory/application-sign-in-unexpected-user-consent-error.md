---
title: "onay tooan uygulama gerçekleştirilirken beklenmeyen hata aaa | Microsoft Docs"
description: "Onaylıyorsunuz tooan uygulama ve bunları hakkında neler yapabileceğinizi hello işlemi sırasında oluşabilecek hatalar açıklanır"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a><span data-ttu-id="a4c50-103">Onay tooan uygulama gerçekleştirirken beklenmeyen bir hata</span><span class="sxs-lookup"><span data-stu-id="a4c50-103">Unexpected error when performing consent tooan application</span></span>

<span data-ttu-id="a4c50-104">Bu makalede onaylıyorsunuz tooan uygulama hello işlemi sırasında oluşabilecek hatalar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="a4c50-104">This article discusses errors that can occur during hello process of consenting tooan application.</span></span> <span data-ttu-id="a4c50-105">Sorun giderme beklenmeyen varsa, onay ister olmayan herhangi bir hata iletisi içeren bkz [Azure AD için kimlik doğrulama senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="a4c50-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="a4c50-106">Azure Active Directory ile tümleştirme pek çok uygulama izinleri tooaccess sipariş toofunction diğer kaynaklar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-106">Many applications that integrate with Azure Active Directory require permissions tooaccess other resources in order toofunction.</span></span> <span data-ttu-id="a4c50-107">Bu kaynaklar ayrıca Azure Active Directory ile tümleşik olduğunda, bunları sık istenen hello ortak kullanarak izinleri tooaccess framework olursunuz.</span><span class="sxs-lookup"><span data-stu-id="a4c50-107">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is often requested using hello common consent framework.</span></span> 

<span data-ttu-id="a4c50-108">Bu, genellikle bir uygulama kullanılır ancak Merhaba uygulaması üzerinde bir sonraki kullanımı da oluşabilir ilk kez hello oluşan görüntülenmesini, bir onay istemi sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a4c50-108">This results in a consent prompt being displayed, which generally occurs hello first time an application is used but can also occur on a subsequent use of hello application.</span></span>

<span data-ttu-id="a4c50-109">Belirli koşullar uygulama gerektiren kullanıcı tooconsent toohello izinlerini doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-109">Certain conditions must be true for a user tooconsent toohello permissions an application requires.</span></span> <span data-ttu-id="a4c50-110">Bu koşullar karşılanmazsa, çeşitli hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="a4c50-111">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="a4c50-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="a4c50-112">Yetki verilmemiş izinleri hata isteme</span><span class="sxs-lookup"><span data-stu-id="a4c50-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="a4c50-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; çalıştığınız bir veya daha fazla izinler yetkili toogrant istiyor.</span><span class="sxs-lookup"><span data-stu-id="a4c50-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized toogrant.</span></span> <span data-ttu-id="a4c50-114">Kimin toothis uygulama sizin adınıza onayı bir yöneticiye başvurun.</span><span class="sxs-lookup"><span data-stu-id="a4c50-114">Contact an administrator, who can consent toothis application on your behalf.</span></span>

<span data-ttu-id="a4c50-115">Şirket Yöneticisi olmayan bir kullanıcı toouse yalnızca bir yönetici verebilirsiniz izinleri isteyen bir uygulama çalıştığında bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="a4c50-115">This error occurs when a user who is not a company administrator attempts toouse an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="a4c50-116">Bu hata, verme erişim toohello uygulama kuruluşu adına bir yönetici tarafından çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-116">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="a4c50-117">İlke engeller izin verme hatası</span><span class="sxs-lookup"><span data-stu-id="a4c50-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="a4c50-118">**AADSTS90093:** yönetici &lt;tenantDisplayName&gt; atamanızı engeller bir ilke ayarladığı &lt;uygulama adını&gt; Merhaba, istediği izinleri.</span><span class="sxs-lookup"><span data-stu-id="a4c50-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; hello permissions it is requesting.</span></span> <span data-ttu-id="a4c50-119">Bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;, kimin izinleri toothis uygulama sizin adınıza vermek.</span><span class="sxs-lookup"><span data-stu-id="a4c50-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions toothis app on your behalf.</span></span>

<span data-ttu-id="a4c50-120">Kullanıcıların tooconsent tooapplications hello yeteneği şirket Yöneticisi kapatır toouse onay gerektiren bir uygulama yönetici olmayan kullanıcı deneyip daha sonra bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="a4c50-120">This error occurs when a company administrator turns off hello ability for users tooconsent tooapplications, then a non-administrator user attempts toouse an application that requires consent.</span></span> <span data-ttu-id="a4c50-121">Bu hata, verme erişim toohello uygulama kuruluşu adına bir yönetici tarafından çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-121">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="a4c50-122">Aralıklı sorun hata</span><span class="sxs-lookup"><span data-stu-id="a4c50-122">Intermittent problem error</span></span>
* <span data-ttu-id="a4c50-123">**AADSTS90090:** çalıştığınız toogrant çok hello izinleri kaydı aralıklı bir sorunla karşılaştık gibi görünüyor&lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="a4c50-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording hello permissions you attempted toogrant too&lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="a4c50-124">Daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a4c50-124">try again later.</span></span>

<span data-ttu-id="a4c50-125">Bu hata, bir aralıklı Hizmet tarafı sorunu oluştuğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="a4c50-126">Tooconsent toohello uygulamayı yeniden deneyerek çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-126">It can be resolved by attempting tooconsent toohello application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="a4c50-127">Kaynak kullanılamaz hatası</span><span class="sxs-lookup"><span data-stu-id="a4c50-127">Resource not available error</span></span>
* <span data-ttu-id="a4c50-128">**AADSTS65005:** hello uygulama &lt;clientAppDisplayName&gt; izinleri tooaccess bir kaynağın istenen &lt;resourceAppDisplayName&gt; kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="a4c50-128">**AADSTS65005:** hello app &lt;clientAppDisplayName&gt; requested permissions tooaccess a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="a4c50-129">Merhaba uygulama geliştiricisine başvurun.</span><span class="sxs-lookup"><span data-stu-id="a4c50-129">Contact hello application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="a4c50-130">Kaynak Kiracı hata mevcut değil</span><span class="sxs-lookup"><span data-stu-id="a4c50-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="a4c50-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; erişim tooa kaynak isteyen &lt;resourceAppDisplayName&gt; , kuruluşunuzda mevcut değil &lt; tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="a4c50-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access tooa resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="a4c50-132">Bu kaynak kullanılabilir olduğundan emin olun veya bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="a4c50-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="a4c50-133">İzinleri uyuşmazlığı hatası</span><span class="sxs-lookup"><span data-stu-id="a4c50-133">Permissions mismatch error</span></span>
* <span data-ttu-id="a4c50-134">**AADSTS65005:** hello uygulama istenen onay tooaccess kaynak &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="a4c50-134">**AADSTS65005:** hello app requested consent tooaccess resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="a4c50-135">Merhaba app uygulama kaydı sırasında önceden yapılandırılmış nasıl eşleşmediğinden bu isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="a4c50-135">This request failed because it does not match how hello app was pre-configured during app registration.</span></span> <span data-ttu-id="a4c50-136">Kişi hello uygulama vendor.* *</span><span class="sxs-lookup"><span data-stu-id="a4c50-136">Contact hello app vendor.**</span></span>

<span data-ttu-id="a4c50-137">Merhaba uygulaması tooconsent toois izinleri tooaccess (Kiracı) hello kuruluşunuzun dizininde bulunan bir kaynak uygulaması isteyen kullanıcı çalışırken tüm bu hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="a4c50-137">These errors all occur when hello application a user is trying tooconsent toois requesting permissions tooaccess a resource application that cannot be found in hello organization’s directory (tenant).</span></span> <span data-ttu-id="a4c50-138">Bu, çeşitli nedenlerle oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="a4c50-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="a4c50-139">Merhaba istemci uygulaması geliştirici kendi uygulama toorequest erişim tooan geçersiz kaynak neden yanlış yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="a4c50-139">hello client application developer has configured their application incorrectly, causing it toorequest access tooan invalid resource.</span></span> <span data-ttu-id="a4c50-140">Bu durumda, hello uygulama geliştiricisinin bu sorunu hello istemci uygulaması tooresolve hello yapılandırmasını güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4c50-140">In this case, hello application developer must update hello configuration of hello client application tooresolve this issue.</span></span>

-   <span data-ttu-id="a4c50-141">Merhaba hedef kaynak uygulaması temsil eden bir hizmet sorumlusu hello kuruluşunuzda mevcut değil veya hello geçmiş vardı ancak kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a4c50-141">A Service Principal representing hello target resource application does not exist in hello organization, or existed in hello past but has been removed.</span></span> <span data-ttu-id="a4c50-142">Bu sorun, bir hizmet sorumlusu Merhaba istemci uygulaması izinleri tooit isteyebilir Merhaba kaynak uygulaması hello kuruluşta sağlanmalıdır için tooresolve.</span><span class="sxs-lookup"><span data-stu-id="a4c50-142">tooresolve this issue, a Service Principal for hello resource application must be provisioned in hello organization so hello client application can request permissions tooit.</span></span> <span data-ttu-id="a4c50-143">Uygulamanın, hello türüne bağlı olarak çeşitli yollarla bir numarasında durum olabilir dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="a4c50-143">This can happen in an number of ways, depending on hello type of application, including:</span></span>

    -   <span data-ttu-id="a4c50-144">Merhaba kaynak uygulaması (Microsoft yayımlanan uygulamaları) için bir abonelik alınıyor</span><span class="sxs-lookup"><span data-stu-id="a4c50-144">Acquiring a subscription for hello resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="a4c50-145">Onaylıyorsunuz toohello kaynak uygulama</span><span class="sxs-lookup"><span data-stu-id="a4c50-145">Consenting toohello resource application</span></span>

    -   <span data-ttu-id="a4c50-146">Hello Azure Portal aracılığıyla Hello uygulama izin verme</span><span class="sxs-lookup"><span data-stu-id="a4c50-146">Granting hello application permissions via hello Azure Portal</span></span>

    -   <span data-ttu-id="a4c50-147">Azure AD uygulama galerisinde hello Hello uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="a4c50-147">Adding hello application from hello Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4c50-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4c50-148">Next steps</span></span> 

[<span data-ttu-id="a4c50-149">Uygulamalar, izinler ve onay Azure Active Directory'de (v1 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="a4c50-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="a4c50-150">Kapsam, izinleri ve hello Azure Active Directory (v2.0 uç noktası) onay</span><span class="sxs-lookup"><span data-stu-id="a4c50-150">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


