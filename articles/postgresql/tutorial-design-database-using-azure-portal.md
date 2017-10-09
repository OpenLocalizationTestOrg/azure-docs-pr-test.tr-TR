---
title: "Azure portalını kullanarak PostgreSQL için ilk Azure veritabanınızı tasarım | Microsoft Docs"
description: "Bu öğretici nasıl tooDesign ilk Azure veritabanı için PostgreSQL hello Azure portal kullanarak gösterir."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="a9f5a-103">İlk Azure veritabanınızı hello Azure portal kullanarak PostgreSQL için tasarlama</span><span class="sxs-lookup"><span data-stu-id="a9f5a-103">Design your first Azure Database for PostgreSQL using hello Azure portal</span></span>

<span data-ttu-id="a9f5a-104">Azure veritabanı PostgreSQL için toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir PostgreSQL veritabanları hello bulutta ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="a9f5a-105">Hello Azure portal kullanarak kolayca sunucunuzu yönetin ve bir veritabanı tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="a9f5a-106">Bu öğreticide, Azure portal toolearn hello nasıl kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9f5a-107">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a9f5a-108">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="a9f5a-109">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="a9f5a-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="a9f5a-110">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-110">Load sample data</span></span>
> * <span data-ttu-id="a9f5a-111">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="a9f5a-111">Query data</span></span>
> * <span data-ttu-id="a9f5a-112">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-112">Update data</span></span>
> * <span data-ttu-id="a9f5a-113">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9f5a-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9f5a-114">Prerequisites</span></span>
<span data-ttu-id="a9f5a-115">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="a9f5a-116">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="a9f5a-116">Log in toohello Azure portal</span></span>
<span data-ttu-id="a9f5a-117">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9f5a-117">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="a9f5a-118">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="a9f5a-119">PostgreSQL için Azure Veritabanı sunucusu, tanımlı bir dizi [işlem ve depolama kaynağı](./concepts-compute-unit-and-storage.md) ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="a9f5a-120">Merhaba server içinde oluşturulur bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9f5a-120">hello server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a9f5a-121">Bu adımları toocreate PostgreSQL sunucu için bir Azure veritabanı izleyin:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-121">Follow these steps toocreate an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="a9f5a-122">Merhaba tıklatın **+ yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-122">Click hello **+ New**  button found on hello upper left-hand corner of hello Azure portal.</span></span>
2.  <span data-ttu-id="a9f5a-123">Seçin **veritabanları** hello gelen **yeni** sayfasında ve seçin **Azure veritabanı PostgreSQL için** hello gelen **veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-123">Select **Databases** from hello **New** page, and select **Azure Database for PostgreSQL** from hello **Databases** page.</span></span>
 <span data-ttu-id="a9f5a-124">![Azure veritabanı için PostgreSQL - hello veritabanı oluşturma](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-124">![Azure Database for PostgreSQL - Create hello database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="a9f5a-125">Yeni Sunucu ayrıntıları form Hello görüntü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurmak:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-125">Fill out hello new server details form with hello following information, as shown on hello preceding image:</span></span>
    - <span data-ttu-id="a9f5a-126">Sunucu adı: **mypgserver 20170401** (bir sunucunun adını tooDNS adını eşler, böylece gerekli toobe genel benzersiz ise)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-126">Server name: **mypgserver-20170401** (name of a server maps tooDNS name and is thus required toobe globally unique)</span></span> 
    - <span data-ttu-id="a9f5a-127">Abonelik: birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-127">Subscription: If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span>
    - <span data-ttu-id="a9f5a-128">Kaynak grubu: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="a9f5a-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="a9f5a-129">Tercih ettiğiniz sunucu yöneticisi oturum açma adı ve parolası</span><span class="sxs-lookup"><span data-stu-id="a9f5a-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="a9f5a-130">Konum</span><span class="sxs-lookup"><span data-stu-id="a9f5a-130">Location</span></span>
    - <span data-ttu-id="a9f5a-131">PostgreSQL Sürümü</span><span class="sxs-lookup"><span data-stu-id="a9f5a-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a9f5a-132">Burada belirttiğiniz Hello Sunucu Yöneticisi oturum açma ve parola toohello Server'daki gerekli toolog ve veritabanlarını Bu hızlı başlangıç devamındaki kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-132">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="a9f5a-133">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="a9f5a-134">Tıklatın **fiyatlandırma katmanı** toospecify hello hizmeti katmanını ve performans düzeyini yeni veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-134">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="a9f5a-135">Bu hızlı başlangıç için **Temel** Katman’ı, **50 İşlem Birimini** ve dahili depolamanın **50 GB**’sini seçin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="a9f5a-136">![Azure veritabanı PostgreSQL - çekme hello hizmet katmanı için](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-136">![Azure Database for PostgreSQL - pick hello service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="a9f5a-137">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="a9f5a-138">Tıklatın **oluşturma** tooprovision hello sunucu.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-138">Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="a9f5a-139">Sağlama birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="a9f5a-140">Merhaba denetleyin **PIN toodashboard** seçeneği tooallow kolay izlenmesini dağıtımlarınızı.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-140">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="a9f5a-141">Merhaba araç çubuğundan, **bildirimleri** toomonitor hello dağıtım işlemi.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-141">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>
 <span data-ttu-id="a9f5a-142">![PostgreSQL için Azure Veritabanı - Bildirimleri inceleme](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="a9f5a-143">Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="a9f5a-144">Merhaba [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanıdır varsayılan bir veritabanı kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-144">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="a9f5a-145">Sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="a9f5a-146">Hello Azure veritabanı PostgreSQL hizmeti için bir güvenlik duvarı hello sunucu düzeyinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-146">hello Azure Database for PostgreSQL service creates a firewall at hello server-level.</span></span> <span data-ttu-id="a9f5a-147">Bu güvenlik duvarı, bir güvenlik duvarı kuralı tooopen hello Güvenlik Duvarı'nı belirli IP adresleri için yapılandırılmadığı sürece toohello sunucusu ve hello sunucudaki tüm veritabanları bağlanmasını harici uygulamalar ve Araçlar önler.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-147">This firewall prevents external applications and tools from connecting toohello server and any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="a9f5a-148">Merhaba dağıtım tamamlandıktan sonra **tüm kaynakları** hello sol menüsünden ve hello adı yazın **mypgserver 20170401** toosearch yeni oluşturulan sunucunuz için.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-148">After hello deployment completes, click **All Resources** from hello left-hand menu and type in hello name **mypgserver-20170401** toosearch for your newly created server.</span></span> <span data-ttu-id="a9f5a-149">Merhaba arama sonucunda listelenen hello sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-149">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="a9f5a-150">Merhaba **genel bakış** sayfası sunucunuz açar ve ek yapılandırma seçeneklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-150">hello **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="a9f5a-151">PostgreSQL için Azure Veritabanı - Sunucu arama</span><span class="sxs-lookup"><span data-stu-id="a9f5a-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="a9f5a-152">Merhaba server dikey penceresinde, seçin **bağlantı güvenliği**.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-152">In hello server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="a9f5a-153">Merhaba metin kutusu altında tıklatın **kural adı** ve yeni bir güvenlik duvarı kuralı toowhitelist hello IP aralığı bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-153">Click in hello text box under **Rule Name,** and add a new firewall rule toowhitelist hello IP range for connectivity.</span></span> <span data-ttu-id="a9f5a-154">Şimdi bu öğreticide, yazarak tüm IP'ler izin **kural adı AllowAllIps =**, **başlangıç IP 0.0.0.0 =** ve **bitiş IP 255.255.255.255 =** ve ardından **Kaydet** .</span><span class="sxs-lookup"><span data-stu-id="a9f5a-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="a9f5a-155">Bir IP aralığı toobe mümkün tooconnect ağınızdan kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-155">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span>
 
 ![PostgreSQL için Azure Veritabanı - Güvenlik Duvarı Kuralı Oluşturma](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="a9f5a-157">Tıklatın **kaydetmek** ve hello ardından **X** tooclose hello **bağlantıları güvenlik** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-157">Click **Save** and then click hello **X** tooclose hello **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a9f5a-158">Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="a9f5a-159">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 5432 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-159">If you are trying tooconnect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a9f5a-160">Öyleyse, BT departmanınızın 5432 bir bağlantı noktası açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-160">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-hello-connection-information"></a><span data-ttu-id="a9f5a-161">Merhaba bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-161">Get hello connection information</span></span>

<span data-ttu-id="a9f5a-162">Bizim Azure veritabanı PostgreSQL sunucu için oluşturduğumuz, varsayılan hello **postgres** veritabanı da oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-162">When we created our Azure Database for PostgreSQL server, hello default **postgres** database also gets created.</span></span> <span data-ttu-id="a9f5a-163">tooconnect tooyour veritabanı sunucusu, tooprovide ana bilgisayar bilgileri ve erişim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-163">tooconnect tooyour database server, you need tooprovide host information and access credentials.</span></span>

1. <span data-ttu-id="a9f5a-164">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve yeni oluşturduğunuz hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-164">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="a9f5a-165">PostgreSQL için Azure Veritabanı - Sunucu arama</span><span class="sxs-lookup"><span data-stu-id="a9f5a-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="a9f5a-166">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-166">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="a9f5a-167">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-167">Select hello server's **Overview** page.</span></span> <span data-ttu-id="a9f5a-168">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-168">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="a9f5a-170">Bulut Kabuğu'nda psql kullanarak tooPostgreSQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="a9f5a-170">Connect tooPostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="a9f5a-171">Şimdi hello psql komut satırı yardımcı programını tooconnect toohello Azure veritabanı PostgreSQL sunucusu için kullanalım.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-171">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="a9f5a-172">Hello terminal simgesi hello üst gezinti bölmesindeki aracılığıyla Hello Azure bulut Kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-172">Launch hello Azure Cloud Shell via hello terminal icon on hello top navigation pane.</span></span>

   ![PostgreSQL için Azure Veritabanı - Azure Cloud Shell terminal simgesi](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="a9f5a-174">Hello Azure bulut Kabuk tootype bash komutları etkinleştirme tarayıcınızda açar.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-174">hello Azure Cloud Shell opens in your browser, enabling you tootype bash commands.</span></span>

   ![PostgreSQL için Azure Veritabanı - Azure Shell Bash İstemi](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="a9f5a-176">Merhaba bulut Kabuk isteminde tooyour Azure veritabanı PostgreSQL sunucusu hello psql komutları kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-176">At hello Cloud Shell prompt, connect tooyour Azure Database for PostgreSQL server using hello psql commands.</span></span> <span data-ttu-id="a9f5a-177">Merhaba aşağıdaki hello PostgreSQL sunucusu için kullanılan tooconnect tooan Azure veritabanı biçimidir [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-177">hello following format is used tooconnect tooan Azure Database for PostgreSQL server with hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="a9f5a-178">Örneğin, komutu aşağıdaki hello adlı toohello varsayılan veritabanı bağlayan **postgres** PostgreSQL sunucunuzda **mypgserver 20170401.postgres.database.azure.com** erişim kimlik bilgileri kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-178">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="a9f5a-179">İstendiğinde sunucu yönetici parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="a9f5a-180">Yeni veritabanı oluştur</span><span class="sxs-lookup"><span data-stu-id="a9f5a-180">Create a New Database</span></span>
<span data-ttu-id="a9f5a-181">Bağlı toohello sunucu olduğunuzda hello isteminde boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-181">Once you're connected toohello server, create a blank database at hello prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="a9f5a-182">Merhaba istemine komut tooswitch bağlantı toohello yeni oluşturulan veritabanı aşağıdaki hello yürütme **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-182">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a><span data-ttu-id="a9f5a-183">Merhaba veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-183">Create tables in hello database</span></span>
<span data-ttu-id="a9f5a-184">Nasıl tooconnect toohello Azure veritabanı PostgreSQL için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-184">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="a9f5a-185">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="a9f5a-186">Envanter bilgilerini izleyen bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="a9f5a-187">Yeni Tablo hello tabvles listesinde şimdi yazarak oluşturulan hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-187">You can see hello newly created table in hello list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="a9f5a-188">Merhaba tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-188">Load data into hello tables</span></span>
<span data-ttu-id="a9f5a-189">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="a9f5a-190">Hello açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-190">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="a9f5a-191">Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-191">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="a9f5a-192">Sorgulamak ve hello hello tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="a9f5a-192">Query and update hello data in hello tables</span></span>
<span data-ttu-id="a9f5a-193">Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-193">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="a9f5a-194">Merhaba tablolardaki hello verileri da güncelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a9f5a-194">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="a9f5a-195">veri aldığınızda hello satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-195">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a><span data-ttu-id="a9f5a-196">Zaman içinde veri tooa önceki noktası geri</span><span class="sxs-lookup"><span data-stu-id="a9f5a-196">Restore data tooa previous point in time</span></span>
<span data-ttu-id="a9f5a-197">Bu tablo yanlışlıkla silinmiş düşünün.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="a9f5a-198">Bu durum, kolayca kurtaramazsınız şeydir.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="a9f5a-199">Azure veritabanı PostgreSQL için toogo geri tooany zaman noktası (hello too7 gün (Temel) en son yukarı ve 35 gün (standart)) verir ve bu zaman içinde nokta tooa yeni sunucu geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-199">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="a9f5a-200">Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-200">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="a9f5a-201">Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-201">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1.  <span data-ttu-id="a9f5a-202">Azure veritabanı PostgreSQL sayfası sunucunuz için Hello üzerinde tıklatın **geri** hello araç.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-202">On hello Azure Database for PostgreSQL page for your server, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="a9f5a-203">Merhaba **geri** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-203">hello **Restore** page opens.</span></span>
  <span data-ttu-id="a9f5a-204">![Azure portal - geri yükleme form seçenekleri](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="a9f5a-205">Merhaba dolgu **geri** form hello gerekli bilgilerle:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-205">Fill out hello **Restore** form with hello required information:</span></span>

  ![Azure portal - geri yükleme form seçenekleri](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="a9f5a-207">**Geri yükleme noktası**: bir noktası hello sunucu değiştirilmeden önce oluşan zaman seçin</span><span class="sxs-lookup"><span data-stu-id="a9f5a-207">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="a9f5a-208">**Hedef sunucu**: toorestore için istediğiniz yeni bir sunucu adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="a9f5a-208">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="a9f5a-209">**Konum**: hello bölge seçemezsiniz, varsayılan olarak hello kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-209">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="a9f5a-210">**Fiyatlandırma katmanı**: bir sunucu geri yüklerken bu değer değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="a9f5a-211">Merhaba kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-211">It is same as hello source server.</span></span> 
3.  <span data-ttu-id="a9f5a-212">Tıklatın **Tamam** toorestore hello sunucu çok[tooa noktası zaman geri](./howto-restore-server-portal.md) hello tabloların silinmişse önce.</span><span class="sxs-lookup"><span data-stu-id="a9f5a-212">Click **OK** toorestore hello server too[restore tooa point-in-time](./howto-restore-server-portal.md) before hello tables was deleted.</span></span> <span data-ttu-id="a9f5a-213">Sunucu tooa farklı bir noktaya geri yükleme zamanında oluşturur yinelenen yeni bir sunucu hello özgün sunucusu olarak hello bir noktada, belirttiğiniz gibi hello saklama süresi içinde olmasını sağlanan, [hizmet katmanı](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="a9f5a-213">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9f5a-214">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a9f5a-214">Next Steps</span></span>
<span data-ttu-id="a9f5a-215">Bu öğreticide, toouse nasıl hello Azure portalı ve diğer yardımcı programları öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="a9f5a-215">In this tutorial, you learned how toouse hello Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9f5a-216">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a9f5a-217">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a9f5a-217">Configure hello server firewall</span></span>
> * <span data-ttu-id="a9f5a-218">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="a9f5a-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="a9f5a-219">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-219">Load sample data</span></span>
> * <span data-ttu-id="a9f5a-220">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="a9f5a-220">Query data</span></span>
> * <span data-ttu-id="a9f5a-221">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-221">Update data</span></span>
> * <span data-ttu-id="a9f5a-222">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="a9f5a-222">Restore data</span></span>

<span data-ttu-id="a9f5a-223">Ardından, bilgi toouse Azure CLI toodo benzer görevleri, Bu öğretici nasıl gözden geçirin: [PostgreSQL için Azure CLI kullanarak ilk Azure veritabanınızı tasarlama](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a9f5a-223">Next, learn how toouse Azure CLI toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
