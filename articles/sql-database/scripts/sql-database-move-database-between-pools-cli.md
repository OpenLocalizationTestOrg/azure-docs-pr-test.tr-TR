---
title: "aaaCLI örnek taşıma Azure SQL veritabanı SQL esnek havuzu | Microsoft Docs"
description: "Azure CLI örnek komut dosyası toomove bir SQL veritabanında SQL esnek havuzu"
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
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="53178-103">SQL esnek havuzda CLI toomove Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="53178-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="53178-104">Bu Azure CLI komut dosyası örneği iki esnek havuzlar oluşturur ve bir Azure SQL veritabanı bir SQL esnek havuzdan başka bir SQL esnek havuza ve ardından hello veritabanı esnek havuz tooa tek Azure veritabanı performans düzeyi dışında taşır.</span><span class="sxs-lookup"><span data-stu-id="53178-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="53178-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="53178-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="53178-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="53178-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="53178-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53178-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="53178-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="53178-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="53178-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="53178-109">Clean up deployment</span></span>

<span data-ttu-id="53178-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="53178-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="53178-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="53178-111">Script explanation</span></span>

<span data-ttu-id="53178-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="53178-112">This script uses hello following commands.</span></span> <span data-ttu-id="53178-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="53178-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="53178-114">Komut</span><span class="sxs-lookup"><span data-stu-id="53178-114">Command</span></span> | <span data-ttu-id="53178-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="53178-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="53178-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="53178-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="53178-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53178-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="53178-118">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="53178-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="53178-119">Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53178-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="53178-120">az sql esnek havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="53178-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="53178-121">Merhaba mantıksal sunucu içindeki bir esnek havuz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53178-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="53178-122">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="53178-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="53178-123">Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53178-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="53178-124">az sql db güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="53178-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="53178-125">Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="53178-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="53178-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="53178-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="53178-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="53178-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="53178-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53178-128">Next steps</span></span>

<span data-ttu-id="53178-129">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53178-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="53178-130">Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53178-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


