---
title: aaaAzure Active Directory rapor bekletme ilkeleri | Microsoft Docs
description: Rapor verileri Azure Active Directory'de bekletme ilkeleri
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="11c6f-103">Azure Active Directory rapor bekletme ilkeleri</span><span class="sxs-lookup"><span data-stu-id="11c6f-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="11c6f-104">Bu konuda yanıtlarla toohello en yaygın sorular hello veri saklama için Azure Active Directory'de hello farklı etkinlik raporları ile birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="11c6f-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="11c6f-105">**S: nasıl etkinlik verileri başlatılan hello koleksiyonu alabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="11c6f-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="11c6f-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="11c6f-106">**A:**</span></span>

| <span data-ttu-id="11c6f-107">Azure AD Edition</span><span class="sxs-lookup"><span data-stu-id="11c6f-107">Azure AD Edition</span></span> | <span data-ttu-id="11c6f-108">Koleksiyon Başlat</span><span class="sxs-lookup"><span data-stu-id="11c6f-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="11c6f-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="11c6f-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="11c6f-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="11c6f-110">Azure AD Premium P2</span></span> | <span data-ttu-id="11c6f-111">Olduğunda, bir abonelik için kaydolma</span><span class="sxs-lookup"><span data-stu-id="11c6f-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="11c6f-112">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="11c6f-112">Azure AD Free</span></span> | <span data-ttu-id="11c6f-113">Merhaba ilk kez açtığınızda hello [Azure Active Directory dikey](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) veya hello [API'leri raporlama](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="11c6f-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="11c6f-114">**S: etkinlik verilerinizi hello Azure portalında kullanılabilir olduğunda?**</span><span class="sxs-lookup"><span data-stu-id="11c6f-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="11c6f-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="11c6f-115">**A:**</span></span>

- <span data-ttu-id="11c6f-116">**Hemen** -, zaten hello Klasik Azure portalı raporlarında ile çalışıyorsanız</span><span class="sxs-lookup"><span data-stu-id="11c6f-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="11c6f-117">**2 saat içinde** -, raporlama hello Klasik Azure portalı açmadıysanız</span><span class="sxs-lookup"><span data-stu-id="11c6f-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="11c6f-118">**S: nasıl başlatılan güvenlik sinyal hello koleksiyonu alabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="11c6f-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="11c6f-119">**Y:** , toouse hello Identity Protection Center katılımı güvenlik sinyalleri için hello toplama işlemi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="11c6f-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="11c6f-120">**S: ne kadar süreyle hello toplanan veriler depolanır?**</span><span class="sxs-lookup"><span data-stu-id="11c6f-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="11c6f-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="11c6f-121">**A:**</span></span>

<span data-ttu-id="11c6f-122">**Etkinlik raporları**</span><span class="sxs-lookup"><span data-stu-id="11c6f-122">**Activity reports**</span></span>    

| <span data-ttu-id="11c6f-123">Rapor</span><span class="sxs-lookup"><span data-stu-id="11c6f-123">Report</span></span>                 | <span data-ttu-id="11c6f-124">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="11c6f-124">Azure AD Free</span></span> | <span data-ttu-id="11c6f-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="11c6f-125">Azure AD Premium P1</span></span> | <span data-ttu-id="11c6f-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="11c6f-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="11c6f-127">Dizin Denetimi</span><span class="sxs-lookup"><span data-stu-id="11c6f-127">Directory Audit</span></span>        | <span data-ttu-id="11c6f-128">7 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-128">7 days</span></span>        | <span data-ttu-id="11c6f-129">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-129">30 days</span></span>             | <span data-ttu-id="11c6f-130">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-130">30 days</span></span>             |
| <span data-ttu-id="11c6f-131">Oturum Açma Etkinliği</span><span class="sxs-lookup"><span data-stu-id="11c6f-131">Sign-in Activity</span></span>       | <span data-ttu-id="11c6f-132">7 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-132">7 days</span></span>        | <span data-ttu-id="11c6f-133">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-133">30 days</span></span>             | <span data-ttu-id="11c6f-134">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-134">30 days</span></span>             |

<span data-ttu-id="11c6f-135">**Güvenlik sinyalleri**</span><span class="sxs-lookup"><span data-stu-id="11c6f-135">**Security Signals**</span></span>

| <span data-ttu-id="11c6f-136">Rapor</span><span class="sxs-lookup"><span data-stu-id="11c6f-136">Report</span></span>         | <span data-ttu-id="11c6f-137">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="11c6f-137">Azure AD Free</span></span> | <span data-ttu-id="11c6f-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="11c6f-138">Azure AD Premium P1</span></span> | <span data-ttu-id="11c6f-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="11c6f-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="11c6f-140">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="11c6f-140">Users at risk</span></span>  | <span data-ttu-id="11c6f-141">7 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-141">7 days</span></span>        | <span data-ttu-id="11c6f-142">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-142">30 days</span></span>             | <span data-ttu-id="11c6f-143">90 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-143">90 days</span></span>             |
| <span data-ttu-id="11c6f-144">Riskli oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="11c6f-144">Risky sign-ins</span></span> | <span data-ttu-id="11c6f-145">7 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-145">7 days</span></span>        | <span data-ttu-id="11c6f-146">30 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-146">30 days</span></span>             | <span data-ttu-id="11c6f-147">90 gün</span><span class="sxs-lookup"><span data-stu-id="11c6f-147">90 days</span></span>             |

---