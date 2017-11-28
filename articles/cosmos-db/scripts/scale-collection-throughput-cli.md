---
title: "aaaAzure CLI betik ölçekli Azure Cosmos DB kapsayıcı işleme | Microsoft Docs"
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
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a><span data-ttu-id="bfe6c-103">Ölçek Azure Cosmos DB kapsayıcı verimlilik Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="bfe6c-103">Scale Azure Cosmos DB container throughput using hello Azure CLI</span></span>

<span data-ttu-id="bfe6c-104">Bu örnek, Azure Cosmos DB kapsayıcı herhangi bir tür için kapsayıcı işleme ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bfe6c-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bfe6c-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bfe6c-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bfe6c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bfe6c-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="bfe6c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bfe6c-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="bfe6c-109">Clean up deployment</span></span>

<span data-ttu-id="bfe6c-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bfe6c-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="bfe6c-111">Script explanation</span></span>

<span data-ttu-id="bfe6c-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-112">This script uses hello following commands.</span></span> <span data-ttu-id="bfe6c-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bfe6c-114">Komut</span><span class="sxs-lookup"><span data-stu-id="bfe6c-114">Command</span></span> | <span data-ttu-id="bfe6c-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="bfe6c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bfe6c-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bfe6c-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="bfe6c-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bfe6c-118">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bfe6c-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="bfe6c-119">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="bfe6c-120">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="bfe6c-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="bfe6c-121">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="bfe6c-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bfe6c-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bfe6c-122">Next steps</span></span>

<span data-ttu-id="bfe6c-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bfe6c-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bfe6c-124">Ek Azure Cosmos DB CLI kod örnekleri hello bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bfe6c-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
