---
title: Azure Active Directory rapor bekletme ilkeleri | Microsoft Docs
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="1d9b5-103">Azure Active Directory rapor bekletme ilkeleri</span><span class="sxs-lookup"><span data-stu-id="1d9b5-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="1d9b5-104">Bu konu, Azure Active Directory'de farklı etkinlik raporları için veri saklama ile birlikte en yaygın sorulara yanıtlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d9b5-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="1d9b5-105">**S: nasıl başlatılan etkinliği veri koleksiyonunu alabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="1d9b5-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-106">**A:**</span></span>

| <span data-ttu-id="1d9b5-107">Azure AD Edition</span><span class="sxs-lookup"><span data-stu-id="1d9b5-107">Azure AD Edition</span></span> | <span data-ttu-id="1d9b5-108">Koleksiyon Başlat</span><span class="sxs-lookup"><span data-stu-id="1d9b5-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="1d9b5-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="1d9b5-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="1d9b5-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="1d9b5-110">Azure AD Premium P2</span></span> | <span data-ttu-id="1d9b5-111">Olduğunda, bir abonelik için kaydolma</span><span class="sxs-lookup"><span data-stu-id="1d9b5-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="1d9b5-112">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="1d9b5-112">Azure AD Free</span></span> | <span data-ttu-id="1d9b5-113">İlk açtığınızda [Azure Active Directory dikey](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) veya [API'leri raporlama](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="1d9b5-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="1d9b5-114">**S: etkinlik verilerinizi Azure portalında kullanılabilir olduğunda?**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="1d9b5-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-115">**A:**</span></span>

- <span data-ttu-id="1d9b5-116">**Hemen** -, zaten Klasik Azure portalındaki raporları ile birlikte çalışıyorsanız</span><span class="sxs-lookup"><span data-stu-id="1d9b5-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="1d9b5-117">**2 saat içinde** -, raporlama Azure Klasik Portalı'nda açmadıysanız</span><span class="sxs-lookup"><span data-stu-id="1d9b5-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="1d9b5-118">**S: nasıl başlatılan güvenlik sinyal koleksiyonu alabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="1d9b5-119">**Y:** , kimlik koruma Merkezi'ni kullanmayı katılımı güvenlik sinyalleri için toplama işlemi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="1d9b5-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="1d9b5-120">**S: toplanan veriler ne kadar süreyle depolanır?**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="1d9b5-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-121">**A:**</span></span>

<span data-ttu-id="1d9b5-122">**Etkinlik raporları**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-122">**Activity reports**</span></span>    

| <span data-ttu-id="1d9b5-123">Rapor</span><span class="sxs-lookup"><span data-stu-id="1d9b5-123">Report</span></span>                 | <span data-ttu-id="1d9b5-124">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="1d9b5-124">Azure AD Free</span></span> | <span data-ttu-id="1d9b5-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="1d9b5-125">Azure AD Premium P1</span></span> | <span data-ttu-id="1d9b5-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="1d9b5-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="1d9b5-127">Dizin Denetimi</span><span class="sxs-lookup"><span data-stu-id="1d9b5-127">Directory Audit</span></span>        | <span data-ttu-id="1d9b5-128">7 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-128">7 days</span></span>        | <span data-ttu-id="1d9b5-129">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-129">30 days</span></span>             | <span data-ttu-id="1d9b5-130">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-130">30 days</span></span>             |
| <span data-ttu-id="1d9b5-131">Oturum Açma Etkinliği</span><span class="sxs-lookup"><span data-stu-id="1d9b5-131">Sign-in Activity</span></span>       | <span data-ttu-id="1d9b5-132">7 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-132">7 days</span></span>        | <span data-ttu-id="1d9b5-133">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-133">30 days</span></span>             | <span data-ttu-id="1d9b5-134">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-134">30 days</span></span>             |

<span data-ttu-id="1d9b5-135">**Güvenlik sinyalleri**</span><span class="sxs-lookup"><span data-stu-id="1d9b5-135">**Security Signals**</span></span>

| <span data-ttu-id="1d9b5-136">Rapor</span><span class="sxs-lookup"><span data-stu-id="1d9b5-136">Report</span></span>         | <span data-ttu-id="1d9b5-137">Azure AD Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="1d9b5-137">Azure AD Free</span></span> | <span data-ttu-id="1d9b5-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="1d9b5-138">Azure AD Premium P1</span></span> | <span data-ttu-id="1d9b5-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="1d9b5-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="1d9b5-140">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="1d9b5-140">Users at risk</span></span>  | <span data-ttu-id="1d9b5-141">7 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-141">7 days</span></span>        | <span data-ttu-id="1d9b5-142">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-142">30 days</span></span>             | <span data-ttu-id="1d9b5-143">90 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-143">90 days</span></span>             |
| <span data-ttu-id="1d9b5-144">Riskli oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="1d9b5-144">Risky sign-ins</span></span> | <span data-ttu-id="1d9b5-145">7 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-145">7 days</span></span>        | <span data-ttu-id="1d9b5-146">30 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-146">30 days</span></span>             | <span data-ttu-id="1d9b5-147">90 gün</span><span class="sxs-lookup"><span data-stu-id="1d9b5-147">90 days</span></span>             |

---