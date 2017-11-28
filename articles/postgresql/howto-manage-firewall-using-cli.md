---
title: "Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme | Microsoft Docs"
description: "Bu makalede, oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI komut satırını kullanarak yönetme açıklar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="7f733-103">Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="7f733-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="7f733-104">Bir Azure veritabanına PostgreSQL sunucusu için belirli bir IP adresi veya IP adresi aralığı erişimi yönetmek üzere yöneticiler sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f733-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="7f733-105">Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silin, listeleyin ve sunucunuzu yönetmek için güvenlik duvarı kuralları gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f733-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="7f733-106">Genel Bakış Azure veritabanı için PostgreSQL güvenlik duvarları için bkz: [PostgreSQL sunucunun güvenlik duvarı kuralları için Azure veritabanı](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="7f733-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f733-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f733-107">Prerequisites</span></span>
<span data-ttu-id="7f733-108">Nasıl yapılır bu kılavuzu adım için gerekir:</span><span class="sxs-lookup"><span data-stu-id="7f733-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7f733-109">Bir [PostgreSQL sunucu ve veritabanı için Azure veritabanı](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7f733-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="7f733-110">Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya tarayıcıda Azure bulut Kabuğu'nu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f733-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="7f733-111">PostgreSQL için Azure veritabanı için güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7f733-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="7f733-112">[Az postgres sunucu güvenlik duvarı kuralı](/cli/azure/postgres/server/firewall-rule) komutlar, güvenlik duvarı kurallarını yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f733-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="7f733-113">Liste güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="7f733-113">List firewall rules</span></span> 
<span data-ttu-id="7f733-114">Var olan sunucu güvenlik duvarı kurallarında listelemek için Çalıştır [az postgres sunucu güvenlik duvarı kuralı listesi](/cli/azure/postgres/server/firewall-rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="7f733-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="7f733-115">Çıkış varsa JSON biçiminde varsayılan kuralları listeler.</span><span class="sxs-lookup"><span data-stu-id="7f733-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="7f733-116">Anahtar kullanabilir `--output table` çıktı olarak daha okunabilir bir tablo biçiminde için.</span><span class="sxs-lookup"><span data-stu-id="7f733-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="7f733-117">Güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f733-117">Create firewall rule</span></span>
<span data-ttu-id="7f733-118">Sunucu üzerinde yeni bir güvenlik duvarı kuralı oluşturmak için çalıştırın [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="7f733-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="7f733-119">Bu örnek sunucuya erişmek için tüm IP adres aralığını sağlayan **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="7f733-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="7f733-120">Erişim için tekil bir IP adresine izin vermek için bu örnekte olduğu gibi aynı adresi IP başlangıç ve bitiş IP olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7f733-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="7f733-121">Başarılı, komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="7f733-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="7f733-122">Bir hata olduğunda çıktı showserror ileti metni yerine.</span><span class="sxs-lookup"><span data-stu-id="7f733-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="7f733-123">Güncelleştirme güvenlik duvarı kuralı</span><span class="sxs-lookup"><span data-stu-id="7f733-123">Update firewall rule</span></span> 
<span data-ttu-id="7f733-124">Kullanarak sunucu üzerinde var olan bir güvenlik duvarı kuralı güncelleştirme [az postgres sunucu güvenlik duvarı kuralı güncelleştirme](/cli/azure/postgres/server/firewall-rule#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="7f733-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="7f733-125">Var olan güvenlik duvarı kuralı adı girişi ve başlangıç güncelleştirmek için IP ve bitiş IP öznitelikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f733-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="7f733-126">Başarılı, komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="7f733-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="7f733-127">Bir hata olduğunda çıktı showserror ileti metni yerine.</span><span class="sxs-lookup"><span data-stu-id="7f733-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="7f733-128">Güvenlik duvarı kuralı mevcut değilse güncelleştirme komutu tarafından oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="7f733-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="7f733-129">Güvenlik duvarı kuralı ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="7f733-129">Show firewall rule details</span></span>
<span data-ttu-id="7f733-130">Çalıştırarak kural ayrıntıları bir sunucu için mevcut Güvenlik Duvarı'nı gösterebilir [az postgres sunucu güvenlik duvarı kuralı Göster](/cli/azure/postgres/server/firewall-rule#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="7f733-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="7f733-131">Başarılı, komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="7f733-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="7f733-132">Bir hata olduğunda çıktı showserror ileti metni yerine.</span><span class="sxs-lookup"><span data-stu-id="7f733-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="7f733-133">Güvenlik duvarı kuralını siler</span><span class="sxs-lookup"><span data-stu-id="7f733-133">Delete firewall rule</span></span>
<span data-ttu-id="7f733-134">Bir IP aralığı sunucusundan erişimi iptal etmek için mevcut bir güvenlik duvarı kuralı yürüterek silmek [az postgres sunucu güvenlik duvarı kuralı silme](/cli/azure/postgres/server/firewall-rule#delete) komutu.</span><span class="sxs-lookup"><span data-stu-id="7f733-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="7f733-135">Var olan güvenlik duvarı kuralının adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7f733-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="7f733-136">Başarı hiçbir çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="7f733-136">Upon success, there is no output.</span></span> <span data-ttu-id="7f733-137">Başarısızlık durumunda, hata iletisi metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="7f733-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f733-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f733-138">Next steps</span></span>
- <span data-ttu-id="7f733-139">Benzer şekilde, bir web tarayıcısı kullanabilirsiniz [oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure Portalı'nı kullanarak yönetme](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7f733-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="7f733-140">Hakkında daha iyi anlamak [Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="7f733-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="7f733-141">PostgreSQL sunucu için bir Azure veritabanına bağlanma konusunda yardım için bkz: [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7f733-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
