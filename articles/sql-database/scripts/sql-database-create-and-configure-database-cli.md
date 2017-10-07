---
title: "bir Azure SQL veritabanı aaaCLI örnek-create | Microsoft Docs"
description: "Azure CLI örnek komut dosyası toocreate bir SQL veritabanı"
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
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="db40a-103">CLI toocreate tek bir Azure SQL veritabanı kullanın ve bir güvenlik duvarı kuralı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="db40a-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="db40a-104">Bu Azure CLI betik örnek bir Azure SQL veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="db40a-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="db40a-105">Hello betik başarılı şekilde gerçekleştirildikten sonra SQL veritabanı tüm Azure hizmetlerinden erişilebilir hello ve başlangıç IP adresi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="db40a-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="db40a-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="db40a-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="db40a-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="db40a-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="db40a-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="db40a-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="db40a-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="db40a-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="db40a-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="db40a-110">Clean up deployment</span></span>

<span data-ttu-id="db40a-111">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="db40a-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="db40a-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="db40a-112">Script explanation</span></span>

<span data-ttu-id="db40a-113">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="db40a-113">This script uses hello following commands.</span></span> <span data-ttu-id="db40a-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="db40a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="db40a-115">Komut</span><span class="sxs-lookup"><span data-stu-id="db40a-115">Command</span></span> | <span data-ttu-id="db40a-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="db40a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="db40a-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="db40a-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="db40a-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db40a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="db40a-119">az sql server oluşturun</span><span class="sxs-lookup"><span data-stu-id="db40a-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="db40a-120">Konaklar SQL veritabanı hello mantıksal sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db40a-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="db40a-121">az sql server güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="db40a-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="db40a-122">Merhaba girilen IP adresi aralığından hello sunucusunda bir güvenlik duvarı kuralı tooallow erişim tooall SQL veritabanları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db40a-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="db40a-123">az sql db oluştur</span><span class="sxs-lookup"><span data-stu-id="db40a-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="db40a-124">SQL veritabanı Hello hello mantıksal Server'da oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db40a-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="db40a-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="db40a-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="db40a-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="db40a-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="db40a-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db40a-127">Next steps</span></span>

<span data-ttu-id="db40a-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db40a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="db40a-129">Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="db40a-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

