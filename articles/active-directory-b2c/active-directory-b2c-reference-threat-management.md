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
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="7679a-103">Azure Active Directory B2C: Tehdit Yönetimi</span><span class="sxs-lookup"><span data-stu-id="7679a-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="7679a-104">Tehdit yönetimi, sistem ve ağ karşı saldırılarına karşı koruma için planlamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="7679a-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="7679a-105">Hizmet reddi saldırılarını kaynakları kullanılamıyor hedeflenen kullanıcılara yapabilir.</span><span class="sxs-lookup"><span data-stu-id="7679a-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="7679a-106">Parola saldırılarını kaynaklara yetkisiz erişim sağlama.</span><span class="sxs-lookup"><span data-stu-id="7679a-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="7679a-107">Azure Active Directory B2C (Azure AD B2C) verilerinizi birden çok yolla bu tehditlere karşı korumanıza yardımcı olabilecek yerleşik özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7679a-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="7679a-108">Hizmet reddi saldırıları</span><span class="sxs-lookup"><span data-stu-id="7679a-108">Denial-of-service attacks</span></span>

<span data-ttu-id="7679a-109">Azure AD B2C algılama ve azaltma teknikler kullanır Eşitlemeye tanımlama bilgileri ve hizmet reddi saldırılarına karşı temel kaynakları korumak için oranı ve bağlantı sınırları ister.</span><span class="sxs-lookup"><span data-stu-id="7679a-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="7679a-110">Parola saldırıları</span><span class="sxs-lookup"><span data-stu-id="7679a-110">Password attacks</span></span>

<span data-ttu-id="7679a-111">Azure AD B2C azaltma teknikleri parola saldırılarını için yerinde de vardır.</span><span class="sxs-lookup"><span data-stu-id="7679a-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="7679a-112">Parola yanılma saldırıları ve sözlük parola saldırılarını azaltma içerir.</span><span class="sxs-lookup"><span data-stu-id="7679a-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="7679a-113">Kullanıcılar tarafından ayarlanan parolaları makul karmaşık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7679a-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="7679a-114">Çeşitli sinyalleri kullanarak, Azure AD B2C isteklerinin bütünlüğünü analiz eder.</span><span class="sxs-lookup"><span data-stu-id="7679a-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="7679a-115">Azure AD B2C, bilgisayar korsanlarını ve botnets hedeflenen kullanıcılar akıllıca ayırt etmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7679a-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="7679a-116">Azure AD B2C, saldırının olasılığını içinde girilen parolalar göre kilit hesapları için Gelişmiş bir strateji sağlar.</span><span class="sxs-lookup"><span data-stu-id="7679a-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="7679a-117">Daha fazla bilgi için ziyaret [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="7679a-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
