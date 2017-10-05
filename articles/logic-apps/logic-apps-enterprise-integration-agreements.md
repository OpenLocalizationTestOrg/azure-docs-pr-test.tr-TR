---
title: "B2B iletişim - Azure Logic Apps sözleşmelerini | Microsoft Docs"
description: "Ortaklar B2B senaryolarda Azure Logic Apps ve kurumsal tümleştirme paketi için iletişim kurabilmesi anlaşmaları oluşturma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="c76cd-103">Azure mantıksal uygulamaları ve Enterprise Integration Pack B2B iletişim için ortak sözleşmeleri</span><span class="sxs-lookup"><span data-stu-id="c76cd-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="c76cd-104">Anlaşmaları dönüm işletmeden işletmeye (B2B) iletişimi için olan ve daha sorunsuz bir şekilde endüstri standardı protokoller kullanarak iletişim kuran iş varlıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c76cd-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="c76cd-105">Logic apps Enterprise tümleştirme paketi ile B2B senaryolarını etkinleştirilirken bir sözleşmesi ticari ortaklar B2B arasındaki iletişimler düzenleme yer alır.</span><span class="sxs-lookup"><span data-stu-id="c76cd-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="c76cd-106">Bu anlaşma ortakları kurmak istiyorsanız ve protokolü iletişimi göre veya taşıma özgü değildir.</span><span class="sxs-lookup"><span data-stu-id="c76cd-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="c76cd-107">Kurumsal tümleştirme bu protokolü veya taşıma standartlarını destekler:</span><span class="sxs-lookup"><span data-stu-id="c76cd-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="c76cd-108">AS2</span><span class="sxs-lookup"><span data-stu-id="c76cd-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="c76cd-109">X12</span><span class="sxs-lookup"><span data-stu-id="c76cd-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="c76cd-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c76cd-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="c76cd-111">Neden anlaşmalarını kullanın</span><span class="sxs-lookup"><span data-stu-id="c76cd-111">Why use agreements</span></span>

<span data-ttu-id="c76cd-112">Anlaşmaları kullanırken sık karşılaşılan bazı avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c76cd-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="c76cd-113">Farklı Kuruluş ve işletmelerin bilgileri bilinen bir biçimde exchange sağlar.</span><span class="sxs-lookup"><span data-stu-id="c76cd-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="c76cd-114">B2B işlemleri yürütülürken verimliliğini artırır</span><span class="sxs-lookup"><span data-stu-id="c76cd-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="c76cd-115">Kolay oluşturmak, yönetmek ve kurumsal tümleştirme uygulamaları oluştururken kullanın</span><span class="sxs-lookup"><span data-stu-id="c76cd-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="c76cd-116">Anlaşmaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c76cd-116">How to create agreements</span></span>

* [<span data-ttu-id="c76cd-117">AS2 sözleşmesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c76cd-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="c76cd-118">Bir X12 oluşturma Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="c76cd-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="c76cd-119">EDIFACT sözleşmesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="c76cd-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="c76cd-120">Bir anlaşma kullanma</span><span class="sxs-lookup"><span data-stu-id="c76cd-120">How to use an agreement</span></span>

<span data-ttu-id="c76cd-121">Oluşturabileceğiniz [logic apps](logic-apps-what-are-logic-apps.md "Logic apps hakkında daha fazla bilgi") oluşturduğunuz sözleşme kullanarak B2B özelliklerine sahip.</span><span class="sxs-lookup"><span data-stu-id="c76cd-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="c76cd-122">Bir anlaşma düzenleme</span><span class="sxs-lookup"><span data-stu-id="c76cd-122">How to edit an agreement</span></span>

<span data-ttu-id="c76cd-123">Aşağıdaki adımları izleyerek herhangi anlaşmayı düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c76cd-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="c76cd-124">Güncelleştirmek istediğiniz sözleşmesi olduğundan tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="c76cd-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="c76cd-125">Seçin **anlaşmaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="c76cd-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="c76cd-126">Üzerinde **anlaşmaları** dikey penceresinde anlaşmasını seçin.</span><span class="sxs-lookup"><span data-stu-id="c76cd-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="c76cd-127">Seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="c76cd-127">Choose **Edit**.</span></span> <span data-ttu-id="c76cd-128">İstediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="c76cd-128">Make your changes.</span></span>

5. <span data-ttu-id="c76cd-129">Değişikliklerinizi kaydetmek üzere seçim yapın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c76cd-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="c76cd-130">Bir anlaşma silme</span><span class="sxs-lookup"><span data-stu-id="c76cd-130">How to delete an agreement</span></span>

<span data-ttu-id="c76cd-131">Aşağıdaki adımları izleyerek herhangi bir anlaşması silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c76cd-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="c76cd-132">Silmek istediğiniz sözleşmesi olduğundan tümleştirme hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="c76cd-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="c76cd-133">Seçin **anlaşmaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="c76cd-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="c76cd-134">Üzerinde **anlaşmaları** dikey penceresinde anlaşmasını seçin.</span><span class="sxs-lookup"><span data-stu-id="c76cd-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="c76cd-135">Seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c76cd-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="c76cd-136">Seçilen anlaşmayı silmek istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="c76cd-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="c76cd-137">Anlaşmaları dikey artık silinen anlaşmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c76cd-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c76cd-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c76cd-138">Next steps</span></span>
* [<span data-ttu-id="c76cd-139">AS2 sözleşmesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c76cd-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
