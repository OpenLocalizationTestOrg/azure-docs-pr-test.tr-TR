---
title: aaaDecode X12 iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve onayları hello X12 ileti kod çözücü ile Azure Logic Apps için hello Kurumsal tümleştirme paketi oluştur"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>X12 kod çözme hello Kurumsal tümleştirme paketi ile Azure Logic Apps için iletileri

Hello kod çözme X12 ileti bağlayıcısıyla, hello Zarf ticari ortak sözleşmesi karşı doğrulamak, EDI ve iş ortağı özgü özellikler doğrulamak, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve Oluştur işlenen işlemler için bildirimler. toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kod çözme X12 ileti Bağlayıcısı olması gerekir.
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [X12 sözleşmesi](logic-apps-enterprise-integration-x12.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="decode-x12-messages"></a>X12 kod çözme iletileri

1. [Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme X12 ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3.  Merhaba arama kutusuna "x12" filtreniz için girin. Seçin **X12-X12 kod çözme ileti**.
   
    !["X12" için arama](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin. 

    ![Hesap bağlantı ayrıntıları tümleştirme sağlar](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

5.  İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir. bağlantı oluşturma toofinish seçin **oluşturma**.
   
    ![Tümleştirme hesap bağlantı ayrıntıları](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra hello X12 düz dosya ileti toodecode seçin.

    ![oluşturulan tümleştirme hesap bağlantı](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Örneğin:

    ![Kod çözme için dosya iletisi SELECT X12 düz](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>X12 kod çözme ayrıntıları

Merhaba X12 kod çözme connector, şu görevleri gerçekleştirir:

* Ticari ortak sözleşmesi karşı hello Zarf doğrular
* EDI ve iş ortağı özgü özellikleri doğrular
  * EDI yapısal doğrulama ve genişletilmiş şema doğrulaması
  * Merhaba değişim Zarf hello yapısını doğrulama.
  * Merhaba zarfının hello denetim şemasına karşılık şema doğrulamasını.
  * Merhaba işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulamasını.
  * İşlem kümesi veri öğelerinde EDI doğrulamanın 
* Merhaba Değişim, Grup ve işlem kümesi denetim numaraları çoğaltmaları olmadığını doğrular
  * Merhaba değiş tokuş denetim numarası önceden alınmış etkileşimler karşı denetler.
  * Merhaba Grup denetim numarası hello değişim diğer Grup denetimi numaraları karşı denetler.
  * Bu gruptaki diğer işlem kümesi denetim numaraları karşı kontrol numarası Hello işlem ayarlamak denetler.
* İşlem kümeleri içine Hello değişim böler veya hello tüm değişim korur:
  * Bölünmüş değişim işlem kümeleri - olarak askıya alma işlem kümeleri hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır. 
  Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.
  * Bölünmüş değişim işlem kümeleri - olarak askıya alma değişim hatası: bölmelerini değişim hareket halinde ayarlar ve her işlem kümesi ayrıştırır. 
  Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`.
  * Değişim korumak - işlem kümeleri askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim. 
  Merhaba X12 kod çözme eylem çıkarır doğrulama çok başarısız işlem kümeleri`badMessages`ve işlemler kalan hello ayarlar çok çıkaran`goodMessages`.
  * Değişim korumak - değişim askıya alma hatası: Preserve hello değişim ve işlem hello tüm toplu değişim. 
  Bir veya daha fazla işlem hello değişim başarısız doğrulama ayarlarsa, tüm hello hareket ayarlar bu değişim çok hello X12 kod çözme eylem çıkarır`badMessages`. 
* Teknik ve/veya işlevsel bir bildirim (yapılandırılmışsa) oluşturur.
  * Teknik bir bildirim başlığı doğrulama sonucu olarak oluşturur. Merhaba Teknik Bildirim hello bir değişim üstbilgi ve toplamı hello adresi alıcı tarafından işlenmesini hello durumunu raporlar.
  * İşlev bildirim gövde doğrulama sonucu olarak oluşturur. Merhaba işlevsel bildirim belge hello işleme alınan karşılaştı her hata raporları

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/x12/). 

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

