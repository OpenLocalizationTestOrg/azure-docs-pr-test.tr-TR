---
title: "Mantıksal uygulamalarınızı aaaAdd hello OneDrive Bağlayıcısı | Microsoft Docs"
description: "REST API parametrelerle hello OneDrive bağlayıcı genel bakış"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Merhaba OneDrive Bağlayıcısı ile çalışmaya başlama
TooOneDrive toomanage karşıya yükleme, get, dosyaları silin ve daha fazlası da dahil olmak üzere dosyalarınızı bağlayın. 

OneDrive ile: 

* Onedrive'daki dosyaları depolayarak, iş akışı oluşturma veya varolan dosyaları OneDrive güncelleştirin. 
* Bir dosya oluşturulduğunda veya OneDrive'ınıza içinde güncelleştirildiğinde kullanım toostart, iş akışını tetikler.
* Eylemler toocreate bir dosyası kullanmak, bir dosya ve daha fazlasını silin. Örneğin, yeni Office 365 e-posta eki (tetikleyici) alındığında, OneDrive (bir eylem) yeni bir dosya oluşturun.

Bu konuda nasıl toouse hello bir mantıksal uygulama OneDrive Bağlayıcısı gösterir ve ayrıca listeleri tetikleyiciler ve Eylemler hello.

Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>TooOneDrive Bağlan
Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet. Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, tooconnect tooOneDrive önce bir OneDrive gerekir *bağlantı*. toocreate bir bağlantı için tooconnect istediğiniz tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin. Bu nedenle, OneDrive ile Merhaba kimlik bilgilerini tooyour OneDrive hesabı toocreate hello bağlantısı girin.

### <a name="create-hello-connection"></a>Merhaba bağlantısı oluşturma
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Bir tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. Tetikleyiciler "Merhaba hizmet bir aralığı ve istediğiniz sıklığı yoklama". [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Merhaba mantıksal uygulama içinde "onedrive" tooget hello Tetikleyicileri listesini yazın:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Seçin **bir dosya değiştirildiği**. Bir bağlantı zaten varsa, hello Seçici Göster düğmesini tooselect bir klasör seçin.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    İçinde istendiğinde toosign varsa, hello oturum ayrıntıları toocreate hello bağlantısında girin. [Merhaba bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konudaki hello adımlar listelenmektedir. 
   
   > [!NOTE]
   > Bu örnekte, hello mantıksal uygulama güncelleştirilir seçtiğiniz hello klasöründe bir dosya açıldığında çalıştırır. Bu tetikleyici toosee hello sonuçlarını bir e-posta gönderir başka bir eylem ekleyin. Örneğin, Office 365 Outlook hello ekleyin *bir e-posta Gönder* bir dosya güncelleştirildiğinde, e-postalar eylem. 

3. Select hello **Düzenle** düğmesine tıklayın ve ayarlama hello **sıklığı** ve **aralığı** değerleri. Örneğin, 15 dakikada bir hello tetikleyici toopoll istiyorsanız, ardından hello ayarlayın **sıklığı** çok**Minute**ve kümesi hello **aralığı** çok**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.

## <a name="use-an-action"></a>Bir eylem kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Merhaba artı işaretini seçin. Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Seçin **Eylem Ekle**.
3. Merhaba metin kutusuna "onedrive" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. Bizim örneğimizde seçin **OneDrive - dosyası oluşturma**. Bir bağlantı zaten varsa, hello seçin **klasör yolu** tooput hello dosya, hello girin **dosya adı**ve hello seçin **dosya içeriği** istediğiniz:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin. [Merhaba bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konuda bu özellikleri açıklar. 
   
   > [!NOTE]
   > Bu örnekte, OneDrive klasöründe yeni bir dosya oluşturun. Başka bir tetikleyici toocreate hello OneDrive dosyasından çıkış kullanabilirsiniz. Örneğin, Office 365 Outlook hello ekleyin *yeni bir e-posta geldiğinde* tetikleyici. Merhaba OneDrive ekleme *dosyası oluştur* ForEach toocreate hello yeni bir dosyada OneDrive içinde hello ekler ve Content-Type alanları kullanan eylem. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.


## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).
