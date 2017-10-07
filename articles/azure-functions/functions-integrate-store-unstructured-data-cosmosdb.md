---
title: "aaaStore yapılandırılmamış verileri Azure işlevleri ve Cosmos DB kullanma"
description: "Azure İşlevleri ve Cosmos DB’yi kullanarak yapılandırılmamış verileri depolama"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, Cosmos DB, dinamik işlem, sunucusuz mimari"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Azure İşlevleri ve Cosmos DB’yi kullanarak yapılandırılmamış verileri depolama

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) mükemmel şekilde toostore yapılandırılmamış ve JSON verileri. Cosmos DB, Azure İşlevleri ile birlikte kullanıldığında verilerin ilişkisel bir veritabanında depolanmasına göre çok daha az kodla verileri hızlı ve kolay bir şekilde depolar.

Azure işlevleri, giriş ve çıkış bağlama işlevinizde bir bildirim temelli yolu tooconnect tooexternal hizmet verileri belirtin. Bu konuda, nasıl tooupdate bir var olan C# işlev tooadd Cosmos DB belgede yapılandırılmamış veri depolayan bir çıktı bağlama hakkında bilgi edinin. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Çıktı bağlaması ekleme

1. İşlev uygulamanızı ve işlevinizi genişletin.

1. Seçin **tümleştir** ve **+ yeni çıkış**, hello olduğu başlangıç sayfasının sağ üst. **Azure Cosmos DB**’yi seçip **Seç**’e tıklayın.

    ![Cosmos DB çıktı bağlaması ekleme](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Kullanım hello **Azure Cosmos DB çıktı** hello tabloda belirtildiği gibi ayarları: 

    ![Cosmos DB çıktı bağlamasını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Ayar      | Önerilen değer  | Açıklama                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Belge parametre adı** | taskDocument | Kodda toohello Cosmos DB Nesne başvurur adı. |
    | **Veritabanı adı** | taskDatabase | Veritabanı toosave belgeleri adı. |
    | **Koleksiyon adı** | TaskCollection | Cosmos DB veritabanları koleksiyonunun adı. |
    | **TRUE ise, hello Cosmos DB veritabanı ve koleksiyonu oluşturur** | İşaretli | Merhaba koleksiyonu zaten mevcut değil; Bu yüzden oluşturun. |

4. Seçin **yeni** sonraki toohello **Cosmos DB belge bağlantısı** etiket ve seçin **+ Yeni Oluştur**. 

5. Kullanım hello **yeni hesabı** hello tabloda belirtildiği gibi ayarları: 

    ![Cosmos DB bağlantısını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Ayar      | Önerilen değer  | Açıklama                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **ID** | Veritabanının adı | Merhaba Cosmos DB veritabanı için benzersiz kimliği  |
    | **API** | SQL (DocumentDB) | Merhaba belge veritabanı API seçin.  |
    | **Abonelik** | Azure Aboneliği | Azure Aboneliği  |
    | **Kaynak Grubu** | myResourceGroup |  İşlev uygulamanızı içeren hello var olan kaynak grubunu kullanın. |
    | **Konum**  | WestEurope | Merhaba depolanan belgeler tooother uygulamaları veya işlev uygulaması tooeither yakın bir konum seçin.  |

6. Tıklatın **Tamam** toocreate hello veritabanı. Birkaç dakika toocreate hello veritabanı sürebilir. Merhaba veritabanı oluşturulduktan sonra hello veritabanı bağlantı dizesi işlevi uygulama ayarı olarak depolanır. Bu uygulama ayarı Hello adını eklenir **Cosmos DB hesap bağlantı**. 
 
8. Merhaba bağlantı dizesi ayarladıktan sonra Seç **kaydetmek** toocreate hello bağlama.

## <a name="update-hello-function-code"></a>Merhaba işlev kodunu güncelleştirmesi

Merhaba varolan C# işlevi kod koddan hello ile değiştirin:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
Bu kod örneği sorgu dizeleri hello HTTP isteğini okur ve bunlara hello toofields atar `taskDocument` nesnesi. Merhaba `taskDocument` bağlama hello ilişkili belge veritabanında depolanan bu bağlama parametresi toobe gelen hello nesne verileri gönderir. Merhaba veritabanı hello hello işlevi ilk çalıştığında oluşturulur.

## <a name="test-hello-function-and-database"></a>Test hello işlevi ve veritabanı

1. Merhaba sağ penceresi genişletin ve seçin **Test**. Altında **sorgu**, tıklatın **+ parametresini ekleyin** ve parametreleri toohello sorgu dizesi aşağıdaki hello ekleyin:

    + `name`
    + `task`
    + `duedate`

2. **Çalıştır**’a tıklayın ve 200 durumunun döndürüldüğünü doğrulayın.

    ![Cosmos DB çıktı bağlamasını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. Sol hello Azure portal tarafı hello üzerinde hello simge çubuğu genişletin türü `cosmos` alan ve select hello arama **Azure Cosmos DB**.

    ![Merhaba Cosmos DB hizmet arama](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Oluşturduğunuz, select hello veritabanını seçip **Veri Gezgini**. Merhaba genişletin **koleksiyonları** düğümleri hello yeni belge seçin ve hello belge içeren bazı ek meta veri yanı sıra, sorgu dizesi değerlerini onaylayın. 

    ![Cosmos DB girişini doğrulama](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Cosmos DB veritabanında yapılandırılmamış veri depolayan bir bağlama tooyour HTTP tetikleyici başarıyla eklediniz.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Bağlama tooa Cosmos DB veritabanı hakkında daha fazla bilgi için bkz: [Azure işlevleri Cosmos DB bağlamaları](functions-bindings-documentdb.md).
