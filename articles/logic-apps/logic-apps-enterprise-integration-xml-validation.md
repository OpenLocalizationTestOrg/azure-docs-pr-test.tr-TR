---
title: aaaValidate XML - Azure Logic Apps | Microsoft Docs
description: "Enterprise Integration Pack Merhaba kullanarak Azure Logic Apps ile B2B senaryoları için şemalarda XML doğrulama"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="bf3ee-103">XML için Kurumsal tümleştirme doğrula</span><span class="sxs-lookup"><span data-stu-id="bf3ee-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="bf3ee-104">Genellikle B2B senaryolarda anlaşmanın hello ortakları veri işleme başlamadan önce bunlar exchange Merhaba iletileri geçerli emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="bf3ee-105">Önceden tanımlanmış bir şemayla belgeleri hello Enterprise Integration Pack hello kullan hello XML doğrulama bağlayıcı kullanarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="bf3ee-106">Bir belgeyi hello XML doğrulama Bağlayıcısı ile doğrula</span><span class="sxs-lookup"><span data-stu-id="bf3ee-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="bf3ee-107">Bir mantıksal uygulama oluşturma ve [bağlantı hello uygulama toohello tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink bir tümleştirme hesap tooa mantıksal uygulama öğrenin") XML verileri doğrulamak için toouse istediğiniz hello şeması vardır.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="bf3ee-108">Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="bf3ee-109">tooadd hello **XML doğrulama** eylemi seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="bf3ee-110">Tüm Eylemler toohello istediğiniz bir hello toofilter girin *xml* hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="bf3ee-111">Seçin **XML doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="bf3ee-112">toospecify hello toovalidate, istediğiniz XML içeriği seçin **içerik**.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="bf3ee-113">Merhaba gövde etiket hello toovalidate istediğiniz içeriği seçin.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="bf3ee-114">Merhaba önceki doğrulamak için toouse istediğiniz toospecify hello şema *içerik* giriş, seçin **şema adı**.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="bf3ee-115">Çalışmanızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="bf3ee-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="bf3ee-116">Şimdi, doğrulama Bağlayıcısı'nı ayarlama ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="bf3ee-117">Gerçek dünya uygulamada toostore doğrulanmış hello veri SalesForce gibi bir satır iş kolu (LOB) uygulamasında isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="bf3ee-118">toosend doğrulanmış çıktı tooSalesforce Merhaba, bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="bf3ee-119">tootest doğrulama eyleminizi bir istek toohello HTTP uç noktası olun.</span><span class="sxs-lookup"><span data-stu-id="bf3ee-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf3ee-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf3ee-120">Next steps</span></span>
[<span data-ttu-id="bf3ee-121">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="bf3ee-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")   

