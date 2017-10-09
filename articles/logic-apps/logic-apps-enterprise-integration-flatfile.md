---
title: "aaaEncode veya Azure mantıksal uygulamaları düz dosyalarda kod çözme | Microsoft Docs"
description: "Toouse nasıl hello dosya dosya Kodlayıcısı veya kod çözücü hello Enterprise Integration Pack logic apps içinde"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Düz dosyalar ile Kurumsal tümleştirme genel bakış

İşletmeden işletmeye (B2B) senaryosunda tooa iş ortağı göndermeden önce tooencode XML içerik isteyebilirsiniz. Bir mantıksal uygulama bağlayıcısı toodo bu kodlama hello düz dosya kullanabilirsiniz. Merhaba, oluşturduğunuz mantıksal uygulama kendi XML bir çeşitli kaynaklardan bir HTTP isteği tetikleyicisi, başka bir uygulama veya hello birinden bile birçok dahil olmak üzere, içerik alabilir [Bağlayıcılar](../connectors/apis-list.md). Merhaba logic apps hakkında daha fazla bilgi için bkz: [logic apps belge](logic-apps-what-are-logic-apps.md "Logic apps hakkında daha fazla bilgi").  

## <a name="create-hello-flat-file-encoding-connector"></a>Merhaba düz dosya kodlama bağlayıcısı oluşturun
Bu adımları tooadd bağlayıcı tooyour mantıksal uygulama kodlama düz bir dosya izleyin.

1. Mantıksal uygulama oluşturma ve [tooyour tümleştirme hesap bağlantı](logic-apps-enterprise-integration-accounts.md "toolink bir tümleştirme hesap tooa mantıksal uygulama öğrenin"). Bu hesap tooencode hello XML verileri kullanacağı hello şeması içerir.  
2. Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.  
   ![Tetikleyici tooselect ekran görüntüsü](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Eylem, aşağıdaki gibi kodlama hello düz dosya ekleyin:
   
    a. Select hello **artı** oturum.
   
    b. Select hello **Eylem Ekle** bağlantı (Merhaba artı işareti seçtikten sonra görünür).
   
    c. Merhaba arama kutusuna *düz* toofilter tüm toouse istediğiniz eylemleri toohello bir hello.
   
    d. Select hello **düz dosya kodlamasını** hello listesindeki seçeneği.   
   ![Ekran görüntüsü düz dosya kodlamasını seçeneği](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Merhaba üzerinde **düz dosya kodlamasını** iletişim kutusu, select hello **içerik** metin kutusu.  
   ![İçerik ekran metin kutusu](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Merhaba gövde etiket hello tooencode istediğiniz içeriği seçin. Merhaba gövde etiketi hello içerik alanını doldurur.     
   ![Gövde etiketinin ekran görüntüsü](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Select hello **şema adı** liste kutusu ve hello şema toouse tooencode hello istediğiniz içerik giriş'ı seçin.    
   ![Şema adı ekran liste kutusu](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Çalışmanızı kaydedin.   
   ![Ekran Kaydet simgesi](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

Bu noktada, düz dosya kodlama Connector kurulumu tamamlandı. Gerçek dünya uygulamada Salesforce gibi bir iş kolu satır uygulama toostore hello kodlanmış verileri isteyebilirsiniz. Veya iş ortağı ticaret bu kodlanmış verileri tooa gönderebilirsiniz. Sağlanan diğer bağlayıcıları hello herhangi birini kullanarak eylem tooSalesforce veya tooyour ticaret iş ortağı, kodlama hello bir eylem toosend hello çıktısını kolayca ekleyebilirsiniz.

Artık, bir istek toohello HTTP uç noktası yapıp hello hello istek gövdesinde hello XML içeriği de dahil olmak üzere Bağlayıcınızı test edebilirsiniz.  

## <a name="create-hello-flat-file-decoding-connector"></a>Bağlayıcı kod çözme hello düz dosya oluşturma

> [!NOTE]
> Aşağıdaki adımları toocomplete toohave bir şema dosyası, tümleştirme dikkate karşıya yüklenmesi gerekir.

1. Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.  
   ![Tetikleyici tooselect ekran görüntüsü](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Eylem, aşağıdaki gibi kod çözme hello düz dosya ekleyin:
   
    a. Select hello **artı** oturum.
   
    b. Select hello **Eylem Ekle** bağlantı (Merhaba artı işareti seçtikten sonra görünür).
   
    c. Merhaba arama kutusuna *düz* toofilter tüm toouse istediğiniz eylemleri toohello bir hello.
   
    d. Select hello **düz dosya kod çözme** hello listesindeki seçeneği.   
   ![Ekran görüntüsü, düz dosya kod çözme seçeneği](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Select hello **içerik** denetim. Bu hello içerik toodecode kullanabileceğiniz önceki adımlarda Merhaba içeriğine listesini oluşturur. Bu hello fark *gövde* hello gelen HTTP istek içerik toodecode hello olarak kullanılan kullanılabilir toobe olduğu. Merhaba içerik toodecode doğrudan hello girebilirsiniz **içerik** denetim.     
4. Select hello *gövde* etiketi. Bildirim hello gövde etiketi olan şimdi hello **içerik** denetim.
5. Merhaba toouse toodecode hello içerik istediğiniz hello şema adını seçin. Merhaba aşağıdaki ekran görüntüsü gösterilmektedir *OrderFile* hello Seçili şema adıdır. Bu şema adı hello tümleştirme dikkate daha önce yüklenen.
   
   ![İletişim kutusunun ekran görüntüsü, düz dosya kod çözme](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Çalışmanızı kaydedin.  
   ![Ekran Kaydet simgesi](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

Bu noktada, düz dosya bağlayıcı kod çözme ayarlama tamamlandı. Gerçek dünya uygulamada Salesforce gibi iş uygulamasında toostore kodunu çözdü hello veri isteyebilirsiniz. Eylem tooSalesforce kod çözme hello bir eylem toosend hello çıktısını kolayca ekleyebilirsiniz.

Bir istek toohello HTTP uç noktası yaparak Bağlayıcınızı artık sınayabilirsiniz ve hello XML içeriği de dahil olmak üzere toodecode hello hello istek gövdesinde istiyorsunuz.  

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin").  

