---
title: "CLI örnek taşıma Azure SQL veritabanı SQL esnek havuzu | Microsoft Docs"
description: "SQL esnek havuzu içinde bir SQL veritabanını taşımak için azure CLI örnek betik"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="f1d8e-103">SQL esnek havuzu içinde bir Azure SQL veritabanını taşımak için CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="f1d8e-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="f1d8e-104">Bu Azure CLI komut dosyası örneği iki esnek havuzlar oluşturur ve bir Azure SQL veritabanı bir SQL esnek havuzdan başka bir SQL esnek havuza ve ardından veritabanı dışına esnek havuz bir tek Azure veritabanı performans düzeyine taşır.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f1d8e-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f1d8e-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f1d8e-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f1d8e-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f1d8e-108">Sample script</span></span>

<span data-ttu-id="f1d8e-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "veritabanı havuzları arasında taşıma")]</span><span class="sxs-lookup"><span data-stu-id="f1d8e-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f1d8e-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f1d8e-110">Clean up deployment</span></span>

<span data-ttu-id="f1d8e-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f1d8e-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f1d8e-112">Script explanation</span></span>

<span data-ttu-id="f1d8e-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-113">This script uses the following commands.</span></span> <span data-ttu-id="f1d8e-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f1d8e-115">Komut</span><span class="sxs-lookup"><span data-stu-id="f1d8e-115">Command</span></span> | <span data-ttu-id="f1d8e-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="f1d8e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1d8e-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1d8e-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f1d8e-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1d8e-119">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="f1d8e-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="f1d8e-120">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f1d8e-121">az sql esnek havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1d8e-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="f1d8e-122">Bir esnek havuz mantıksal sunucu içindeki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="f1d8e-123">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="f1d8e-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="f1d8e-124">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f1d8e-125">az sql db güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f1d8e-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="f1d8e-126">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f1d8e-127">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f1d8e-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f1d8e-128">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1d8e-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f1d8e-129">Next steps</span></span>

<span data-ttu-id="f1d8e-130">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f1d8e-131">Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


