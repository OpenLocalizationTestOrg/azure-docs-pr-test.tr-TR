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
# <a name="add-maps-for-xml-data-transform"></a>XML veri dönüştürme için eşlemeleri ekleme

Enterprise Integration kullanır tootransform XML veri biçimleri arasında eşler. Bir harita başka bir biçime dönüştürülmesi gereken bir belgedeki hello verileri tanımlayan bir XML dosyasıdır. 

## <a name="why-use-maps"></a>Maps neden kullanılır?

Düzenli olarak B2B sipariş veya fatura tarihlerini hello YYYMMDD biçimi kullanan bir müşterinin aldığınız varsayalım. Ancak, kuruluşunuzda hello MMDDYYY biçimindeki tarihler depolar. Bir harita kullanabileceğine*dönüştürme* hello YYYMMDD tarih biçimine hello sipariş veya fatura ayrıntıları müşteri etkinlik veritabanınızda depolamak önce MMDDYYY hello.

## <a name="how-do-i-create-a-map"></a>Bir harita nasıl oluşturulur?

BizTalk tümleştirme projeleri ile Merhaba oluşturabilirsiniz [Kurumsal tümleştirme paketi](logic-apps-enterprise-integration-overview.md "hello Kurumsal tümleştirme paketi hakkında bilgi edinin") Visual Studio 2015 için. Daha sonra görsel öğeleri iki XML şema dosyaları arasında eşlemenize olanak sağlayan bir tümleştirme haritası dosyası oluşturabilirsiniz. Bu projeyi derledikten sonra XSLT belge sahip olur.

## <a name="how-do-i-add-a-map"></a>Bir harita nasıl eklenir?

1. Hello Azure portal, seçin **Gözat**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Merhaba filtre arama kutusuna **tümleştirme**seçeneğini belirleyip **tümleştirme hesapları** hello sonuçları listesinden.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Merhaba tümleştirme hesabı tooadd hello harita istediğiniz yeri seçin.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Select hello **eşlemeleri** döşeme.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Merhaba eşlemeleri dikey penceresi açıldıktan sonra Seç **Ekle**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Girin bir **adı** haritanızı için. tooupload hello harita dosya, hello klasör simgesine hello hello sağ tarafındaki seçin **harita** metin kutusu. Merhaba karşıya yükleme işlemi tamamlandıktan sonra Seç **Tamam**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Azure hello harita tooyour tümleştirme hesabını ekledikten sonra harita dosya veya eklenmiş olan gösteren bir ekranda iletisi alırsınız. Bu iletiyi aldıktan sonra hello seçin **eşlemeleri** hello yeni görüntüleyebilmeniz döşeme eşlemesi eklendi.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Bir harita düzenleme nasıl?

Yeni bir harita dosyası istediğiniz hello değişikliklerle yüklemeniz gerekir. Merhaba harita düzenlemek için önce yükleyebilirsiniz.

tooupload hello varolan harita, yerini alan yeni bir harita şu adımları izleyin.

1. Merhaba seçin **eşlemeleri** döşeme.

2. Merhaba eşlemeleri dikey penceresi açıldıktan sonra hello harita tooedit istediğinizi seçin.

3. Merhaba üzerinde **eşlemeleri** dikey penceresinde, seçin **güncelleştirme**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. Merhaba dosya seçicide tooupload istediğiniz sonra seçin hello eşleme dosyasını seçin **açık**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Nasıl toodelete bir harita?

1. Merhaba seçin **eşlemeleri** döşeme.

2. Merhaba eşlemeleri dikey penceresi açıldıktan sonra toodelete istediğiniz hello harita seçin.

3. Seçin **silmek**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Toodelete hello harita istediğinizi onaylayın.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Sonraki Adımlar
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  
* [Anlaşmaları hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
* [Dönüşümler hakkında daha fazla bilgi](logic-apps-enterprise-integration-transform.md "Kurumsal tümleştirme dönüşümler hakkında bilgi edinin")  

