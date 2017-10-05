---
title: "Bir uygulama için oturum açarken beklenmeyen onay istemi | Microsoft Docs"
description: "Bir kullanıcı değil beklediğiniz neydi Azure AD ile tümleşik bir uygulama için bir onay istemi gördüğünde ile ilgili sorunları giderme"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="73cf3-103">Bir uygulama için oturum açarken beklenmeyen onay istemi</span><span class="sxs-lookup"><span data-stu-id="73cf3-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="73cf3-104">Azure Active Directory ile tümleştirme birçok uygulamaları çalıştırmak için çeşitli kaynaklara izinleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="73cf3-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="73cf3-105">Ne zaman bu kaynakları Azure Active Directory ile bunlara erişmek için izinleri de tümleştirilmiştir Azure AD onay framework kullanılarak istenir.</span><span class="sxs-lookup"><span data-stu-id="73cf3-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="73cf3-106">Bu tek seferlik bir işlem olduğu çoğunlukla ilk kez bir uygulama kullanıldığında, gösterilen bir onay istemi olan içinde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="73cf3-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="73cf3-107">Hangi kullanıcıların gördüğü senaryoları istemleri onayı</span><span class="sxs-lookup"><span data-stu-id="73cf3-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="73cf3-108">Ek istekler çeşitli senaryolarda beklenebilir:</span><span class="sxs-lookup"><span data-stu-id="73cf3-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="73cf3-109">Uygulama için gereken izinler kümesi değişti.</span><span class="sxs-lookup"><span data-stu-id="73cf3-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="73cf3-110">İlk olarak uygulamaya rıza kullanıcı yönetici değil ve farklı (yönetici olmayan) bir kullanıcı ilk kez uygulama artık kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="73cf3-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="73cf3-111">İlk olarak uygulamaya rıza kullanıcı için bir yönetici olsa da, bunlar tüm kuruluş ın adına izin değil.</span><span class="sxs-lookup"><span data-stu-id="73cf3-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="73cf3-112">Uygulamayı kullanarak [artımlı ve dinamik izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) onay başlangıçta verildi sonra ilave izin istemek için.</span><span class="sxs-lookup"><span data-stu-id="73cf3-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="73cf3-113">Ek bir uygulamanın isteğe bağlı özellikler ötesinde temel işlevleri için gereken izinleri gerektirir, bu genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73cf3-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="73cf3-114">Onay, başlangıçta verilmeden sonra iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="73cf3-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="73cf3-115">Geliştirici uygulamayı her kullanılışında bir onay istemi gerektirecek şekilde yapılandırılmış olduğundan (Not: Bu en iyi yöntem değildir).</span><span class="sxs-lookup"><span data-stu-id="73cf3-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73cf3-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73cf3-116">Next steps</span></span>

-   [<span data-ttu-id="73cf3-117">Uygulamalar, izinler ve onay Azure Active Directory'de (v1.0 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="73cf3-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="73cf3-118">Kapsam, izinleri ve onay Azure Active Directory'de (v2.0 uç noktası)</span><span class="sxs-lookup"><span data-stu-id="73cf3-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


