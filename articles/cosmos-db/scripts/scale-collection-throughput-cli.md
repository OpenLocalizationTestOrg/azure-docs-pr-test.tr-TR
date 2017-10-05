---
title: "Azure CLI betik ölçekli Azure Cosmos DB kapsayıcı işleme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - ölçek Azure Cosmos DB contianer işleme"
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
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="933eb-103">Azure CLI kullanarak ölçek Azure Cosmos DB kapsayıcı işleme</span><span class="sxs-lookup"><span data-stu-id="933eb-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="933eb-104">Bu örnek, Azure Cosmos DB kapsayıcı herhangi bir tür için kapsayıcı işleme ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="933eb-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="933eb-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="933eb-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="933eb-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="933eb-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="933eb-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="933eb-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="933eb-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="933eb-108">Sample script</span></span>

<span data-ttu-id="933eb-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "ölçek Azure Cosmos DB işleme")]</span><span class="sxs-lookup"><span data-stu-id="933eb-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="933eb-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="933eb-110">Clean up deployment</span></span>

<span data-ttu-id="933eb-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="933eb-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="933eb-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="933eb-112">Script explanation</span></span>

<span data-ttu-id="933eb-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="933eb-113">This script uses the following commands.</span></span> <span data-ttu-id="933eb-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="933eb-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="933eb-115">Komut</span><span class="sxs-lookup"><span data-stu-id="933eb-115">Command</span></span> | <span data-ttu-id="933eb-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="933eb-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="933eb-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="933eb-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="933eb-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="933eb-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="933eb-119">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="933eb-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="933eb-120">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="933eb-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="933eb-121">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="933eb-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="933eb-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="933eb-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="933eb-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="933eb-123">Next steps</span></span>

<span data-ttu-id="933eb-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="933eb-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="933eb-125">Ek Azure Cosmos DB CLI kod örnekleri bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="933eb-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
