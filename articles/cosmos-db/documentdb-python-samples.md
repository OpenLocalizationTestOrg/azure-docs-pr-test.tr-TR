---
title: "aaaDocumentDB API Python örnekler için Azure Cosmos DB | Microsoft Docs"
description: "Python örnekler github'da Azure Cosmos veritabanı CRUD işlemleri dahil olmak üzere, ortak görevler için bulun."
keywords: "Python örnekleri"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Azure Cosmos DB Python örnekleri
> [!div class="op_single_selector"]
> * [.NET örnekleri](documentdb-dotnet-samples.md)
> * [Node.js Örnekleri](documentdb-nodejs-samples.md)
> * [Python örnekleri](documentdb-python-samples.md)
> * [Azure Kod örnek Galerisi](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

CRUD işlemleri ve Azure Cosmos DB kaynaklardaki ortak diğer işlemleri gerçekleştirmek örnek çözümleri hello dahil [azure documentdb python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub depo. Bu makalede aşağıdakiler sunulmaktadır:

* Her hello Python örnek proje dosyalarının bağlantılar toohello görevler. 
* Bağlantılar toohello API başvuru içeriği ilgili.

**Önkoşullar**

1. Bir Azure hesabı toouse bu Python örnekler gerekir:
   * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/): krediler alırsınız tootry çıkışı Ücretli Azure hizmetlerini kullanabilirsiniz ve hatta kullanıldıktan sonra en fazla hello hesabı tutabilir ve ücretsiz Web siteleri gibi Azure hizmetlerini kullanabilirsiniz. Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınız asla ücretlendirilir.
     * Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
2. Merhaba etmeniz [Python SDK](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Her örnek kendi içinde bulunan, kendisini ayarlayan ve kendisini sonra temizler. Bu nedenle, hello örnekleri birden fazla çağrı çok sorun[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Bu, aboneliğinizin yapılır her zaman 1 saat hello performans katmanı oluşturulmakta hello koleksiyonunun başına kullanım için faturalandırılır. 
   > 
   > 

## <a name="database-examples"></a>Veritabanı örnekleri
Merhaba [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) hello dosyasının [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) proje, nasıl tooperform hello aşağıdaki görevleri gösterir.

| Görev | API başvurusu |
| --- | --- |
| [Bir veritabanı oluşturun](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client. CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Sorgu bir veritabanı için bir hesap](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client. QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Bir veritabanı kimliğiyle okuma](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client. ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Bir hesap için veritabanlarını Listele](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client. ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Veritabanı silme](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client. DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Koleksiyon örnekleri
Merhaba [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) hello dosyasının [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) proje, nasıl tooperform hello aşağıdaki görevleri gösterir.

| Görev | API başvurusu |
| --- | --- |
| [Koleksiyon oluşturma](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Veritabanındaki tüm koleksiyonlar listesini okur](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client. ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Bir koleksiyon kimliğine göre alma](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client. ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Bir koleksiyonun performans katmanı Al](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Bir koleksiyonun performans katmanı değiştirme](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client. ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Bir koleksiyonu silin](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client. DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

