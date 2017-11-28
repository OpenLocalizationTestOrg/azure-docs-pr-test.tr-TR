---
title: XSLT haritalar - Azure Logic Apps ile XML aaaTransform | Microsoft Docs
description: "XSLT tootransform XML verileriyle Azure Logic Apps ve Enterprise Integration Pack Merhaba eşlemeleri ekleme"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="52759-103">XML veri dönüştürme için eşlemeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="52759-103">Add maps for XML data transform</span></span>

<span data-ttu-id="52759-104">Enterprise Integration kullanır tootransform XML veri biçimleri arasında eşler.</span><span class="sxs-lookup"><span data-stu-id="52759-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="52759-105">Bir harita başka bir biçime dönüştürülmesi gereken bir belgedeki hello verileri tanımlayan bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="52759-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="52759-106">Maps neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="52759-106">Why use maps?</span></span>

<span data-ttu-id="52759-107">Düzenli olarak B2B sipariş veya fatura tarihlerini hello YYYMMDD biçimi kullanan bir müşterinin aldığınız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="52759-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="52759-108">Ancak, kuruluşunuzda hello MMDDYYY biçimindeki tarihler depolar.</span><span class="sxs-lookup"><span data-stu-id="52759-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="52759-109">Bir harita kullanabileceğine*dönüştürme* hello YYYMMDD tarih biçimine hello sipariş veya fatura ayrıntıları müşteri etkinlik veritabanınızda depolamak önce MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="52759-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="52759-110">Bir harita nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="52759-110">How do I create a map?</span></span>

<span data-ttu-id="52759-111">BizTalk tümleştirme projeleri ile Merhaba oluşturabilirsiniz [Kurumsal tümleştirme paketi](logic-apps-enterprise-integration-overview.md "hello Kurumsal tümleştirme paketi hakkında bilgi edinin") Visual Studio 2015 için.</span><span class="sxs-lookup"><span data-stu-id="52759-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="52759-112">Daha sonra görsel öğeleri iki XML şema dosyaları arasında eşlemenize olanak sağlayan bir tümleştirme haritası dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52759-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="52759-113">Bu projeyi derledikten sonra XSLT belge sahip olur.</span><span class="sxs-lookup"><span data-stu-id="52759-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="52759-114">Bir harita nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="52759-114">How do I add a map?</span></span>

1. <span data-ttu-id="52759-115">Hello Azure portal, seçin **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="52759-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="52759-116">Merhaba filtre arama kutusuna **tümleştirme**seçeneğini belirleyip **tümleştirme hesapları** hello sonuçları listesinden.</span><span class="sxs-lookup"><span data-stu-id="52759-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="52759-117">Merhaba tümleştirme hesabı tooadd hello harita istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="52759-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="52759-118">Select hello **eşlemeleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="52759-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="52759-119">Merhaba eşlemeleri dikey penceresi açıldıktan sonra Seç **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="52759-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="52759-120">Girin bir **adı** haritanızı için.</span><span class="sxs-lookup"><span data-stu-id="52759-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="52759-121">tooupload hello harita dosya, hello klasör simgesine hello hello sağ tarafındaki seçin **harita** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="52759-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="52759-122">Merhaba karşıya yükleme işlemi tamamlandıktan sonra Seç **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="52759-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="52759-123">Azure hello harita tooyour tümleştirme hesabını ekledikten sonra harita dosya veya eklenmiş olan gösteren bir ekranda iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="52759-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="52759-124">Bu iletiyi aldıktan sonra hello seçin **eşlemeleri** hello yeni görüntüleyebilmeniz döşeme eşlemesi eklendi.</span><span class="sxs-lookup"><span data-stu-id="52759-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="52759-125">Bir harita düzenleme nasıl?</span><span class="sxs-lookup"><span data-stu-id="52759-125">How do I edit a map?</span></span>

<span data-ttu-id="52759-126">Yeni bir harita dosyası istediğiniz hello değişikliklerle yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="52759-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="52759-127">Merhaba harita düzenlemek için önce yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52759-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="52759-128">tooupload hello varolan harita, yerini alan yeni bir harita şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="52759-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="52759-129">Merhaba seçin **eşlemeleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="52759-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="52759-130">Merhaba eşlemeleri dikey penceresi açıldıktan sonra hello harita tooedit istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="52759-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="52759-131">Merhaba üzerinde **eşlemeleri** dikey penceresinde, seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="52759-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="52759-132">Merhaba dosya seçicide tooupload istediğiniz sonra seçin hello eşleme dosyasını seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="52759-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="52759-133">Nasıl toodelete bir harita?</span><span class="sxs-lookup"><span data-stu-id="52759-133">How toodelete a map?</span></span>

1. <span data-ttu-id="52759-134">Merhaba seçin **eşlemeleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="52759-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="52759-135">Merhaba eşlemeleri dikey penceresi açıldıktan sonra toodelete istediğiniz hello harita seçin.</span><span class="sxs-lookup"><span data-stu-id="52759-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="52759-136">Seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="52759-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="52759-137">Toodelete hello harita istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="52759-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="52759-138">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="52759-138">Next Steps</span></span>
* [<span data-ttu-id="52759-139">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="52759-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  
* [<span data-ttu-id="52759-140">Anlaşmaları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="52759-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
* [<span data-ttu-id="52759-141">Dönüşümler hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="52759-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Kurumsal tümleştirme dönüşümler hakkında bilgi edinin")  

