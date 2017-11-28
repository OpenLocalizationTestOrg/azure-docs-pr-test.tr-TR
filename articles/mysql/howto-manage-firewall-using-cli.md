---
title: "aaaCreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme | Microsoft Docs"
description: "Bu makalede nasıl toocreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI komut satırını kullanarak yönetebilirsiniz."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="4864c-103">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure CLI kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="4864c-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="4864c-104">MySQL sunucusu için belirli bir IP adresi veya IP adresi aralığı Yöneticiler toomanage erişim tooan Azure veritabanı sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4864c-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="4864c-105">Uygun Azure CLI komutları kullanarak, oluşturabilir, güncelleştirme, silme, liste ve sunucunuzun güvenlik duvarı kuralları toomanage göster.</span><span class="sxs-lookup"><span data-stu-id="4864c-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="4864c-106">Genel Bakış Azure veritabanı için MySQL güvenlik duvarları için bkz: [Azure veritabanı için MySQL server güvenlik duvarı kuralları](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4864c-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4864c-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4864c-107">Prerequisites</span></span>
* [<span data-ttu-id="4864c-108">Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="4864c-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="4864c-109">PostgreSQL ve MySQL Hizmetleri için Azure Python SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="4864c-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="4864c-110">Hello Azure CLI bileşeni PostgreSQL ve MySQL hizmeti yükleyin</span><span class="sxs-lookup"><span data-stu-id="4864c-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="4864c-111">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4864c-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="4864c-112">Güvenlik duvarı kuralı komutlar:</span><span class="sxs-lookup"><span data-stu-id="4864c-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="4864c-113">Merhaba **az mysql server güvenlik duvarı kuralı** komutu, Azure CLI toocreate kullanıldığında, silme, listesinde, Göster ve güvenlik duvarı kurallarını güncelleştir.</span><span class="sxs-lookup"><span data-stu-id="4864c-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="4864c-114">Komutlar:</span><span class="sxs-lookup"><span data-stu-id="4864c-114">Commands:</span></span>
- <span data-ttu-id="4864c-115">**oluşturma**: bir Azure MySQL server güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4864c-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4864c-116">**silme**: Azure MySQL server güvenlik duvarı kuralını siler.</span><span class="sxs-lookup"><span data-stu-id="4864c-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4864c-117">**Liste** : hello Azure MySQL server güvenlik duvarı kuralları listesi.</span><span class="sxs-lookup"><span data-stu-id="4864c-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="4864c-118">**Göster** : güvenlik duvarı kuralı Azure MySQL server hello ayrıntılarını gösterin.</span><span class="sxs-lookup"><span data-stu-id="4864c-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4864c-119">**Güncelleştirme**: bir Azure MySQL server güvenlik duvarı kuralı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4864c-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="4864c-120">Oturum açma tooAzure ve MySQL sunucuları için Azure veritabanınızı listesi</span><span class="sxs-lookup"><span data-stu-id="4864c-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="4864c-121">Güvenli bir şekilde Azure CLI ile Azure hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="4864c-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="4864c-122">Kullanım hello **az oturum açma** toodo bu komutu.</span><span class="sxs-lookup"><span data-stu-id="4864c-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="4864c-123">Komut hello komut satırından aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4864c-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="4864c-124">Bu komut, bir kod toouse hello sonraki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="4864c-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="4864c-125">Bir web tarayıcısı tooopen hello sayfası kullanmak [https://aka.ms/devicelogin](https://aka.ms/devicelogin) ve hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="4864c-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="4864c-126">Merhaba isteminde Azure kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4864c-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="4864c-127">Oturumunuzla yetkilendirildikten sonra Aboneliklerin listesini hello konsolunda basılır.</span><span class="sxs-lookup"><span data-stu-id="4864c-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="4864c-128">İlerleyen kullanılan istenen hello abonelik tooset hello geçerli abonelik toobe Hello kimliğini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="4864c-129">Merhaba adlarını değilseniz hello Azure veritabanları MySQL sunucuları abonelik ve kaynak grubunuz için listeleyin.</span><span class="sxs-lookup"><span data-stu-id="4864c-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="4864c-130">Kullanılan toospecify olacağı hello adı özniteliği listeleme hello hangi MySQL server toowork unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="4864c-131">Bu sunucu toousing hello adı özniteliği tooconfirm adının doğru olduğundan için gerekirse, hello ayrıntılarınızı doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="4864c-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="4864c-132">MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralları listesi</span><span class="sxs-lookup"><span data-stu-id="4864c-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="4864c-133">Hello sunucu adını ve hello kaynak grubu adı, liste hello var olan sunucu güvenlik duvarı kuralları hello sunucuda kullanma.</span><span class="sxs-lookup"><span data-stu-id="4864c-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="4864c-134">Bu hello sunucu adı özniteliği hello belirtilen dikkat edin **--server** geçin ve değil hello **--ad** geçin.</span><span class="sxs-lookup"><span data-stu-id="4864c-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="4864c-135">varsa, varsayılan değer JSON olarak biçimlendirmek istiyorsanız hello çıktı hello kuralları listeler.</span><span class="sxs-lookup"><span data-stu-id="4864c-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="4864c-136">Merhaba anahtar kullanabilir **--çıktı tablosu** daha okunabilir bir tablo biçiminde hello çıktı olarak için.</span><span class="sxs-lookup"><span data-stu-id="4864c-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4864c-137">Güvenlik duvarı kuralı Azure veritabanı için MySQL sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4864c-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4864c-138">Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, hello sunucusunda yeni bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4864c-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="4864c-139">Merhaba kural toocover bir dizi IP adreslerini tooallow erişim hello kuralı, hello başlangıç IP ve bitiş IP için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="4864c-140">Erişime izin toobe için tekil bir IP adresi, sağlayın IP başlangıç ve bitiş IP, bu örnekteki hello gibi hello aynı adres.</span><span class="sxs-lookup"><span data-stu-id="4864c-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="4864c-141">Başarı hello komut çıktısı JSON biçiminde varsayılan olarak, oluşturmuş olduğunuz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="4864c-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="4864c-142">Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="4864c-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4864c-143">MySQL sunucusu için Azure veritabanı güncelleştirme güvenlik duvarı kuralı</span><span class="sxs-lookup"><span data-stu-id="4864c-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="4864c-144">Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı hello sunucuda güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4864c-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="4864c-145">Merhaba mevcut güvenlik duvarı kuralı giriş ve hello başlangıç IP ve bitiş IP öznitelikleri tooupdate olarak Hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="4864c-146">Başarı hello komut çıktısı varsayılan olarak JSON biçiminde güncelleştirdiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="4864c-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="4864c-147">Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="4864c-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="4864c-148">Merhaba güvenlik duvarı kuralı mevcut değilse hello güncelleştirme komutu tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4864c-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="4864c-149">MySQL sunucusu için Azure veritabanında güvenlik duvarı kuralı ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="4864c-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4864c-150">Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, hello mevcut güvenlik duvarı kuralı bilgileri hello sunucusundan gösterir.</span><span class="sxs-lookup"><span data-stu-id="4864c-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="4864c-151">Merhaba mevcut güvenlik duvarı kuralı Hello adını girdi olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4864c-152">Başarı hello komut çıktısı JSON biçiminde varsayılan olarak belirttiğiniz hello güvenlik duvarı kuralı hello ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="4864c-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="4864c-153">Merhaba çıkış hatası varsa, hata iletisi metni bunun yerine gösterir.</span><span class="sxs-lookup"><span data-stu-id="4864c-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4864c-154">MySQL sunucusu için Azure veritabanı üzerinde güvenlik duvarı kuralını siler</span><span class="sxs-lookup"><span data-stu-id="4864c-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4864c-155">Hello Azure MySQL sunucu adı ve hello kaynak grubu adı kullanarak, mevcut bir güvenlik duvarı kuralı hello sunucudan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4864c-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="4864c-156">Merhaba mevcut güvenlik duvarı kuralı Hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4864c-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4864c-157">Başarı hiçbir çıktısı yok.</span><span class="sxs-lookup"><span data-stu-id="4864c-157">Upon success, there is no output.</span></span> <span data-ttu-id="4864c-158">Başarısızlık durumunda, hello hata iletisi metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4864c-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4864c-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4864c-159">Next steps</span></span>
- <span data-ttu-id="4864c-160">Hakkında daha iyi anlamak [Azure veritabanı için MySQL Server güvenlik duvarı kuralları](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4864c-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="4864c-161">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="4864c-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
