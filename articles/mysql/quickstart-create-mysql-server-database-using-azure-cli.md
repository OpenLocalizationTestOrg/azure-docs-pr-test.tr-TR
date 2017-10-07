---
title: "Hızlı Başlangıç: MySQL için Azure Veritabanı sunucusu Oluşturma - Azure CLI | Microsoft Docs"
description: "Bu hızlı başlangıç nasıl toouse hello Azure CLI toocreate bir Azure kaynak grubu içindeki MySQL sunucusu için bir Azure veritabanı açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="71ade-103">Azure CLI aracını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71ade-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="71ade-104">Bu hızlı başlangıç nasıl toouse hello Azure CLI toocreate bir Azure kaynak grubu içindeki MySQL sunucusu için bir Azure veritabanı yaklaşık beş dakika içinde açıklar.</span><span class="sxs-lookup"><span data-stu-id="71ade-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="71ade-105">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="71ade-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="71ade-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71ade-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="71ade-107">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="71ade-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="71ade-108">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="71ade-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="71ade-109">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="71ade-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="71ade-110">Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="71ade-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="71ade-111">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="71ade-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="71ade-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71ade-112">Create a resource group</span></span>
<span data-ttu-id="71ade-113">Oluşturma bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) hello kullanarak [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="71ade-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="71ade-114">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="71ade-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="71ade-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myresourcegroup` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="71ade-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="71ade-116">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="71ade-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="71ade-117">MySQL sunucusu için bir Azure veritabanı ile Merhaba oluşturma **az mysql sunucusu oluşturun** komutu.</span><span class="sxs-lookup"><span data-stu-id="71ade-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="71ade-118">Bir sunucu birden çok veritabanını yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="71ade-118">A server can manage multiple databases.</span></span> <span data-ttu-id="71ade-119">Genellikle her proje veya kullanıcı için farklı bir veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71ade-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="71ade-120">Merhaba aşağıdaki örnek bir Azure veritabanı bulunan MySQL sunucusu için oluşturur `westus` hello kaynak grubunda `myresourcegroup` adla `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="71ade-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="71ade-121">Merhaba sunucu sahip bir yönetici oturumu adlı `myadmin` ve parola `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="71ade-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="71ade-122">Merhaba sunucusu ile oluşturulur **temel** performans katmanı ve **50** hello Server'daki tüm hello veritabanları arasında paylaşılan birimler işlem.</span><span class="sxs-lookup"><span data-stu-id="71ade-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="71ade-123">İşlem ve depolama yukarı veya aşağı hello uygulamanızın gereksinimlerine bağlı olarak ölçekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71ade-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="71ade-124">Güvenlik duvarı kuralını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71ade-124">Configure firewall rule</span></span>
<span data-ttu-id="71ade-125">Hello kullanarak MySQL sunucu düzeyinde güvenlik duvarı kuralı için bir Azure veritabanı oluştur **az mysql server güvenlik duvarı kuralı oluşturmak** komutu.</span><span class="sxs-lookup"><span data-stu-id="71ade-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="71ade-126">Sunucu düzeyinde güvenlik duvarı kuralı hello gibi bir dış uygulamaya verir **mysql.exe** komut satırı aracını veya MySQL çalışma ekranı tooconnect tooyour sunucu hello Azure MySQL hizmeti güvenlik duvarı üzerinden.</span><span class="sxs-lookup"><span data-stu-id="71ade-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="71ade-127">Merhaba aşağıdaki örnek, bu örnekte hello tüm olası IP adres aralığı olan önceden tanımlanmış adres aralığı için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71ade-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="71ade-128">SSL ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="71ade-128">Configure SSL settings</span></span>
<span data-ttu-id="71ade-129">Varsayılan olarak sunucunuz ile istemci uygulamaları arasında SSL bağlantıları zorunlu tutulur.</span><span class="sxs-lookup"><span data-stu-id="71ade-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="71ade-130">Bu "hareket halinde" güvenliğini sağlar hello Internet üzerinden hello veri akışı şifreleme verileri.</span><span class="sxs-lookup"><span data-stu-id="71ade-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="71ade-131">Bu hızlı başlangıç daha kolay toomake, biz SSL bağlantıları için sunucunuzu devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="71ade-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="71ade-132">Üretim sunucuları için bunu yapmanız önerilmez.</span><span class="sxs-lookup"><span data-stu-id="71ade-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="71ade-133">Daha fazla bilgi için bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="71ade-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="71ade-134">Merhaba aşağıdaki örnek, MySQL server zorunlu SSL devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="71ade-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="71ade-135">Merhaba bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="71ade-135">Get hello connection information</span></span>

<span data-ttu-id="71ade-136">tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="71ade-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="71ade-137">Merhaba, JSON biçiminde sonucudur.</span><span class="sxs-lookup"><span data-stu-id="71ade-137">hello result is in JSON format.</span></span> <span data-ttu-id="71ade-138">Merhaba Not **fullyQualifiedDomainName** ve **Admınıstratorlogın**.</span><span class="sxs-lookup"><span data-stu-id="71ade-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="71ade-139">Merhaba mysql.exe komut satırı aracını kullanarak toohello sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="71ade-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="71ade-140">Hello kullanarak tooyour sunucusuna **mysql.exe** komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="71ade-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="71ade-141">MySQL'i [buradan](https://dev.mysql.com/downloads/) indirerek bilgisayarınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71ade-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="71ade-142">Bunun yerine, ayrıca hello tıklatarak **deneyin** düğmesini kod örnekleri üzerinde veya hello `>_` hello üst sağ araç hello Azure portal ve başlatma hello düğmesinden **Azure bulut Kabuk**.</span><span class="sxs-lookup"><span data-stu-id="71ade-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="71ade-143">Merhaba sonraki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="71ade-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="71ade-144">Sunucu toohello kullanarak bağlan **mysql** komut satırı aracı:</span><span class="sxs-lookup"><span data-stu-id="71ade-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="71ade-145">Sunucu durumunu görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="71ade-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="71ade-146">Her şey yolunda giderse hello komut satırı aracı metin aşağıdaki hello çıkış:</span><span class="sxs-lookup"><span data-stu-id="71ade-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="71ade-147">Ek komutlar için bkz. [MySQL 5.7 Başvuru Kılavuzu - Bölüm 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="71ade-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="71ade-148">Merhaba MySQL çalışma ekranı GUI aracını kullanarak toohello sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="71ade-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="71ade-149">Merhaba, istemci bilgisayardaki MySQL çalışma ekranı uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="71ade-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="71ade-150">MySQL Workbench uygulamasını [buradan](https://dev.mysql.com/downloads/workbench/) indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71ade-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="71ade-151">Merhaba, **yeni bağlantı kurma** iletişim kutusunda, aşağıdaki bilgilerle hello girin **parametreleri** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="71ade-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![yeni bağlantı oluştur](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="71ade-153">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="71ade-153">**Setting**</span></span> | <span data-ttu-id="71ade-154">**Önerilen Değer**</span><span class="sxs-lookup"><span data-stu-id="71ade-154">**Suggested Value**</span></span> | <span data-ttu-id="71ade-155">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="71ade-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="71ade-156">Bağlantı Adı</span><span class="sxs-lookup"><span data-stu-id="71ade-156">Connection Name</span></span> | <span data-ttu-id="71ade-157">Bağlantım</span><span class="sxs-lookup"><span data-stu-id="71ade-157">My Connection</span></span> | <span data-ttu-id="71ade-158">Bu bağlantı için bir etiket belirtin (herhangi bir şey olabilir)</span><span class="sxs-lookup"><span data-stu-id="71ade-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="71ade-159">Bağlantı Yöntemi</span><span class="sxs-lookup"><span data-stu-id="71ade-159">Connection Method</span></span> | <span data-ttu-id="71ade-160">Standart (TCP/IP) seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="71ade-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="71ade-161">TCP/IP Protokolü tooconnect tooAzure veritabanı için MySQL kullanmak ></span><span class="sxs-lookup"><span data-stu-id="71ade-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="71ade-162">Ana Bilgisayar Adı</span><span class="sxs-lookup"><span data-stu-id="71ade-162">Hostname</span></span> | <span data-ttu-id="71ade-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="71ade-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="71ade-164">Daha önce not aldığınız sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="71ade-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="71ade-165">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="71ade-165">Port</span></span> | <span data-ttu-id="71ade-166">3306</span><span class="sxs-lookup"><span data-stu-id="71ade-166">3306</span></span> | <span data-ttu-id="71ade-167">MySQL için Hello varsayılan bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71ade-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="71ade-168">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="71ade-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="71ade-169">Merhaba Sunucu Yöneticisi oturum açma, daha önce not ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="71ade-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="71ade-170">Parola</span><span class="sxs-lookup"><span data-stu-id="71ade-170">Password</span></span> | **** | <span data-ttu-id="71ade-171">Daha önce yapılandırılmış hello yönetici hesabı parolasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="71ade-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="71ade-172">Tıklatın **Bağlantıyı Sına** tüm parametrelerin doğru yapılandırılmışsa tootest.</span><span class="sxs-lookup"><span data-stu-id="71ade-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="71ade-173">Artık, hello bağlantıyı tıklatabilir toosuccessfully toohello sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="71ade-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="71ade-174">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="71ade-174">Clean up resources</span></span>
<span data-ttu-id="71ade-175">Başka bir hızlı başlangıç/öğretici için bu kaynakları gerek duymuyorsanız, komutu aşağıdaki hello yaparak silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="71ade-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="71ade-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71ade-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71ade-177">Azure CLI ile bir MySQL Veritabanı tasarlama</span><span class="sxs-lookup"><span data-stu-id="71ade-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
