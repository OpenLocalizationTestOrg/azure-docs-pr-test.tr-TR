---
title: "İlk Azure veritabanı için MySQL veritabanı - Azure Portal aaaDesign | Microsoft Docs"
description: "Bu öğretici açıklar nasıl toocreate Azure veritabanı için MySQL sunucusunu yönetmek ve Azure portalını kullanarak veritabanı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="d03b0-103">İlk Azure veritabanınızı MySQL veritabanı için tasarlama</span><span class="sxs-lookup"><span data-stu-id="d03b0-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="d03b0-104">Azure veritabanı için MySQL toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir MySQL veritabanları hello bulutta ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="d03b0-105">Hello Azure portal kullanarak kolayca sunucunuzu yönetin ve bir veritabanı tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="d03b0-106">Bu öğreticide, Azure portal toolearn hello nasıl kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="d03b0-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d03b0-107">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d03b0-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d03b0-108">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d03b0-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="d03b0-109">MySQL komut satırı aracı toocreate bir veritabanını kullanın</span><span class="sxs-lookup"><span data-stu-id="d03b0-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="d03b0-110">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="d03b0-110">Load sample data</span></span>
> * <span data-ttu-id="d03b0-111">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="d03b0-111">Query data</span></span>
> * <span data-ttu-id="d03b0-112">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d03b0-112">Update data</span></span>
> * <span data-ttu-id="d03b0-113">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d03b0-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="d03b0-114">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="d03b0-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="d03b0-115">Sık kullanılan web tarayıcınızı açın ve hello ziyaret [Microsoft Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d03b0-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d03b0-116">Kimlik bilgileri toosign toohello Portalı'nda girin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="d03b0-117">Hizmet panonuz Hello varsayılan görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="d03b0-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="d03b0-118">MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d03b0-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="d03b0-119">MySQL için Azure Veritabanı sunucusu, tanımlı bir dizi [işlem ve depolama kaynağı](./concepts-compute-unit-and-storage.md) ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d03b0-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="d03b0-120">Merhaba server içinde oluşturulur bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="d03b0-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="d03b0-121">Çok gidin**veritabanları** > **Azure veritabanı için MySQL**.</span><span class="sxs-lookup"><span data-stu-id="d03b0-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="d03b0-122">MySQL sunucusu altında bulamazsa **veritabanları** kategorisi, tıklatın **tümünü görmek** tooshow kullanılabilir tüm Hizmetleri veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d03b0-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="d03b0-123">Ayrıca yazabilirsiniz **Azure veritabanı için MySQL** hello arama kutusu tooquickly hello hizmeti bulamadı.</span><span class="sxs-lookup"><span data-stu-id="d03b0-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="d03b0-124">![2-1 Bul tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="d03b0-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="d03b0-125">Tıklatın **Azure veritabanı için MySQL** kutucuğuna ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d03b0-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="d03b0-126">Bizim örneğimizde, hello Azure veritabanı MySQL form için aşağıdaki bilgilerle hello ile doldurun:</span><span class="sxs-lookup"><span data-stu-id="d03b0-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="d03b0-127">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="d03b0-127">**Setting**</span></span> | <span data-ttu-id="d03b0-128">**Önerilen değer**</span><span class="sxs-lookup"><span data-stu-id="d03b0-128">**Suggested value**</span></span> | <span data-ttu-id="d03b0-129">**Alan Açıklaması**</span><span class="sxs-lookup"><span data-stu-id="d03b0-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="d03b0-130">*Sunucu adı*</span><span class="sxs-lookup"><span data-stu-id="d03b0-130">*Server name*</span></span> | <span data-ttu-id="d03b0-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="d03b0-131">myserver4demo</span></span>  | <span data-ttu-id="d03b0-132">Sunucu adı toobe genel benzersiz sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d03b0-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="d03b0-133">*Abonelik*</span><span class="sxs-lookup"><span data-stu-id="d03b0-133">*Subscription*</span></span> | <span data-ttu-id="d03b0-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="d03b0-134">mysubscription</span></span> | <span data-ttu-id="d03b0-135">Aboneliğinizi hello açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="d03b0-136">*Kaynak grubu*</span><span class="sxs-lookup"><span data-stu-id="d03b0-136">*Resource group*</span></span> | <span data-ttu-id="d03b0-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="d03b0-137">myresourcegroup</span></span> | <span data-ttu-id="d03b0-138">Bir kaynak grubu oluşturun veya mevcut olanlardan birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="d03b0-139">*Sunucu yöneticisi oturum açma bilgileri*</span><span class="sxs-lookup"><span data-stu-id="d03b0-139">*Server admin login*</span></span> | <span data-ttu-id="d03b0-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="d03b0-140">myadmin</span></span> | <span data-ttu-id="d03b0-141">Kurulum Yönetici hesap adı.</span><span class="sxs-lookup"><span data-stu-id="d03b0-141">Setup admin account name.</span></span> |
| <span data-ttu-id="d03b0-142">*Parola*</span><span class="sxs-lookup"><span data-stu-id="d03b0-142">*Password*</span></span> |  | <span data-ttu-id="d03b0-143">Güçlü bir yönetici hesabı parolası belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="d03b0-144">*Parolayı onayla*</span><span class="sxs-lookup"><span data-stu-id="d03b0-144">*Confirm password*</span></span> |  | <span data-ttu-id="d03b0-145">Merhaba yönetici hesabı parolasını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="d03b0-146">*Konum*</span><span class="sxs-lookup"><span data-stu-id="d03b0-146">*Location*</span></span> |  | <span data-ttu-id="d03b0-147">Kullanılabilir bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-147">Select an available region.</span></span> |
| <span data-ttu-id="d03b0-148">*Sürüm*</span><span class="sxs-lookup"><span data-stu-id="d03b0-148">*Version*</span></span> | <span data-ttu-id="d03b0-149">5.7</span><span class="sxs-lookup"><span data-stu-id="d03b0-149">5.7</span></span> | <span data-ttu-id="d03b0-150">Merhaba en son sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="d03b0-151">*Performansı yapılandır*</span><span class="sxs-lookup"><span data-stu-id="d03b0-151">*Configure performance*</span></span> | <span data-ttu-id="d03b0-152">Temel, 50 birimleri, 50 GB işlem</span><span class="sxs-lookup"><span data-stu-id="d03b0-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="d03b0-153">**Fiyatlandırma katmanı**, **İşlem Birimleri**, **Depolama (GB)** öğelerini seçip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="d03b0-154">*PIN tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="d03b0-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="d03b0-155">İşaretli</span><span class="sxs-lookup"><span data-stu-id="d03b0-155">Check</span></span> | <span data-ttu-id="d03b0-156">Toocheck, bu kutu önerilir, böylece hello sunucu üzerinde kolayca daha sonra bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d03b0-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="d03b0-157">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-157">Then, click **Create**.</span></span> <span data-ttu-id="d03b0-158">Bir veya iki dakika içinde MySQL sunucusu için yeni bir Azure veritabanı hello bulutta çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d03b0-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="d03b0-159">Tıklayabilirsiniz **bildirimleri** hello araç toomonitor hello dağıtım işlemi düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="d03b0-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="d03b0-160">Güvenlik duvarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d03b0-160">Configure firewall</span></span>
<span data-ttu-id="d03b0-161">Azure veritabanları MySQL için bir güvenlik duvarı tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="d03b0-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="d03b0-162">Varsayılan olarak, tüm bağlantılar toohello sunucusu ve hello veritabanları hello Sunucusu'ndaki reddedilir.</span><span class="sxs-lookup"><span data-stu-id="d03b0-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="d03b0-163">TooAzure veritabanı için MySQL hello için ilk kez bağlanmadan önce hello güvenlik duvarı tooadd hello istemci makinenin ortak ağ IP adresi (veya IP adresi aralığı) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="d03b0-164">Yeni oluşturulan sunucunuz tıklayın ve ardından **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="d03b0-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="d03b0-165">![3 1 bağlantı güvenliği](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="d03b0-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="d03b0-166">Yapabilecekleriniz **eklemek IP**, veya güvenlik duvarı kurallarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="d03b0-167">Tooclick unutmayın **kaydetmek** hello kuralları oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="d03b0-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="d03b0-168">Şimdi, mysql komut satırı aracını veya MySQL çalışma ekranı GUI aracını kullanarak toohello sunucusuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d03b0-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="d03b0-169">MySQL sunucusu için Azure veritabanı 3306 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d03b0-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="d03b0-170">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 3306 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="d03b0-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d03b0-171">BT departmanınız 3306 bir bağlantı noktası açar sürece bu durumda, tooAzure MySQL server bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="d03b0-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d03b0-172">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d03b0-172">Get connection information</span></span>
<span data-ttu-id="d03b0-173">Tam alma hello **sunucu adı** ve **sunucu yönetici oturum açma adı** hello Azure portal MySQL sunucudan için Azure veritabanınızın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="d03b0-174">Mysql komut satırı aracını kullanarak hello tam adı tooconnect tooyour sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="d03b0-175">İçinde [Azure portal](https://portal.azure.com/), tıklatın **tüm kaynakları** hello sol taraftaki menüyü, hello adını yazın ve arama MySQL server için Azure veritabanınızın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="d03b0-176">Merhaba sunucu adı tooview hello Ayrıntılar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="d03b0-177">Hello ayarları altında başlığını tıklatın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="d03b0-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="d03b0-178">Aşağı Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="d03b0-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="d03b0-179">Hello Kopyala düğmesine bir sonraki tooeach alan toocopy toohello Pano tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03b0-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="d03b0-180">![4-2 sunucu özellikleri](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="d03b0-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="d03b0-181">Bu örnekte, hello sunucu adıdır *myserver4demo.mysql.database.azure.com*, ve hello Sunucu Yöneticisi oturum açma  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="d03b0-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="d03b0-182">MySQL kullanarak toohello sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="d03b0-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="d03b0-183">Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish MySQL sunucusu için bağlantı tooyour Azure veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d03b0-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="d03b0-184">Hello Azure bulut Kabuk hello tarayıcıda veya mysql araçlarının yüklü kullanarak yerel olarak kendi makineden hello mysql komut satırı aracını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03b0-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="d03b0-185">toolaunch hello Azure bulut Kabuk tıklatın hello `Try It` bu makaledeki kod bloğu düğmesine veya hello Azure portalını ziyaret edin ve hello tıklatın `>_` hello üst sağ araç çubuğunda simge.</span><span class="sxs-lookup"><span data-stu-id="d03b0-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="d03b0-186">Merhaba komutu tooconnect yazın:</span><span class="sxs-lookup"><span data-stu-id="d03b0-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="d03b0-187">Boş veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d03b0-187">Create a blank database</span></span>
<span data-ttu-id="d03b0-188">Bağlı toohello sunucu olduğunuzda, bir boş veritabanı toowork ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d03b0-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="d03b0-189">Merhaba isteminde komut tooswitch bağlantı toothis yeni oluşturulan veritabanı aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d03b0-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="d03b0-190">Merhaba veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d03b0-190">Create tables in hello database</span></span>
<span data-ttu-id="d03b0-191">Nasıl tooconnect toohello Azure veritabanı MySQL veritabanı için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="d03b0-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="d03b0-192">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="d03b0-193">Envanter bilgilerini depolayan bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="d03b0-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="d03b0-194">Merhaba tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d03b0-194">Load data into hello tables</span></span>
<span data-ttu-id="d03b0-195">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03b0-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="d03b0-196">Merhaba açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="d03b0-197">Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="d03b0-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="d03b0-198">Sorgulamak ve hello hello tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="d03b0-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="d03b0-199">Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="d03b0-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="d03b0-200">Ayrıca hello tablolardaki hello verileri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03b0-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="d03b0-201">veri aldığınızda hello satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d03b0-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="d03b0-202">Zaman içinde veritabanı tooa önceki bir noktaya geri</span><span class="sxs-lookup"><span data-stu-id="d03b0-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="d03b0-203">Önemli veritabanı tablosu yanlışlıkla sildiyseniz ve hello verileri kolayca kurtaramazsınız düşünün.</span><span class="sxs-lookup"><span data-stu-id="d03b0-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="d03b0-204">Azure veritabanı için MySQL yeni sunucuyu hello veritabanları bir kopyası oluşturuluyor, zaman içindeki toorestore hello sunucusu tooa noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="d03b0-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="d03b0-205">Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d03b0-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="d03b0-206">Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.</span><span class="sxs-lookup"><span data-stu-id="d03b0-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="d03b0-207">Hello Azure portal, Azure veritabanı için MySQL bulun.</span><span class="sxs-lookup"><span data-stu-id="d03b0-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="d03b0-208">Merhaba üzerinde **genel bakış** sayfasında, **geri** hello araç.</span><span class="sxs-lookup"><span data-stu-id="d03b0-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="d03b0-209">Merhaba geri yükleme sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="d03b0-209">hello Restore page opens.</span></span>

   ![10-1, bir veritabanını geri yükleyin](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="d03b0-211">Merhaba doldurun **geri** hello gerekli bilgilerle formu.</span><span class="sxs-lookup"><span data-stu-id="d03b0-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 geri yükleme formu](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="d03b0-213">**Geri yükleme noktası**: bir noktası listelenen hello zaman çerçevesi içinde toorestore için istediğiniz zaman seçin.</span><span class="sxs-lookup"><span data-stu-id="d03b0-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="d03b0-214">Yerel saat dilimi tooUTC tooconvert emin olun.</span><span class="sxs-lookup"><span data-stu-id="d03b0-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="d03b0-215">**Toonew sunucuyu geri**: toorestore için istediğiniz yeni bir sunucu adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d03b0-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="d03b0-216">**Konum**: hello bölge hello kaynak sunucu ile aynı olması ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d03b0-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="d03b0-217">**Fiyatlandırma katmanı**: fiyatlandırma katmanı hello olduğu hello hello aynı kaynak sunucu ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d03b0-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="d03b0-218">Tıklatın **Tamam** toorestore hello sunucu çok[tooa noktası zaman içinde geri](./howto-restore-server-portal.md) hello tablo silinmeden önce.</span><span class="sxs-lookup"><span data-stu-id="d03b0-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="d03b0-219">Bir sunucuyu geri belirttiğiniz hello noktaya itibariyle hello sunucu yeni bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d03b0-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d03b0-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d03b0-220">Next steps</span></span>
<span data-ttu-id="d03b0-221">Bu öğreticide, Azure portal toolearned hello nasıl kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="d03b0-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d03b0-222">MySQL için Azure bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d03b0-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d03b0-223">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d03b0-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="d03b0-224">MySQL komut satırı aracı toocreate bir veritabanını kullanın</span><span class="sxs-lookup"><span data-stu-id="d03b0-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="d03b0-225">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="d03b0-225">Load sample data</span></span>
> * <span data-ttu-id="d03b0-226">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="d03b0-226">Query data</span></span>
> * <span data-ttu-id="d03b0-227">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d03b0-227">Update data</span></span>
> * <span data-ttu-id="d03b0-228">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d03b0-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d03b0-229">Nasıl tooconnect uygulamaları tooAzure veritabanı için MySQL</span><span class="sxs-lookup"><span data-stu-id="d03b0-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
