---
title: "aaaSubscription ve azure'da Windows sanal makineleri için hesapları | Microsoft Docs"
description: "Merhaba abonelikleri ve Azure ile ilgili hesapları için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
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
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="9e250-103">Windows sanal makineleri Azure aboneliği ve hesapları yönergeleri</span><span class="sxs-lookup"><span data-stu-id="9e250-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9e250-104">Bu makalede tooapproach aboneliği ve hesabı yönetim ortamı ve kullanıcı temel olarak nasıl genişletileceğini anlamaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="9e250-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="9e250-105">Abonelikler ve hesapları için uygulama rehberi</span><span class="sxs-lookup"><span data-stu-id="9e250-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="9e250-106">Kararları:</span><span class="sxs-lookup"><span data-stu-id="9e250-106">Decisions:</span></span>

* <span data-ttu-id="9e250-107">Hangi abonelikleri ve hesapları toohost BT iş yükü veya altyapı ihtiyacınız var?</span><span class="sxs-lookup"><span data-stu-id="9e250-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="9e250-108">Nasıl toobreak hello hiyerarşi toofit aşağı kuruluşunuz?</span><span class="sxs-lookup"><span data-stu-id="9e250-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="9e250-109">Görevler:</span><span class="sxs-lookup"><span data-stu-id="9e250-109">Tasks:</span></span>

* <span data-ttu-id="9e250-110">Toomanage istediğiniz gibi mantıksal kuruluş hiyerarşinizi tanımlayın, bir abonelik düzeyinden.</span><span class="sxs-lookup"><span data-stu-id="9e250-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="9e250-111">toomatch bu mantıksal hiyerarşi gereken hello hesaplar ve abonelikler her hesap altında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9e250-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="9e250-112">Merhaba birtakım abonelikleri ve adlandırma kuralınızın kullanarak hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e250-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="9e250-113">Abonelik ve hesaplar</span><span class="sxs-lookup"><span data-stu-id="9e250-113">Subscriptions and accounts</span></span>
<span data-ttu-id="9e250-114">toowork Azure ile bir veya daha fazla Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e250-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="9e250-115">Sanal ağlar bu abonelikleri mevcut veya sanal makineleri (VM'ler) kaynakları gibi.</span><span class="sxs-lookup"><span data-stu-id="9e250-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="9e250-116">Kurumsal müşteriler genellikle hello hiyerarşideki hello en üstteki kaynaktır ve ilişkili tooone ya da daha fazla hesapları olan bir işletme kaydı, vardır.</span><span class="sxs-lookup"><span data-stu-id="9e250-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="9e250-117">Tüketiciler ve kurumsal kayıt olmadan müşteriler için hello en üstteki kaynak hello hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="9e250-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="9e250-118">İlişkili tooaccounts abonelikleri olan ve hesap başına bir veya daha fazla abonelik olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e250-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="9e250-119">Fatura hello abonelik düzeyinde bilgileri azure kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9e250-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="9e250-120">Toohello sınırı hello hesabı/aboneliği ilişkisindeki iki hiyerarşi düzeylerinde, önemli tooalign hello adlandırma kuralı gereksinimlerini faturalama hesaplar ve abonelikler toohello'dir.</span><span class="sxs-lookup"><span data-stu-id="9e250-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="9e250-121">Örneği için bir genel şirket Azure kullanıyorsa, her bölge toohave bir hesap seçebilirsiniz ve abonelikleri adresindeki yönetilen hello bölge düzeyi:</span><span class="sxs-lookup"><span data-stu-id="9e250-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="9e250-122">Örneğin, yapı izlenerek hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e250-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="9e250-123">Bir abonelik ilişkili tooa belirli grubu birden çok toohave bir bölge karar verirse, hello adlandırma kuralı bir şekilde tooencode eklemeniz gerekir hello hello hesabı ya da hello abonelik adı ek veriler.</span><span class="sxs-lookup"><span data-stu-id="9e250-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="9e250-124">Bu kuruluşunuzun fatura veri toogenerate hello yeni hiyerarşi düzeyleri Fatura raporları sırasında massaging olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="9e250-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="9e250-125">Merhaba kuruluş aşağıdaki örneğine hello gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="9e250-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="9e250-126">Bir Kurumsal Anlaşma aracılığıyla indirilebilir bir dosyayı veya tüm hesapları tek bir hesap için ayrıntılı faturalama sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="9e250-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e250-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e250-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

