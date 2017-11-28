---
title: "MongoDB uygulamaları için Azure CLI betik Get Azure Cosmos DB bağlantı dizesi | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Get Azure Cosmos DB bağlantı dizesi MongoDB uygulamalar için"
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
ms.openlocfilehash: 916c92cab39306352fdf9dff0e0685fd61832d16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a><span data-ttu-id="f16ea-103">Azure CLI kullanarak MongoDB uygulamaları için Azure Cosmos DB bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="f16ea-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span></span>

<span data-ttu-id="f16ea-104">Bu örnek bir Azure CLI kullanarak MongoDB uygulamaları için Azure Cosmos DB bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="f16ea-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f16ea-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f16ea-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f16ea-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f16ea-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f16ea-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f16ea-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f16ea-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f16ea-108">Sample script</span></span>

<span data-ttu-id="f16ea-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "MongoDB uygulamaları için Azure Cosmos DB alma bağlantı dizesi")]</span><span class="sxs-lookup"><span data-stu-id="f16ea-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f16ea-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f16ea-110">Clean up deployment</span></span>

<span data-ttu-id="f16ea-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f16ea-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f16ea-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f16ea-112">Script explanation</span></span>

<span data-ttu-id="f16ea-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="f16ea-113">This script uses the following commands.</span></span> <span data-ttu-id="f16ea-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="f16ea-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f16ea-115">Komut</span><span class="sxs-lookup"><span data-stu-id="f16ea-115">Command</span></span> | <span data-ttu-id="f16ea-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="f16ea-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f16ea-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f16ea-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f16ea-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f16ea-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f16ea-119">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f16ea-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="f16ea-120">Bir Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f16ea-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="f16ea-121">az cosmosdb listesi-bağlantı-dizeleri</span><span class="sxs-lookup"><span data-stu-id="f16ea-121">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-connection-strings) | <span data-ttu-id="f16ea-122">Hesap için bağlantı dizesini alır.</span><span class="sxs-lookup"><span data-stu-id="f16ea-122">Gets the connection string for the account.</span></span>|
| [<span data-ttu-id="f16ea-123">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f16ea-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f16ea-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="f16ea-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f16ea-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f16ea-125">Next steps</span></span>

<span data-ttu-id="f16ea-126">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f16ea-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f16ea-127">Ek Azure Cosmos DB CLI kod örnekleri bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f16ea-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
