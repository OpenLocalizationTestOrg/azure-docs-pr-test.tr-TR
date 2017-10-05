---
title: "Azure CLI: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure CLI kullanarak SQL Veritabanı mantıksal sunucusu, sunucu düzeyi güvenlik duvarı kuralı ve veritabanı oluşturmayı öğrenin."
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
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="d0660-104">Azure CLI ile tek Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0660-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="d0660-105">Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0660-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d0660-106">Bu kılavuzda bir [Azure SQL Veritabanı mantıksal sunucusundaki](sql-database-features.md) [Azure kaynak grubuna](../azure-resource-manager/resource-group-overview.md) Azure SQL veritabanı dağıtmak için Azure CLI kullanma ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0660-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="d0660-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0660-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d0660-108">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0660-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d0660-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d0660-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d0660-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d0660-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="d0660-111">Değişkenleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="d0660-111">Define variables</span></span>

<span data-ttu-id="d0660-112">Bu hızlı başlangıçtaki betiklerde kullanılacak değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d0660-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d0660-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0660-113">Create a resource group</span></span>

<span data-ttu-id="d0660-114">[az group create](/cli/azure/group#create) komutunu kullanarak bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0660-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d0660-115">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d0660-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d0660-116">Aşağıdaki örnek `westeurope` konumunda `myResourceGroup` adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0660-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="d0660-117">Mantıksal sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0660-117">Create a logical server</span></span>

<span data-ttu-id="d0660-118">[az sql server create](/cli/azure/sql/server#create) komutunu kullanarak [Azure SQL Veritabanı mantıksal sunucusu](sql-database-features.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0660-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="d0660-119">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="d0660-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="d0660-120">Aşağıdaki örnek, kaynak grubunuzda `ServerAdmin` yönetici oturum açma bilgileri ve `ChangeYourAdminPassword1` parolası ile rastgele olarak adlandırılmış bir sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0660-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="d0660-121">Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d0660-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="d0660-122">Sunucu güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0660-122">Configure a server firewall rule</span></span>

<span data-ttu-id="d0660-123">[az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) komutunu kullanarak [sunucu düzeyinde bir Azure SQL Veritabanı güvenlik duvarı kuralı](sql-database-firewall-configure.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0660-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d0660-124">Bir sunucu düzeyi güvenlik duvarı kuralı SQL Server Management Studio veya SQLCMD yardımcı programı gibi bir dış uygulamanın SQL Veritabanı hizmet güvenlik duvarı üzerinden bir SQL veritabanına bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0660-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="d0660-125">Aşağıdaki örnekte, güvenlik duvarı yalnızca diğer Azure kaynakları için açılır.</span><span class="sxs-lookup"><span data-stu-id="d0660-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="d0660-126">Dışarıdan bağlantı kurulabilmesi için IP adresini ortamınız için uygun bir adres olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d0660-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="d0660-127">Tüm IP adreslerini açmak için başlangıç IP adresi olarak 0.0.0.0’ı, bitiş adresi olaraksa 255.255.255.255’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0660-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="d0660-128">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d0660-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d0660-129">Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0660-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d0660-130">Bu durumda, BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL veritabanı sunucusuna bağlanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d0660-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="d0660-131">Sunucuda örnek verilerle veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0660-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="d0660-132">[az sql db create](/cli/azure/sql/db#create) komutunu kullanarak [S0 performans düzeyine](sql-database-service-tiers.md) sahip bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0660-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="d0660-133">Aşağıdaki örnek, `mySampleDatabase` adlı bir veritabanı oluşturur ve AdventureWorksLT örnek verilerini bu veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="d0660-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="d0660-134">Önceden tanımlanmış bu değerleri istediğiniz gibi değiştirin (bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıçtaki değerlere göre belirlenir).</span><span class="sxs-lookup"><span data-stu-id="d0660-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="d0660-135">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="d0660-135">Clean up resources</span></span>

<span data-ttu-id="d0660-136">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d0660-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="d0660-137">Sonraki hızlı başlangıçlarla çalışmaya devam etmeyi planlıyorsanız, bu hızlı başlangıçta oluşturulan kaynakları temizlemeyin.</span><span class="sxs-lookup"><span data-stu-id="d0660-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="d0660-138">Devam etmeyi planlamıyorsanız, Azure portalda bu hızlı başlangıç ile oluşturulan tüm kaynakları silmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0660-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="d0660-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0660-139">Next steps</span></span>

<span data-ttu-id="d0660-140">Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0660-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="d0660-141">Aşağıdan aracınızı seçerek daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="d0660-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="d0660-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d0660-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="d0660-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d0660-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="d0660-144">.NET</span><span class="sxs-lookup"><span data-stu-id="d0660-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="d0660-145">PHP</span><span class="sxs-lookup"><span data-stu-id="d0660-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="d0660-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="d0660-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="d0660-147">Java</span><span class="sxs-lookup"><span data-stu-id="d0660-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="d0660-148">Python</span><span class="sxs-lookup"><span data-stu-id="d0660-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="d0660-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="d0660-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

