---
title: "Aboneliği ve azure'da Windows sanal makineleri için hesapları | Microsoft Docs"
description: "Abonelikleri ve Azure ile ilgili hesapları için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b54e18ed6ecef26a059a6ce742bca03a6434183
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="76d61-103">Windows sanal makineleri Azure aboneliği ve hesapları yönergeleri</span><span class="sxs-lookup"><span data-stu-id="76d61-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="76d61-104">Bu makalede ortamınızın olarak abonelik ve hesap yönetim yaklaşımını nasıl anlamaya odaklanır ve kullanıcı tabanını büyür.</span><span class="sxs-lookup"><span data-stu-id="76d61-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="76d61-105">Abonelikler ve hesapları için uygulama rehberi</span><span class="sxs-lookup"><span data-stu-id="76d61-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="76d61-106">Kararları:</span><span class="sxs-lookup"><span data-stu-id="76d61-106">Decisions:</span></span>

* <span data-ttu-id="76d61-107">Hangi birtakım abonelikleri ve hesapları BT iş yükü veya altyapı barındırmak için ihtiyacınız?</span><span class="sxs-lookup"><span data-stu-id="76d61-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="76d61-108">Kuruluşunuz uyacak şekilde hiyerarşide aşağıda ayırmak nasıl?</span><span class="sxs-lookup"><span data-stu-id="76d61-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="76d61-109">Görevler:</span><span class="sxs-lookup"><span data-stu-id="76d61-109">Tasks:</span></span>

* <span data-ttu-id="76d61-110">Bir abonelik düzeyinden yönetmek istediğiniz gibi mantıksal kuruluş hiyerarşinizi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="76d61-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="76d61-111">Bu mantıksal hiyerarşi eşleştirmek için gereken hesaplar ve abonelikler her hesap altında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="76d61-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="76d61-112">Abonelikler ve adlandırma kuralınızın kullanarak hesapları kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="76d61-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="76d61-113">Abonelik ve hesaplar</span><span class="sxs-lookup"><span data-stu-id="76d61-113">Subscriptions and accounts</span></span>
<span data-ttu-id="76d61-114">Azure ile çalışmak için bir veya daha fazla Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="76d61-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="76d61-115">Sanal ağlar bu abonelikleri mevcut veya sanal makineleri (VM'ler) kaynakları gibi.</span><span class="sxs-lookup"><span data-stu-id="76d61-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="76d61-116">Kurumsal müşteriler, hiyerarşideki en üst kaynaktır ve bir veya daha fazla hesaplarına ilişkili olan bir işletme kaydı, genellikle vardır.</span><span class="sxs-lookup"><span data-stu-id="76d61-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="76d61-117">Tüketiciler ve kurumsal kayıt olmadan müşteriler için en üstteki kaynak hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="76d61-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="76d61-118">Abonelik hesaplarına ilişkilendirilmiş ve hesap başına bir veya daha fazla abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="76d61-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="76d61-119">Abonelik düzeyinde bilgi faturalama azure kaydeder.</span><span class="sxs-lookup"><span data-stu-id="76d61-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="76d61-120">Hesabı/aboneliği ilişkisindeki iki hiyerarşi düzeyleri sınırı nedeniyle, hesapları ve fatura gereksinimlerine abonelikleri adlandırma kuralı hizalamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="76d61-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="76d61-121">Örneğin, genel şirket Azure kullanıyorsa, bir hesap bölge başına sahip olmayı seçebilirsiniz ve Abonelikleri, yönetilen bölge düzeyi:</span><span class="sxs-lookup"><span data-stu-id="76d61-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="76d61-122">Örneğin, aşağıdaki yapısını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76d61-122">For instance, you might use the following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="76d61-123">Bir bölge belirli bir gruba ilişkili birden fazla aboneliğiniz varsa karar verirse, adlandırma kuralı hesabı ya da abonelik adını üzerindeki fazladan verileri kodlamak için bir yol eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76d61-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="76d61-124">Bu kuruluş hiyerarşi yeni düzeylerini sırasında fatura raporlar üretmek için faturalama verisi massaging sağlar:</span><span class="sxs-lookup"><span data-stu-id="76d61-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="76d61-125">Kuruluş aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="76d61-125">The organization could look like the following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="76d61-126">Bir Kurumsal Anlaşma aracılığıyla indirilebilir bir dosyayı veya tüm hesapları tek bir hesap için ayrıntılı faturalama sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="76d61-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d61-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76d61-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

