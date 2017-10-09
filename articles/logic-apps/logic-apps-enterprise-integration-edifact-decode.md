---
title: aaaDecode EDIFACT iletileri - Azure Logic Apps | Microsoft Docs
description: "EDI doğrulamak ve onayları hello EDIFACT ileti kod çözücü ile Azure Logic Apps için hello Kurumsal tümleştirme paketi oluştur"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>EDIFACT iletileri Enterprise Integration Pack Merhaba ile Azure mantıksal uygulamaları için kod çözme

Hello kod çözme EDIFACT ileti bağlayıcısıyla EDI ve iş ortağı özgü özellikleri doğrulayın, işlemleri kümeleri içine etkileşimler bölme veya tüm etkileşimler korumak ve işlenen işlemler için ilgili kaynaklar oluşturur. toouse bu bağlayıcı mantıksal uygulamanızı tetikleyici varolan hello bağlayıcı tooan eklemeniz gerekir.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kod çözme EDIFACT ileti Bağlayıcısı olması gerekir. 
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [EDIFACT sözleşmesi](logic-apps-enterprise-integration-edifact.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="decode-edifact-messages"></a>EDIFACT iletileri kod çözme

1. [Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme EDIFACT ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3. Merhaba arama kutusuna "EDIFACT", filtre olarak girin. Seçin **EDIFACT ileti kod çözme**.
   
    ![EDIFACT arama](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.
   
    ![Tümleştirme hesabı oluşturma](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

4. Bağlantınızı oluşturma toofinish bittiğinde, seçin **oluşturma**. Bağlantı ayrıntıları benzer toothis örnek gibi görünmelidir:

    ![Tümleştirme hesap ayrıntıları](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra hello EDIFACT düz dosya ileti toodecode seçin.

    ![oluşturulan tümleştirme hesap bağlantı](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Örneğin:

    ![Kod çözme için EDIFACT düz dosya iletiyi seçin](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>EDIFACT kod çözücü ayrıntıları

Merhaba kod çözme EDIFACT connector, şu görevleri gerçekleştirir: 

* Ticari ortak sözleşmesi karşı hello Zarf doğrular.
* Merhaba sözleşmesi hello gönderen Niteleyici Tanımlayıcısı ve alıcı niteleyicisi & tanımlayıcı eşleştirerek çözümler.
* Merhaba değişim ayarlarını yapılandırmayı alacağını birden fazla işlem hello anlaşmasına göre ait olduğunda bir değişim birden çok işlem halinde ayırır.
* Merhaba değişim ayrıştırır.
* EDI ve iş ortağı özgü özellikler de dahil olmak üzere doğrular:
  * Doğrulama hello değişim Zarf yapısı
  * Merhaba zarfının hello denetim şemasına karşılık şema doğrulaması
  * Hello işlem kümesi veri öğeleri hello ileti şemasına karşılık şema doğrulaması
  * İşlem kümesi veri öğelerinde EDI doğrulamanın
* Merhaba Değişim, Grup ve işlem kümesi denetim numaraları (yapılandırılmışsa) tekrarı olmayan olduğunu doğrular 
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
* Teknik (Denetim) ve/veya işlev bildirim (yapılandırılmışsa) oluşturur.
  * Bir teknik bildirim veya hello CONTRL ACK hello tam alınan değişim söz dizimi kontrol hello sonuçlarını raporlar.
  * İşlev bildirimi kabul ettikten kabul edin veya alınan Değişim veya bir grup Reddet

## <a name="view-swagger-file"></a>Görünüm Swagger dosyası
tooview hello Swagger hello EDIFACT bağlayıcı ayrıntılarını görmek [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

