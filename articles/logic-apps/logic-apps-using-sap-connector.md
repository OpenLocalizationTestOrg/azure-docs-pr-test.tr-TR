---
title: "aaaConnect tooan şirket içi Azure Logic Apps SAP sisteminde | Microsoft Docs"
description: "Mantıksal uygulama akışınızı hello şirket içi veri ağ geçidi üzerinden tooan şirket içi SAP sistemine bağlanması"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Logic apps hello SAP Bağlayıcısı ile tooan şirket içi SAP sistemine bağlanması 

Merhaba şirket içi veri ağ geçidi toomanage veri sağlar ve şirket içi kaynaklara güvenle erişin. Bu konu, logic apps tooan şirket içi SAP sistemine nasıl bağlanacağını gösterir. Bu örnekte, mantıksal uygulamanızı IDOC HTTP istekleri ve hello yanıtı geri gönderir.    

> [!NOTE]
> Geçerli sınırlamalar: 
> - Merhaba yanıt için gereken tüm adımları hello içinde son yok, mantıksal uygulamanızı zaman aşımına [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md). Bu senaryoda, istekleri engellenen. 
> - Merhaba dosya seçiciyi tüm hello kullanılabilir alanlar görüntülenmez. Bu senaryoda, yollarını el ile ekleyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- Merhaba son yükleyip [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127) sürüm 1.15.6150.1 ya da daha yeni. [Nasıl tooconnect toohello bir mantıksal uygulama veri ağ geçidi şirket içi](http://aka.ms/logicapps-gateway) hello adımları listeler. devam etmeden önce bir şirket içi makinede hello ağ geçidi yüklenmelidir.

- İndirme ve yükleme hello son SAP istemci kitaplığı hello üzerinde aynı hello veri ağ geçidinin yüklü olduğu makine. SAP sürümleri aşağıdaki hello birini kullanın: 
    - SAP sunucusuna
        - Herhangi bir SAP sunucusuna bu destek hello .NET Connector (NCo) 3.0
 
    - SAP istemci
        - SAP .NET bağlayıcı (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Tetikleyiciler ve Eylemler tooyour SAP sistemine bağlanmak için ekleme

Merhaba SAP bağlayıcısı Eylemler ancak değil Tetikleyicileri vardır. Bu nedenle, hello hello iş akışının başlangıcında başka bir tetikleyici toouse sunuyoruz. 

1. Merhaba istek/yanıt tetikleyicisi ekleyin ve ardından **yeni adım**.

2. Seçin **Eylem Ekle**seçip hello SAP bağlayıcısı yazarak `SAP` hello arama alanında:    

     ![SAP uygulama sunucusu ya da SAP ileti sunucusu seçin](media/logic-apps-using-sap-connector/sap-action.png)

3. Seçin [ **SAP uygulama sunucusu** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) veya [ **SAP ileti sunucusu**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), SAP kurulumunuzu göre. Varolan bir bağlantıyı yoksa, istendiğinde toocreate biri demektir.

   1. Seçin **Connect şirket içi veri ağ geçidi üzerinden**ve SAP sisteminizi hello ayrıntılarını girin:   

       ![Bağlantı dizesi tooSAP Ekle](media/logic-apps-using-sap-connector/picture2.png)  

   2. Altında **ağ geçidi**, bir var olan ağ geçidi ya da tooinstall yeni bir ağ geçidi seçin, **ağ geçidi yükleme**.

        ![Yeni bir ağ geçidi yükleyin](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Tüm hello ayrıntıları girdikten sonra Seç **oluşturma**. 
   Logic Apps yapılandırır ve hello bağlantı düzgün çalıştığından emin olmayı hello bağlantısını test eder.

4. SAP bağlantınız için bir ad girin.

5. Merhaba farklı SAP seçenekleri şimdi kullanılabilir. toofind, IDOC kategorisi, hello listeden seçin. Merhaba yolu ve select hello HTTP yanıt hello olarak el ile yazın veya **gövde** alan:

     ![SAP eylemi](media/logic-apps-using-sap-connector/picture3.png)

6. Merhaba eylem oluşturmak için Ekle bir **HTTP yanıtı**. Merhaba yanıt iletisi hello SAP çıktısını olmalıdır.

7. Mantıksal uygulamanızı kaydedin. IDOC hello HTTP tetikleme URL'si aracılığıyla göndererek test. IDOC gönderilen hello sonra hello mantıksal uygulama hello yanıttan bekleyin:   

     > [!TIP]
     > Nasıl çok denetleyin[mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Merhaba SAP bağlayıcısı tooyour mantıksal uygulama eklenir, diğer işlevleri keşfetmeye başlayın:

- BAPI
- RFC

## <a name="get-help"></a>Yardım alın

tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

- Bilgi nasıl toovalidate, dönüştürme ve diğer BizTalk benzeri işlevleri hello [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Tooon içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan
