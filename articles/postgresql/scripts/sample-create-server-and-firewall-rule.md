---
title: "Azure CLI SCRIPT - PostgreSQL için bir Azure veritabanı oluşturma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - PostgreSQL sunucu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="28a07-103">PostgreSQL sunucu için bir Azure veritabanı oluşturma ve Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="28a07-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="28a07-104">Bu örnek CLI betik PostgreSQL sunucu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="28a07-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="28a07-105">Betik başarılı şekilde gerçekleştirildikten sonra tüm Azure hizmetlerini ve yapılandırılan IP adresi PostgreSQL sunucunun erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="28a07-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="28a07-106">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="28a07-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="28a07-107">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28a07-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="28a07-108">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="28a07-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="28a07-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="28a07-109">Sample script</span></span>
<span data-ttu-id="28a07-110">Bu örnek betik yönetici kullanıcı adı ve parola özelleştirmek için vurgulanan satırlar düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="28a07-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="28a07-111">[!code-azurecli-interactive[Ana](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "PostgreSQL ve sunucu düzeyinde güvenlik duvarı kuralı için bir Azure veritabanı oluşturun.")]</span><span class="sxs-lookup"><span data-stu-id="28a07-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="28a07-112">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="28a07-112">Clean up deployment</span></span>
<span data-ttu-id="28a07-113">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="28a07-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="28a07-114">[!code-azurecli-interactive[Ana](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "kaynak grubunu silebilirsiniz.")]</span><span class="sxs-lookup"><span data-stu-id="28a07-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="28a07-115">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="28a07-115">Script explanation</span></span>
<span data-ttu-id="28a07-116">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="28a07-116">This script uses the following commands.</span></span> <span data-ttu-id="28a07-117">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="28a07-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="28a07-118">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="28a07-118">**Command**</span></span> | <span data-ttu-id="28a07-119">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="28a07-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="28a07-120">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="28a07-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="28a07-121">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="28a07-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="28a07-122">az postgres sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="28a07-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="28a07-123">Veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="28a07-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="28a07-124">az postgres sunucu güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="28a07-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="28a07-125">Girilen IP adresi aralığından altındaki veritabanlarını ve sunucu erişmesine izin vermek için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="28a07-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="28a07-126">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="28a07-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="28a07-127">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="28a07-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="28a07-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="28a07-128">Next steps</span></span>
- <span data-ttu-id="28a07-129">Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="28a07-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="28a07-130">Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="28a07-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
