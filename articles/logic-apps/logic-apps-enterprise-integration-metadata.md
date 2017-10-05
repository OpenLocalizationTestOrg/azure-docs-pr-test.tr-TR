---
title: "Tümleştirme hesap yapı meta verileri - Azure mantıksal uygulamaları yönetme | Microsoft Docs"
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
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="32e90-103">Tümleştirme hesapları logic apps için yapı meta verilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="32e90-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="32e90-104">Bu meta veri çalışma zamanı sırasında mantıksal uygulamanızı almak ve tümleştirme hesaplarında yapıları için özel meta verileri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="32e90-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="32e90-105">Örneğin, iş ortakları, anlaşmalar, şemalar ve haritalar gibi yapıları için meta veri belirtebilirsiniz - tüm anahtar-değer çiftleri kullanarak meta verileri depolama.</span><span class="sxs-lookup"><span data-stu-id="32e90-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="32e90-106">Şu anda kullanıcı Arabirimi aracılığıyla meta veri yapıları oluşturulamıyor, ancak meta verileri oluşturmak için REST API'ler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32e90-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="32e90-107">Oluşturduğunuzda ya da bir iş ortağı, anlaşma ya da şema Azure portalında seçin meta veri eklemek için **JSON olarak Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="32e90-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="32e90-108">Logic apps içinde yapı meta verilerini almak için tümleştirme hesap yapı arama özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32e90-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="32e90-109">Meta veri yapıları tümleştirme hesapları ekleyin</span><span class="sxs-lookup"><span data-stu-id="32e90-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="32e90-110">Oluşturma bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="32e90-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="32e90-111">Örneğin bir yapı tümleştirme hesabınıza ekleyin, bir [iş ortağı](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [sözleşmesi](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), veya [şema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="32e90-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="32e90-112">Yapıyı seçin, **JSON olarak Düzenle**ve meta veri ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="32e90-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Meta veri girin](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="32e90-114">Logic apps için yapılardan meta veri alma</span><span class="sxs-lookup"><span data-stu-id="32e90-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="32e90-115">Oluşturma bir [mantıksal uygulama](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32e90-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="32e90-116">Oluşturma bir [mantıksal uygulamanızı bir bağlantıdan tümleştirme hesabınıza](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="32e90-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="32e90-117">Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici gibi ekleme *isteği* veya *HTTP* mantığı uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="32e90-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="32e90-118">Seçin **sonraki adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="32e90-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="32e90-119">Arama *tümleştirme* bulun ve ardından **tümleştirme hesabı - tümleştirme hesap yapı arama**.</span><span class="sxs-lookup"><span data-stu-id="32e90-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Tümleştirme hesap yapı arama seçin](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="32e90-121">Seçin **yapay nesne türü**ve sağlamak **yapı adı**.</span><span class="sxs-lookup"><span data-stu-id="32e90-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Yapay nesne türü seçin ve yapı adı belirtin](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="32e90-123">Örnek: Alma ortak meta veriler</span><span class="sxs-lookup"><span data-stu-id="32e90-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="32e90-124">İş ortağı meta veri olan bu `routingUrl` ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="32e90-124">Partner metadata has these `routingUrl` details:</span></span>

![İş ortağı "routingURL" meta veri bulma](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="32e90-126">Mantıksal uygulamanızı, tetikleyici eklemek bir **tümleştirme hesabı - tümleştirme hesap yapı arama** için iş ortağınızla için eylem ve bir **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="32e90-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Tetikleyici, yapı arama ve "HTTP" mantıksal uygulamanızı ekleme](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="32e90-128">URI'yi almak için mantığı uygulamanız için kod görünümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="32e90-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="32e90-129">Mantıksal uygulama tanımını bu örnekteki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="32e90-129">Your logic app definition should look like this example:</span></span>

    ![Arama arama](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="32e90-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32e90-131">Next steps</span></span>
* [<span data-ttu-id="32e90-132">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="32e90-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
