---
title: "aaaAzure Active Directory PoC Playbook giriş | Microsoft Docs"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="6bd50-104">Azure Active Directory Playbook kavram kanıtı: Giriş</span><span class="sxs-lookup"><span data-stu-id="6bd50-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="6bd50-105">Bu makalede bir kavram kanıtı (PoC) tooexplore farklı Azure AD yetenekler yönergeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bd50-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="6bd50-106">Merhaba, bu belgenin hedef kitle kimlik mimarları, BT uzmanları ve sistem tümleştiricileri tasarlanmıştır</span><span class="sxs-lookup"><span data-stu-id="6bd50-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="6bd50-107">Nasıl toouse bu Playbook</span><span class="sxs-lookup"><span data-stu-id="6bd50-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="6bd50-108">Kullanım hello [tema](active-directory-playbook-ingredients.md#theme) bölümünde ve gereksinimlerinize göre ilgi hello çizilen seçin.</span><span class="sxs-lookup"><span data-stu-id="6bd50-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="6bd50-109">Kapsam hello seçerek iş hedeflerinize Hizala hello senaryoları PoC.</span><span class="sxs-lookup"><span data-stu-id="6bd50-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="6bd50-110">Merhaba kısa hello daha iyi.</span><span class="sxs-lookup"><span data-stu-id="6bd50-110">hello shorter hello better.</span></span> <span data-ttu-id="6bd50-111">Kısa yapılması önerilir ve olası tooconvey hello değeri kısa en aza indirme sırasında toohello Paydaşlar karmaşıklık toorealize Merhaba.</span><span class="sxs-lookup"><span data-stu-id="6bd50-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="6bd50-112">Kullanım hello [uygulama](active-directory-playbook-implementation.md) bölüm toounderstand hello senaryoları ve anlamları ortamınız için.</span><span class="sxs-lookup"><span data-stu-id="6bd50-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="6bd50-113">Her senaryo, biz açıklamak nasıl tooset bunun (veririz [yapı taşları](active-directory-playbook-building-blocks.md)), ve nasıl toonavigate hello senaryoları.</span><span class="sxs-lookup"><span data-stu-id="6bd50-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="6bd50-114">Her yapı bloğu gereken hello önkoşulların yanı sıra bir yaklaşık zaman toocomplete açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6bd50-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="6bd50-115">Bu hello Planlama işlemi sırasında yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6bd50-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="6bd50-116">1-3 bağlı olarak, hello tanımlamak [ortam](active-directory-playbook-ingredients.md#environment) hangi tooexecute içinde.</span><span class="sxs-lookup"><span data-stu-id="6bd50-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="6bd50-117">Bir üretim ortamında tooget hello deneyiminin kullanıcılarınız için iyi bir fikir toostrive öneririz.</span><span class="sxs-lookup"><span data-stu-id="6bd50-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="6bd50-118">Çakışan gereksinimlerine sahip olduğunda, bu yararlı kolaylığını matrisi kullanma</span><span class="sxs-lookup"><span data-stu-id="6bd50-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="6bd50-119">Değerinin tema merkezli gösterme</span><span class="sxs-lookup"><span data-stu-id="6bd50-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="6bd50-120">Düzgünlük tooprepare, tooset yukarı ve tooexecute hello senaryoları</span><span class="sxs-lookup"><span data-stu-id="6bd50-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="6bd50-121">En az zaman tooexecute hello hedef senaryoları</span><span class="sxs-lookup"><span data-stu-id="6bd50-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="6bd50-122">Kısıtlamaları içindeki uygun olarak Kapat tooproduction</span><span class="sxs-lookup"><span data-stu-id="6bd50-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="6bd50-123">Bu makale bazı belirli üçüncü taraf uygulamalar ve kolaylık sağlamak için örnek olarak belirtilen ürünleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6bd50-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="6bd50-124">Azure AD destekleyen uygulamalarda binlerce bizim [uygulama Galerisi](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) , gereksinimleri ve ortam bağlı olarak, kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd50-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]