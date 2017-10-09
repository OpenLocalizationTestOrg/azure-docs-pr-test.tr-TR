---
title: "aaaBuild Azure içinde Java ve MySQL bir web uygulaması"
description: "Bilgi nasıl tooget bir Java uygulaması bağlanan Azure uygulama hizmeti çalışan toohello Azure MySQL veritabanı hizmeti."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="bb433-103">Azure'da Java ve MySQL bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="bb433-104">Bu öğretici nasıl toocreate bir Java web uygulaması Azure ve tooa MySQL veritabanına bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb433-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="bb433-105">İşiniz bittiğinde, olacaktır bir [yay önyükleme](https://projects.spring.io/spring-boot/) veri depolarken uygulama [Azure veritabanı için MySQL](https://docs.microsoft.com/azure/mysql/overview) üzerinde çalışan [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="bb433-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Azure uygulama hizmeti çalışan Java uygulaması](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="bb433-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="bb433-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb433-108">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="bb433-109">Örnek uygulama toohello veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="bb433-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="bb433-110">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="bb433-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bb433-111">Güncelleştirme ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="bb433-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="bb433-112">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="bb433-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="bb433-113">Hello Azure portal'ın Hello uygulamayı izleme</span><span class="sxs-lookup"><span data-stu-id="bb433-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bb433-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bb433-114">Prerequisites</span></span>

1. [<span data-ttu-id="bb433-115">Git yükleyip</span><span class="sxs-lookup"><span data-stu-id="bb433-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="bb433-116">Merhaba Java 7 JDK yükleyip veya üstü</span><span class="sxs-lookup"><span data-stu-id="bb433-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="bb433-117">İndirme, yükleme ve MySQL Başlat</span><span class="sxs-lookup"><span data-stu-id="bb433-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb433-118">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bb433-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb433-119">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="bb433-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bb433-120">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb433-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="bb433-121">Yerel MySQL hazırlama</span><span class="sxs-lookup"><span data-stu-id="bb433-121">Prepare local MySQL</span></span> 

<span data-ttu-id="bb433-122">Bu adımda, bir veritabanı kullanmak için yerel bir MySQL Server test hello uygulamada yerel olarak makinenizde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb433-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="bb433-123">TooMySQL sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="bb433-123">Connect tooMySQL server</span></span>

<span data-ttu-id="bb433-124">Bir terminal penceresi tooyour yerel MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bb433-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="bb433-125">Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb433-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="bb433-126">İçin bir parola istenirse Merhaba hello parolayı girin `root` hesabı.</span><span class="sxs-lookup"><span data-stu-id="bb433-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="bb433-127">Kök hesap parolanızı hatırlamıyorsanız bkz [MySQL: nasıl tooReset hello kök parola](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="bb433-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="bb433-128">Komutunuzu başarıyla çalışırsa, MySQL sunucunuzu zaten çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="bb433-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="bb433-129">Aksi takdirde, yerel MySQL sunucunuz tarafından aşağıdaki hello başlatıldığından emin olun [MySQL yükleme sonrası adımları](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="bb433-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="bb433-130">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-130">Create a database</span></span> 

<span data-ttu-id="bb433-131">Merhaba, `mysql` isteminde, bir veritabanı ve tablo hello için yapılacaklar öğelerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb433-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="bb433-132">Sunucu bağlantısı yazarak çıkmak `quit`.</span><span class="sxs-lookup"><span data-stu-id="bb433-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="bb433-133">Oluşturma ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bb433-133">Create and run hello sample app</span></span> 

<span data-ttu-id="bb433-134">Bu adımda, örnek yay önyükleme uygulama kopyalama, toouse hello yerel MySQL veritabanını yapılandırın ve bilgisayarınızda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bb433-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="bb433-135">Kopya hello örnek</span><span class="sxs-lookup"><span data-stu-id="bb433-135">Clone hello sample</span></span>

<span data-ttu-id="bb433-136">Merhaba terminal penceresinde dizin ve kopya hello örnek depo çalışma tooa gidin.</span><span class="sxs-lookup"><span data-stu-id="bb433-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="bb433-137">Merhaba uygulama toouse hello MySQL veritabanını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bb433-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="bb433-138">Güncelleştirme hello `spring.datasource.password` ve değer *spring-boot-mysql-todo/src/main/resources/application.properties* hello ile aynı kök parola tooopen hello MySQL istemi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="bb433-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="bb433-139">Derleme ve hello örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bb433-139">Build and run hello sample</span></span>

<span data-ttu-id="bb433-140">Derleme ve hello bağlantıların bulunması dahil hello Maven sarmalayıcı kullanarak hello örnek çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bb433-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="bb433-141">Tarayıcı toohttp://localhost:8080 toosee eylemin hello örneği açın.</span><span class="sxs-lookup"><span data-stu-id="bb433-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="bb433-142">Görevleri toohello listesinde eklediğinizde, aşağıdaki SQL komut istemi tooview hello veri MySQL içinde depolanan hello MySQL komutları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="bb433-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="bb433-143">Devreyi tarafından Hello uygulamayı durdurun `Ctrl` + `C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="bb433-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="bb433-144">Bir Azure MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="bb433-145">Bu adımda, oluşturduğunuz bir [Azure veritabanı için MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) hello kullanarak örneğini [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb433-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="bb433-146">Hello örnek uygulama toouse bu veritabanını daha sonra hello öğreticide yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bb433-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="bb433-147">Bir terminal penceresi toocreate hello kaynakları kullanım hello Azure CLI 2.0 toohost Java uygulamanızı Azure uygulama hizmeti gerekli.</span><span class="sxs-lookup"><span data-stu-id="bb433-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="bb433-148">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="bb433-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="bb433-149">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-149">Create a resource group</span></span>

<span data-ttu-id="bb433-150">Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello ile [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bb433-151">Bir Azure kaynak grubu web uygulamaları, veritabanları ve depolama hesapları gibi ilgili kaynaklar burada dağıtılan ve yönetilen mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="bb433-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="bb433-152">Merhaba aşağıdaki örnekte bir kaynak grubu hello Kuzey Avrupa bölgede oluşturur:</span><span class="sxs-lookup"><span data-stu-id="bb433-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="bb433-153">toosee hello olası değerler için kullanabileceğiniz `--location`, hello kullan [az appservice listesi-konumları](/cli/azure/appservice#list-locations) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="bb433-154">MySQL sunucusu oluşturun</span><span class="sxs-lookup"><span data-stu-id="bb433-154">Create a MySQL server</span></span>

<span data-ttu-id="bb433-155">Bir sunucu Azure veritabanı'nda MySQL (Önizleme) ile Merhaba oluşturmak [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="bb433-156">Merhaba gördüğünüz kendi benzersiz MySQL sunucu adı yerine `<mysql_server_name>` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="bb433-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="bb433-157">Bu ad, MySQL sunucunuzun ana bilgisayar adı, bir parçasıdır `<mysql_server_name>.mysql.database.azure.com`, toobe genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb433-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="bb433-158">Ayrıca yerine `<admin_user>` ve `<admin_password>` kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="bb433-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="bb433-159">Merhaba MySQL server oluşturulduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="bb433-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="bb433-160">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bb433-160">Configure server firewall</span></span>

<span data-ttu-id="bb433-161">Bağlantılar için MySQL server tooallow istemcinizi hello kullanarak bir güvenlik duvarı kuralı oluşturun [az mysql server güvenlik duvarı kuralı oluşturmak](/cli/azure/mysql/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="bb433-162">Azure veritabanı için MySQL (Önizleme) Azure Hizmetleri bağlantılarından şu anda otomatik olarak etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="bb433-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="bb433-163">Dinamik olarak atanmış IP adresleri Azure gibi tüm IP adresleri için daha iyi tooenable olan şimdi.</span><span class="sxs-lookup"><span data-stu-id="bb433-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="bb433-164">Merhaba hizmet önizlemesini devam ettikçe, veritabanınızın güvenliğini sağlamak için daha iyi yöntemleri etkinleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="bb433-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="bb433-165">Hello Azure MySQL veritabanını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bb433-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="bb433-166">Merhaba terminal penceresinde, bilgisayarınızda, azure'da toohello MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bb433-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="bb433-167">Daha önce için belirttiğiniz başlangıç değeri kullanın `<admin_user>` ve `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="bb433-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="bb433-168">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-168">Create a database</span></span> 

<span data-ttu-id="bb433-169">Merhaba, `mysql` isteminde, bir veritabanı ve tablo hello için yapılacaklar öğelerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb433-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="bb433-170">İzinleri olan bir kullanıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="bb433-170">Create a user with permissions</span></span>

<span data-ttu-id="bb433-171">Bir veritabanı kullanıcısı oluşturmak ve hello tüm ayrıcalıkları vermek `tododb` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="bb433-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="bb433-172">Merhaba yer tutucuları değiştirmek `<Javaapp_user>` ve `<Javaapp_password>` kendi benzersiz uygulama adıyla.</span><span class="sxs-lookup"><span data-stu-id="bb433-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="bb433-173">Sunucu bağlantısı yazarak çıkmak `quit`.</span><span class="sxs-lookup"><span data-stu-id="bb433-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="bb433-174">Merhaba örnek tooAzure uygulama hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="bb433-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="bb433-175">Merhaba ile bir Azure uygulama hizmeti planı oluştur **serbest** fiyatlandırma katmanı hello kullanarak [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="bb433-176">Merhaba uygulama hizmeti planı hello kullanılan fiziksel kaynakları toohost uygulamalarınızı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bb433-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="bb433-177">Tooan uygulama hizmeti planı atanan tüm uygulamaların birden fazla uygulama barındırdığında toosave maliyet izin vererek, bu kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="bb433-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="bb433-178">Hello planı hazır olduğunda, Azure CLI benzer gösterir hello aşağıdaki örneğine toohello çıktı:</span><span class="sxs-lookup"><span data-stu-id="bb433-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="bb433-179">Bir Azure Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-179">Create an Azure Web app</span></span>

 <span data-ttu-id="bb433-180">Kullanım hello [az webapp oluşturma](/cli/azure/appservice/web#create) CLI komutu toocreate bir web uygulaması tanımı'nda hello `myAppServicePlan` uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="bb433-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="bb433-181">Merhaba web uygulaması tanımı URL tooaccess uygulamanızla sağlar ve çeşitli seçenekler toodeploy kod tooAzure yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bb433-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="bb433-182">Yedek hello `<app_name>` kendi benzersiz uygulama adıyla yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="bb433-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="bb433-183">Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="bb433-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="bb433-184">Tooyour kullanıcılar kullanıma önce bir özel etki alanı adı girişi toohello web uygulaması eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb433-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="bb433-185">Merhaba web uygulaması tanımı hazır olduğunda, aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:</span><span class="sxs-lookup"><span data-stu-id="bb433-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="bb433-186">Java yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bb433-186">Configure Java</span></span> 

<span data-ttu-id="bb433-187">Uygulamanızın ile Merhaba gerektiğini hello Java Çalışma zamanı yapılandırma ayarlama [az appservice web yapılandırma güncelleştirmesi](/cli/azure/appservice/web/config#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="bb433-188">Merhaba aşağıdaki komutu hello web uygulama toorun üzerinde yeni bir Java 8 JDK yapılandırır ve [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="bb433-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="bb433-189">Merhaba uygulama toouse hello Azure SQL veritabanını Yapılandır</span><span class="sxs-lookup"><span data-stu-id="bb433-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="bb433-190">Merhaba örnek uygulamayı çalıştırmadan önce uygulama ayarları hello web uygulama toouse hello Azure MySQL veritabanı Azure içinde oluşturulan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bb433-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="bb433-191">Bu özellikler ortam değişkenleri olarak sunulan toohello web uygulaması ve hello application.properties hello paketlenmiş web app içinde kümesindeki hello değerlerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="bb433-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="bb433-192">Uygulama ayarlarını kullanarak [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI içinde:</span><span class="sxs-lookup"><span data-stu-id="bb433-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="bb433-193">FTP dağıtımı kimlik bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="bb433-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="bb433-194">Uygulama tooAzure appservice FTP, yerel Git, GitHub, Visual Studio Team Services ve BitBucket dahil olmak üzere çeşitli yollarla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb433-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="bb433-195">Bu örneğin, FTP toodeploy hello. WAR dosyası daha önce yerel makine tooAzure uygulama hizmeti oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="bb433-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="bb433-196">toodetermine ne kimlik bilgileri bir ftp komutu toohello Web uygulaması, kullanım içinde boyunca toopass [az appservice web dağıtım listesi-yayımlama-profilleri](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) komutu:</span><span class="sxs-lookup"><span data-stu-id="bb433-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="bb433-197">FTP kullanarak hello uygulamayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="bb433-197">Upload hello app using FTP</span></span>

<span data-ttu-id="bb433-198">Sık kullandığınız FTP aracı toodeploy hello kullanın. WAR dosyası toohello */site/wwwroot/webapps* hello alınan hello sunucu adresi klasöründe `URL` alanındaki hello önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="bb433-199">Merhaba var olan varsayılan (kök) uygulama dizini kaldırın ve ROOT.war ile Merhaba varolan hello değiştirin. WAR dosyası Hello hello öğreticide daha önce oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="bb433-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="bb433-200">Test hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="bb433-200">Test hello web app</span></span>

<span data-ttu-id="bb433-201">Çok Gözat`http://<app_name>.azurewebsites.net/` ve birkaç görevleri toohello listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb433-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Azure uygulama hizmeti çalışan Java uygulaması](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="bb433-203">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="bb433-203">**Congratulations!**</span></span> <span data-ttu-id="bb433-204">Azure App Service'te bir veri güdümlü Java uygulaması kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="bb433-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="bb433-205">Güncelleştirme hello uygulama ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="bb433-205">Update hello app and redeploy</span></span>

<span data-ttu-id="bb433-206">Merhaba uygulama tooinclude hello Yapılacaklar listesinde hangi gün hello öğesinin oluşturulduğu için ek bir sütun güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb433-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="bb433-207">Yay önyükleme güncelleştirme hello veritabanı şeması hello veri modeli değişikliklerini, var olan veritabanı kayıtlarını değiştirmeden işler.</span><span class="sxs-lookup"><span data-stu-id="bb433-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="bb433-208">Yerel sisteminizde açık *src/main/java/com/example/fabrikam/TodoItem.java* ve hello aşağıdaki alır toohello sınıfı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bb433-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="bb433-209">Ekleme bir `String` özelliği `timeCreated` çok*src/main/java/com/example/fabrikam/TodoItem.java*, nesne oluşturma sırasında bir zaman damgasına sahip başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="bb433-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="bb433-210">Alıcıları/ayarlayıcılar hello yeni için ekleme `timeCreated` bu dosyayı düzenlerken özelliği.</span><span class="sxs-lookup"><span data-stu-id="bb433-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="bb433-211">Güncelleştirme *src/main/java/com/example/fabrikam/TodoDemoController.java* hello bir satır ile `updateTodo` yöntemi tooset hello zaman damgası:</span><span class="sxs-lookup"><span data-stu-id="bb433-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="bb433-212">Merhaba yeni alan için destek hello Thymeleaf şablonunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bb433-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="bb433-213">Güncelleştirme *src/main/resources/templates/index.html* hello zaman damgası ve her bir tablo veri satırının hello timestamp yeni alan toodisplay hello değeri için yeni bir tablo üstbilgiyle.</span><span class="sxs-lookup"><span data-stu-id="bb433-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="bb433-214">Merhaba uygulaması yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bb433-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="bb433-215">FTP hello güncelleştirildi. Hello varolan kaldırma WAR olarak önce *site/wwwroot/webapps/ROOT* dizin ve *ROOT.war*, sonra da güncelleştirilmiş hello karşıya yükleme. WAR dosyası olarak ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="bb433-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="bb433-216">Merhaba uygulama yenilediğinizde bir **saat oluşturulan** sütundur artık görünür.</span><span class="sxs-lookup"><span data-stu-id="bb433-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="bb433-217">Yeni bir görev eklediğinizde, hello uygulama hello zaman damgası otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="bb433-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="bb433-218">Veri modelini temel hello değişti olsa bile varolan görevlerinizi değişmeden ve hello uygulama ile çalışmak kalır.</span><span class="sxs-lookup"><span data-stu-id="bb433-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Java uygulaması olan yeni bir sütun güncelleştirildi](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="bb433-220">Akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="bb433-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="bb433-221">Java uygulamanızı Azure App Service'te çalışırken hello konsol alabilirsiniz günlükleri yöneltilen doğrudan tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="bb433-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="bb433-222">Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.</span><span class="sxs-lookup"><span data-stu-id="bb433-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="bb433-223">Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/appservice/web/log#tail) komutu.</span><span class="sxs-lookup"><span data-stu-id="bb433-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="bb433-224">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="bb433-224">Manage your Azure web app</span></span>

<span data-ttu-id="bb433-225">Oluşturduğunuz toohello Azure portal toosee hello web uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="bb433-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="bb433-226">toodo Bu, çok oturum[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb433-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="bb433-227">Merhaba sol menüden **uygulama hizmeti**, Azure web uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bb433-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="bb433-229">Varsayılan olarak, web uygulamanızın dikey penceresinde hello gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="bb433-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="bb433-230">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb433-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="bb433-231">Burada, Durdur, Başlat, yeniden başlatma ve silme gibi yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb433-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="bb433-232">hello sol tarafındaki hello dikey penceresinde Hello sekmeleri açabilir hello farklı yapılandırma sayfalarında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bb433-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Azure portalında App Service dikey penceresi](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="bb433-234">Bu sekme hello dikey penceresinde hello tooyour web uygulama eklemek için birçok harika özellikler gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb433-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="bb433-235">liste aşağıdaki hello birkaçı hello olasılıklar sunar:</span><span class="sxs-lookup"><span data-stu-id="bb433-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="bb433-236">Özel bir DNS adı eşleme</span><span class="sxs-lookup"><span data-stu-id="bb433-236">Map a custom DNS name</span></span>
* <span data-ttu-id="bb433-237">Özel bir SSL sertifikası bağlama</span><span class="sxs-lookup"><span data-stu-id="bb433-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="bb433-238">Sürekli dağıtımı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bb433-238">Configure continuous deployment</span></span>
* <span data-ttu-id="bb433-239">Ölçeği artırma ve genişletme</span><span class="sxs-lookup"><span data-stu-id="bb433-239">Scale up and out</span></span>
* <span data-ttu-id="bb433-240">Kullanıcı kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="bb433-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bb433-241">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="bb433-241">Clean up resources</span></span>

<span data-ttu-id="bb433-242">Başka bir öğretici için bu kaynakları gerekmiyorsa (bkz [sonraki adımlar](#next)), bunları hello aşağıdaki komutu çalıştırarak silin:</span><span class="sxs-lookup"><span data-stu-id="bb433-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="bb433-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb433-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb433-244">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb433-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="bb433-245">Bir örnek Java uygulama toohello MySQL Bağlan</span><span class="sxs-lookup"><span data-stu-id="bb433-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="bb433-246">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="bb433-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bb433-247">Güncelleştirme ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="bb433-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="bb433-248">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="bb433-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="bb433-249">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="bb433-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="bb433-250">İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad toohello uygulama.</span><span class="sxs-lookup"><span data-stu-id="bb433-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="bb433-251">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="bb433-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
