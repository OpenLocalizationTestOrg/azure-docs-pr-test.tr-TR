---
title: "Azure Active Directory kimlik koruması ile ilgili SSS | Microsoft Docs"
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
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="b805c-103">Azure Active Directory kimlik koruması ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="b805c-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="b805c-104">Neden bazı risk olayları "Kapalı (Sistem)" durum var mı?</span><span class="sxs-lookup"><span data-stu-id="b805c-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="b805c-105">**Y:** bu Azure Active Directory kimlik koruması algıladı ve olayları artık riskli olduğu kabul için daha sonra kapattı olaylardır.</span><span class="sxs-lookup"><span data-stu-id="b805c-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="b805c-106">Bu olaylar, kullanıcının risk düzeyi sayılmaz.</span><span class="sxs-lookup"><span data-stu-id="b805c-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="b805c-107">Azure portalında kimlik koruması kullanmak için genel yönetici olmanız gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="b805c-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="b805c-108">**Y:** **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="b805c-108">**A:** **No**.</span></span> <span data-ttu-id="b805c-109">Bir güvenlik Okuyucu, bir güvenlik yöneticisi veya genel yönetici kimlik koruması kullanmayı ya da olabilir.</span><span class="sxs-lookup"><span data-stu-id="b805c-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="b805c-110">Kimlik koruması nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="b805c-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="b805c-111">**Y:** bkz [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md) bu yanıtını için.</span><span class="sxs-lookup"><span data-stu-id="b805c-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="b805c-112">Azure Active Directory Premium 2 Deneme sürümünüzün süresi dolduğunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="b805c-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="b805c-113">**Y:** değil compliance ile olsa bile, Azure Active Directory ücretsiz, temel veya Premium 1 Edition'da Azure Active Directory Premium 2 Deneme sürümünüzün süresi doldu ve kimlik koruması etkin olan hala erişiminiz varsa Lisans.</span><span class="sxs-lookup"><span data-stu-id="b805c-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
