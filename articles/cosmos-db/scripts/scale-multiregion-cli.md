---
title: "Azure Cosmos DB için Azure CLI betik-Multiregion çoğaltma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Azure Cosmos DB için Multiregion çoğaltma"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="bc02b-103">Birden çok bölgeye Azure Cosmos DB veritabanı hesabı çoğaltabilir ve yük devretme öncelikleri Azure CLI kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bc02b-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="bc02b-104">Bu örnek, birden çok bölgelerdeki Azure Cosmos DB veritabanı hesabı her türlü yinelenir ve Azure CLI kullanarak yük devretme öncelikleri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bc02b-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bc02b-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc02b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bc02b-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc02b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="bc02b-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bc02b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bc02b-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="bc02b-108">Sample script</span></span>

<span data-ttu-id="bc02b-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "ölçek Azure Cosmos birden çok bölgeye Veritabanına")]</span><span class="sxs-lookup"><span data-stu-id="bc02b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="bc02b-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="bc02b-110">Clean up deployment</span></span>

<span data-ttu-id="bc02b-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc02b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bc02b-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="bc02b-112">Script explanation</span></span>

<span data-ttu-id="bc02b-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="bc02b-113">This script uses the following commands.</span></span> <span data-ttu-id="bc02b-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="bc02b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bc02b-115">Komut</span><span class="sxs-lookup"><span data-stu-id="bc02b-115">Command</span></span> | <span data-ttu-id="bc02b-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="bc02b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bc02b-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc02b-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="bc02b-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc02b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bc02b-119">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bc02b-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="bc02b-120">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bc02b-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="bc02b-121">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="bc02b-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="bc02b-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="bc02b-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bc02b-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc02b-123">Next steps</span></span>

<span data-ttu-id="bc02b-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc02b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bc02b-125">Ek Azure Cosmos DB CLI kod örnekleri bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bc02b-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
