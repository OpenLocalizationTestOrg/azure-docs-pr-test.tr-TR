---
title: Active Directory PoC Playbook malzemeleri aaaAzure | Microsoft Docs
description: "Keşfetmek ve hızlı bir şekilde kimlik ve erişim yönetimi senaryoları uygulayan"
services: active-directory
keywords: "Azure active directory, playbook, kavram kanıtı, PT"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="e600e-104">Azure Active Directory Playbook malzemeleri kavram kanıtı</span><span class="sxs-lookup"><span data-stu-id="e600e-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="e600e-105">Tema</span><span class="sxs-lookup"><span data-stu-id="e600e-105">Theme</span></span>
<span data-ttu-id="e600e-106">Azure AD kimlik ve erişim çözümleri birden fazla alanda hello kuruluş genelinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="e600e-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="e600e-107">Biz hello hello alanları aşağıdaki senaryolarda sınıflandırmak:</span><span class="sxs-lookup"><span data-stu-id="e600e-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="e600e-108">Birçok uygulama, bir kimlik</span><span class="sxs-lookup"><span data-stu-id="e600e-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="e600e-109">Güvenlik Artırma</span><span class="sxs-lookup"><span data-stu-id="e600e-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="e600e-110">Self Servis ölçekli</span><span class="sxs-lookup"><span data-stu-id="e600e-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="e600e-111">Bu iş hedeflerini ile denenmemesi PT toofocus hello çabalarına yardımcı olan bir tema tooframe hello tanımlama, görmemeleri kavram kanıtı hello ilgi hello ilk yerinde hello tetikleyici olduğu.</span><span class="sxs-lookup"><span data-stu-id="e600e-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="e600e-112">Ortam</span><span class="sxs-lookup"><span data-stu-id="e600e-112">Environment</span></span>

<span data-ttu-id="e600e-113">Bu önemli toodetermine hello burada hello PoC teslim eder hello ortamı ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e600e-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="e600e-114">İdeal olarak üzerine hello PoC tamamlandıktan sonra oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e600e-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="e600e-115">Merhaba hedef ortam çok önemlidir ve olabildiğince gerçek ve sınırlamalar veya ek konular hello yükünü yapmadan arasında doğru dengeyi hello bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e600e-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="e600e-116">Merhaba tipik ortamları kanıtları için şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e600e-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="e600e-117">**Üretim:** hello senaryoları Canlı ortamınızda uygulanan ve Microsoft Cloud services (üretim AD, Office 365, Azure AD Kiracı/SSO çözüm) zaten dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="e600e-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="e600e-118">**Kullanıcı kabul testi (UAT) / geliştirme ortamında:** test altyapısına sahip (AD ve potansiyel olarak Azure AD paralel Kiracı/SSO çözüm) test verilerle üretim benzer.</span><span class="sxs-lookup"><span data-stu-id="e600e-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="e600e-119">Genellikle, hello test ortamı hello kuruluştaki birden çok projeler arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="e600e-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="e600e-120">Bu kılavuzdaki çoğu senaryolar yapısı eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e600e-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="e600e-121">Sonuç olarak, bunlar hello üretim kiracısında hello PoC dışındaki kullanıcılar etkilemeden dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="e600e-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="e600e-122">Bu belge boyunca biz Kiracı genelinde etkisi hangi senaryolar yoktur çağırma.</span><span class="sxs-lookup"><span data-stu-id="e600e-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="e600e-123">Bu durumda, bir üretim ortamı dışındaki tooconsider isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e600e-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="e600e-124">Hedef Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="e600e-124">Target Users</span></span>

<span data-ttu-id="e600e-125">Bu önemli toodetermine hello hedef özellikle hello ortam üretim ya da test olduğunda hello senaryoları çalışma kullanıcıları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="e600e-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="e600e-126">PoC için hedef kullanıcı Hello kategorileri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e600e-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="e600e-127">**Pilot kullanıcıları:** hello çözümü kendi gün tooday için kullandıkları hello hesabıyla kullanarak hello ortamında gerçek kullanıcıların iş işlevleri</span><span class="sxs-lookup"><span data-stu-id="e600e-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="e600e-128">**Test kullanıcılarını:** Test hello ortamında oluşturulan hesaplar</span><span class="sxs-lookup"><span data-stu-id="e600e-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="e600e-129">Bu kılavuz Çoğu senaryoda, pilot kullanıcılar tarafından kullandı.</span><span class="sxs-lookup"><span data-stu-id="e600e-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="e600e-130">Bu belge boyunca biz hedef kullanıcı konuları gerekirse sizi arayacaktır.</span><span class="sxs-lookup"><span data-stu-id="e600e-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]