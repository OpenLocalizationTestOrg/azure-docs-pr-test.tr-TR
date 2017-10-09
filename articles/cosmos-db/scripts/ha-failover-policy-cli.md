---
title: "aaaAzure CLI oluşturmak betik yüksek kullanılabilirlik için yük devretme ilke | Microsoft Docs"
description: "Azure CLI betik örnek - yüksek kullanılabilirlik için yük devretme ilkesi oluşturma"
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
ms.openlocfilehash: 9076f4ef23fceb4208c934c57ac6899f0b58ffd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-hello-azure-cli"></a><span data-ttu-id="e071b-103">Hello Azure CLI kullanarak yüksek kullanılabilirlik için yük devretme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e071b-103">Create a failover policy for high availability using hello Azure CLI</span></span>

<span data-ttu-id="e071b-104">Bu örnek CLI betik bir Azure Cosmos DB hesabı oluşturur ve yüksek kullanılabilirlik için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e071b-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e071b-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e071b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e071b-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e071b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e071b-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e071b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e071b-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e071b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e071b-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e071b-109">Clean up deployment</span></span>

<span data-ttu-id="e071b-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="e071b-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e071b-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e071b-111">Script explanation</span></span>

<span data-ttu-id="e071b-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="e071b-112">This script uses hello following commands.</span></span> <span data-ttu-id="e071b-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="e071b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e071b-114">Komut</span><span class="sxs-lookup"><span data-stu-id="e071b-114">Command</span></span> | <span data-ttu-id="e071b-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="e071b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e071b-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e071b-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e071b-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e071b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e071b-118">az cosmosdb oluşturma</span><span class="sxs-lookup"><span data-stu-id="e071b-118">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="e071b-119">Bir Azure Cosmos DB hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e071b-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="e071b-120">az cosmosdb güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e071b-120">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="e071b-121">Azure Cosmos DB hesabını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e071b-121">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="e071b-122">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="e071b-122">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="e071b-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="e071b-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e071b-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e071b-124">Next steps</span></span>

<span data-ttu-id="e071b-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e071b-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e071b-126">Ek Azure Cosmos DB CLI kod örnekleri hello bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e071b-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
