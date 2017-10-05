---
title: "Azure Cosmos DB Azure PowerShell örnekleri | Microsoft Docs"
description: "Azure PowerShell örnekleri - Azure Cosmos DB hesaplarını oluşturmak ve yönetmek amacıyla komut dosyaları."
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
ms.openlocfilehash: 7698e03c0dc8d1c6d1e926f45e903a909bfd0c93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="60e57-103">Azure Cosmos DB Azure PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="60e57-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="60e57-104">Aşağıdaki tabloda Azure Cosmos DB için örnek Azure PowerShell betikleri bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="60e57-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span>

| |  |
|---|---|
|<span data-ttu-id="60e57-105">**Bir Azure Cosmos DB hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="60e57-105">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="60e57-106">Bir DocumentDB API hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="60e57-106">Create a DocumentDB API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="60e57-107">DocumentDB API'si ile kullanmak için tek bir Azure Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60e57-107">Creates a single Azure Cosmos DB account to use with the DocumentDB API.</span></span> |
|<span data-ttu-id="60e57-108">**Azure Cosmos DB ölçeklendirme**</span><span class="sxs-lookup"><span data-stu-id="60e57-108">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="60e57-109">Birden çok bölgeye Azure Cosmos DB hesabında çoğaltabilir ve yük devretme öncelikleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="60e57-109">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="60e57-110">Belirtilen yük devretme önceliğe sahip birden çok bölgeleri genel hesap verilerini çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="60e57-110">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="60e57-111">**Azure Cosmos DB güvenli**</span><span class="sxs-lookup"><span data-stu-id="60e57-111">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="60e57-112">Hesap anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="60e57-112">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="60e57-113">Birincil ve ikincil ana yazma anahtarları ve birincil ve ikincil salt okunur hesabı için anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="60e57-113">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="60e57-114">MongoDB bağlantı dizesi Al</span><span class="sxs-lookup"><span data-stu-id="60e57-114">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="60e57-115">MongoDB uygulamanızı Azure Cosmos DB hesabınıza bağlanmak için bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="60e57-115">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="60e57-116">Hesabı anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="60e57-116">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="60e57-117">Hesabı için asıl veya salt okunur anahtarı yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60e57-117">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="60e57-118">Bir güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="60e57-118">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="60e57-119">Onaylanan bir dizi makineyi hesabına erişimi sınırlamak ve/veya Bulut Hizmetleri için bir gelen IP erişim denetimi ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60e57-119">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="60e57-120">**Yüksek kullanılabilirlik, olağanüstü durum kurtarma, yedekleme ve geri yükleme**</span><span class="sxs-lookup"><span data-stu-id="60e57-120">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="60e57-121">Yük devretme ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="60e57-121">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="60e57-122">Hesap çoğaltılır her bölgede yük devretme öncelik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="60e57-122">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||