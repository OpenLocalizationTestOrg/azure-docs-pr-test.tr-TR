---
title: "aaaAzure Azure Cosmos DB CLI örnekleri | Microsoft Docs"
description: "Azure CLI örnekler - Azure Cosmos DB hesapları, veritabanları, kapsayıcıları, bölgeler ve güvenlik duvarları oluşturun ve yönetin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Azure Cosmos DB için Azure CLI örnekleri

Merhaba aşağıdaki tabloda bağlantıları toosample Azure CLI betikler için Azure Cosmos DB içerir. Tüm Azure Cosmos DB CLI komutları için başvuru sayfaları hello kullanılabilir [Azure CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Azure Cosmos DB hesap, veritabanı ve kapsayıcıları oluşturma**||
|[Bir DocumentDB API, grafik veya tablo API hesabı oluşturun](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Bir tek Azure Cosmos DB API hesabını, veritabanını ve kullanmak için kapsayıcı hello DocumentDB, grafik veya tablo API'ler oluşturur. |
| [MongoDB API hesabı oluşturma](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Bir tek Azure Cosmos DB MongoDB API hesap, veritabanı ve koleksiyonu oluşturur. |
|**Azure Cosmos DB ölçeklendirme**||
| [Ölçek kapsayıcı işleme](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Değişiklikleri hello bir kapsayıcısı üzerinde througput sağlandı.|
|[Birden çok bölgelerdeki Azure Cosmos DB veritabanı hesabı çoğaltabilir ve yük devretme öncelikleri yapılandırın](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Belirtilen yük devretme önceliğe sahip birden çok bölgeleri genel hesap verilerini çoğaltır.|
|**Azure Cosmos DB güvenli**||
| [Hesap anahtarı alma](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Merhaba birincil ve ikincil ana yazma anahtarları ve birincil ve ikincil salt okunur anahtarları hello hesabı alır.|
| [MongoDB bağlantı dizesi Al](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Merhaba bağlantı dizesi tooconnect MongoDB uygulama tooyour Azure Cosmos DB hesabı alır.|
|[Hesabı anahtarlarını yeniden oluştur](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Hello Yöneticisi veya hello hesabı için salt okunur anahtarı yeniden oluşturur.|
|[Bir güvenlik duvarı oluşturma](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Onaylanan bir makine ve/veya Bulut Hizmetleri kümesinden bir gelen IP erişim denetimi İlkesi toolimit erişim toohello hesabı oluşturur.|
|**Yüksek kullanılabilirlik, olağanüstü durum kurtarma, yedekleme ve geri yükleme**||
|[Yük devretme ilkesi yapılandırma](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Ayarlar hello hesap çoğaltılır her bölgede yük devretme öncelik hello.|
|**Azure Cosmos DB kaynaklarına bağlanma**||
|[Bir web uygulaması tooAzure Cosmos DB Bağlan](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Oluşturabilir ve bir Azure Cosmos DB veritabanı ve Azure web uygulaması bağlayabilirsiniz.|
|||
