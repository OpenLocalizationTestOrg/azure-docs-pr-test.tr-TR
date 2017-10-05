---
title: "Azure CLI komut dosyası oluştur Azure Cosmos DB DocumentDB API'si hesabınız, veritabanı ve koleksiyonu | Microsoft Docs"
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
ms.openlocfilehash: 28f99d56404e47adcd375d9f3106cc234469cbfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="91623-103">Azure Cosmos DB: CLI kullanarak bir DocumentDB API hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91623-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="91623-104">Bu örnek CLI betik Azure Cosmos DB DocumentDB API hesabını, veritabanını ve koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91623-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91623-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91623-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91623-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="91623-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="91623-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91623-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="91623-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="91623-108">Sample script</span></span>

<span data-ttu-id="91623-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Azure Cosmos DB DocumentDB API hesabı, veritabanınızı ve koleksiyonunuzu oluşturun")]</span><span class="sxs-lookup"><span data-stu-id="91623-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="91623-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="91623-110">Clean up deployment</span></span>

<span data-ttu-id="91623-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91623-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="91623-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="91623-112">Script explanation</span></span>

<span data-ttu-id="91623-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="91623-113">This script uses the following commands.</span></span> <span data-ttu-id="91623-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="91623-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="91623-115">Komut</span><span class="sxs-lookup"><span data-stu-id="91623-115">Command</span></span> | <span data-ttu-id="91623-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="91623-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91623-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="91623-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="91623-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91623-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91623-119">az cosmosdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="91623-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="91623-120">Bir Azure Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91623-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="91623-121">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="91623-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="91623-122">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="91623-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91623-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91623-123">Next steps</span></span>

<span data-ttu-id="91623-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91623-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91623-125">Ek Azure Cosmos DB CLI kod örnekleri bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91623-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
