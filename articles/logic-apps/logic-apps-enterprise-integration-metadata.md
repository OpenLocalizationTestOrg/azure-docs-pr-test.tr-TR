---
title: "aaaManage tümleştirme Azure Logic Apps yapı meta verileri - hesap | Microsoft Docs"
description: "Ekleme veya yapı meta veri tümleştirme hesaplarından Azure Logic Apps için alma"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="24992-103">Tümleştirme hesapları logic apps için yapı meta verilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="24992-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="24992-104">Bu meta veri çalışma zamanı sırasında mantıksal uygulamanızı almak ve tümleştirme hesaplarında yapıları için özel meta verileri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="24992-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="24992-105">Örneğin, iş ortakları, anlaşmalar, şemalar ve haritalar gibi yapıları için meta veri belirtebilirsiniz - tüm anahtar-değer çiftleri kullanarak meta verileri depolama.</span><span class="sxs-lookup"><span data-stu-id="24992-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="24992-106">Şu anda kullanıcı Arabirimi aracılığıyla meta veri yapıları oluşturulamıyor, ancak REST API'leri toocreate meta verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24992-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="24992-107">oluşturduğunuzda ya da bir iş ortağı, anlaşma ya da şema hello Azure portal seçin tooadd meta veri seçin **JSON olarak Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="24992-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="24992-108">tooretrieve yapı logic apps meta verileri, hello tümleştirme hesap yapı arama özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24992-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="24992-109">Meta veri tooartifacts tümleştirme hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="24992-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="24992-110">Oluşturma bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="24992-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="24992-111">Örneğin bir yapı tooyour tümleştirme hesap ekleyin, bir [iş ortağı](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [sözleşmesi](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), veya [şema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="24992-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="24992-112">Merhaba yapı seçin, **JSON olarak Düzenle**ve meta veri ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="24992-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Meta veri girin](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="24992-114">Logic apps için yapılardan meta veri alma</span><span class="sxs-lookup"><span data-stu-id="24992-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="24992-115">Oluşturma bir [mantıksal uygulama](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="24992-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="24992-116">Oluşturma bir [mantığı uygulama tooyour tümleştirme hesabınızı bağlantısından](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="24992-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="24992-117">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici gibi ekleme *isteği* veya *HTTP* tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="24992-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="24992-118">Seçin **sonraki adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="24992-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="24992-119">Arama *tümleştirme* bulun ve ardından **tümleştirme hesabı - tümleştirme hesap yapı arama**.</span><span class="sxs-lookup"><span data-stu-id="24992-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Tümleştirme hesap yapı arama seçin](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="24992-121">Select hello **yapay nesne türü**ve hello sağlamak **yapı adı**.</span><span class="sxs-lookup"><span data-stu-id="24992-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Yapay nesne türü seçin ve yapı adı belirtin](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="24992-123">Örnek: Alma ortak meta veriler</span><span class="sxs-lookup"><span data-stu-id="24992-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="24992-124">İş ortağı meta veri olan bu `routingUrl` ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="24992-124">Partner metadata has these `routingUrl` details:</span></span>

![İş ortağı "routingURL" meta veri bulma](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="24992-126">Mantıksal uygulamanızı, tetikleyici eklemek bir **tümleştirme hesabı - tümleştirme hesap yapı arama** için iş ortağınızla için eylem ve bir **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="24992-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Tetikleyici, yapı arama ve "HTTP" tooyour mantıksal uygulama Ekle](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="24992-128">tooretrieve hello URI, mantıksal uygulamanız için Görünüm tooCode gidin.</span><span class="sxs-lookup"><span data-stu-id="24992-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="24992-129">Mantıksal uygulama tanımını bu örnekteki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="24992-129">Your logic app definition should look like this example:</span></span>

    ![Arama arama](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="24992-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24992-131">Next steps</span></span>
* [<span data-ttu-id="24992-132">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="24992-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
