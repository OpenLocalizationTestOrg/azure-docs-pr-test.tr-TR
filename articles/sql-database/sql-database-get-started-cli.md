---
title: "Azure CLI: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure CLI toocreate SQL Database mantıksal sunucusu, sunucu düzeyinde güvenlik duvarı kuralı ve kullanarak veritabanlarını nasıl hello öğrenin."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="3ad9d-104">Hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ad9d-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="3ad9d-105">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="3ad9d-106">Bir Azure SQL veritabanında bu kılavuzu kullanarak hello Azure CLI toodeploy ayrıntılarını bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) içinde bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="3ad9d-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="3ad9d-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3ad9d-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3ad9d-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3ad9d-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3ad9d-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="3ad9d-111">Değişkenleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="3ad9d-111">Define variables</span></span>

<span data-ttu-id="3ad9d-112">Bu hızlı başlangıç hello komut içinde kullanmak için değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3ad9d-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ad9d-113">Create a resource group</span></span>

<span data-ttu-id="3ad9d-114">Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3ad9d-115">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3ad9d-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="3ad9d-117">Mantıksal sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ad9d-117">Create a logical server</span></span>

<span data-ttu-id="3ad9d-118">Oluşturma bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md) hello kullanarak [az sql server oluşturun](/cli/azure/sql/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="3ad9d-119">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="3ad9d-120">Merhaba aşağıdaki örnek rastgele adlandırılmış bir sunucu, kaynak grubunda adlı bir yönetici oturum açma ile oluşturur `ServerAdmin` ve bir parola `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="3ad9d-121">Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="3ad9d-122">Sunucu güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3ad9d-122">Configure a server firewall rule</span></span>

<span data-ttu-id="3ad9d-123">Oluşturma bir [Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) hello kullanarak [az sql server güvenlik duvarı oluşturma](/cli/azure/sql/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="3ad9d-124">Sunucu düzeyinde güvenlik duvarı kuralı SQL Server Management Studio veya hello SQLCMD yardımcı programını tooconnect tooa SQL veritabanı gibi hello SQL Database hizmeti güvenlik duvarı üzerinden bir dış uygulamaya verir.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="3ad9d-125">Aşağıdaki örneğine hello hello Güvenlik Duvarı'nı yalnızca diğer Azure kaynakları için açıldı.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="3ad9d-126">tooenable harici bağlantı, başlangıç IP adresi tooan uygun adresini Değiştir ortamınız için.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="3ad9d-127">tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="3ad9d-128">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3ad9d-129">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3ad9d-130">Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="3ad9d-131">Merhaba sunucu örnek verilerle bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3ad9d-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="3ad9d-132">Bir veritabanı oluşturmak bir [S0 performans düzeyi](sql-database-service-tiers.md) hello kullanarak hello Server'daki [az sql db Oluştur](/cli/azure/sql/db#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="3ad9d-133">Merhaba aşağıdaki örnek adlı bir veritabanı oluşturur `mySampleDatabase` ve bu veritabanına yükleri hello AdventureWorksLT örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="3ad9d-134">Bu önceden tanımlanmış Değiştir istendiği gibi (Bu koleksiyonu yapıda Bu hızlı başlangıç hello değerleri bağlı diğer hızlı başlar) değerleri.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="3ad9d-135">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="3ad9d-135">Clean up resources</span></span>

<span data-ttu-id="3ad9d-136">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="3ad9d-137">Sonraki hızlı başlangıçlar ile toowork üzerinde toocontinue planlıyorsanız, temiz oluşturulan bu hızlı başlangıç kaynakları başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="3ad9d-138">Toocontinue düşünmüyorsanız bu hızlı başlangıç bölümünde hello Azure portal tarafından oluşturulan tüm kaynakları adımları toodelete aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3ad9d-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ad9d-139">Next steps</span></span>

<span data-ttu-id="3ad9d-140">Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ad9d-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="3ad9d-141">Aşağıdan aracınızı seçerek daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="3ad9d-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="3ad9d-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3ad9d-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="3ad9d-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3ad9d-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="3ad9d-144">.NET</span><span class="sxs-lookup"><span data-stu-id="3ad9d-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="3ad9d-145">PHP</span><span class="sxs-lookup"><span data-stu-id="3ad9d-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="3ad9d-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="3ad9d-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="3ad9d-147">Java</span><span class="sxs-lookup"><span data-stu-id="3ad9d-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="3ad9d-148">Python</span><span class="sxs-lookup"><span data-stu-id="3ad9d-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="3ad9d-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="3ad9d-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

