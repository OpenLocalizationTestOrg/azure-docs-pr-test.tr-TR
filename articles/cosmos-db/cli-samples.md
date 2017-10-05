---
title: "Azure Cosmos DB için Azure CLI örnek | Microsoft Docs"
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
ms.openlocfilehash: 709d2ccce0f4b9827a8076f683c7e0f74cbdd4ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="4a7fc-103">Azure Cosmos DB için Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="4a7fc-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="4a7fc-104">Aşağıdaki tabloda Azure Cosmos DB için örnek Azure CLI komutlar bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="4a7fc-105">Başvuru sayfaları tüm Azure Cosmos DB CLI komutları için de kullanılabilir [Azure CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="4a7fc-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="4a7fc-106">**Azure Cosmos DB hesap, veritabanı ve kapsayıcıları oluşturma**</span><span class="sxs-lookup"><span data-stu-id="4a7fc-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="4a7fc-107">Bir DocumentDB API, grafik veya tablo API hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="4a7fc-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4a7fc-108">Bir tek Azure Cosmos DB API hesabını, veritabanını ve kullanmak için kapsayıcı DocumentDB, grafik veya tablo API'ler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-108">Creates a single Azure Cosmos DB API account, database, and container for use with the DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="4a7fc-109">MongoDB API hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a7fc-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4a7fc-110">Bir tek Azure Cosmos DB MongoDB API hesap, veritabanı ve koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="4a7fc-111">**Azure Cosmos DB ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="4a7fc-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4a7fc-112">Ölçek kapsayıcı işleme</span><span class="sxs-lookup"><span data-stu-id="4a7fc-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4a7fc-113">Bir kapsayıcı üzerinde sağlanan througput değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-113">Changes the provisioned througput on a container.</span></span>|
|[<span data-ttu-id="4a7fc-114">Birden çok bölgelerdeki Azure Cosmos DB veritabanı hesabı çoğaltabilir ve yük devretme öncelikleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4a7fc-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4a7fc-115">Belirtilen yük devretme önceliğe sahip birden çok bölgeleri genel hesap verilerini çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="4a7fc-116">**Azure Cosmos DB güvenli**</span><span class="sxs-lookup"><span data-stu-id="4a7fc-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="4a7fc-117">Hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="4a7fc-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4a7fc-118">Birincil ve ikincil ana yazma anahtarları ve birincil ve ikincil salt okunur hesabı için anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-118">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="4a7fc-119">MongoDB bağlantı dizesi Al</span><span class="sxs-lookup"><span data-stu-id="4a7fc-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="4a7fc-120">MongoDB uygulamanızı Azure Cosmos DB hesabınıza bağlanmak için bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-120">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="4a7fc-121">Hesabı anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="4a7fc-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4a7fc-122">Hesabı için asıl veya salt okunur anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-122">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="4a7fc-123">Bir güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a7fc-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="4a7fc-124">Onaylanan bir dizi makineyi hesabına erişimi sınırlamak ve/veya Bulut Hizmetleri için bir gelen IP erişim denetimi ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-124">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="4a7fc-125">**Yüksek kullanılabilirlik, olağanüstü durum kurtarma, yedekleme ve geri yükleme**</span><span class="sxs-lookup"><span data-stu-id="4a7fc-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="4a7fc-126">Yük devretme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4a7fc-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4a7fc-127">Hesap çoğaltılır her bölgede yük devretme öncelik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-127">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="4a7fc-128">**Azure Cosmos DB kaynaklarına bağlanma**</span><span class="sxs-lookup"><span data-stu-id="4a7fc-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="4a7fc-129">Bir web uygulaması Azure Cosmos Veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="4a7fc-129">Connect a web app to Azure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="4a7fc-130">Oluşturabilir ve bir Azure Cosmos DB veritabanı ve Azure web uygulaması bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7fc-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
