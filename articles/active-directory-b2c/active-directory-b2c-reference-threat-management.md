---
title: "Azure Active Directory B2C: Tehdit Yönetimi | Microsoft Docs"
description: "Hizmet reddi saldırılarını ve Azure Active Directory B2C parola saldırılarını algılama ve azaltma teknikleri hakkında bilgi edinin."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="2577d-103">Azure Active Directory B2C: Tehdit Yönetimi</span><span class="sxs-lookup"><span data-stu-id="2577d-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="2577d-104">Tehdit yönetimi, sistem ve ağ karşı saldırılarına karşı koruma için planlamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="2577d-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="2577d-105">Hizmet reddi saldırılarını kaynakları kullanılamıyor toointended kullanıcılar yapabilir.</span><span class="sxs-lookup"><span data-stu-id="2577d-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="2577d-106">Parola saldırılarını sağlama toounauthorized erişim tooresources.</span><span class="sxs-lookup"><span data-stu-id="2577d-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="2577d-107">Azure Active Directory B2C (Azure AD B2C) verilerinizi birden çok yolla bu tehditlere karşı korumanıza yardımcı olabilecek yerleşik özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2577d-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="2577d-108">Hizmet reddi saldırıları</span><span class="sxs-lookup"><span data-stu-id="2577d-108">Denial-of-service attacks</span></span>

<span data-ttu-id="2577d-109">Azure AD B2C Eşitlemeye tanımlama bilgileri ve hizmet reddi saldırılarına karşı kaynakları temel oranı ve bağlantı sınırları tooprotect gibi algılama ve azaltma teknikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2577d-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="2577d-110">Parola saldırıları</span><span class="sxs-lookup"><span data-stu-id="2577d-110">Password attacks</span></span>

<span data-ttu-id="2577d-111">Azure AD B2C azaltma teknikleri parola saldırılarını için yerinde de vardır.</span><span class="sxs-lookup"><span data-stu-id="2577d-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="2577d-112">Parola yanılma saldırıları ve sözlük parola saldırılarını azaltma içerir.</span><span class="sxs-lookup"><span data-stu-id="2577d-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="2577d-113">Kullanıcılar tarafından ayarlanan parolaları gerekli toobe makul karmaşık ' dir.</span><span class="sxs-lookup"><span data-stu-id="2577d-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="2577d-114">Çeşitli sinyalleri kullanarak, Azure AD B2C istekleri hello bütünlüğünü analiz eder.</span><span class="sxs-lookup"><span data-stu-id="2577d-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="2577d-115">Azure AD B2C tasarlanmıştır toointelligently ayırt hedeflenen kullanıcılar bilgisayar korsanlarının ve botnets.</span><span class="sxs-lookup"><span data-stu-id="2577d-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="2577d-116">Azure AD B2C, saldırının hello olasılığını içinde girilen hello parolalar göre hesapları Gelişmiş stratejisi toolock sağlar.</span><span class="sxs-lookup"><span data-stu-id="2577d-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="2577d-117">Daha fazla bilgi için hello ziyaret [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="2577d-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
