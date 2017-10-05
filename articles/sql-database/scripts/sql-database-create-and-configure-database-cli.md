---
title: "CLI oluşturmak örnek bir Azure SQL veritabanı | Microsoft Docs"
description: "Bir SQL veritabanı oluşturmak için azure CLI örnek betik"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="12f6b-103">Tek bir Azure SQL veritabanı oluşturma ve bir güvenlik duvarı kuralı yapılandırmak için CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="12f6b-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="12f6b-104">Bu Azure CLI betik örnek bir Azure SQL veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="12f6b-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="12f6b-105">Betik başarılı şekilde gerçekleştirildikten sonra SQL veritabanı tüm Azure hizmetlerini ve yapılandırılan IP adresi erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="12f6b-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="12f6b-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="12f6b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="12f6b-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="12f6b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="12f6b-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12f6b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="12f6b-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="12f6b-109">Sample script</span></span>

<span data-ttu-id="12f6b-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "SQL veritabanı oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="12f6b-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="12f6b-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="12f6b-111">Clean up deployment</span></span>

<span data-ttu-id="12f6b-112">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="12f6b-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="12f6b-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="12f6b-113">Script explanation</span></span>

<span data-ttu-id="12f6b-114">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="12f6b-114">This script uses the following commands.</span></span> <span data-ttu-id="12f6b-115">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="12f6b-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="12f6b-116">Komut</span><span class="sxs-lookup"><span data-stu-id="12f6b-116">Command</span></span> | <span data-ttu-id="12f6b-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="12f6b-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12f6b-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="12f6b-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="12f6b-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12f6b-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12f6b-120">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="12f6b-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="12f6b-121">SQL veritabanı barındıran bir mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12f6b-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="12f6b-122">az sql server güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="12f6b-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="12f6b-123">Girilen IP adresi aralığından sunucusundaki tüm SQL veritabanlarına erişim sağlamak için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12f6b-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="12f6b-124">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="12f6b-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="12f6b-125">SQL Database mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12f6b-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="12f6b-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="12f6b-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="12f6b-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="12f6b-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12f6b-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12f6b-128">Next steps</span></span>

<span data-ttu-id="12f6b-129">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12f6b-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="12f6b-130">Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="12f6b-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

