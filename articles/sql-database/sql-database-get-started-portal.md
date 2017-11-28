---
title: "Azure portalı: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure portalında SQL Veritabanı mantıksal sunucusu, sunucu düzeyi güvenlik duvarı kuralı ve veritabanı oluşturmayı öğrenin. Ayrıca Azure portalını kullanarak bir Azure SQL veritabanında sorgu yürütmeyi öğrenirsiniz."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="c7905-105">Azure portalında Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7905-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="c7905-106">Bu hızlı başlangıç öğreticisinde, Azure’da SQL veritabanı oluşturma adımlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c7905-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="c7905-107">Azure SQL Veritabanı, bulutta yüksek oranda kullanılabilir SQL Server veritabanlarını çalıştırıp ölçeklendirmenize olanak tanıyan bir “Hizmet Olarak Veritabanı” teklifidir.</span><span class="sxs-lookup"><span data-stu-id="c7905-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="c7905-108">Bu hızlı başlangıç, Azure portalını kullanarak bir SQL veritabanı oluşturma işlemini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c7905-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="c7905-109">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7905-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="c7905-110">Azure portalında oturum açma</span><span class="sxs-lookup"><span data-stu-id="c7905-110">Log in to the Azure portal</span></span>

<span data-ttu-id="c7905-111">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c7905-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="c7905-112">SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7905-112">Create a SQL database</span></span>

<span data-ttu-id="c7905-113">Azure SQL veritabanı bir dizi [işlem ve depolama kaynağı](sql-database-service-tiers.md) ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7905-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="c7905-114">Veritabanı bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL Veritabanı mantıksal sunucusu](sql-database-features.md) içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7905-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="c7905-115">Adventure Works LT örnek verilerini içeren bir SQL veritabanı oluşturmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c7905-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="c7905-116">Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="c7905-117">**Yeni** penceresinden **Veritabanları**’nı seçin ve **Veritabanları** penceresinden **SQL Veritabanı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="c7905-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="c7905-119">SQL Veritabanı formunu, önceki görüntüde gösterildiği gibi aşağıdaki bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="c7905-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="c7905-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="c7905-120">Setting</span></span>       | <span data-ttu-id="c7905-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="c7905-121">Suggested value</span></span> | <span data-ttu-id="c7905-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c7905-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="c7905-123">**Veritabanı adı**</span><span class="sxs-lookup"><span data-stu-id="c7905-123">**Database name**</span></span> | <span data-ttu-id="c7905-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="c7905-124">mySampleDatabase</span></span> | <span data-ttu-id="c7905-125">Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="c7905-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="c7905-126">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="c7905-126">**Subscription**</span></span> | <span data-ttu-id="c7905-127">Aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="c7905-127">Your subscription</span></span>  | <span data-ttu-id="c7905-128">Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="c7905-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="c7905-129">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="c7905-129">**Resource group**</span></span>  | <span data-ttu-id="c7905-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7905-130">myResourceGroup</span></span> | <span data-ttu-id="c7905-131">Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="c7905-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="c7905-132">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="c7905-132">**Source source**</span></span> | <span data-ttu-id="c7905-133">Örnek (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="c7905-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="c7905-134">AdventureWorksLT şemasını ve verilerini yeni veritabanınıza yükler</span><span class="sxs-lookup"><span data-stu-id="c7905-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="c7905-135">Bu hızlı başlangıcın geri kalanında kullanılacağı için bu formdaki örnek veritabanını seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7905-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="c7905-136">**Sunucu** altında **Gerekli ayarları yapılandır**’a tıklayıp, aşağıdaki görüntüde gösterildiği gibi SQL sunucusu (mantıksal sunucu) formunu aşağıdaki bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="c7905-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="c7905-137">Ayar</span><span class="sxs-lookup"><span data-stu-id="c7905-137">Setting</span></span>       | <span data-ttu-id="c7905-138">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="c7905-138">Suggested value</span></span> | <span data-ttu-id="c7905-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c7905-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="c7905-140">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="c7905-140">**Server name**</span></span> | <span data-ttu-id="c7905-141">Genel olarak benzersiz bir ad</span><span class="sxs-lookup"><span data-stu-id="c7905-141">Any globally unique name</span></span> | <span data-ttu-id="c7905-142">Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="c7905-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="c7905-143">**Sunucu yöneticisi oturum açma bilgileri**</span><span class="sxs-lookup"><span data-stu-id="c7905-143">**Server admin login**</span></span> | <span data-ttu-id="c7905-144">Geçerli bir ad</span><span class="sxs-lookup"><span data-stu-id="c7905-144">Any valid name</span></span> | <span data-ttu-id="c7905-145">Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="c7905-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="c7905-146">**Parola**</span><span class="sxs-lookup"><span data-stu-id="c7905-146">**Password**</span></span> | <span data-ttu-id="c7905-147">Geçerli bir parola</span><span class="sxs-lookup"><span data-stu-id="c7905-147">Any valid password</span></span> | <span data-ttu-id="c7905-148">Parolanızda en az 8 karakter bulunmalı ve parolanız şu üç kategoriden karakterler içermelidir: büyük harf karakterler, küçük harf karakterler, sayılar ve alfasayısal olmayan karakterler.</span><span class="sxs-lookup"><span data-stu-id="c7905-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="c7905-149">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="c7905-149">**Subscription**</span></span> | <span data-ttu-id="c7905-150">Aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="c7905-150">Your subscription</span></span> | <span data-ttu-id="c7905-151">Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="c7905-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="c7905-152">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="c7905-152">**Resource group**</span></span> | <span data-ttu-id="c7905-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7905-153">myResourceGroup</span></span> | <span data-ttu-id="c7905-154">Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="c7905-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="c7905-155">**Konum**</span><span class="sxs-lookup"><span data-stu-id="c7905-155">**Location**</span></span> | <span data-ttu-id="c7905-156">Geçerli bir konum</span><span class="sxs-lookup"><span data-stu-id="c7905-156">Any valid location</span></span> | <span data-ttu-id="c7905-157">Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="c7905-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="c7905-158">Burada belirttiğiniz sunucu yöneticisi kullanıcı adı ve parolası, bu hızlı başlangıcın sonraki bölümlerinde sunucuda ve veritabanlarında oturum açmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c7905-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="c7905-159">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c7905-159">Remember or record this information for later use.</span></span> 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="c7905-161">Formu tamamladığınızda **Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="c7905-162">Yeni veritabanınıza ait hizmet katmanını ve performans düzeyini belirtmek için **Fiyatlandırma katmanı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="c7905-163">**20 DTU** ve **250** GB depolama seçmek için kaydırıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7905-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="c7905-164">DTU hakkında daha fazla bilgi için bkz. [DTU nedir?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="c7905-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="c7905-166">DTU miktarını seçtikten sonra **Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="c7905-167">SQL Veritabanı formunu tamamladıktan sonra veritabanını sağlamak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="c7905-168">Sağlama birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="c7905-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="c7905-169">Araç çubuğunda **Bildirimler**’e tıklayarak dağıtım işlemini izleyin.</span><span class="sxs-lookup"><span data-stu-id="c7905-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![bildirim](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="c7905-171">Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7905-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="c7905-172">SQL Veritabanı hizmeti, güvenlik duvarını belirli IP adreslerine açmaya yönelik bir güvenlik duvarı kuralı oluşturulmadıkça, dış uygulama ve araçların sunucuya ya da sunucu üzerindeki herhangi bir veritabanına bağlanmasını engelleyen sunucu düzeyinde bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c7905-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="c7905-173">SQL Veritabanı güvenlik duvarı üzerinden yalnızca IP adresinize yönelik dış bağlantıları etkinleştirmek üzere istemcinizin IP adresi için bir [SQL Veritabanı sunucu düzeyi güvenlik duvarı kuralı](sql-database-firewall-configure.md) oluşturmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c7905-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="c7905-174">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="c7905-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="c7905-175">Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7905-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c7905-176">Bu durumda BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL Veritabanı sunucunuza bağlanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c7905-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="c7905-177">Dağıtım tamamlandıktan sonra, soldaki menüden **SQL veritabanları**'na ve ardından **SQL veritabanları** sayfasında **mySampleDatabase** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="c7905-178">Veritabanınıza ilişkin genel bakış sayfası açılır ve tam sunucu adı (örneğin, **mynewserver20170313.database.windows.net**) görüntülenerek daha fazla yapılandırma seçeneği sunulur.</span><span class="sxs-lookup"><span data-stu-id="c7905-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="c7905-179">Daha sonra kullanmak üzere bu tam sunucu adını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c7905-180">Sonraki hızlı başlangıçlarda sunucunuza ve veritabanlarına bağlanmak için bu tam sunucu adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7905-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![sunucu adı](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="c7905-182">Önceki görüntüde gösterildiği gibi araç çubuğundaki **sunucu güvenlik duvarı ayarla** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="c7905-183">SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="c7905-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="c7905-185">Geçerli IP adresinizi yeni bir güvenlik duvarı kuralına eklemek için araç çubuğunda **İstemci IP’si Ekle** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="c7905-186">Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.</span><span class="sxs-lookup"><span data-stu-id="c7905-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="c7905-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-187">Click **Save**.</span></span> <span data-ttu-id="c7905-188">Geçerli IP adresiniz için mantıksal sunucuda 1433 numaralı bağlantı noktası açılarak sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7905-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="c7905-190">**Tamam**’a tıklayın ve sonra **Güvenlik duvarı ayarları** sayfasını kapatın.</span><span class="sxs-lookup"><span data-stu-id="c7905-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="c7905-191">Artık SQL Server Management Studio’yu veya seçtiğiniz başka bir aracı kullanarak, daha önce oluşturduğunuz sunucu yöneticisi hesabıyla bu IP adresinden SQL Veritabanı sunucusuna ve sunucuya ait veritabanlarına bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7905-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7905-192">Varsayılan olarak, SQL Veritabanı güvenlik duvarı üzerinden erişim tüm Azure hizmetleri için etkindir.</span><span class="sxs-lookup"><span data-stu-id="c7905-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="c7905-193">Tüm Azure hizmetleri için devre dışı bırakmak isterseniz bu sayfadaki **KAPALI** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="c7905-194">SQL veritabanını sorgulama</span><span class="sxs-lookup"><span data-stu-id="c7905-194">Query the SQL database</span></span>

<span data-ttu-id="c7905-195">Azure’da bir örnek veritabanı oluşturduktan sonra, veritabanına bağlanabildiğinizi ve verileri sorgulayabildiğinizi onaylamak üzere Azure portalındaki yerleşik sorgu aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7905-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="c7905-196">Veritabanınız için SQL Veritabanı sayfasında, araç çubuğundaki **Araçlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="c7905-197">**Araçlar** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="c7905-197">The **Tools** page opens.</span></span>

   ![araçlar menüsü](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="c7905-199">**Sorgu düzenleyicisi (önizleme)**’ye tıklayın, **Önizleme koşulları** onay kutusuna tıklayın ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="c7905-200">Sorgu düzenleyicisi sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="c7905-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="c7905-201">**Oturum aç**’a tıklayın ve istendiğinde **SQL Server kimlik doğrulamasını** seçin ve daha önce oluşturduğunuz sunucu yöneticisi oturum açma bilgilerini ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="c7905-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![oturum açma](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="c7905-203">Oturum açmak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="c7905-204">Kimlik doğrulaması yaptıktan sonra sorgu düzenleyici bölmesine aşağıdaki sorguyu yazın.</span><span class="sxs-lookup"><span data-stu-id="c7905-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="c7905-205">**Çalıştır**’a tıklayın ve **Sonuçlar** bölmesindeki sorgu sonuçlarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="c7905-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![sorgu düzenleyicisi sonuçları](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="c7905-207">**Sorgu düzenleyicisi** sayfasını ve **Araçlar** sayfasını kapatın.</span><span class="sxs-lookup"><span data-stu-id="c7905-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="c7905-208">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="c7905-208">Clean up resources</span></span>

<span data-ttu-id="c7905-209">Bu kaynaklara başka bir hızlı başlangıç kılavuzu/öğretici (bkz. [Sonraki adımlar](#next-steps)) için gereksinim duymuyorsanız, aşağıdaki yaparak bu kaynakları silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7905-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="c7905-210">Azure portalında sol taraftaki menüden, **Kaynak grupları**’na tıklayın ve ardından **myResourceGroup**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="c7905-211">Kaynak grubu sayfanızda, **Sil**’e tıklayın, metin kutusuna **myResourceGroup** yazın ve ardından **Sil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7905-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7905-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7905-212">Next steps</span></span>

<span data-ttu-id="c7905-213">Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7905-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="c7905-214">Aşağıdan aracınızı seçerek daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="c7905-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="c7905-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c7905-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="c7905-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c7905-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="c7905-217">.NET</span><span class="sxs-lookup"><span data-stu-id="c7905-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="c7905-218">PHP</span><span class="sxs-lookup"><span data-stu-id="c7905-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="c7905-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="c7905-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="c7905-220">Java</span><span class="sxs-lookup"><span data-stu-id="c7905-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="c7905-221">Python</span><span class="sxs-lookup"><span data-stu-id="c7905-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="c7905-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="c7905-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
