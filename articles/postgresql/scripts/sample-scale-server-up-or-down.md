---
title: "aaa \"Azure CLI betik ölçekli Azure veritabanı için PostgreSQL | Microsoft Docs\""
description: "Azure CLI komut dosyası örneği - hello ölçümleri sorgulama sonra PostgreSQL sunucu tooa farklı performans düzeyinde için ölçek Azure veritabanı."
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
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="a9c23-103">İzleme ve Azure CLI kullanarak tek bir PostgreSQL sunucu ölçekleme</span><span class="sxs-lookup"><span data-stu-id="a9c23-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="a9c23-104">Bu örnek CLI betik hello ölçümleri sorgulama sonra PostgreSQL sunucu tooa farklı performans düzeyi için tek bir Azure veritabanına ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="a9c23-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9c23-105">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a9c23-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9c23-106">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="a9c23-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a9c23-107">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9c23-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a9c23-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a9c23-108">Sample script</span></span>
<span data-ttu-id="a9c23-109">Bu örnek komut dosyasında, vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adını ve parolasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a9c23-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="a9c23-110">Merhaba az İzleyici komutları kendi abonelik kimliği ile kullanılan hello abonelik kimliği değiştirin.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="a9c23-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a9c23-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="a9c23-111">Clean up deployment</span></span>
<span data-ttu-id="a9c23-112">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9c23-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="a9c23-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a9c23-113">Script explanation</span></span>
<span data-ttu-id="a9c23-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9c23-114">This script uses hello following commands.</span></span> <span data-ttu-id="a9c23-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="a9c23-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9c23-116">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="a9c23-116">**Command**</span></span> | <span data-ttu-id="a9c23-117">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="a9c23-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="a9c23-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9c23-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a9c23-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9c23-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9c23-120">az postgres sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9c23-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="a9c23-121">Merhaba veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9c23-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="a9c23-122">az İzleyici ölçümleri listesi</span><span class="sxs-lookup"><span data-stu-id="a9c23-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="a9c23-123">Merhaba kaynakların listesi hello ölçüm değeri.</span><span class="sxs-lookup"><span data-stu-id="a9c23-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="a9c23-124">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="a9c23-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="a9c23-125">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="a9c23-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9c23-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9c23-126">Next steps</span></span>
- <span data-ttu-id="a9c23-127">Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="a9c23-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="a9c23-128">Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a9c23-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="a9c23-129">Ölçeklendirme hakkında daha fazla bilgi okuyun: [hizmet katmanları](../concepts-service-tiers.md) ve [işlem birimleri ve depolama birimleri](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a9c23-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
