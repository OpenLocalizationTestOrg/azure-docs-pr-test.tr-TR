---
title: "aaaProtect kişisel verileri Microsoft Azure | Microsoft Docs"
description: "İlk makale makaleleri toohelp bir dizi Azure tooprotect kişisel verilerinizi kullanın"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="2d34f-103">Microsoft Azure kişisel verileri korumak</span><span class="sxs-lookup"><span data-stu-id="2d34f-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="2d34f-104">Bu makalede, Yardım makaleleri bir dizi tanıtılır Azure güvenlik teknolojileri ve Hizmetleri tooprotect kişisel verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d34f-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="2d34f-105">Çoğu Kurumsal Anahtar gereksinimini ve endüstri uyumluluk ve idare girişimleri budur.</span><span class="sxs-lookup"><span data-stu-id="2d34f-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="2d34f-106">Merhaba senaryo, sorun bildirimi ve şirket hedeflerini buraya dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="2d34f-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="2d34f-107">Senaryo ve sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="2d34f-107">Scenario and problem statement</span></span>

<span data-ttu-id="2d34f-108">Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="2d34f-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="2d34f-109">toosupport bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere</span><span class="sxs-lookup"><span data-stu-id="2d34f-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="2d34f-110">Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2d34f-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="2d34f-111">Bu çalışan ve/veya müşteri bilgileri gibi içerebilir:</span><span class="sxs-lookup"><span data-stu-id="2d34f-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="2d34f-112">adresleri</span><span class="sxs-lookup"><span data-stu-id="2d34f-112">addresses</span></span>
- <span data-ttu-id="2d34f-113">Telefon numaraları</span><span class="sxs-lookup"><span data-stu-id="2d34f-113">phone numbers</span></span>
- <span data-ttu-id="2d34f-114">Vergi kimlik numaraları</span><span class="sxs-lookup"><span data-stu-id="2d34f-114">tax identification numbers</span></span>
- <span data-ttu-id="2d34f-115">Sağlık bilgileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-115">medical information</span></span>
- <span data-ttu-id="2d34f-116">Kredi kartı bilgileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-116">credit card information</span></span>

<span data-ttu-id="2d34f-117">Merhaba şirket ihtiyaç veri erişilebilir toothose Departmanlar yaparken hello gizlilik çalışan ve Müşteri verilerinin korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d34f-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="2d34f-118">(bordro ve ayırmaları Departmanlar gibi)</span><span class="sxs-lookup"><span data-stu-id="2d34f-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="2d34f-119">Şirketin hedeflerine</span><span class="sxs-lookup"><span data-stu-id="2d34f-119">Company goals</span></span> 

- <span data-ttu-id="2d34f-120">Kişisel verileri içeren veri kaynakları, bulut depolama alanında bulunan zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="2d34f-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="2d34f-121">Tek bir konumda tooanother aktarılan kişisel veriler aktarım sırasında sırasında şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="2d34f-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="2d34f-122">Merhaba veri hello sanal ağ üzerinden veya hello Internet üzerinden hello Azure bulut hello kurumsal veri merkezi arasında seyahat ederken olduğunda true olur.</span><span class="sxs-lookup"><span data-stu-id="2d34f-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="2d34f-123">Gizlilik ve kişisel verilerin bütünlüğünü güçlü kimlik yönetimi ve erişim denetimi teknolojileri tarafından yetkisiz erişimden korunur.</span><span class="sxs-lookup"><span data-stu-id="2d34f-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="2d34f-124">Kişisel verileri Etkilenme Güvenlik Açıkları ve tehditleri için izleme aracılığıyla veri ihlali aracılığıyla gelen korunur.</span><span class="sxs-lookup"><span data-stu-id="2d34f-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="2d34f-125">Merhaba, saklamak veya kişisel verilerin aktarılması Azure Hizmetleri güvenlik durumunu değerlendirildiği tooidentify fırsatları toobetter kişisel verilerini korur.</span><span class="sxs-lookup"><span data-stu-id="2d34f-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="2d34f-126">Veri koruma Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="2d34f-126">Data protection guidance</span></span>

<span data-ttu-id="2d34f-127">aşağıdaki makaleleri hello teknik nasıl-yukarıda listelenen hello kişisel veri koruma hedeflerini elde yardımcı olacak tooguidance içerir:</span><span class="sxs-lookup"><span data-stu-id="2d34f-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="2d34f-128">Azure şifreleme teknolojileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="2d34f-129">Azure şifreleme teknolojileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="2d34f-130">Azure kimlik ve erişim teknolojileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="2d34f-131">Azure ağı güvenlik teknolojileri</span><span class="sxs-lookup"><span data-stu-id="2d34f-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="2d34f-132">Azure Güvenlik Merkezi</span><span class="sxs-lookup"><span data-stu-id="2d34f-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="2d34f-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d34f-133">Next steps</span></span>

- [<span data-ttu-id="2d34f-134">Azure güvenlik bilgileri Site</span><span class="sxs-lookup"><span data-stu-id="2d34f-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="2d34f-135">Microsoft Güven Merkezi</span><span class="sxs-lookup"><span data-stu-id="2d34f-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="2d34f-136">Azure Güvenlik Merkezi</span><span class="sxs-lookup"><span data-stu-id="2d34f-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="2d34f-137">Azure Güvenlik Ekibi Blogu</span><span class="sxs-lookup"><span data-stu-id="2d34f-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="2d34f-138">Azure.com Blog - güvenlik</span><span class="sxs-lookup"><span data-stu-id="2d34f-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
