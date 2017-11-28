---
title: "aaaLogic uygulamaları EDIFACT kod çözme B2B gidermek UNH2.5 - Azure Logic Apps | Microsoft Docs"
description: "EDIFACT kod çözme Azure Logic Apps B2B UNH2.5 çözmek"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="8b5ec-103">Nasıl toohandle EDIFACT UNH2.5 sahip belgeleri kesimi</span><span class="sxs-lookup"><span data-stu-id="8b5ec-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="8b5ec-104">UNH2.5 hello EDIFACT belgede mevcut olduğunda, şema arama için kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="8b5ec-105">Örnek: Merhaba UNH alandır **EAN008** hello EDIFACT iletisi</span><span class="sxs-lookup"><span data-stu-id="8b5ec-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="8b5ec-106">UNH + SSDD1 + SİPARİŞLERİ: D: 03B: KALDIRIN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="8b5ec-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="8b5ec-107">Adımları toofollow toohandle hello iletisi</span><span class="sxs-lookup"><span data-stu-id="8b5ec-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="8b5ec-108">Merhaba Şemayı Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8b5ec-108">Update hello schema</span></span>
2. <span data-ttu-id="8b5ec-109">Merhaba sözleşmesi ayarlarını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="8b5ec-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="8b5ec-110">Merhaba Şemayı Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8b5ec-110">Update hello schema</span></span>
<span data-ttu-id="8b5ec-111">tooprocess selamlama iletisine toodeploy hello UNH2.5 kök düğümü adı şemasıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="8b5ec-112">Merhaba şema kök adı verilen bir örnek için olacaktır **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="8b5ec-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="8b5ec-113">Farklı bir UNH2.5 segment ile her D03B_ORDERS için tek bir şema toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="8b5ec-114">Şema toohello EDIFACT sözleşmesi ekleme</span><span class="sxs-lookup"><span data-stu-id="8b5ec-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="8b5ec-115">EDIFACT kod çözme</span><span class="sxs-lookup"><span data-stu-id="8b5ec-115">EDIFACT Decode</span></span>
<span data-ttu-id="8b5ec-116">tooDecode gelen ileti Merhaba, hello şema yapılandırma hello EDIFACT sözleşmesi alma ayarları</span><span class="sxs-lookup"><span data-stu-id="8b5ec-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="8b5ec-117">Merhaba şema toohello tümleştirme hesabı Ekle</span><span class="sxs-lookup"><span data-stu-id="8b5ec-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="8b5ec-118">Merhaba şema yapılandırma hello EDIFACT sözleşmesi ayarları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="8b5ec-119">EDIFACT sözleşmesi tıklatıp **JSON olarak Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="8b5ec-120">Merhaba alma sözleşmesinde UNH2.5 değeri eklemek **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8b5ec-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="8b5ec-121">EDIFACT kodlama</span><span class="sxs-lookup"><span data-stu-id="8b5ec-121">EDIFACT Encode</span></span>
<span data-ttu-id="8b5ec-122">tooEncode gelen ileti Merhaba, hello şema hello EDIFACT sözleşmesi gönderme ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8b5ec-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="8b5ec-123">Merhaba şema toohello tümleştirme hesabı Ekle</span><span class="sxs-lookup"><span data-stu-id="8b5ec-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="8b5ec-124">Merhaba şema hello EDIFACT sözleşmesi gönderme ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="8b5ec-125">EDIFACT sözleşmesi tıklatıp **JSON olarak Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="8b5ec-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="8b5ec-126">Merhaba Gönderme Sözleşmesi UNH2.5 değeri eklemek **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="8b5ec-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b5ec-127">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8b5ec-127">Next Steps</span></span>
* [<span data-ttu-id="8b5ec-128">Tümleştirme hesap anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="8b5ec-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  