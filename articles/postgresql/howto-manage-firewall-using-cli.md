---
title: "aaaCreate ve PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak Azure veritabanını yönetme | Microsoft Docs"
description: "Bu makalede nasıl toocreate ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI komut satırını kullanarak yönetebilirsiniz."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="79bfe-103">Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="79bfe-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="79bfe-104">Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler toomanage erişim tooan Azure veritabanı PostgreSQL sunucu için belirli bir IP adresi veya IP adresleri aralığını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="79bfe-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="79bfe-105">Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silme, liste ve sunucunuzun güvenlik duvarı kuralları toomanage göster.</span><span class="sxs-lookup"><span data-stu-id="79bfe-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="79bfe-106">Genel Bakış Azure veritabanı için PostgreSQL güvenlik duvarları için bkz: [PostgreSQL sunucunun güvenlik duvarı kuralları için Azure veritabanı](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="79bfe-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79bfe-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79bfe-107">Prerequisites</span></span>
<span data-ttu-id="79bfe-108">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="79bfe-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="79bfe-109">Bir [PostgreSQL sunucu ve veritabanı için Azure veritabanı](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="79bfe-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="79bfe-110">Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="79bfe-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="79bfe-111">PostgreSQL için Azure veritabanı için güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="79bfe-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="79bfe-112">Merhaba [az postgres sunucu güvenlik duvarı kuralı](/cli/azure/postgres/server/firewall-rule) kullanılan tooconfigure güvenlik duvarı kuralları komutlardır.</span><span class="sxs-lookup"><span data-stu-id="79bfe-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="79bfe-113">Liste güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="79bfe-113">List firewall rules</span></span> 
<span data-ttu-id="79bfe-114">Merhaba toolist varolan hello çalıştırmak hello sunucuda Sunucu güvenlik duvarı kuralları [az postgres sunucu güvenlik duvarı kuralı listesi](/cli/azure/postgres/server/firewall-rule#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="79bfe-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="79bfe-115">varsa, varsayılan değer JSON olarak biçimlendirmek istiyorsanız hello çıktı hello kuralları listeler.</span><span class="sxs-lookup"><span data-stu-id="79bfe-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="79bfe-116">Merhaba anahtar kullanabilir `--output table` daha okunabilir bir tablo biçiminde hello çıktı olarak için.</span><span class="sxs-lookup"><span data-stu-id="79bfe-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="79bfe-117">Güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="79bfe-117">Create firewall rule</span></span>
<span data-ttu-id="79bfe-118">toocreate hello çalıştırmak hello sunucuda yeni bir güvenlik duvarı kuralı [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="79bfe-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="79bfe-119">Bu örnekte tüm IP adresleri tooaccess hello server çeşitli verir **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="79bfe-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="79bfe-120">tooallow tekil bir IP adresi tooaccess sağlamak IP başlangıç ve bitiş IP, bu örnekteki hello gibi hello aynı adres.</span><span class="sxs-lookup"><span data-stu-id="79bfe-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="79bfe-121">Başarı hello komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="79bfe-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="79bfe-122">Bir hata olduğunda hello showserror ileti metni yerine çıktı.</span><span class="sxs-lookup"><span data-stu-id="79bfe-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="79bfe-123">Güncelleştirme güvenlik duvarı kuralı</span><span class="sxs-lookup"><span data-stu-id="79bfe-123">Update firewall rule</span></span> 
<span data-ttu-id="79bfe-124">Hello kullanarak sunucu üzerinde var olan bir güvenlik duvarı kuralı güncelleştirme [az postgres sunucu güvenlik duvarı kuralı güncelleştirme](/cli/azure/postgres/server/firewall-rule#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="79bfe-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="79bfe-125">Merhaba mevcut güvenlik duvarı kuralı giriş ve hello başlangıç IP ve bitiş IP öznitelikleri tooupdate olarak Hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="79bfe-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="79bfe-126">Başarı hello komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="79bfe-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="79bfe-127">Bir hata olduğunda hello showserror ileti metni yerine çıktı.</span><span class="sxs-lookup"><span data-stu-id="79bfe-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="79bfe-128">Merhaba güvenlik duvarı kuralı mevcut değilse hello güncelleştirme komutu tarafından oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="79bfe-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="79bfe-129">Güvenlik duvarı kuralı ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="79bfe-129">Show firewall rule details</span></span>
<span data-ttu-id="79bfe-130">Çalıştırarak bir sunucu için kural ayrıntılarını hello mevcut güvenlik duvarı gösterebilir [az postgres sunucu güvenlik duvarı kuralı Göster](/cli/azure/postgres/server/firewall-rule#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="79bfe-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="79bfe-131">Başarı hello komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="79bfe-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="79bfe-132">Bir hata olduğunda hello showserror ileti metni yerine çıktı.</span><span class="sxs-lookup"><span data-stu-id="79bfe-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="79bfe-133">Güvenlik duvarı kuralını siler</span><span class="sxs-lookup"><span data-stu-id="79bfe-133">Delete firewall rule</span></span>
<span data-ttu-id="79bfe-134">toorevoke erişim hello sunucusundan bir IP aralığı için hello yürüterek mevcut bir güvenlik duvarı kuralını silme [az postgres sunucu güvenlik duvarı kuralı silme](/cli/azure/postgres/server/firewall-rule#delete) komutu.</span><span class="sxs-lookup"><span data-stu-id="79bfe-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="79bfe-135">Merhaba mevcut güvenlik duvarı kuralı Hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="79bfe-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="79bfe-136">Başarı hiçbir çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="79bfe-136">Upon success, there is no output.</span></span> <span data-ttu-id="79bfe-137">Başarısızlık durumunda, hello hata iletisi metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="79bfe-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79bfe-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79bfe-138">Next steps</span></span>
- <span data-ttu-id="79bfe-139">Benzer şekilde, bir web tarayıcısı çok kullanabileceğiniz[oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="79bfe-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="79bfe-140">Hakkında daha iyi anlamak [Azure veritabanı PostgreSQL sunucunun güvenlik duvarı kuralları için](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="79bfe-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="79bfe-141">Tooan Azure veritabanı PostgreSQL sunucusu bağlanma konusunda yardım için bkz [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="79bfe-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
