---
title: "MySQL sunucusu için bir Azure veritabanı ölçeklendirmek için azure CLI örnekleri | Microsoft Docs"
description: "Bu örnek CLI betik ölçümleri sorgulama sonra farklı performans düzeyine MySQL sunucusu için Azure veritabanı ölçeklendirir."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="c6f74-103">İzleme ve Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı ölçekleme</span><span class="sxs-lookup"><span data-stu-id="c6f74-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="c6f74-104">Bu örnek CLI betik ölçümleri sorgulama sonra farklı performans düzeyine MySQL sunucusu için tek bir Azure veritabanına ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="c6f74-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c6f74-105">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6f74-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c6f74-106">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c6f74-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c6f74-107">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c6f74-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c6f74-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c6f74-108">Sample script</span></span>
<span data-ttu-id="c6f74-109">Bu örnek betik yönetici kullanıcı adı ve parola özelleştirmek için vurgulanan satırları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c6f74-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="c6f74-110">Kendi abonelik kimliği ile az İzleyici komutlarda kullanılan abonelik kimliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c6f74-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="c6f74-111">[!code-azurecli-interactive[Ana](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "oluşturma ve ölçek Azure veritabanı için MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="c6f74-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c6f74-112">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c6f74-112">Clean up deployment</span></span>
<span data-ttu-id="c6f74-113">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6f74-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="c6f74-114">[!code-azurecli-interactive[Ana](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "kaynak grubunu silebilirsiniz.")]</span><span class="sxs-lookup"><span data-stu-id="c6f74-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="c6f74-115">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c6f74-115">Script explanation</span></span>
<span data-ttu-id="c6f74-116">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6f74-116">This script uses the following commands.</span></span> <span data-ttu-id="c6f74-117">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="c6f74-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c6f74-118">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="c6f74-118">**Command**</span></span> | <span data-ttu-id="c6f74-119">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="c6f74-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="c6f74-120">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6f74-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c6f74-121">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6f74-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6f74-122">az mysql sunucusu oluşturun</span><span class="sxs-lookup"><span data-stu-id="c6f74-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="c6f74-123">Veritabanlarını barındıran MySQL server oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6f74-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="c6f74-124">az İzleyici ölçümleri listesi</span><span class="sxs-lookup"><span data-stu-id="c6f74-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="c6f74-125">Kaynaklar için ölçüm değeri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="c6f74-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="c6f74-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="c6f74-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c6f74-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="c6f74-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6f74-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6f74-128">Next steps</span></span>
- <span data-ttu-id="c6f74-129">Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c6f74-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="c6f74-130">Ek komut dosyaları deneyin: [Azure veritabanı için MySQL için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c6f74-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="c6f74-131">Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [hizmet katmanları](../concepts-service-tiers.md) ve [işlem birimleri ve depolama birimleri](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c6f74-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
