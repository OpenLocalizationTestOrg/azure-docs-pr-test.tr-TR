---
title: "İlk Azure veritabanı için MySQL veritabanı - Azure CLI aaaDesign | Microsoft Docs"
description: "Bu öğretici açıklar nasıl toocreate Azure veritabanı için MySQL sunucusunu yönetmek ve Azure CLI 2.0 hello komut satırından kullanma veritabanı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="90bb9-103">İlk Azure veritabanınızı MySQL veritabanı için tasarlama</span><span class="sxs-lookup"><span data-stu-id="90bb9-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="90bb9-104">Azure veritabanı için MySQL bir hello MySQL Community Edition veritabanı altyapısını temel Microsoft bulut ilişkisel veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="90bb9-105">Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları toolearn nasıl kullanacağınız için:</span><span class="sxs-lookup"><span data-stu-id="90bb9-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90bb9-106">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="90bb9-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="90bb9-107">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90bb9-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="90bb9-108">Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="90bb9-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="90bb9-109">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="90bb9-109">Load sample data</span></span>
> * <span data-ttu-id="90bb9-110">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="90bb9-110">Query data</span></span>
> * <span data-ttu-id="90bb9-111">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="90bb9-111">Update data</span></span>
> * <span data-ttu-id="90bb9-112">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="90bb9-112">Restore data</span></span>

<span data-ttu-id="90bb9-113">Hello Azure bulut Kabuk hello tarayıcıda kullanabilir veya [yükleme Azure CLI 2.0]( /cli/azure/install-azure-cli) kendi bilgisayar toorun hello kod blokları bu öğreticideki üzerinde.</span><span class="sxs-lookup"><span data-stu-id="90bb9-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="90bb9-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="90bb9-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="90bb9-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="90bb9-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="90bb9-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="90bb9-117">Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="90bb9-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="90bb9-118">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="90bb9-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="90bb9-119">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="90bb9-119">Create a resource group</span></span>
<span data-ttu-id="90bb9-120">Oluşturma bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) ile [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="90bb9-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="90bb9-121">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="90bb9-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="90bb9-122">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `mycliresource` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="90bb9-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="90bb9-123">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="90bb9-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="90bb9-124">MySQL sunucusu hello az mysql server ile oluşturmak için komutu bir Azure veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90bb9-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="90bb9-125">Bir sunucu birden çok veritabanını yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-125">A server can manage multiple databases.</span></span> <span data-ttu-id="90bb9-126">Genellikle her proje veya kullanıcı için farklı bir veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90bb9-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="90bb9-127">Merhaba aşağıdaki örnek bir Azure veritabanı bulunan MySQL sunucusu için oluşturur `westus` hello kaynak grubunda `mycliresource` adla `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="90bb9-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="90bb9-128">Merhaba sunucu sahip bir yönetici oturumu adlı `myadmin` ve parola `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="90bb9-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="90bb9-129">Merhaba sunucusu ile oluşturulur **temel** performans katmanı ve **50** hello Server'daki tüm hello veritabanları arasında paylaşılan birimler işlem.</span><span class="sxs-lookup"><span data-stu-id="90bb9-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="90bb9-130">İşlem ve depolama yukarı veya aşağı hello uygulamanızın gereksinimlerine bağlı olarak ölçekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90bb9-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="90bb9-131">Güvenlik duvarı kuralını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90bb9-131">Configure firewall rule</span></span>
<span data-ttu-id="90bb9-132">MySQL sunucu düzeyinde güvenlik duvarı kuralı ile Merhaba az mysql server güvenlik duvarı kuralı oluşturmak için komutu bir Azure veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90bb9-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="90bb9-133">Sunucu düzeyinde güvenlik duvarı kuralı gibi bir dış uygulamaya izin verir **mysql** komut satırı aracını veya MySQL çalışma ekranı tooconnect tooyour sunucu hello Azure MySQL hizmeti güvenlik duvarı üzerinden.</span><span class="sxs-lookup"><span data-stu-id="90bb9-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="90bb9-134">Merhaba aşağıdaki örnek bir önceden tanımlanmış adres aralığı için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90bb9-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="90bb9-135">Bu örnek hello tüm olası IP adresleri aralığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="90bb9-136">Merhaba bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="90bb9-136">Get hello connection information</span></span>

<span data-ttu-id="90bb9-137">tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="90bb9-138">Merhaba, JSON biçiminde sonucudur.</span><span class="sxs-lookup"><span data-stu-id="90bb9-138">hello result is in JSON format.</span></span> <span data-ttu-id="90bb9-139">Merhaba Not **fullyQualifiedDomainName** ve **Admınıstratorlogın**.</span><span class="sxs-lookup"><span data-stu-id="90bb9-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="90bb9-140">MySQL kullanarak toohello sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="90bb9-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="90bb9-141">Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish MySQL sunucusu için bağlantı tooyour Azure veritabanı.</span><span class="sxs-lookup"><span data-stu-id="90bb9-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="90bb9-142">Bu örnekte, hello komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="90bb9-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="90bb9-143">Boş veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90bb9-143">Create a blank database</span></span>
<span data-ttu-id="90bb9-144">Bağlı toohello sunucu olduğunuzda, boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90bb9-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="90bb9-145">Merhaba isteminde komut tooswitch hello bağlantı toothis yeni oluşturulan veritabanı aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90bb9-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="90bb9-146">Merhaba veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="90bb9-146">Create tables in hello database</span></span>
<span data-ttu-id="90bb9-147">Nasıl tooconnect toohello Azure veritabanı MySQL veritabanı için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="90bb9-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="90bb9-148">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="90bb9-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="90bb9-149">Envanter bilgilerini depolayan bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="90bb9-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="90bb9-150">Merhaba tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="90bb9-150">Load data into hello tables</span></span>
<span data-ttu-id="90bb9-151">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90bb9-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="90bb9-152">Merhaba açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="90bb9-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="90bb9-153">Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="90bb9-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="90bb9-154">Sorgulamak ve hello hello tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="90bb9-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="90bb9-155">Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="90bb9-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="90bb9-156">Ayrıca hello tablolardaki hello verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90bb9-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="90bb9-157">veri aldığınızda hello satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="90bb9-158">Zaman içinde veritabanı tooa önceki bir noktaya geri</span><span class="sxs-lookup"><span data-stu-id="90bb9-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="90bb9-159">Bu tablo yanlışlıkla silinmiş düşünün.</span><span class="sxs-lookup"><span data-stu-id="90bb9-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="90bb9-160">Bu, kolayca kurtaramazsınız şeydir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="90bb9-161">Azure veritabanı için MySQL toogo geri tooany noktası hello zamanda son too35 günleri sağlar ve zaman tooa yeni sunucu bu noktaya geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="90bb9-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="90bb9-162">Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90bb9-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="90bb9-163">Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.</span><span class="sxs-lookup"><span data-stu-id="90bb9-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="90bb9-164">Geri yükleme Hello için aşağıdaki bilgilerle hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="90bb9-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="90bb9-165">Geri yükleme noktası: bir noktası hello sunucu değiştirilmeden önce oluşan zamanında seçin.</span><span class="sxs-lookup"><span data-stu-id="90bb9-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="90bb9-166">Büyüktür veya toohello kaynak veritabanının en eski yedekleme değerine eşit gerekir.</span><span class="sxs-lookup"><span data-stu-id="90bb9-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="90bb9-167">Hedef sunucu: toorestore için istediğiniz yeni bir sunucu adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="90bb9-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="90bb9-168">Kaynak sunucu: Merhaba toorestore gelen istediğiniz hello sunucunun adını belirtin</span><span class="sxs-lookup"><span data-stu-id="90bb9-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="90bb9-169">Konumu: Hello bölge seçemezsiniz, varsayılan olarak hello kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="90bb9-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="90bb9-170">toorestore hello sunucu ve [tooa noktası zaman geri](./howto-restore-server-portal.md) hello tablo silinmeden önce.</span><span class="sxs-lookup"><span data-stu-id="90bb9-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="90bb9-171">Sunucu tooa farklı bir noktaya geri yükleme zamanında oluşturur yinelenen yeni bir sunucu hello özgün sunucusu olarak hello bir noktada, belirttiğiniz gibi hello saklama süresi içinde olmasını sağlanan, [hizmet katmanı](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="90bb9-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90bb9-172">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="90bb9-172">Next Steps</span></span>
<span data-ttu-id="90bb9-173">Bu öğreticide için öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="90bb9-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="90bb9-174">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="90bb9-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="90bb9-175">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90bb9-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="90bb9-176">Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="90bb9-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="90bb9-177">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="90bb9-177">Load sample data</span></span>
> * <span data-ttu-id="90bb9-178">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="90bb9-178">Query data</span></span>
> * <span data-ttu-id="90bb9-179">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="90bb9-179">Update data</span></span>
> * <span data-ttu-id="90bb9-180">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="90bb9-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90bb9-181">Azure veritabanı için MySQL - Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="90bb9-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
