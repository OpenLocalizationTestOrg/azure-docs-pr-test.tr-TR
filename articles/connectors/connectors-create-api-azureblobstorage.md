---
title: "aaaAdd hello Azure blob depolama Logic Apps bağlayıcı | Microsoft Docs"
description: "Başlama ve bir mantıksal uygulama hello Azure blob depolama bağlayıcısını yapılandırma"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Bir mantıksal uygulama Hello Azure blob depolama Bağlayıcısı kullanma
Kullanım hello Azure Blob Depolama bağlayıcı tooupload, güncelleştirme, almak ve depolama hesabınızda, tüm mantıksal uygulama içinde BLOB'ları silme.  

Azure blob storage ile:

* İş akışınızı yeni projeler karşıya yükleme veya en son güncelleştirilen dosyaları alma oluşturun.
* Eylemler tooget dosya meta verileri kullanmak, bir dosya, dosyaları kopyala ve daha fazlasını silin. Örneğin, bir aracı bir Azure web sitesinde (bir tetikleyici) güncelleştirildiğinde, ardından bir blob depolama (bir eylem) dosyasında güncelleştirin. 

Bu konu nasıl toouse hello blob depolama bağlayıcı bir mantıksal uygulama içinde gösterir.

Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>TooAzure blob depolama birimini bağlayın
Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet. Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, tooconnect tooa depolama hesabı, önce bir blob depolama oluşturmanız *bağlantı*. toocreate bir bağlantı, bağlandığınız tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin. Bu nedenle Azure storage ile Merhaba kimlik bilgilerini tooyour depolama hesabı toocreate hello bağlantısı girin. 

#### <a name="create-hello-connection"></a>Merhaba bağlantısı oluşturma
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Bir tetikleyici kullanın
Bu bağlayıcı hiçbir tetikleyici yok. Diğer Tetikleyicileri toostart hello mantıksal uygulama, bir yineleme tetikleyici, bir HTTP Web kancası tetikleyici, tetikleyici diğer bağlayıcıları ve daha fazla ile kullanılabilir gibi kullanın. [Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) bir örnek sağlar.

## <a name="use-an-action"></a>Bir eylem kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.

1. Merhaba artı işaretini seçin. Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Seçin **Eylem Ekle**.
3. "Tooget tüm hello kullanılabilir eylemlerin bir listesini blob" Merhaba metin kutusuna yazın.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. Bizim örneğimizde seçin **AzureBlob - Get dosya meta veri yolu kullanarak**. Bir bağlantı zaten varsa, hello seçin **...** (Göster Seçici) düğmesini tooselect bir dosya.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin. [Merhaba bağlantı oluşturmak](connectors-create-api-azureblobstorage.md#create-the-connection) bu konuda bu özellikleri açıklar. 
   
   > [!NOTE]
   > Bu örnekte, bir dosyanın hello meta verileri alın. toosee meta verileri Merhaba, başka bir bağlayıcı kullanarak yeni bir dosya oluşturur başka bir eylem ekleyin. Örneğin, hello meta verileri temel alarak yeni bir "test" dosyası oluşturur OneDrive eylemi ekleyin. 


5. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.

> [!TIP]
> [Depolama Gezgini](http://storageexplorer.com/) harika bir aracı birden çok depolama hesabı çok yönettiği yerdir.

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

