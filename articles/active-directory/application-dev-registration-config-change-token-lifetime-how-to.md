---
title: "aaaHow toochange hello belirteç ömrü özel geliştirilmiş bir uygulama için varsayılan olarak | Microsoft Docs"
description: "Nasıl üzerinde Azure AD geliştirdiğiniz uygulamanız için tooupdate belirteç ömrü ilkeleri"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="11d1e-103">Nasıl toochange hello belirteç ömrü özel geliştirilmiş bir uygulama için varsayılanları</span><span class="sxs-lookup"><span data-stu-id="11d1e-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="11d1e-104">Azure AD Premium uygulama geliştiricileri ve Kiracı yöneticileri tooconfigure hello ömrü gizli olmayan istemciler için yayınlanan belirteçleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="11d1e-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="11d1e-105">Belirteç ömrü ilkeleri Kiracı genelinde veya erişilen hello kaynakların üzerinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="11d1e-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="11d1e-106">bir belirteç ömrü ilkesi tooset, gereksinim duyduğunuz toodownload hello [Azure AD PowerShell Modülü](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="11d1e-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="11d1e-107">Merhaba çalıştırmak **Connect-Azuread'i-Onayla** komutu.</span><span class="sxs-lookup"><span data-stu-id="11d1e-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="11d1e-108">Merhaba Maksimum yaş tek Faktörlü yenileme belirteci ayarlar bir örnek İlkesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="11d1e-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="11d1e-109">Hello ilkesi oluşturun:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="11d1e-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="11d1e-110">Checkout hello [yapılandırma belirteç ömrü](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) toolearn nasıl belge toocreate diğer özel.</span><span class="sxs-lookup"><span data-stu-id="11d1e-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11d1e-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11d1e-111">Next steps</span></span>
[<span data-ttu-id="11d1e-112">Belirteç ömrü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="11d1e-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="11d1e-113">Azure AD belirteç başvurusu</span><span class="sxs-lookup"><span data-stu-id="11d1e-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

