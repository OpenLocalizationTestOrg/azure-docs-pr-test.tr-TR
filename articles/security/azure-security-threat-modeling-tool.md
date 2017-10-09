---
title: "aaaMicrosoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Merhaba Microsoft tehdit modelleme hello tehdit modelleme işlemi dahil olmak üzere hello aracı ile çalışmaya başlama hakkında bilgi içeren aracı için ana sayfası"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="c4be6-103">Microsoft tehdit modelleme aracı</span><span class="sxs-lookup"><span data-stu-id="c4be6-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="c4be6-104">Merhaba tehdit modelleme aracı hello Microsoft Security Development Lifecycle (SDL) temel öğesidir.</span><span class="sxs-lookup"><span data-stu-id="c4be6-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="c4be6-105">Yazılım sağlar architects tooidentify ve görece kolay ve düşük maliyetli tooresolve olduklarında olası güvenlik sorunlarını erkenden, etkisini azaltır.</span><span class="sxs-lookup"><span data-stu-id="c4be6-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="c4be6-106">Sonuç olarak, geliştirme hello toplam maliyetini büyük ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="c4be6-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="c4be6-107">Ayrıca, biz uzmanlarla tehdit modelleme tüm geliştiriciler için oluşturma ve tehdit modelleri analiz etme konusunda açık yönergeler sağlayarak kolaylaştırma güvenlikle ilgili olmayan unutmayın, hello aracı tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c4be6-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="c4be6-108">Merhaba aracı herkese sağlar:</span><span class="sxs-lookup"><span data-stu-id="c4be6-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="c4be6-109">Sistemlerinin Hello güvenlik tasarımı hakkında iletişim</span><span class="sxs-lookup"><span data-stu-id="c4be6-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="c4be6-110">Bu tasarım kanıtlanmış yöntemi kullanarak olası güvenlik sorunlarını çözümleme</span><span class="sxs-lookup"><span data-stu-id="c4be6-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="c4be6-111">Önermek ve bunları azaltmanın yollarını güvenlik sorunları yönetme</span><span class="sxs-lookup"><span data-stu-id="c4be6-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="c4be6-112">Birkaç bazı araçları yetenekleri ve yenilik, yalnızca tooname şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c4be6-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="c4be6-113">**Otomasyon:** kılavuzunu ve bir modeli çizim geri bildirim</span><span class="sxs-lookup"><span data-stu-id="c4be6-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="c4be6-114">**STRIDE öğesi:** tehditlere ve bunları azaltmanın yollarını analizini Destekli</span><span class="sxs-lookup"><span data-stu-id="c4be6-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="c4be6-115">**Raporlama:** güvenlik etkinlikleri ve hello doğrulama aşamasında test etme</span><span class="sxs-lookup"><span data-stu-id="c4be6-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="c4be6-116">**Benzersiz yöntemi:** etkinleştirir kullanıcılar toobetter görselleştirmek ve tehditleri anlama</span><span class="sxs-lookup"><span data-stu-id="c4be6-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="c4be6-117">**Geliştiriciler ve ortalanmış yazılım için tasarlanmış:** birçok yaklaşım varlıklar veya saldırganların ortalanır.</span><span class="sxs-lookup"><span data-stu-id="c4be6-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="c4be6-118">Biz yazılımı ortalanır.</span><span class="sxs-lookup"><span data-stu-id="c4be6-118">We are centered on software.</span></span> <span data-ttu-id="c4be6-119">Biz tüm yazılım geliştiricileri ve mimarlar yazılım mimarilerini resim çizim gibi--bilginiz etkinliklerde derleme</span><span class="sxs-lookup"><span data-stu-id="c4be6-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="c4be6-120">**Tasarım çözümleme odaklanmış:** gereksinimler ya da bir tasarım analiz teknik hello terimi "tehdit modelleme" tooeither başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="c4be6-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="c4be6-121">Bazı durumlarda, karmaşık karışımı hello iki tooa başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="c4be6-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="c4be6-122">Merhaba Microsoft SDL yaklaşım toothreat modelleme Odaklı Tasarım analiz tekniktir</span><span class="sxs-lookup"><span data-stu-id="c4be6-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4be6-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4be6-123">Next steps</span></span>

<span data-ttu-id="c4be6-124">Merhaba tabloda hello tehdit modelleme aracı ile başlatılan önemli bağlantılar tooget içerir:</span><span class="sxs-lookup"><span data-stu-id="c4be6-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="c4be6-125">Adım</span><span class="sxs-lookup"><span data-stu-id="c4be6-125">Step</span></span>  | <span data-ttu-id="c4be6-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4be6-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="c4be6-127">**1**</span><span class="sxs-lookup"><span data-stu-id="c4be6-127">**1**</span></span> | [<span data-ttu-id="c4be6-128">Merhaba tehdit modelleme aracı yükle</span><span class="sxs-lookup"><span data-stu-id="c4be6-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="c4be6-129">**2**</span><span class="sxs-lookup"><span data-stu-id="c4be6-129">**2**</span></span> | [<span data-ttu-id="c4be6-130">Bizim Başlarken Kılavuzu okuyun</span><span class="sxs-lookup"><span data-stu-id="c4be6-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="c4be6-131">**3**</span><span class="sxs-lookup"><span data-stu-id="c4be6-131">**3**</span></span> | [<span data-ttu-id="c4be6-132">Merhaba özellikleriyle tanışın</span><span class="sxs-lookup"><span data-stu-id="c4be6-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="c4be6-133">**4**</span><span class="sxs-lookup"><span data-stu-id="c4be6-133">**4**</span></span> | [<span data-ttu-id="c4be6-134">Oluşturulan tehdit kategorileri hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c4be6-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="c4be6-135">**5**</span><span class="sxs-lookup"><span data-stu-id="c4be6-135">**5**</span></span> | [<span data-ttu-id="c4be6-136">Azaltıcı toogenerated tehditleri Bul</span><span class="sxs-lookup"><span data-stu-id="c4be6-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="c4be6-137">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c4be6-137">Resources</span></span>

<span data-ttu-id="c4be6-138">Bazı eski makaleler hala ilgili toothreat modelleme bugün şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c4be6-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="c4be6-139">Merhaba üzerinde önem düzeyi, tehdit modelleme makalesi</span><span class="sxs-lookup"><span data-stu-id="c4be6-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="c4be6-140">Güvenilir bilgi işlem tarafından yayımlanan eğitim</span><span class="sxs-lookup"><span data-stu-id="c4be6-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="c4be6-141">Birkaç tehdit modelleme aracı uzmanlar yapmış olmanız denetleyin:</span><span class="sxs-lookup"><span data-stu-id="c4be6-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="c4be6-142">Tehditler Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="c4be6-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="c4be6-143">Simone Curzi güvenlik blogu</span><span class="sxs-lookup"><span data-stu-id="c4be6-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)