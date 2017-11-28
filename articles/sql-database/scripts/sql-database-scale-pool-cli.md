---
title: "aaaCLI örnek bir SQL esnek havuzu Azure SQL veritabanı ölçeklendirir | Microsoft Docs"
description: "Azure CLI örnek komut dosyası tooscale Azure SQL veritabanındaki bir SQL esnek havuzu"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="fb6ea-103">CLI tooscale Azure SQL veritabanındaki bir SQL esnek havuzu kullanın</span><span class="sxs-lookup"><span data-stu-id="fb6ea-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="fb6ea-104">Bu Azure CLI betik örnek SQL esnek havuzu oluşturur, havuza alınmış veritabanları taşır ve esnek havuz performans düzeyleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb6ea-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb6ea-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fb6ea-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb6ea-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fb6ea-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fb6ea-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fb6ea-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="fb6ea-109">Clean up deployment</span></span>

<span data-ttu-id="fb6ea-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fb6ea-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fb6ea-111">Script explanation</span></span>

<span data-ttu-id="fb6ea-112">Bu komut dosyası komutları toocreate bir kaynak grubu, mantıksal sunucusu, SQL veritabanı ve güvenlik duvarı kuralları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="fb6ea-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb6ea-114">Komut</span><span class="sxs-lookup"><span data-stu-id="fb6ea-114">Command</span></span> | <span data-ttu-id="fb6ea-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="fb6ea-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb6ea-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb6ea-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb6ea-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb6ea-118">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="fb6ea-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="fb6ea-119">Konaklar SQL veritabanı hello mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="fb6ea-120">az sql esnek havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb6ea-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="fb6ea-121">Merhaba mantıksal sunucu içindeki esnek veritabanı havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="fb6ea-122">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="fb6ea-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="fb6ea-123">SQL veritabanı Hello hello mantıksal Server'da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="fb6ea-124">az sql esnek havuzu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fb6ea-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="fb6ea-125">Bu örnek değişiklikleri hello eDTU atanmış bir esnek veritabanı havuzundaki güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="fb6ea-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="fb6ea-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fb6ea-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb6ea-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb6ea-128">Next steps</span></span>

<span data-ttu-id="fb6ea-129">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb6ea-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb6ea-130">Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fb6ea-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
