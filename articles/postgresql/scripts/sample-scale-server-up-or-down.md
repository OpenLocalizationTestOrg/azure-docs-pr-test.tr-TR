---
title: "Azure CLI betik ölçekli Azure veritabanı için PostgreSQL | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - PostgreSQL Sunucusu ölçümleri sorgulama sonra farklı performans düzeyi için ölçek Azure veritabanı."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="e3a5b-103">İzleme ve Azure CLI kullanarak tek bir PostgreSQL sunucu ölçekleme</span><span class="sxs-lookup"><span data-stu-id="e3a5b-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="e3a5b-104">Bu örnek CLI betik ölçümleri sorgulama sonra PostgreSQL sunucusu farklı performans düzeyi için tek bir Azure veritabanı ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e3a5b-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e3a5b-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="e3a5b-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e3a5b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e3a5b-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e3a5b-108">Sample script</span></span>
<span data-ttu-id="e3a5b-109">Bu örnek betik yönetici kullanıcı adı ve parola özelleştirmek için vurgulanan satırları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="e3a5b-110">Kendi abonelik kimliği ile az İzleyici komutlarda kullanılan abonelik kimliğini değiştirin. [!code-azurecli-interactive [ana](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "oluşturma ve ölçek Azure veritabanı PostgreSQL için.")]</span><span class="sxs-lookup"><span data-stu-id="e3a5b-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e3a5b-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e3a5b-111">Clean up deployment</span></span>
<span data-ttu-id="e3a5b-112">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="e3a5b-113">[!code-azurecli-interactive[Ana](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "kaynak grubunu silebilirsiniz.")]</span><span class="sxs-lookup"><span data-stu-id="e3a5b-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="e3a5b-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e3a5b-114">Script explanation</span></span>
<span data-ttu-id="e3a5b-115">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-115">This script uses the following commands.</span></span> <span data-ttu-id="e3a5b-116">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e3a5b-117">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="e3a5b-117">**Command**</span></span> | <span data-ttu-id="e3a5b-118">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="e3a5b-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="e3a5b-119">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3a5b-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e3a5b-120">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e3a5b-121">az postgres sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3a5b-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="e3a5b-122">Veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="e3a5b-123">az İzleyici ölçümleri listesi</span><span class="sxs-lookup"><span data-stu-id="e3a5b-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="e3a5b-124">Kaynaklar için ölçüm değeri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="e3a5b-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="e3a5b-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="e3a5b-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="e3a5b-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e3a5b-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3a5b-127">Next steps</span></span>
- <span data-ttu-id="e3a5b-128">Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e3a5b-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="e3a5b-129">Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e3a5b-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="e3a5b-130">Ölçeklendirme hakkında daha fazla bilgi okuyun: [hizmet katmanları](../concepts-service-tiers.md) ve [işlem birimleri ve depolama birimleri](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="e3a5b-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
