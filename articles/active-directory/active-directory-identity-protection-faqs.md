---
title: "aaaAzure Active Directory kimlik koruması ile ilgili SSS | Microsoft Docs"
description: "Azure AD kimlik koruması ile ilgili sık sorulan sorular"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="56a6f-103">Azure Active Directory kimlik koruması ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="56a6f-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="56a6f-104">Neden bazı risk olayları "Kapalı (Sistem)" durum var mı?</span><span class="sxs-lookup"><span data-stu-id="56a6f-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="56a6f-105">**Y:** bu Azure Active Directory kimlik koruması algıladı ve hello olayları artık riskli olduğu kabul için daha sonra kapattı olaylardır.</span><span class="sxs-lookup"><span data-stu-id="56a6f-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="56a6f-106">Bu olaylar hello kullanıcının risk düzeyi sayılmaz.</span><span class="sxs-lookup"><span data-stu-id="56a6f-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="56a6f-107">Toobe hello Azure portalında bir genel yönetici toouse kimlik koruması gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="56a6f-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="56a6f-108">**Y:** **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="56a6f-108">**A:** **No**.</span></span> <span data-ttu-id="56a6f-109">Bir güvenlik Okuyucu, bir güvenlik yöneticisi veya genel yönetici toouse kimlik koruması ya da olabilir.</span><span class="sxs-lookup"><span data-stu-id="56a6f-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="56a6f-110">Kimlik koruması nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="56a6f-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="56a6f-111">**Y:** bkz [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md) bir yanıt toothis soru için.</span><span class="sxs-lookup"><span data-stu-id="56a6f-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="56a6f-112">Azure Active Directory Premium 2 Deneme sürümünüzün süresi dolduğunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="56a6f-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="56a6f-113">**Y:** , compliance ile olmasa da, Azure Active Directory ücretsiz, temel veya Premium 1 Edition'da Azure Active Directory Premium 2 Deneme sürümünüzün süresi doldu ve kimlik koruması etkin olan hala erişim tooit varsa Lisans.</span><span class="sxs-lookup"><span data-stu-id="56a6f-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
