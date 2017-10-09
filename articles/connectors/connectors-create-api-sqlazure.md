---
title: "aaaAdd hello Azure SQL Database mantıksal uygulamalarınızı Connector'daki | Microsoft Docs"
description: "Azure SQL veritabanı bağlayıcı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Hello Azure SQL Veritabanı Bağlayıcısı ile çalışmaya başlama
Hello Azure SQL Veritabanı Bağlayıcısı'nı kullanarak, tablolardaki verileri yönetmek, kuruluşunuz için iş akışları oluşturun. 

SQL Database:

* Yeni bir müşteri tooa müşteriler veritabanı ekleyerek veya bir sırada siparişler veritabanını güncelleştirmek, iş akışı oluşturma.
* Eylemler tooget bir veri satırı kullanın, yeni bir satır ekleyin ve hatta silin. Örneğin, bir kayıt Dynamics CRM Online içinde (tetikleyici) oluşturulduğunda, bir satır bir Azure SQL veritabanı'nda (bir eylem) ekleyin. 

Bu konuda nasıl toouse hello bir mantıksal uygulama içinde SQL Veritabanı Bağlayıcısı gösterir ve ayrıca listeleri Eylemler hello.

Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>TooAzure SQL veritabanına bağlanma
Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet. Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, tooconnect tooSQL veritabanı, önce bir SQL veritabanı oluşturmanız *bağlantı*. toocreate bir bağlantı, bağlandığınız tooaccess hello hizmet normalde kullandığınız hello kimlik girin. Bu nedenle, SQL veritabanı'nda SQL veritabanı kimlik bilgileri toocreate hello bağlantınızı girin. 

#### <a name="create-hello-connection"></a>Merhaba bağlantısı oluşturma
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Bir tetikleyici kullanın
Bu bağlayıcı hiçbir tetikleyici yok. Diğer Tetikleyicileri toostart hello mantıksal uygulama, bir yineleme tetikleyici, bir HTTP Web kancası tetikleyici, tetikleyici diğer bağlayıcıları ve daha fazla ile kullanılabilir gibi kullanın. [Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) bir örnek sağlar.

## <a name="use-an-action"></a>Bir eylem kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Merhaba artı işaretini seçin. Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Seçin **Eylem Ekle**.
3. Merhaba metin kutusuna "sql" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Bizim örneğimizde seçin **SQL Server - Get satır**. Bir bağlantı zaten varsa, hello seçin **tablo adı** hello açılan dan listesinde ve hello girin **satır kimliği** tooreturn istediğiniz.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin. [Merhaba bağlantı oluşturmak](connectors-create-api-sqlazure.md#create-the-connection) bu konuda bu özellikleri açıklar. 
   
   > [!NOTE]
   > Bu örnekte, biz bir tablodan bir satırı döndürür. Bu satırda toosee hello veri Merhaba tablonun hello alanlarını kullanarak bir dosya oluşturur başka bir eylem ekleyin. Örneğin, hello FirstName ve LastName alanları toocreate hello bulut depolama hesabı yeni bir dosyada kullanan bir OneDrive eylem ekleyin. 
   > 
   > 
5. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sql/). 

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

