---
title: "CLI İzleyici ölçek tek örnek Azure SQL veritabanı | Microsoft Docs"
description: "Tek bir Azure SQL veritabanı ölçekleme ve izlemek için azure CLI örnek betik"
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="94fda-103">İzlemek ve tek bir SQL veritabanı ölçeklendirmek için CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="94fda-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="94fda-104">Bu Azure CLI betik örnek veritabanının boyutu bilgileri sorgulama sonra farklı performans düzeyi tek bir Azure SQL veritabanına ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="94fda-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94fda-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="94fda-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="94fda-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94fda-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="94fda-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94fda-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="94fda-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="94fda-108">Sample script</span></span>

<span data-ttu-id="94fda-109">[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "İzleyici ve ölçek tek SQL veritabanı")]</span><span class="sxs-lookup"><span data-stu-id="94fda-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="94fda-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="94fda-110">Clean up deployment</span></span>

<span data-ttu-id="94fda-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="94fda-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="94fda-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="94fda-112">Script explanation</span></span>

<span data-ttu-id="94fda-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="94fda-113">This script uses the following commands.</span></span> <span data-ttu-id="94fda-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="94fda-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="94fda-115">Komut</span><span class="sxs-lookup"><span data-stu-id="94fda-115">Command</span></span> | <span data-ttu-id="94fda-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="94fda-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94fda-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="94fda-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="94fda-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94fda-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="94fda-119">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="94fda-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="94fda-120">Bir veritabanını barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94fda-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="94fda-121">az sql db Göster-kullanım</span><span class="sxs-lookup"><span data-stu-id="94fda-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="94fda-122">Bir veritabanı boyutu kullanım bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="94fda-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="94fda-123">az sql db güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="94fda-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="94fda-124">Veritabanı Özellikleri (örneğin, hizmet katmanı veya performans düzeyini) güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="94fda-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="94fda-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="94fda-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="94fda-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="94fda-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="94fda-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94fda-127">Next steps</span></span>

<span data-ttu-id="94fda-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="94fda-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="94fda-129">Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94fda-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
