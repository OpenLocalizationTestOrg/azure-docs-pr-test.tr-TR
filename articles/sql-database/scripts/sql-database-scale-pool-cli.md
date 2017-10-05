---
title: "CLI örnek bir SQL esnek havuzu Azure SQL veritabanı ölçeklendirir | Microsoft Docs"
description: "Azure SQL veritabanındaki bir SQL esnek havuzu ölçeklendirmek için azure CLI örnek betik"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="3470f-103">Azure SQL veritabanındaki bir SQL esnek havuzu ölçeklemek için CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="3470f-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="3470f-104">Bu Azure CLI betik örnek SQL esnek havuzu oluşturur, havuza alınmış veritabanları taşır ve esnek havuz performans düzeyleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3470f-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3470f-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3470f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3470f-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3470f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="3470f-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3470f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3470f-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3470f-108">Sample script</span></span>

<span data-ttu-id="3470f-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "veritabanı havuzları arasında taşıma")]</span><span class="sxs-lookup"><span data-stu-id="3470f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3470f-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="3470f-110">Clean up deployment</span></span>

<span data-ttu-id="3470f-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3470f-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3470f-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3470f-112">Script explanation</span></span>

<span data-ttu-id="3470f-113">Bu komut, bir kaynak grubu, mantıksal sunucusu, SQL veritabanı ve güvenlik duvarı kuralları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="3470f-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="3470f-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="3470f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3470f-115">Komut</span><span class="sxs-lookup"><span data-stu-id="3470f-115">Command</span></span> | <span data-ttu-id="3470f-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="3470f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3470f-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3470f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3470f-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3470f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3470f-119">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="3470f-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="3470f-120">SQL veritabanı barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3470f-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="3470f-121">az sql esnek havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="3470f-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="3470f-122">Mantıksal sunucu içindeki esnek veritabanı havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3470f-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="3470f-123">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="3470f-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="3470f-124">SQL Database mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3470f-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="3470f-125">az sql esnek havuzu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3470f-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="3470f-126">Esnek veritabanı havuzu güncelleştirmeleri, bu örnekte atanan eDTU değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3470f-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="3470f-127">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="3470f-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3470f-128">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="3470f-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3470f-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3470f-129">Next steps</span></span>

<span data-ttu-id="3470f-130">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3470f-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3470f-131">Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3470f-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
