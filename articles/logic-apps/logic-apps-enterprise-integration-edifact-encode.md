---
title: aaaEncode EDIFACT iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve Azure Logic Apps için EDIFACT ileti Kodlayıcısı hello Kurumsal tümleştirme paketi ile birlikte XML oluştur"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>EDIFACT iletileri için Azure Logic Apps Enterprise Integration Pack Merhaba ile kodlayın.

Merhaba kodlamak EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikler doğrulamak, her işlem kümesi için bir XML belgesi oluşturmak ve teknik bir bildirim, işlevsel bildirim ya da her ikisini de isteyin.
toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kodlamak EDIFACT ileti Bağlayıcısı olması gerekir. 
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="encode-edifact-messages"></a>EDIFACT iletileri kodlama

1. [Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodlamak EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3.  Merhaba arama kutusuna "EDIFACT", filtre olarak girin. Şunlardan birini seçin **EDIFACT iletiyle kodlamak anlaşma adı** veya **kodla tooEDIFACT iletisi kimlikleri tarafından**.
   
    ![EDIFACT arama](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.

    ![Tümleştirme hesap bağlantısı oluşturma](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

5.  İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir. bağlantı oluşturma toofinish seçin **oluşturma**.

    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    Bağlantınızı şimdi oluşturulur.

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Anlaşma adı tarafından EDIFACT ileti kodlama

Anlaşma adı tarafından EDIFACT iletileri tooencode seçerseniz, hello açmak **adı, EDIFACT sözleşmesi** listesinde, girin veya EDIFACT sözleşmesi adınızı seçin. Merhaba XML ileti tooencode girin.

![EDIFACT sözleşmesi adını ve XML ileti tooencode girin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>EDIFACT iletisi kimlikleri tarafından kodlama

Tarafından kimlikleri EDIFACT iletileri tooencode seçerseniz, hello gönderen tanımlayıcısı, gönderen Niteleyici, alıcı tanımlayıcısı ve EDIFACT sözleşmenizde yapılandırılan alıcı niteleyici girin. Merhaba XML ileti tooencode seçin.

![Göndereni ve alıcısı için kimlikleri sağlamak için XML ileti tooencode seçin](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>EDIFACT kodlamak ayrıntıları

Hello kodlamak EDIFACT connector, şu görevleri gerçekleştirir: 

* Merhaba gönderen niteleyicisi & tanımlayıcısı ve alıcı niteleyicisi ve tanımlayıcısı eşleştirerek Hello sözleşmesi çözümleyin
* EDI işlem hello değişim kümelerinde XML olarak kodlanmış iletileri dönüştürme hello EDI değişim serileştirir.
* İşlem kümesi üstbilgi ve toplamı kesimleri uygular
* Bir değişim denetim sayısı, Grup denetim numarası ve her giden değişim için bir işlem kümesi denetim sayı oluşturur
* Ayırıcı hello yükü veri olarak değiştirir
* EDI ve iş ortağı özgü özellikleri doğrular
  * Merhaba işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulamasını.
  * EDI, üzerinde işlem kümesi veri öğeleri doğrulamanın.
  * İşlem kümesi veri öğeleri üzerinde Genişletilmiş doğrulamanın
* Her işlem kümesi için bir XML belgesi oluşturur.
* Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) ister.
  * Teknik bir bildirim hello CONTRL ileti bir değişim alınmasını gösterir.
  * İşlevsel bir bildirim hello CONTRL ileti, kabul veya alınan hello Değişim, Grup veya ileti reddine hataları veya desteklenmeyen işlevlerin listesini gösterir.

## <a name="view-swagger-file"></a>Görünüm Swagger dosyası
tooview hello Swagger hello EDIFACT bağlayıcı ayrıntılarını görmek [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

