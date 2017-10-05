---
title: "Azure'da güvenli sağlık çözümleri tasarlama için pratik bir kılavuz | Microsoft Docs"
description: " Bu makalede, yapılandırma özellikleri ve Azure Hizmetleri kullanarak güvenlik sağlık çözümleriniz için iyileştirmek nasıl tasarlandığını anlamanıza yardımcı olur. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 7e5b082d-dc9c-4d4f-b3f1-75edcdafbd8f
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2017
ms.author: terrylan
ms.openlocfilehash: 34ded89eb7fe005be2341f96e5b883ec73d9e0a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="a-practical-guide-to-designing-secure-health-care-solutions-in-azure"></a><span data-ttu-id="6ff1d-103">Azure'da güvenli sağlık çözümleri tasarlama için pratik bir kılavuz</span><span class="sxs-lookup"><span data-stu-id="6ff1d-103">A practical guide to designing secure health care solutions in Azure</span></span>
<span data-ttu-id="6ff1d-104">Sistem durumu endüstri startup'lar, sistem tümleştiricileri (SIS), bağımsız yazılım satıcılarının (ISV'ler) ve Azure Git bunları yardımcı olan yönergeler için arayan planlayan sağlık kuruluşlar kendi uyumluluk yükümlülüklerin karşılamak için güvenlik denetimleri dahil.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-104">Health industry startups, system integrators (SIs), independent software vendors (ISVs), and healthcare organizations considering a move to Azure are looking for guidance that helps them incorporate security controls to meet their compliance obligations.</span></span>

<span data-ttu-id="6ff1d-105">[Tasarlama güvenli sağlık çözümlerinde Microsoft Azure pratik bir kılavuz](https://aka.ms/azureindustrysecurity) gereksinimlerinize göre Azure Hizmetleri ve yapılandırabileceğiniz özellikleri kullanarak çözümlerinizi tabanlı için nasıl güvenliği artırabilirsiniz anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-105">[A Practical Guide to Designing Secure Health Care Solutions in Microsoft Azure](https://aka.ms/azureindustrysecurity) helps you understand how you can improve security for your solutions by using the Azure services and features that you can configure based on your requirements.</span></span>
<span data-ttu-id="6ff1d-106">İçerik üç ana bölümlere ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="6ff1d-106">The content is divided into three major sections:</span></span>

1. <span data-ttu-id="6ff1d-107">Dikkat edilecek noktalar Kılavuzu risk yönetimi gibi bulut teknolojisini kullanarak bir bilgi güvenliği yönetimi sistemi, anlama endüstri ve yerel düzenlemelerle oluşturma ve standart işletim yordamlarını oluşturma sorumluluk paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-107">Considerations guidance for using cloud technology, including risk management, shared responsibility, establishing an information security management system, understanding industry and local regulations, and establishing standard operating procedures.</span></span>
2. <span data-ttu-id="6ff1d-108">Her ikisi de anahtar güvenlik ilkeleri, ISO 27001, gibi standart bilgi güvenliği yönetimi standart ve standart geliştirme süreçleri, Microsoft Security Development Lifecycle (SDL) gibi hizalı.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-108">Key security principles that are both aligned to a standard information security management standard, such as ISO 27001, and standard development processes, such as Microsoft’s Security Development Lifecycle (SDL).</span></span>
3. <span data-ttu-id="6ff1d-109">Bir çözümü Mimarı perspektifinden hizalamasını gösteren tarafından gereksinimleri çözümler için bilgi güvenliği yönetimi için standart burada hizalanır kullanım için anahtar ilkelerinin uygulanması.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-109">Applying the key principles to use cases by demonstrating alignment from a solution architect perspective, where requirements for the solutions are aligned to the information security management standard.</span></span>

<span data-ttu-id="6ff1d-110">Bulduğunuz umuyoruz [güvenli sağlık çözümleri tasarlama pratik Kılavuzu](https://aka.ms/azureindustrysecurity) yararlı ve herhangi bir sorunuz veya önerileri varsa, bize bir yorum bırakarak bildirin.</span><span class="sxs-lookup"><span data-stu-id="6ff1d-110">We hope you find [A Practical Guide to Designing Secure Health Care Solutions](https://aka.ms/azureindustrysecurity) helpful and if you have any questions or suggestions, let us know by leaving a comment below.</span></span>
