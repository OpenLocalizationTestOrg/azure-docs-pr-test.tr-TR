---
title: "aaaAzure CLI komut dosyası oluşturma bir Azure Cosmos DB DocumentDB API hesap, veritabanı ve koleksiyonu | Microsoft Docs"
description: "Azure CLI betik örnek - bir Azure Cosmos DB DocumentDB API hesap, veritabanı ve koleksiyonu oluşturma"
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
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 53919a849e04fa69680219e51c0289b9f2affe07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="aff3e-103">Azure Cosmos DB: CLI kullanarak bir DocumentDB API hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="aff3e-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="aff3e-104">Bu örnek CLI betik Azure Cosmos DB DocumentDB API hesabını, veritabanını ve koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aff3e-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aff3e-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aff3e-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aff3e-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="aff3e-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="aff3e-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aff3e-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="aff3e-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="aff3e-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="aff3e-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="aff3e-109">Clean up deployment</span></span>

<span data-ttu-id="aff3e-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="aff3e-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="aff3e-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="aff3e-111">Script explanation</span></span>

<span data-ttu-id="aff3e-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="aff3e-112">This script uses hello following commands.</span></span> <span data-ttu-id="aff3e-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="aff3e-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aff3e-114">Komut</span><span class="sxs-lookup"><span data-stu-id="aff3e-114">Command</span></span> | <span data-ttu-id="aff3e-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="aff3e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aff3e-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aff3e-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="aff3e-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aff3e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aff3e-118">az cosmosdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="aff3e-118">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="aff3e-119">Bir Azure Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aff3e-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="aff3e-120">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="aff3e-120">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="aff3e-121">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="aff3e-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aff3e-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aff3e-122">Next steps</span></span>

<span data-ttu-id="aff3e-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aff3e-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="aff3e-124">Ek Azure Cosmos DB CLI kod örnekleri hello bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="aff3e-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
