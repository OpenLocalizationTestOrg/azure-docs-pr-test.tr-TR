---
title: "aaaCLI İzleyici ölçek tek örnek Azure SQL veritabanı | Microsoft Docs"
description: "Azure CLI örnek komut dosyası toomonitor ve ölçek tek bir Azure SQL veritabanı"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="91cc9-103">CLI toomonitor kullanın ve tek bir SQL veritabanı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="91cc9-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="91cc9-104">Bu Azure CLI betik örnek hello boyutu bilgileri hello veritabanının sorgulama sonra tek bir Azure SQL veritabanı tooa farklı performans düzeyi ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="91cc9-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91cc9-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="91cc9-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91cc9-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="91cc9-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="91cc9-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91cc9-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="91cc9-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="91cc9-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="91cc9-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="91cc9-109">Clean up deployment</span></span>

<span data-ttu-id="91cc9-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="91cc9-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="91cc9-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="91cc9-111">Script explanation</span></span>

<span data-ttu-id="91cc9-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="91cc9-112">This script uses hello following commands.</span></span> <span data-ttu-id="91cc9-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="91cc9-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="91cc9-114">Komut</span><span class="sxs-lookup"><span data-stu-id="91cc9-114">Command</span></span> | <span data-ttu-id="91cc9-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="91cc9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91cc9-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="91cc9-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91cc9-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91cc9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91cc9-118">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="91cc9-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="91cc9-119">Bir veritabanını barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="91cc9-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="91cc9-120">az sql db Göster-kullanım</span><span class="sxs-lookup"><span data-stu-id="91cc9-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="91cc9-121">Bir veritabanı için başlangıç boyutu kullanım bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="91cc9-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="91cc9-122">az sql db güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="91cc9-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="91cc9-123">Veritabanı Özellikleri (örneğin, hello hizmet katmanı veya performans düzeyini) güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır.</span><span class="sxs-lookup"><span data-stu-id="91cc9-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="91cc9-124">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="91cc9-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="91cc9-125">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="91cc9-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="91cc9-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91cc9-126">Next steps</span></span>

<span data-ttu-id="91cc9-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91cc9-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91cc9-128">Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91cc9-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
