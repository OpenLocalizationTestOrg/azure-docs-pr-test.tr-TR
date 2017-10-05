---
title: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme | Microsoft Docs"
description: "Bu makalede, oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI komut satırını kullanarak yönetme açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="752a9-103">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="752a9-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="752a9-104">Azure veritabanı için MySQL sunucusu için belirli bir IP adresi veya IP adresi aralığı erişimi yönetmek üzere yöneticiler sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="752a9-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="752a9-105">Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silin, listeleyin ve sunucunuzu yönetmek için güvenlik duvarı kuralları gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a9-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="752a9-106">Genel Bakış Azure veritabanı için MySQL güvenlik duvarları için bkz: [Azure veritabanı için MySQL server güvenlik duvarı kuralları](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="752a9-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="752a9-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="752a9-107">Prerequisites</span></span>
* [<span data-ttu-id="752a9-108">Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="752a9-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="752a9-109">PostgreSQL ve MySQL Hizmetleri için Azure Python SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="752a9-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="752a9-110">Azure CLI bileşeni PostgreSQL ve MySQL hizmeti yükleyin</span><span class="sxs-lookup"><span data-stu-id="752a9-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="752a9-111">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="752a9-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="752a9-112">Güvenlik duvarı kuralı komutlar:</span><span class="sxs-lookup"><span data-stu-id="752a9-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="752a9-113">**Az mysql server güvenlik duvarı kuralı** komut oluşturma, silme, liste, Göster ve güvenlik duvarı kurallarını güncelleştir için Azure CLI üzerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="752a9-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="752a9-114">Komutlar:</span><span class="sxs-lookup"><span data-stu-id="752a9-114">Commands:</span></span>
- <span data-ttu-id="752a9-115">**oluşturma**: bir Azure MySQL server güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="752a9-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="752a9-116">**silme**: Azure MySQL server güvenlik duvarı kuralını siler.</span><span class="sxs-lookup"><span data-stu-id="752a9-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="752a9-117">**Liste** : Azure MySQL server güvenlik duvarı kuralları listesi.</span><span class="sxs-lookup"><span data-stu-id="752a9-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="752a9-118">**Göster** : güvenlik duvarı kuralı Azure MySQL server ayrıntılarını gösterin.</span><span class="sxs-lookup"><span data-stu-id="752a9-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="752a9-119">**Güncelleştirme**: bir Azure MySQL server güvenlik duvarı kuralı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="752a9-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="752a9-120">Azure ve listesine Azure veritabanınızı MySQL sunucuları için oturum açma</span><span class="sxs-lookup"><span data-stu-id="752a9-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="752a9-121">Güvenli bir şekilde Azure CLI ile Azure hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="752a9-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="752a9-122">Kullanım **az oturum açma** Bunu yapmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="752a9-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="752a9-123">Komut satırından aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="752a9-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="752a9-124">Bu komutun çıkışı, sonraki adımda kullanılacak bir kod olacaktır.</span><span class="sxs-lookup"><span data-stu-id="752a9-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="752a9-125">Web tarayıcısı kullanarak [https://aka.ms/devicelogin](https://aka.ms/devicelogin) adresine gidin ve kodu girin.</span><span class="sxs-lookup"><span data-stu-id="752a9-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="752a9-126">İstendiğinde, Azure kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="752a9-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="752a9-127">Oturumunuzla yetkilendirildikten sonra konsolda Aboneliklerin listesini basılır.</span><span class="sxs-lookup"><span data-stu-id="752a9-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="752a9-128">İleri taşıma kullanılacak şu anki aboneliği ayarlamak için istenen abonelik kimliğini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="752a9-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="752a9-129">Adlarını değilseniz MySQL sunucuları abonelik ve kaynak grubunuz için Azure veritabanlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="752a9-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="752a9-130">Üzerinde çalışmak için MySQL sunucuyu belirtmek için kullanılan listenin adı özniteliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="752a9-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="752a9-131">Gerekirse, adının doğru olduğunu doğrulamak için name özniteliği kullanarak bu sunucu için ayrıntıları onaylayın:</span><span class="sxs-lookup"><span data-stu-id="752a9-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="752a9-132">MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralları listesi</span><span class="sxs-lookup"><span data-stu-id="752a9-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="752a9-133">Sunucu adı ve kaynak grubu adı kullanarak, sunucu üzerinde var olan sunucunun güvenlik duvarı kuralları listesi.</span><span class="sxs-lookup"><span data-stu-id="752a9-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="752a9-134">Sunucu adı özniteliği belirtilen bildirimi **--sunucu** geçiş ve **--adı** geçin.</span><span class="sxs-lookup"><span data-stu-id="752a9-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="752a9-135">Çıktı varsa JSON biçiminde varsayılan kuralları listeler.</span><span class="sxs-lookup"><span data-stu-id="752a9-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="752a9-136">Anahtar kullanabilir **--çıktı tablosu** çıktı olarak daha okunabilir bir tablo biçiminde için.</span><span class="sxs-lookup"><span data-stu-id="752a9-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="752a9-137">Güvenlik duvarı kuralı Azure veritabanı için MySQL sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="752a9-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="752a9-138">Azure MySQL sunucu adını ve kaynak grubu adı kullanarak, sunucu üzerinde yeni bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="752a9-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="752a9-139">Kural, başlangıç IP ve bir IP adresi aralığı kapsayacak şekilde bitiş IP kuralı için erişimine izin vermek için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="752a9-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="752a9-140">Erişim izin verilmesi tekil için bir IP adresi, bu örnekte olduğu gibi IP başlangıç ve bitiş IP aynı adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="752a9-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="752a9-141">Başarılı, komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="752a9-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="752a9-142">Çıkış hatası varsa, hata iletisi metni yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a9-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="752a9-143">MySQL sunucusu için Azure veritabanı güncelleştirme güvenlik duvarı kuralı</span><span class="sxs-lookup"><span data-stu-id="752a9-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="752a9-144">Azure MySQL sunucu adı ve kaynak grubu adı kullanarak, sunucuda mevcut bir güvenlik duvarı kuralı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="752a9-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="752a9-145">Var olan güvenlik duvarı kuralı adı girişi ve başlangıç güncelleştirmek için IP ve bitiş IP öznitelikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="752a9-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="752a9-146">Başarılı, komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="752a9-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="752a9-147">Çıkış hatası varsa, hata iletisi metni yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a9-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="752a9-148">Güvenlik duvarı kuralı mevcut değilse güncelleştirme komutu tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="752a9-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="752a9-149">MySQL sunucusu için Azure veritabanında güvenlik duvarı kuralı ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="752a9-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="752a9-150">Azure MySQL sunucu adını ve kaynak grubu adı kullanarak, var olan Güvenlik Duvarı'nı sunucudan kural ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a9-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="752a9-151">Var olan güvenlik duvarı kuralının adını girdi olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="752a9-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="752a9-152">Başarılı, komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz güvenlik duvarı kuralı ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="752a9-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="752a9-153">Çıkış hatası varsa, hata iletisi metni yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="752a9-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="752a9-154">MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralını siler</span><span class="sxs-lookup"><span data-stu-id="752a9-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="752a9-155">Azure MySQL sunucu adı ve kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı sunucudan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="752a9-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="752a9-156">Var olan güvenlik duvarı kuralının adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="752a9-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="752a9-157">Başarı hiçbir çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="752a9-157">Upon success, there is no output.</span></span> <span data-ttu-id="752a9-158">Başarısızlık durumunda, hata iletisi metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="752a9-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="752a9-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="752a9-159">Next steps</span></span>
- <span data-ttu-id="752a9-160">Hakkında daha iyi anlamak [Azure veritabanı için MySQL Server güvenlik duvarı kuralları](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="752a9-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="752a9-161">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure Portalı'nı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="752a9-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
