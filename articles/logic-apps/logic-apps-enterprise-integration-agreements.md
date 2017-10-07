---
title: "B2B iletişim - Azure Logic Apps için aaaAgreements | Microsoft Docs"
description: "Ortaklar B2B senaryolarda Azure Logic Apps ve hello Kurumsal tümleştirme paketi için iletişim kurabilmesi anlaşmaları oluşturma"
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
ms.openlocfilehash: 499edcbab1cd67fbc169e393c3cad7b81658a250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="6d644-103">Azure mantıksal uygulamaları ve Enterprise Integration Pack B2B iletişim için ortak sözleşmeleri</span><span class="sxs-lookup"><span data-stu-id="6d644-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="6d644-104">Anlaşmaları hello dönüm işletmeden işletmeye (B2B) iletişimi için olan ve daha sorunsuz bir şekilde endüstri standardı protokoller kullanarak iletişim kuran iş varlıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d644-104">Agreements let business entities communicate seamlessly using industry standard protocols and are hello cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="6d644-105">Logic apps hello Kurumsal tümleştirme paketi ile B2B senaryolarını etkinleştirilirken bir sözleşmesi ticari ortaklar B2B arasındaki iletişimler düzenleme yer alır.</span><span class="sxs-lookup"><span data-stu-id="6d644-105">When enabling B2B scenarios for logic apps with hello Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="6d644-106">Bu anlaşma hello ortakları istediğiniz iletişimleri çok kurmak ve protokolü veya taşıma özgü hello üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="6d644-106">This agreement is based on hello communications that hello partners want too establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="6d644-107">Kurumsal tümleştirme bu protokolü veya taşıma standartlarını destekler:</span><span class="sxs-lookup"><span data-stu-id="6d644-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="6d644-108">AS2</span><span class="sxs-lookup"><span data-stu-id="6d644-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="6d644-109">X12</span><span class="sxs-lookup"><span data-stu-id="6d644-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="6d644-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="6d644-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="6d644-111">Neden anlaşmalarını kullanın</span><span class="sxs-lookup"><span data-stu-id="6d644-111">Why use agreements</span></span>

<span data-ttu-id="6d644-112">Anlaşmaları kullanırken sık karşılaşılan bazı avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6d644-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="6d644-113">İyi bilinen bir biçimde farklı organizasyonlar ve işletmeler tooexchange bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d644-113">Enables different organizations and businesses tooexchange information in a well-known format.</span></span>
* <span data-ttu-id="6d644-114">B2B işlemleri yürütülürken verimliliğini artırır</span><span class="sxs-lookup"><span data-stu-id="6d644-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="6d644-115">Kolay toocreate, yönetmek ve kurumsal tümleştirme uygulamaları oluştururken kullanın</span><span class="sxs-lookup"><span data-stu-id="6d644-115">Easy toocreate, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-toocreate-agreements"></a><span data-ttu-id="6d644-116">Nasıl toocreate anlaşmaları</span><span class="sxs-lookup"><span data-stu-id="6d644-116">How toocreate agreements</span></span>

* [<span data-ttu-id="6d644-117">AS2 sözleşmesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d644-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="6d644-118">Bir X12 oluşturma Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="6d644-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="6d644-119">EDIFACT sözleşmesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="6d644-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-toouse-an-agreement"></a><span data-ttu-id="6d644-120">Nasıl toouse sözleşme</span><span class="sxs-lookup"><span data-stu-id="6d644-120">How toouse an agreement</span></span>

<span data-ttu-id="6d644-121">Oluşturabileceğiniz [logic apps](logic-apps-what-are-logic-apps.md "Logic apps hakkında daha fazla bilgi") oluşturduğunuz sözleşme kullanarak B2B özelliklerine sahip.</span><span class="sxs-lookup"><span data-stu-id="6d644-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-tooedit-an-agreement"></a><span data-ttu-id="6d644-122">Nasıl tooedit sözleşme</span><span class="sxs-lookup"><span data-stu-id="6d644-122">How tooedit an agreement</span></span>

<span data-ttu-id="6d644-123">Aşağıdaki adımları izleyerek herhangi anlaşmayı düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d644-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="6d644-124">Merhaba tümleştirme tooupdate istediğiniz hello sözleşmesi olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="6d644-124">Select hello integration account that has hello agreement you want tooupdate.</span></span>

2. <span data-ttu-id="6d644-125">Merhaba seçin **anlaşmaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="6d644-125">Choose hello **Agreements** tile.</span></span>

3. <span data-ttu-id="6d644-126">Merhaba üzerinde **anlaşmaları** dikey penceresinde, select hello anlaşma.</span><span class="sxs-lookup"><span data-stu-id="6d644-126">On hello **Agreements** blade, select hello agreement.</span></span>

4. <span data-ttu-id="6d644-127">Seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="6d644-127">Choose **Edit**.</span></span> <span data-ttu-id="6d644-128">İstediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="6d644-128">Make your changes.</span></span>

5. <span data-ttu-id="6d644-129">yaptığınız değişiklikleri toosave seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6d644-129">toosave your changes, choose **OK**.</span></span>

## <a name="how-toodelete-an-agreement"></a><span data-ttu-id="6d644-130">Nasıl toodelete sözleşme</span><span class="sxs-lookup"><span data-stu-id="6d644-130">How toodelete an agreement</span></span>

<span data-ttu-id="6d644-131">Aşağıdaki adımları izleyerek herhangi bir anlaşması silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d644-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="6d644-132">Merhaba tümleştirme toodelete istediğiniz hello sözleşmesi olan bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="6d644-132">Select hello integration account that has hello agreement you want toodelete.</span></span>
2. <span data-ttu-id="6d644-133">Merhaba seçin **anlaşmaları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="6d644-133">Choose hello **Agreements** tile.</span></span>
3. <span data-ttu-id="6d644-134">Merhaba üzerinde **anlaşmaları** dikey penceresinde, select hello anlaşma.</span><span class="sxs-lookup"><span data-stu-id="6d644-134">On hello **Agreements** blade, select hello agreement.</span></span>
4. <span data-ttu-id="6d644-135">Seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="6d644-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="6d644-136">Toodelete seçili hello sözleşmesi istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="6d644-136">Confirm that you want toodelete hello selected agreement.</span></span>

    <span data-ttu-id="6d644-137">Merhaba anlaşmaları dikey artık silinen hello anlaşmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6d644-137">hello Agreements blade no longer shows hello deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d644-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d644-138">Next steps</span></span>
* [<span data-ttu-id="6d644-139">AS2 sözleşmesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d644-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
