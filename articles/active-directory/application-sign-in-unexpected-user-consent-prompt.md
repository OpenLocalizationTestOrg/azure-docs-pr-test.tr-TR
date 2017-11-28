---
title: "tooan uygulamada oturum açarken aaaUnexpected onay istemi | Microsoft Docs"
description: "Nasıl bir kullanıcı bir uygulama için bir onay istemi gördüğünde tootroubleshoot, değil beklediğiniz neydi Azure AD ile tümleşik"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="61b06-103">Tooan uygulamada oturum açarken beklenmeyen onay istemi</span><span class="sxs-lookup"><span data-stu-id="61b06-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="61b06-104">Azure Active Directory ile tümleştirme pek çok uygulama sipariş toorun toovarious kaynaklarında izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="61b06-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="61b06-105">Bu kaynaklar ayrıca Azure Active Directory ile tümleşik olduğunda bunları istenen hello Azure AD kullanarak izinleri tooaccess framework olursunuz.</span><span class="sxs-lookup"><span data-stu-id="61b06-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="61b06-106">Bu, bir onay istemi hello tek seferlik bir işlem olduğu çoğunlukla bir uygulama kullanılır, ilk kez gösteriliyor sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="61b06-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="61b06-107">Hangi kullanıcıların gördüğü senaryoları istemleri onayı</span><span class="sxs-lookup"><span data-stu-id="61b06-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="61b06-108">Ek istekler çeşitli senaryolarda beklenebilir:</span><span class="sxs-lookup"><span data-stu-id="61b06-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="61b06-109">Merhaba uygulama için gereken izinleri Hello kümesi değişti.</span><span class="sxs-lookup"><span data-stu-id="61b06-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="61b06-110">Başlangıçta toohello uygulama rıza hello kullanıcı yönetici değil ve şimdi farklı (yönetici olmayan) bir kullanıcı Merhaba uygulaması hello için ilk kez kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="61b06-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="61b06-111">ilk olarak toohello uygulama rıza hello kullanıcı için bir yönetici olsa da, bunlar hello tüm kuruluş ın adına izin değil.</span><span class="sxs-lookup"><span data-stu-id="61b06-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="61b06-112">Merhaba uygulaması kullanarak [artımlı ve dinamik izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) onay başlangıçta verildi sonra toorequest ek izinler.</span><span class="sxs-lookup"><span data-stu-id="61b06-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="61b06-113">Ek bir uygulamanın isteğe bağlı özellikler ötesinde temel işlevleri için gereken izinleri gerektirir, bu genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61b06-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="61b06-114">Onay, başlangıçta verilmeden sonra iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="61b06-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="61b06-115">her kullanılışında Hello Geliştirici hello uygulama toorequire bir onay istemi yapılandırmamış (Not: Bu en iyi yöntem değildir).</span><span class="sxs-lookup"><span data-stu-id="61b06-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61b06-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61b06-116">Next steps</span></span>

-   [<span data-ttu-id="61b06-117">Uygulamalar, izinler ve onay Azure Active Directory'de (v1.0 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="61b06-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="61b06-118">Kapsam, izinleri ve hello Azure Active Directory (v2.0 uç noktası) onay</span><span class="sxs-lookup"><span data-stu-id="61b06-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


