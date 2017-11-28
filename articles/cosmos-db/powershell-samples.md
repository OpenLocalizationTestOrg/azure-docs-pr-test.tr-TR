---
title: "aaaAzure Azure Cosmos DB PowerShell örnekleri | Microsoft Docs"
description: "Azure PowerShell örnekleri - oluşturun ve Azure Cosmos DB hesaplarını yönetme betikleri toohelp."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 8815e775f720226e98cc8dcf7743e481c213272b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="6f819-103">Azure Cosmos DB Azure PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="6f819-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="6f819-104">Merhaba aşağıdaki tabloda bağlantıları toosample Azure PowerShell komut dosyalarını Azure Cosmos DB içerir.</span><span class="sxs-lookup"><span data-stu-id="6f819-104">hello following table includes links toosample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="6f819-105">**Bir Azure Cosmos DB hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="6f819-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="6f819-106">Bir DocumentDB API hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="6f819-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="6f819-107">Tek bir Azure Cosmos DB hesap toouse hello DocumentDB API ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f819-107">Creates a single Azure Cosmos DB account toouse with hello DocumentDB API.</span></span> |
|<span data-ttu-id="6f819-108">**Azure Cosmos DB ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="6f819-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="6f819-109">Birden çok bölgeye Azure Cosmos DB hesabında çoğaltabilir ve yük devretme öncelikleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6f819-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="6f819-110">Belirtilen yük devretme önceliğe sahip birden çok bölgeleri genel hesap verilerini çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="6f819-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="6f819-111">**Azure Cosmos DB güvenli**</span><span class="sxs-lookup"><span data-stu-id="6f819-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="6f819-112">Hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="6f819-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="6f819-113">Merhaba birincil ve ikincil ana yazma anahtarları ve birincil ve ikincil salt okunur anahtarları hello hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="6f819-113">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="6f819-114">MongoDB bağlantı dizesi Al</span><span class="sxs-lookup"><span data-stu-id="6f819-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="6f819-115">Merhaba bağlantı dizesi tooconnect MongoDB uygulama tooyour Azure Cosmos DB hesabı alır.</span><span class="sxs-lookup"><span data-stu-id="6f819-115">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="6f819-116">Hesabı anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="6f819-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="6f819-117">Hello Yöneticisi veya hello hesabı için salt okunur anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f819-117">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="6f819-118">Bir güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f819-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="6f819-119">Onaylanan bir makine ve/veya Bulut Hizmetleri kümesinden bir gelen IP erişim denetimi İlkesi toolimit erişim toohello hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6f819-119">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="6f819-120">**Yüksek kullanılabilirlik, olağanüstü durum kurtarma, yedekleme ve geri yükleme**</span><span class="sxs-lookup"><span data-stu-id="6f819-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="6f819-121">Yük devretme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6f819-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="6f819-122">Ayarlar hello hesap çoğaltılır her bölgede yük devretme öncelik hello.</span><span class="sxs-lookup"><span data-stu-id="6f819-122">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|||