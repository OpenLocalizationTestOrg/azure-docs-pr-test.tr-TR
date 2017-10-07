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
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="04b9b-103">Azure Cosmos DB için Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="04b9b-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="04b9b-104">Merhaba aşağıdaki tabloda bağlantıları toosample Azure CLI betikler için Azure Cosmos DB içerir.</span><span class="sxs-lookup"><span data-stu-id="04b9b-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="04b9b-105">Tüm Azure Cosmos DB CLI komutları için başvuru sayfaları hello kullanılabilir [Azure CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="04b9b-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="04b9b-106">**Azure Cosmos DB hesap, veritabanı ve kapsayıcıları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="04b9b-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="04b9b-107">Bir DocumentDB API, grafik veya tablo API hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="04b9b-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="04b9b-108">Bir tek Azure Cosmos DB API hesabını, veritabanını ve kullanmak için kapsayıcı hello DocumentDB, grafik veya tablo API'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04b9b-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="04b9b-109">MongoDB API hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b9b-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="04b9b-110">Bir tek Azure Cosmos DB MongoDB API hesap, veritabanı ve koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04b9b-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="04b9b-111">**Azure Cosmos DB ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="04b9b-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="04b9b-112">Ölçek kapsayıcı işleme</span><span class="sxs-lookup"><span data-stu-id="04b9b-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="04b9b-113">Değişiklikleri hello bir kapsayıcısı üzerinde througput sağlandı.</span><span class="sxs-lookup"><span data-stu-id="04b9b-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="04b9b-114">Birden çok bölgelerdeki Azure Cosmos DB veritabanı hesabı çoğaltabilir ve yük devretme öncelikleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="04b9b-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="04b9b-115">Belirtilen yük devretme önceliğe sahip birden çok bölgeleri genel hesap verilerini çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="04b9b-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="04b9b-116">**Azure Cosmos DB güvenli**</span><span class="sxs-lookup"><span data-stu-id="04b9b-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="04b9b-117">Hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="04b9b-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="04b9b-118">Merhaba birincil ve ikincil ana yazma anahtarları ve birincil ve ikincil salt okunur anahtarları hello hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="04b9b-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="04b9b-119">MongoDB bağlantı dizesi Al</span><span class="sxs-lookup"><span data-stu-id="04b9b-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="04b9b-120">Merhaba bağlantı dizesi tooconnect MongoDB uygulama tooyour Azure Cosmos DB hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="04b9b-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="04b9b-121">Hesabı anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="04b9b-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="04b9b-122">Hello Yöneticisi veya hello hesabı için salt okunur anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04b9b-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="04b9b-123">Bir güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="04b9b-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="04b9b-124">Onaylanan bir makine ve/veya Bulut Hizmetleri kümesinden bir gelen IP erişim denetimi İlkesi toolimit erişim toohello hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04b9b-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="04b9b-125">**Yüksek kullanılabilirlik, olağanüstü durum kurtarma, yedekleme ve geri yükleme**</span><span class="sxs-lookup"><span data-stu-id="04b9b-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="04b9b-126">Yük devretme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="04b9b-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="04b9b-127">Ayarlar hello hesap çoğaltılır her bölgede yük devretme öncelik hello.</span><span class="sxs-lookup"><span data-stu-id="04b9b-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="04b9b-128">**Azure Cosmos DB kaynaklarına bağlanma**</span><span class="sxs-lookup"><span data-stu-id="04b9b-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="04b9b-129">Bir web uygulaması tooAzure Cosmos DB Bağlan</span><span class="sxs-lookup"><span data-stu-id="04b9b-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="04b9b-130">Oluşturabilir ve bir Azure Cosmos DB veritabanı ve Azure web uygulaması bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04b9b-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
