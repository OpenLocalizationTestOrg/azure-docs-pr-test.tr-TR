---
title: "Azure Cosmos DB ve İşlevler’i kullanarak yapılandırılmamış verileri depolama | Microsoft Docs"
description: "Azure İşlevleri ve Cosmos DB’yi kullanarak yapılandırılmamış verileri depolama"
services: functions
documentationcenter: functions
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, Cosmos DB, dinamik işlem, sunucusuz mimari"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/19/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: b9bb71adf85490fe68bf6b73133017c5e9c377e1
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/11/2018
---
# <a name="store-unstructured-data-using-azure-functions-and-azure-cosmos-db"></a>Azure İşlevleri ve Azure Cosmos DB’yi kullanarak yapılandırılmamış verileri depolama

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), yapılandırılmamış verileri ve JSON verilerini depolamanın harika bir yoludur. Cosmos DB, Azure İşlevleri ile birlikte kullanıldığında verilerin ilişkisel bir veritabanında depolanmasına göre çok daha az kodla verileri hızlı ve kolay bir şekilde depolar.

> [!NOTE]
> Şu anda Azure Cosmos DB tetikleyicisi, giriş bağlamaları ve çıkış bağlamaları yalnızca SQL API ve Graph API hesaplarıyla çalışır.

Azure İşlevleri’nde giriş ve çıkış bağlamaları, işlevinizden dış hizmet verilerine bağlanmanın bildirim temelli bir yöntemini sağlar. Bu konuda, yapılandırılmamış verileri bir Cosmos DB belgesinde depolayan bir çıktı bağlaması eklemek için var olan bir C# işlevini güncelleştirme hakkında bilgi edinin. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiyi tamamlamak için:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Çıktı bağlaması ekleme

1. İşlev uygulamanızı ve işlevinizi genişletin.

1. **Tümleştir** öğesini ve sayfanın sağ üst kısmındaki **+ Yeni Çıktı**’yı seçin. **Azure Cosmos DB**’yi seçip **Seç**’e tıklayın.

    ![Cosmos DB çıktı bağlaması ekleme](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Tabloda belirtilen **Azure Cosmos DB çıktısı** ayarlarını kullanın: 

    ![Cosmos DB çıktı bağlamasını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Ayar      | Önerilen değer  | Açıklama                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Belge parametre adı** | taskDocument | Kodda Cosmos DB nesnesine başvuran ad. |
    | **Veritabanı adı** | taskDatabase | Belgelerin kaydedileceği veritabanının adı. |
    | **Koleksiyon adı** | TaskCollection | Veritabanı koleksiyonunun adı. |
    | **True ise, Cosmos DB veritabanı ve koleksiyonunu oluşturur** | İşaretli | Koleksiyon henüz mevcut değil, bu yüzden oluşturun. |

4. **Azure Cosmos DB belge bağlantısı** etiketinin yanındaki **Yeni**’yi ve **+ Yeni oluştur** öğesini seçin. 

5. Tabloda belirtilen **Yeni hesap** ayarlarını kullanın: 

    ![Cosmos DB bağlantısını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Ayar      | Önerilen değer  | Açıklama                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **ID** | Veritabanının adı | Azure Cosmos DB veritabanı için benzersiz kimlik  |
    | **API** | SQL | SQL API’yi seçin. Şu anda Azure Cosmos DB tetikleyicisi, giriş bağlamaları ve çıkış bağlamaları yalnızca SQL API ve Graph API hesaplarıyla çalışır. |
    | **Abonelik** | Azure Aboneliği | Azure Aboneliği  |
    | **Kaynak Grubu** | myResourceGroup |  İşlevi uygulamanızı içeren mevcut kaynak grubunu kullanın. |
    | **Konum**  | WestEurope | İşlev uygulamanıza veya depolanmış belgeleri kullanan diğer uygulamalara yakın olan bir konum seçin.  |

6. Veritabanını oluşturmak için **Tamam**’a tıklayın. Veritabanının oluşturulması birkaç dakika sürebilir. Veritabanı oluşturulduktan sonra, veritabanı bağlantı dizesi bir işlev uygulaması ayarı olarak depolanır. Bu uygulama ayarının adı **Azure Cosmos DB hesap bağlantısına** eklenir. 
 
8. Bağlantı dizesi ayarlandıktan sonra, bağlamayı oluşturmak için **Kaydet**’i seçin.

## <a name="update-the-function-code"></a>İşlev kodunu güncelleştirme

Mevcut C# işlev kodunu aşağıdaki kodla değiştirin:

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
Bu kod örneği, HTTP İsteği sorgu dizelerini okur ve `taskDocument` nesnesindeki alanlara atar. `taskDocument` bağlaması bu bağlama parametresindeki nesne verilerini, bağlanan belge veritabanında depolanmak üzere gönderir. Veritabanı, işlev ilk kez çalıştırıldığında oluşturulur.

## <a name="test-the-function-and-database"></a>İşlevi ve veritabanını test etme

1. Sağ pencereyi genişletip **Test**’i seçin. **Sorgu** altında **+ Parametre ekle**’ye tıklayıp aşağıdaki parametreleri sorgu dizesine ekleyin:

    + `name`
    + `task`
    + `duedate`

2. **Çalıştır**’a tıklayın ve 200 durumunun döndürüldüğünü doğrulayın.

    ![Cosmos DB çıktı bağlamasını yapılandırma](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. Azure portalının sol tarafındaki simge çubuğunu genişletin, arama alanına `cosmos` yazın ve **Azure Cosmos DB**’yi seçin.

    ![Cosmos DB hizmetini arama](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Azure Cosmos DB hesabınızı seçin ve ardından **Veri Gezgini**’ni seçin. 

3. **Koleksiyonlar** düğümünü genişletin, yeni belgeyi seçin ve belgenin sorgu dizesi değerlerinizin yanı sıra bazı ek meta verileri içerdiğini onaylayın. 

    ![Cosmos DB girişini doğrulama](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Yapılandırılmamış verileri bir Azure Cosmos DB’de depolayan HTTP tetikleyicinize başarıyla bir bağlama eklediniz.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Cosmos DB veritabanına bağlama hakkında daha fazla bilgi için bkz. [Azure İşlevleri Cosmos DB bağlamaları](functions-bindings-cosmosdb.md).
