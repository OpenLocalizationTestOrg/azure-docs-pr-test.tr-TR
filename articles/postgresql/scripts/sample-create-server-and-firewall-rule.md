---
title: "aaa \"Azure CLI SCRIPT - PostgreSQL için bir Azure veritabanı oluşturma | Microsoft Docs\""
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
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="4e8bf-103">PostgreSQL sunucu için bir Azure veritabanı oluşturma ve hello Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e8bf-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="4e8bf-104">Bu örnek CLI betik PostgreSQL sunucu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="4e8bf-105">Hello betik başarılı şekilde gerçekleştirildikten sonra tüm Azure hizmetlerinden hello PostgreSQL sunucu erişilebilir ve IP adresi hello yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4e8bf-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4e8bf-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4e8bf-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4e8bf-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4e8bf-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4e8bf-109">Sample script</span></span>
<span data-ttu-id="4e8bf-110">Bu örnek komut dosyasında vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adı ve parola düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4e8bf-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="4e8bf-111">Clean up deployment</span></span>
<span data-ttu-id="4e8bf-112">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="4e8bf-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="4e8bf-113">Script explanation</span></span>
<span data-ttu-id="4e8bf-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-114">This script uses hello following commands.</span></span> <span data-ttu-id="4e8bf-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4e8bf-116">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="4e8bf-116">**Command**</span></span> | <span data-ttu-id="4e8bf-117">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="4e8bf-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="4e8bf-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e8bf-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4e8bf-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4e8bf-120">az postgres sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e8bf-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="4e8bf-121">Merhaba veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="4e8bf-122">az postgres sunucu güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e8bf-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="4e8bf-123">Bir güvenlik duvarı kuralı tooallow erişim toohello sunucusu ve altındaki veritabanlarını hello girilen IP adresi aralığından oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="4e8bf-124">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="4e8bf-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="4e8bf-125">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="4e8bf-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e8bf-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e8bf-126">Next steps</span></span>
- <span data-ttu-id="4e8bf-127">Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="4e8bf-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="4e8bf-128">Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="4e8bf-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
