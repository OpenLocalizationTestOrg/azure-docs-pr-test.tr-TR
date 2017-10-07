---
title: aaaEncode X12 iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve XML ile kodlanmış Dönüştür X12 iletilerle ileti Kodlayıcısı hello Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>X12 kodlamak hello Kurumsal tümleştirme paketi ile Azure Logic Apps için iletileri

Merhaba kodla X12 ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, XML olarak kodlanmış iletileri EDI işlem hello değişim kümelerinde dönüştürmek ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.
toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kodla X12 ileti Bağlayıcısı olması gerekir.
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="encode-x12-messages"></a>X12 kodlamak iletileri

1. [Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodla X12 ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3.  Merhaba arama kutusuna "x12" filtreniz için girin. Şunlardan birini seçin **X12-tooX12 ileti sözleşmesi adıyla kodlamak** veya **X12-tooX12 iletisi kimlikleri tarafından kodla**.
   
    !["X12" için arama](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin. 
   
    ![Tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

5.  İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir. bağlantı oluşturma toofinish seçin **oluşturma**.

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    Bağlantınızı şimdi oluşturulur.

    ![Tümleştirme hesap bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>X12 kodlamak iletileri göre anlaşma adı

Anlaşma adı tarafından tooencode X12 iletileri seçerseniz hello açmak **X12 adını anlaşma** listesinde, girin veya mevcut X12 seçin anlaşma. Merhaba XML ileti tooencode girin.

![X12 girin adı ve XML tooencode ileti sözleşmesi](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>X12 kodlamak kimlikleri iletileri

Kimlikleri tarafından tooencode X12 iletileri seçerseniz hello gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve alıcı Niteleyici, X12 yapılandırıldığı gibi girin anlaşma. Merhaba XML ileti tooencode seçin.
   
![Göndereni ve alıcısı için kimlikleri sağlamak için XML ileti tooencode seçin](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 kodlamak ayrıntıları

Merhaba X12 kodla connector, şu görevleri gerçekleştirir:

* Eşleşen göndereni ve alıcısı bağlam özellikleri tarafından sözleşmesi çözünürlüğü.
* EDI işlem hello değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme hello EDI değişim serileştirir.
* İşlem kümesi üstbilgi ve toplamı kesimleri uygular
* Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur
* Ayırıcı hello yükü veri olarak değiştirir
* EDI ve iş ortağı özgü özellikleri doğrular
  * Selamlama iletisine şema karşı hello işlem kümesi veri öğelerinin şema doğrulaması
  * EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.
  * İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın
* Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.
  * Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur. Merhaba Teknik Bildirim hello bir değişim üstbilgi ve toplamı hello adresi alıcı tarafından işlenmesini hello durumunu raporlar
  * İşlev bildirim gövde doğrulama sonucu olarak oluşturur. Merhaba işlevsel bildirim belge hello işleme alınan karşılaştı her hata raporları

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/x12/). 

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

