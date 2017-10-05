---
title: "İlk Azure veritabanınızı MySQL veritabanı - Azure Portal için Tasarım | Microsoft Docs"
description: "Bu öğretici, oluşturma ve MySQL server ve Azure portalını kullanarak veritabanı için Azure veritabanı yönetme açıklanmaktadır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="61b34-103">İlk Azure veritabanınızı MySQL veritabanı için tasarlama</span><span class="sxs-lookup"><span data-stu-id="61b34-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="61b34-104">MySQL için Azure Veritabanı, bulutta yüksek oranda kullanılabilir olan MySQL veritabanları çalıştırmanızı, yönetmenizi ve ölçeklendirmenizi sağlayan ve yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="61b34-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="61b34-105">Azure Portalı'nı kullanarak, kolayca sunucunuzu yönetin ve bir veritabanı tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="61b34-106">Bu öğreticide, bilgi edinmek için Azure portalını kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="61b34-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61b34-107">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="61b34-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="61b34-108">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="61b34-108">Configure the server firewall</span></span>
> * <span data-ttu-id="61b34-109">Bir veritabanı oluşturmak için MySQL komut satırı aracını kullanın</span><span class="sxs-lookup"><span data-stu-id="61b34-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="61b34-110">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-110">Load sample data</span></span>
> * <span data-ttu-id="61b34-111">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="61b34-111">Query data</span></span>
> * <span data-ttu-id="61b34-112">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="61b34-112">Update data</span></span>
> * <span data-ttu-id="61b34-113">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="61b34-114">Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="61b34-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="61b34-115">Sık kullanılan web tarayıcınızı açın ve ziyaret [Microsoft Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="61b34-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="61b34-116">Portalda oturum açmak için kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="61b34-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="61b34-117">Varsayılan görünüm hizmet panonuzu içerir.</span><span class="sxs-lookup"><span data-stu-id="61b34-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="61b34-118">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="61b34-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="61b34-119">MySQL için Azure Veritabanı sunucusu, tanımlı bir dizi [işlem ve depolama kaynağı](./concepts-compute-unit-and-storage.md) ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="61b34-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="61b34-120">Sunucu, [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="61b34-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="61b34-121">Gidin **veritabanları** > **Azure veritabanı için MySQL**.</span><span class="sxs-lookup"><span data-stu-id="61b34-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="61b34-122">MySQL sunucusu altında bulamazsa **veritabanları** kategori tıklatın **tümünü görmek** tüm kullanılabilir veritabanı hizmetleri göstermek için.</span><span class="sxs-lookup"><span data-stu-id="61b34-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="61b34-123">Ayrıca yazabilirsiniz **Azure veritabanı için MySQL** hizmeti hızla bulmak için arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="61b34-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="61b34-124">![MySQL için 2-1 gidin](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="61b34-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="61b34-125">Tıklatın **Azure veritabanı için MySQL** kutucuğuna ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="61b34-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="61b34-126">Bizim örneğimizde, Azure veritabanı için MySQL form aşağıdaki bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="61b34-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="61b34-127">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="61b34-127">**Setting**</span></span> | <span data-ttu-id="61b34-128">**Önerilen değer**</span><span class="sxs-lookup"><span data-stu-id="61b34-128">**Suggested value**</span></span> | <span data-ttu-id="61b34-129">**Alan Açıklaması**</span><span class="sxs-lookup"><span data-stu-id="61b34-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="61b34-130">*Sunucu adı*</span><span class="sxs-lookup"><span data-stu-id="61b34-130">*Server name*</span></span> | <span data-ttu-id="61b34-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="61b34-131">myserver4demo</span></span>  | <span data-ttu-id="61b34-132">Sunucu adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="61b34-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="61b34-133">*Abonelik*</span><span class="sxs-lookup"><span data-stu-id="61b34-133">*Subscription*</span></span> | <span data-ttu-id="61b34-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="61b34-134">mysubscription</span></span> | <span data-ttu-id="61b34-135">Açılan listeden aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="61b34-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="61b34-136">*Kaynak grubu*</span><span class="sxs-lookup"><span data-stu-id="61b34-136">*Resource group*</span></span> | <span data-ttu-id="61b34-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="61b34-137">myresourcegroup</span></span> | <span data-ttu-id="61b34-138">Bir kaynak grubu oluşturun veya mevcut olanlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="61b34-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="61b34-139">*Sunucu yöneticisi oturum açma bilgileri*</span><span class="sxs-lookup"><span data-stu-id="61b34-139">*Server admin login*</span></span> | <span data-ttu-id="61b34-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="61b34-140">myadmin</span></span> | <span data-ttu-id="61b34-141">Kurulum Yönetici hesap adı.</span><span class="sxs-lookup"><span data-stu-id="61b34-141">Setup admin account name.</span></span> |
| <span data-ttu-id="61b34-142">*Parola*</span><span class="sxs-lookup"><span data-stu-id="61b34-142">*Password*</span></span> |  | <span data-ttu-id="61b34-143">Güçlü bir yönetici hesabı parolası belirleyin.</span><span class="sxs-lookup"><span data-stu-id="61b34-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="61b34-144">*Parolayı onayla*</span><span class="sxs-lookup"><span data-stu-id="61b34-144">*Confirm password*</span></span> |  | <span data-ttu-id="61b34-145">Yönetici hesabı parolasını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="61b34-146">*Konum*</span><span class="sxs-lookup"><span data-stu-id="61b34-146">*Location*</span></span> |  | <span data-ttu-id="61b34-147">Kullanılabilir bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="61b34-147">Select an available region.</span></span> |
| <span data-ttu-id="61b34-148">*Sürüm*</span><span class="sxs-lookup"><span data-stu-id="61b34-148">*Version*</span></span> | <span data-ttu-id="61b34-149">5.7</span><span class="sxs-lookup"><span data-stu-id="61b34-149">5.7</span></span> | <span data-ttu-id="61b34-150">En son sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="61b34-150">Choose the latest version.</span></span> |
| <span data-ttu-id="61b34-151">*Performansı yapılandır*</span><span class="sxs-lookup"><span data-stu-id="61b34-151">*Configure performance*</span></span> | <span data-ttu-id="61b34-152">Temel, 50 birimleri, 50 GB işlem</span><span class="sxs-lookup"><span data-stu-id="61b34-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="61b34-153">**Fiyatlandırma katmanı**, **İşlem Birimleri**, **Depolama (GB)** öğelerini seçip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="61b34-154">*Panoya Sabitle*</span><span class="sxs-lookup"><span data-stu-id="61b34-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="61b34-155">İşaretli</span><span class="sxs-lookup"><span data-stu-id="61b34-155">Check</span></span> | <span data-ttu-id="61b34-156">Sunucuyu daha sonra kolayca bulabilmeniz için bu kutunun işaretlenmesi önerilir</span><span class="sxs-lookup"><span data-stu-id="61b34-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="61b34-157">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-157">Then, click **Create**.</span></span> <span data-ttu-id="61b34-158">Bir veya iki dakika içinde, bulutta MySQL sunucusu için yeni bir Azure Veritabanı çalışmaya başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="61b34-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="61b34-159">Tıklayabilirsiniz **bildirimleri** dağıtım işlemi izlemek için araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="61b34-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="61b34-160">Güvenlik duvarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="61b34-160">Configure firewall</span></span>
<span data-ttu-id="61b34-161">Azure veritabanları MySQL için bir güvenlik duvarı tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="61b34-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="61b34-162">Varsayılan olarak, sunucu ve veritabanları Sunucusu'ndaki tüm bağlantıları reddedilir.</span><span class="sxs-lookup"><span data-stu-id="61b34-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="61b34-163">Azure veritabanı için MySQL için ilk kez bağlanmadan önce istemci makinenin ortak ağ IP adresi (veya IP adresi aralığı) eklemek için Güvenlik Duvarı'nı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="61b34-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="61b34-164">Yeni oluşturulan sunucunuz tıklayın ve ardından **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="61b34-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="61b34-165">![3 1 bağlantı güvenliği](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="61b34-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="61b34-166">Yapabilecekleriniz **eklemek IP**, veya güvenlik duvarı kurallarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="61b34-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="61b34-167">Kuralları oluşturduktan sonra **Kaydet**’e tıklamayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="61b34-168">Şimdi, mysql komut satırı aracını veya MySQL çalışma ekranı GUI aracını kullanarak sunucuya bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="61b34-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="61b34-169">MySQL sunucusu için Azure veritabanı 3306 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="61b34-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="61b34-170">Kurumsal ağ içinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 3306 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="61b34-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="61b34-171">BT departmanınız 3306 bir bağlantı noktası açar sürece bu durumda, Azure MySQL sunucusuna bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="61b34-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="61b34-172">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="61b34-172">Get connection information</span></span>
<span data-ttu-id="61b34-173">Tam alma **sunucu adı** ve **sunucu yönetici oturum açma adı** Azure portalından MySQL server için Azure veritabanınızın.</span><span class="sxs-lookup"><span data-stu-id="61b34-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="61b34-174">Mysql komut satırı aracını kullanarak sunucunuza bağlanmak için tam sunucu adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="61b34-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="61b34-175">İçinde [Azure portal](https://portal.azure.com/), tıklatın **tüm kaynakları** sol taraftaki menüden bir ad yazın ve arama MySQL server için Azure veritabanınızın.</span><span class="sxs-lookup"><span data-stu-id="61b34-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="61b34-176">Ayrıntılarını görüntülemek için sunucu adını seçin.</span><span class="sxs-lookup"><span data-stu-id="61b34-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="61b34-177">Ayarlar altında başlığını tıklatın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="61b34-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="61b34-178">Aşağı Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="61b34-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="61b34-179">Panoya kopyalamak için her alanın yanındaki Kopyala düğmesini tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="61b34-180">![4-2 sunucu özellikleri](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="61b34-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="61b34-181">Bu örnekte sunucu adı *myserver4demo.mysql.database.azure.com*, sunucu yöneticisi oturum açma bilgileri ise *myadmin@myserver4demo* şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="61b34-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="61b34-182">MySQL kullanarak sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="61b34-182">Connect to the server using mysql</span></span>
<span data-ttu-id="61b34-183">MySQL sunucusu için Azure Veritabanınız ile bağlantı kurmak üzere [mysql komut satırı aracını](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) kullanın.</span><span class="sxs-lookup"><span data-stu-id="61b34-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="61b34-184">Tarayıcıda Azure bulut Kabuğu'ndan veya mysql araçlarının yüklü kullanarak yerel olarak kendi makineden mysql komut satırı aracını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="61b34-185">Azure bulut Kabuğu'nu başlatmak için tıklatın `Try It` bu makaledeki kod bloğu düğmesine veya Azure portalını ziyaret edin ve `>_` sağ üst araç çubuğunda simge.</span><span class="sxs-lookup"><span data-stu-id="61b34-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="61b34-186">Bağlanma komutunu yazın:</span><span class="sxs-lookup"><span data-stu-id="61b34-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="61b34-187">Boş veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="61b34-187">Create a blank database</span></span>
<span data-ttu-id="61b34-188">Bir kez sunucusuna bağlandıktan sonra çalışmak için boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61b34-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="61b34-189">İsteminde bağlantı yeni veritabanı oluşturulan bu geçiş yapmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="61b34-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="61b34-190">Veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="61b34-190">Create tables in the database</span></span>
<span data-ttu-id="61b34-191">MySQL veritabanı için Azure veritabanına bağlanmak nasıl bildiğinize göre biz temel bazı görevlerin nasıl üzerinden gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="61b34-192">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="61b34-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="61b34-193">Envanter bilgilerini depolayan bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="61b34-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="61b34-194">Veri tablolarına yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-194">Load data into the tables</span></span>
<span data-ttu-id="61b34-195">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="61b34-196">Açık komut istemi penceresinde, bazı veri satırı eklemek için aşağıdaki sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="61b34-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="61b34-197">Şimdi örnek verilerin daha önce oluşturduğunuz tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="61b34-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="61b34-198">Sorgulamak ve tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="61b34-198">Query and update the data in the tables</span></span>
<span data-ttu-id="61b34-199">Veritabanı tablosundan bilgi almak için aşağıdaki sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="61b34-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="61b34-200">Ayrıca tablolardaki verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="61b34-201">Veri aldığınızda satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="61b34-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="61b34-202">Bir veritabanını daha önceki bir noktaya geri yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="61b34-203">Önemli veritabanı tablosu yanlışlıkla sildiyseniz ve verileri kolayca kurtaramazsınız düşünün.</span><span class="sxs-lookup"><span data-stu-id="61b34-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="61b34-204">Azure veritabanı için MySQL sunucu zaman içinde bir noktaya geri veritabanlarını yeni sunucuyu oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="61b34-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="61b34-205">Bu yeni sunucu silinen verilerinizi kurtarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61b34-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="61b34-206">Tablo eklenmeden önce aşağıdaki adımları örnek sunucunun bir noktaya geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="61b34-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="61b34-207">Azure portalında Azure veritabanı için MySQL bulun.</span><span class="sxs-lookup"><span data-stu-id="61b34-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="61b34-208">Üzerinde **genel bakış** sayfasında, **geri** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="61b34-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="61b34-209">Geri yükleme sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="61b34-209">The Restore page opens.</span></span>

   ![10-1, bir veritabanını geri yükleyin](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="61b34-211">Doldurmak **geri** form gerekli bilgileri.</span><span class="sxs-lookup"><span data-stu-id="61b34-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 geri yükleme formu](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="61b34-213">**Geri yükleme noktası**: bir noktası için listelenen zaman çerçevesi içinde geri yüklemek istediğiniz zaman seçin.</span><span class="sxs-lookup"><span data-stu-id="61b34-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="61b34-214">Yerel saat dilimi UTC'ye dönüştürülecek emin olun.</span><span class="sxs-lookup"><span data-stu-id="61b34-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="61b34-215">**Yeni bir sunucuya geri**: geri yüklemek istediğiniz yeni bir sunucu adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="61b34-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="61b34-216">**Konum**: bölge kaynak sunucu ile aynı olması ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="61b34-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="61b34-217">**Fiyatlandırma katmanı**: fiyatlandırma katmanı kaynak sunucu ile aynıdır ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="61b34-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="61b34-218">Tıklatın **Tamam** sunucuya geri yüklemek için [zaman içinde bir noktaya geri](./howto-restore-server-portal.md) tablo silinmeden önce.</span><span class="sxs-lookup"><span data-stu-id="61b34-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="61b34-219">Bir sunucuyu geri belirttiğiniz zaman içinde nokta itibariyle sunucunun yeni bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="61b34-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="61b34-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61b34-220">Next steps</span></span>
<span data-ttu-id="61b34-221">Bu öğreticide, Azure portal öğrenilen için nasıl kullanın:</span><span class="sxs-lookup"><span data-stu-id="61b34-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61b34-222">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="61b34-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="61b34-223">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="61b34-223">Configure the server firewall</span></span>
> * <span data-ttu-id="61b34-224">Bir veritabanı oluşturmak için MySQL komut satırı aracını kullanın</span><span class="sxs-lookup"><span data-stu-id="61b34-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="61b34-225">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-225">Load sample data</span></span>
> * <span data-ttu-id="61b34-226">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="61b34-226">Query data</span></span>
> * <span data-ttu-id="61b34-227">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="61b34-227">Update data</span></span>
> * <span data-ttu-id="61b34-228">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="61b34-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61b34-229">MySQL için Azure veritabanı uygulamalara bağlanma</span><span class="sxs-lookup"><span data-stu-id="61b34-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
