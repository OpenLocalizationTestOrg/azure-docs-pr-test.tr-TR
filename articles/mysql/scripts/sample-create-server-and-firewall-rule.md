---
title: "aaa \"Azure CLI komut dosyası - Azure veritabanı için MySQL oluşturun. | Microsoft Docs\""
description: "Bu örnek CLI betik MySQL sunucusu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="763ee-103">MySQL sunucusu oluşturun ve hello Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="763ee-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="763ee-104">Bu örnek CLI betik MySQL sunucusu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="763ee-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="763ee-105">Hello komut dosyası başarıyla çalıştıktan sonra hello MySQL server tüm Azure Hizmetleri tarafından erişilebilir ve IP adresi hello yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="763ee-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="763ee-106">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="763ee-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="763ee-107">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="763ee-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="763ee-108">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="763ee-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="763ee-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="763ee-109">Sample script</span></span>
<span data-ttu-id="763ee-110">Bu örnek komut dosyasında vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adı ve parola düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="763ee-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="763ee-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="763ee-111">Clean up deployment</span></span>
<span data-ttu-id="763ee-112">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="763ee-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="763ee-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="763ee-113">Script explanation</span></span>
<span data-ttu-id="763ee-114">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="763ee-114">This script uses hello following commands.</span></span> <span data-ttu-id="763ee-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="763ee-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="763ee-116">**Komutu**</span><span class="sxs-lookup"><span data-stu-id="763ee-116">**Command**</span></span> | <span data-ttu-id="763ee-117">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="763ee-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="763ee-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="763ee-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="763ee-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="763ee-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="763ee-120">az mysql sunucusu oluşturun</span><span class="sxs-lookup"><span data-stu-id="763ee-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="763ee-121">Merhaba veritabanlarını barındıran MySQL server oluşturur.</span><span class="sxs-lookup"><span data-stu-id="763ee-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="763ee-122">az mysql server güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="763ee-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="763ee-123">Bir güvenlik duvarı kuralı tooallow erişim toohello sunucusu ve altındaki veritabanlarını hello girilen IP adresi aralığından oluşturur.</span><span class="sxs-lookup"><span data-stu-id="763ee-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="763ee-124">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="763ee-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="763ee-125">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="763ee-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="763ee-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="763ee-126">Next steps</span></span>
- <span data-ttu-id="763ee-127">Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="763ee-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="763ee-128">Ek komut dosyaları deneyin: [Azure veritabanı için MySQL için Azure CLI örnekleri](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="763ee-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
