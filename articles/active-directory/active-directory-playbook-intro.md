---
title: "Azure Active Directory PoC Playbook giriş | Microsoft Docs"
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
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="9dbf8-104">Azure Active Directory Playbook kavram kanıtı: Giriş</span><span class="sxs-lookup"><span data-stu-id="9dbf8-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="9dbf8-105">Bu makalede farklı Azure keşfetmek için yönergeler sağlanmaktadır bir kavram kanıtı (PoC)'de AD özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="9dbf8-106">Bu belgenin hedef kitle kimlik mimarları, BT uzmanları ve sistem tümleştiricileri olduğu</span><span class="sxs-lookup"><span data-stu-id="9dbf8-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="9dbf8-107">Bu Playbook kullanma</span><span class="sxs-lookup"><span data-stu-id="9dbf8-107">How to use this Playbook</span></span>

1. <span data-ttu-id="9dbf8-108">Kullanım [tema](active-directory-playbook-ingredients.md#theme) bölümünde ve gereksinimlerinize göre ilgi çizilen seçin.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="9dbf8-109">Kapsam iş hedeflerinize Hizala senaryoları seçerek PoC.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="9dbf8-110">Daha kısa iyi olur.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-110">The shorter the better.</span></span> <span data-ttu-id="9dbf8-111">Kısa ve bunun farkına karmaşıklığını azaltırken katılımcılara değeri iletmek mümkün olduğunca kısa olarak yapmakta öneririz.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="9dbf8-112">Kullanım [uygulama](active-directory-playbook-implementation.md) senaryolarını ve ne geldiklerini ortamınız için anlamak için bölüm.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="9dbf8-113">Her senaryoda, biz kurulacağını açıklar (veririz [yapı taşları](active-directory-playbook-building-blocks.md)) ve nasıl senaryolardan gidin.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="9dbf8-114">Her yapı bloğu tamamlamak için yaklaşık bir saat yanı sıra, gerekli ön koşullar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="9dbf8-115">Bu planlama işlemi sırasında yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="9dbf8-116">1-3 bağlı olarak, tanımlamak [ortam](active-directory-playbook-ingredients.md#environment) yürütmek üzere.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="9dbf8-117">Kullanıcılarınız için iyi bir deneyim yapısını almak bir üretim ortamı için mücadele etmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="9dbf8-118">Çakışan gereksinimlerine sahip olduğunda, bu yararlı kolaylığını matrisi kullanma</span><span class="sxs-lookup"><span data-stu-id="9dbf8-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="9dbf8-119">Değerinin tema merkezli gösterme</span><span class="sxs-lookup"><span data-stu-id="9dbf8-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="9dbf8-120">Düzgünlük hazırlamak için Kurulum ve senaryoları yürütmek için</span><span class="sxs-lookup"><span data-stu-id="9dbf8-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="9dbf8-121">Hedef senaryoları çalıştırmak için en az süre</span><span class="sxs-lookup"><span data-stu-id="9dbf8-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="9dbf8-122">Olarak üretim kısıtlamaları içindeki uygun olarak yakın</span><span class="sxs-lookup"><span data-stu-id="9dbf8-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="9dbf8-123">Bu makale bazı belirli üçüncü taraf uygulamalar ve kolaylık sağlamak için örnek olarak belirtilen ürünleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="9dbf8-124">Azure AD destekleyen uygulamalarda binlerce bizim [uygulama Galerisi](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) , gereksinimleri ve ortam bağlı olarak, kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9dbf8-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]