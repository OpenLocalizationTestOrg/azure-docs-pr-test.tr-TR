---
title: "işletmeden işletmeye (B2B) iletileri - Azure Logic Apps aaaCreate ortakları | Microsoft Docs"
description: "Tooadd ortakları tooyour tümleştirme nasıl hesap hello Kurumsal tümleştirme paketi ve Logic Apps ile bilgi edinin"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="863f4-103">Ekleyin veya iş iş akışınızı sözleşmelerde ortakları güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="863f4-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="863f4-104">İşletmeden işletmeye (B2B) işlemlere katılmasına ve birbirleri arasındaki iletileri exchange varlıklar ortaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="863f4-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="863f4-105">Ve bu işlemler başka bir kuruluştaki temsil eden iş ortakları oluşturabilmeniz için önce her ikisi gerekir tanımlar ve diğer tarafından gönderilen iletileri doğrular bilgileri paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="863f4-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="863f4-106">Bu ayrıntıları ele almaktadır ve iş ilişkiniz hazır toostart olan sonra tümleştirme hesap toorepresent ortakları oluşturabilirsiniz, her iki.</span><span class="sxs-lookup"><span data-stu-id="863f4-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="863f4-107">Hangi rollerin ortakları tümleştirme hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="863f4-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="863f4-108">İş ortakları arasında alınıp hello ileti ayrıntılarını toodefine, bu iş ortakları arasında anlaşmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="863f4-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="863f4-109">Ancak, bir anlaşma oluşturabilmeniz için önce en az iki iş ortağı tooyour tümleştirme hesabın eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="863f4-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="863f4-110">Kuruluşunuz hello sözleşmesi hello olarak bir parçası olması **ana iş ortağı**.</span><span class="sxs-lookup"><span data-stu-id="863f4-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="863f4-111">diğer iş ortağı hello veya **Konuk iş ortağı** Merhaba iletileri kuruluşunuz ile alış verişleri kuruluş temsil eder.</span><span class="sxs-lookup"><span data-stu-id="863f4-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="863f4-112">Merhaba Konuk iş ortağı, başka bir şirket veya bile bir bölüm veya kendi kuruluşunuzdaki olabilir.</span><span class="sxs-lookup"><span data-stu-id="863f4-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="863f4-113">Bu iş ortaklarının ekledikten sonra bir anlaşma oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="863f4-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="863f4-114">Alma ve gönderme ayarlarını hello açısından bakıldığında hello barındırılan iş ortağı olarak yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="863f4-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="863f4-115">Örneğin, hello alma ayarlarını bir anlaşma barındırılan hello ortak bir konuk ortağından gönderilen iletilerin nasıl aldığını belirlemek.</span><span class="sxs-lookup"><span data-stu-id="863f4-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="863f4-116">Benzer şekilde, nasıl barındırılan hello ortağı iletileri toohello Konuk iş ortağı gönderir hello anlaşmasında hello gönderme ayarlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="863f4-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="863f4-117">Nasıl toocreate bir iş ortağı?</span><span class="sxs-lookup"><span data-stu-id="863f4-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="863f4-118">Hello Azure portal, seçin **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="863f4-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="863f4-119">Merhaba filtre arama kutusuna **tümleştirme**seçeneğini belirleyip **tümleştirme hesapları** hello sonuçları listesinde.</span><span class="sxs-lookup"><span data-stu-id="863f4-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="863f4-120">Merhaba tümleştirme hesabı ortaklarınızdan tooadd istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="863f4-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="863f4-121">Select hello **ortakları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="863f4-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="863f4-122">Merhaba ortakları dikey penceresinde, seçin **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="863f4-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="863f4-123">İş ortağınız için bir ad girin ve ardından bir **niteleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="863f4-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="863f4-124">Son olarak, girin bir **değeri** toohelp uygulamalarınızla gelen belgeleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="863f4-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="863f4-125">select Merhaba, iş ortağı oluşturma işlemi için toosee hello ilerlemesi *zil* bildirim simgesi.</span><span class="sxs-lookup"><span data-stu-id="863f4-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="863f4-126">Yeni iş ortaklarınıza başarıyla olan tooconfirm eklenen, select hello **ortakları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="863f4-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="863f4-127">Merhaba ortakları döşeme seçtikten sonra yeni eklenen iş ortakları hello ortakları dikey penceresinde de görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="863f4-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="863f4-128">Tooedit varolan tümleştirme hesabınızı nasıl ortakları</span><span class="sxs-lookup"><span data-stu-id="863f4-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="863f4-129">Select hello **ortakları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="863f4-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="863f4-130">Merhaba ortakları dikey penceresi açıldıktan sonra tooedit istediğiniz hello ortağı seçin.</span><span class="sxs-lookup"><span data-stu-id="863f4-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="863f4-131">Merhaba üzerinde **güncelleştirme iş ortağı** döşeme, istediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="863f4-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="863f4-132">Bitirdikten sonra seçin **kaydetmek**, veya toocancel yaptığınız değişiklikleri seçin **atmak**.</span><span class="sxs-lookup"><span data-stu-id="863f4-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="863f4-133">Nasıl toodelete bir iş ortağı</span><span class="sxs-lookup"><span data-stu-id="863f4-133">How toodelete a partner</span></span>

1. <span data-ttu-id="863f4-134">Select hello **ortakları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="863f4-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="863f4-135">Hello iş ortağı dikey penceresi açıldıktan sonra hello ortağı toodelete istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="863f4-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="863f4-136">Seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="863f4-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="863f4-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="863f4-137">Next steps</span></span>
* [<span data-ttu-id="863f4-138">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="863f4-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  

