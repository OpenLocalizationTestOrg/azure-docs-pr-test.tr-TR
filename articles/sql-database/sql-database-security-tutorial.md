---
title: "Azure SQL veritabanınızı güvenli | Microsoft Docs"
description: "Teknikleri ve Azure SQL veritabanınızın güvenliğini sağlamak için özellikleri hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 4bc09ad13ed0c9dc9257e9c75ec6f9ff3d689a0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="154a5-103">Azure SQL veritabanınızı güvenli</span><span class="sxs-lookup"><span data-stu-id="154a5-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="154a5-104">SQL Veritabanı veritabanınıza erişimi sınırlamak için güvenlik duvarı kurallarını, kullanıcıların kimliğini doğrulamak için kimlik doğrulama sistemlerini, rol tabanlı üyelikler ve izinler ile veri yetkilendirmeyi, satır düzeyi güvenliği ve dinamik veri maskelemeyi kullanarak verilerinizin güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-104">SQL Database secures your data by limiting access to your database using firewall rules, authentication mechanisms requiring users to prove their identity, and authorization to data through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="154a5-105">Veritabanınızı kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı koruma artırabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-105">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="154a5-106">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="154a5-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="154a5-107">Azure portalında sunucunuz için sunucu düzeyinde güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="154a5-107">Set up server-level firewall rules for your server in the Azure portal</span></span>
> * <span data-ttu-id="154a5-108">SSMS kullanarak, veritabanı için veritabanı düzeyinde güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="154a5-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="154a5-109">Güvenli bağlantı dizesi kullanarak veritabanınıza bağlanmak</span><span class="sxs-lookup"><span data-stu-id="154a5-109">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="154a5-110">Kullanıcı erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="154a5-110">Manage user access</span></span>
> * <span data-ttu-id="154a5-111">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="154a5-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="154a5-112">SQL veritabanı denetimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="154a5-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="154a5-113">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="154a5-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="154a5-114">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="154a5-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="154a5-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="154a5-115">Prerequisites</span></span>

<span data-ttu-id="154a5-116">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="154a5-116">To complete this tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="154a5-117">En son sürümü yüklü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="154a5-117">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="154a5-118">Yüklü Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="154a5-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="154a5-119">Bir Azure SQL server ve veritabanı - oluşturulan bkz [Azure portalında bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md), [Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-cli.md), ve [PowerShell kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="154a5-119">Created an Azure SQL server and database - See [Create an Azure SQL database in the Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using the Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="154a5-120">Azure portalında oturum açma</span><span class="sxs-lookup"><span data-stu-id="154a5-120">Log in to the Azure portal</span></span>

<span data-ttu-id="154a5-121">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="154a5-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="154a5-122">Azure portalında sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="154a5-122">Create a server-level firewall rule in the Azure portal</span></span>

<span data-ttu-id="154a5-123">SQL veritabanları Azure güvenlik duvarı tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="154a5-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="154a5-124">Varsayılan olarak, diğer Azure hizmetleriyle bağlantılarından dışında sunucusunu ve veritabanlarını Sunucusu'ndaki tüm bağlantıları reddedilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-124">By default, all connections to the server and the databases inside the server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="154a5-125">Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="154a5-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="154a5-126">En güvenli yapılandırma, 'OFF olarak Azure hizmetlerine erişime izin ver' ayarlamaktır.</span><span class="sxs-lookup"><span data-stu-id="154a5-126">The most secure configuration is to set 'Allow access to Azure services' to OFF.</span></span> <span data-ttu-id="154a5-127">Bir Azure VM veya Bulut hizmetinden veritabanına bağlanmak gerekiyorsa, oluşturmalısınız bir [ayrılmış IP](../virtual-network/virtual-networks-reserved-public-ip.md) ve yalnızca ayrılmış IP adresi erişim güvenlik duvarı aracılığıyla izin verin.</span><span class="sxs-lookup"><span data-stu-id="154a5-127">If you need to connect to the database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only the reserved IP address access through the firewall.</span></span> 

<span data-ttu-id="154a5-128">Oluşturmak için bu adımları bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) sunucunuz belirli bir IP adresinden gelen bağlantılara izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="154a5-128">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="154a5-129">Önceki öğreticileri veya quickstarts birini kullanarak Azure'da bir örnek veritabanı oluşturdunuz ve bu öğreticileri gitti sırasındaki aynı IP adresine sahip bir bilgisayarda bu öğreticiyi gerçekleştirmeden, sunucu düzeyinde güvenlik duvarı kuralı oluşturmuş şekilde, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="154a5-129">If you have created a sample database in Azure using one of the previous tutorials or quickstarts and are performing this tutorial on a computer with the same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="154a5-130">Tıklatın **SQL veritabanları** üzerinde Güvenlik Duvarı'nı yapılandırmak istediğiniz veritabanı kural için tıklatın ve sol taraftaki menüden **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="154a5-130">Click **SQL databases** from the left-hand menu and click the database you would like to configure the firewall rule for on the **SQL databases** page.</span></span> <span data-ttu-id="154a5-131">Veritabanınız için genel bakış sayfası açılır ve tam sunucu adını gösteren (gibi **mynewserver 20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-131">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![sunucu güvenlik duvarı kuralı](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="154a5-133">Önceki görüntüde gösterildiği gibi araç çubuğundaki **sunucu güvenlik duvarı ayarla** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="154a5-133">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="154a5-134">SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="154a5-134">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="154a5-135">Tıklatın **istemci IP'si Ekle** genel portal ile bağlı bilgisayarın IP adresini ekleyin veya güvenlik duvarı kuralı el ile girin ve ardından araç çubuğundaki **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="154a5-135">Click **Add client IP** on the toolbar to add the public IP address of the computer connected to the portal with or enter the firewall rule manually and then click **Save**.</span></span>

      ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="154a5-137">**Tamam**’a tıklayın ve ardından **Güvenlik duvarı ayarları** sayfasını kapatmak için **X** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="154a5-137">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="154a5-138">Şimdi belirtilen IP adresi veya IP adresi aralığı sunucusuyla herhangi bir veritabanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-138">You can now connect to any database in the server with the specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="154a5-139">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="154a5-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="154a5-140">Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-140">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="154a5-141">Bu durumda, BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL veritabanı sunucusuna bağlanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="154a5-141">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="154a5-142">SSMS kullanarak bir veritabanı düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="154a5-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="154a5-143">Veritabanı düzeyinde güvenlik duvarı kurallarını etkinleştirmek, aynı mantıksal sunucu içindeki farklı veritabanları için farklı bir güvenlik duvarı ayarları oluşturma ve taşınabilir - takip etmeleri sırasında veritabanı anlamına gelen güvenlik duvarı kuralları oluşturmak için bir [yük devretme](sql-database-geo-replication-overview.md) yerine SQL server üzerinde depolanıyor.</span><span class="sxs-lookup"><span data-stu-id="154a5-143">Database-level firewall rules enable you to create different firewall settings for different databases within the same logical server and to create firewall rules that are portable - meaning that they follow the database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on the SQL server.</span></span> <span data-ttu-id="154a5-144">İlk sunucu düzeyinde güvenlik duvarı kuralını yapılandırdıktan sonra veritabanı düzeyinde güvenlik duvarı kuralları yalnızca Transact-SQL deyimi kullanarak yapılandırılmış ve yalnızca olabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured the first server-level firewall rule.</span></span> <span data-ttu-id="154a5-145">Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="154a5-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="154a5-146">Bir veritabanı özel güvenlik duvarı kuralı oluşturmak için şu adımları izler.</span><span class="sxs-lookup"><span data-stu-id="154a5-146">Follows these steps to create a database-specific firewall rule.</span></span>

1. <span data-ttu-id="154a5-147">Örneğin kullanarak, bir veritabanına bağlanmak [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="154a5-147">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="154a5-148">Nesne Gezgini'nde, önce için bir güvenlik duvarı kuralı eklemek istediğiniz veritabanını sağ tıklatın **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="154a5-148">In Object Explorer, right-click on the database you want to add a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="154a5-149">Veritabanınıza bağlı boş bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="154a5-149">A blank query window opens that is connected to your database.</span></span>

3. <span data-ttu-id="154a5-150">Sorgu penceresinde, genel IP adresi IP adresini değiştirin ve aşağıdaki sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="154a5-150">In the query window, modify the IP address to your public IP address and then execute the following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="154a5-151">Araç çubuğunda tıklatın **yürütme** güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="154a5-151">On the toolbar, click **Execute** to create the firewall rule.</span></span>

## <a name="view-how-to-connect-an-application-to-your-database-using-a-secure-connection-string"></a><span data-ttu-id="154a5-152">Güvenli bağlantı dizesi kullanarak veritabanını bir uygulamaya bağlanmak nasıl görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="154a5-152">View how to connect an application to your database using a secure connection string</span></span>

<span data-ttu-id="154a5-153">Bir istemci uygulaması ve SQL veritabanı arasında güvenli, şifreli bir bağlantı sağlamak için bağlantı dizesi için yapılandırılması gerekir:</span><span class="sxs-lookup"><span data-stu-id="154a5-153">To ensure a secure, encrypted connection between a client application and SQL Database, the connection string has to be configured to:</span></span>

- <span data-ttu-id="154a5-154">Şifreli bir bağlantı isteği ve</span><span class="sxs-lookup"><span data-stu-id="154a5-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="154a5-155">Sunucu sertifikası güvenmediğiniz için.</span><span class="sxs-lookup"><span data-stu-id="154a5-155">To not trust the server certificate.</span></span> 

<span data-ttu-id="154a5-156">Bu Aktarım Katmanı Güvenliği (TLS) kullanarak bağlantı kurar ve man-in--middle saldırıları riski azaltılır.</span><span class="sxs-lookup"><span data-stu-id="154a5-156">This establishes a connection using Transport Layer Security (TLS) and reduces the risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="154a5-157">Doğru yapılandırılmış bağlantı dizeleri desteklenen istemci için SQL veritabanınızın sürücüleri Azure portalından ADO.net için bu ekran görüntüsünde gösterildiği gibi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="154a5-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from the Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="154a5-158">Seçin **SQL veritabanları** sol taraftaki menüden ve veritabanınızı tıklayın **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="154a5-158">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span>

2. <span data-ttu-id="154a5-159">Üzerinde **genel bakış** sayfasında veritabanınız için **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="154a5-159">On the **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="154a5-160">Tam **ADO.NET** bağlantı dizesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="154a5-160">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesi](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="154a5-162">Veritabanı kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="154a5-162">Creating database users</span></span>

<span data-ttu-id="154a5-163">Herhangi bir kullanıcı oluşturmadan önce ilk Azure SQL veritabanı tarafından desteklenen iki kimlik doğrulama türleri birini seçmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="154a5-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="154a5-164">**SQL kimlik doğrulaması**, kullanan kullanıcı adı ve parola oturum açmalar ve yalnızca bir mantıksal sunucu içinde belirli bir veritabanı bağlamında geçerli olan kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="154a5-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in the context of a specific database within a logical server.</span></span> 

<span data-ttu-id="154a5-165">**Azure Active Directory kimlik doğrulaması**, Azure Active Directory tarafından yönetilen kimlikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="154a5-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="154a5-166">Kullanmak istiyorsanız, [Azure Active Directory](./sql-database-aad-authentication.md) devam etmeden önce SQL veritabanında kimlik doğrulaması için doldurulan bir Azure Active Directory bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="154a5-166">If you want to use [Azure Active Directory](./sql-database-aad-authentication.md) to authenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="154a5-167">SQL kimlik doğrulaması kullanarak bir kullanıcı oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="154a5-167">Follow these steps to create a user using SQL Authentication:</span></span>

1. <span data-ttu-id="154a5-168">Örneğin kullanarak, bir veritabanına bağlanmak [SQL Server Management Studio](./sql-database-connect-query-ssms.md) server yönetici kimlik bilgilerinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="154a5-168">Connect to your database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="154a5-169">Nesne Gezgini'nde, önce yeni bir kullanıcı eklemek istediğiniz veritabanını sağ tıklatın **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="154a5-169">In Object Explorer, right-click on the database you want to add a new user on and click **New Query**.</span></span> <span data-ttu-id="154a5-170">Seçilen veritabanına bağlı bir boş sorgu penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="154a5-170">A blank query window opens that is connected to the selected database.</span></span>

3. <span data-ttu-id="154a5-171">Sorgu penceresine aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="154a5-171">In the query window, enter the following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="154a5-172">Araç çubuğunda tıklatın **yürütme** kullanıcı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="154a5-172">On the toolbar, click **Execute** to create the user.</span></span>

5. <span data-ttu-id="154a5-173">Varsayılan olarak, kullanıcının veritabanına bağlanabilirsiniz, ancak okuma veya veri yazma izni olduğundan.</span><span class="sxs-lookup"><span data-stu-id="154a5-173">By default, the user can connect to the database, but has no permissions to read or write data.</span></span> <span data-ttu-id="154a5-174">Yeni oluşturulan kullanıcı bu izinleri vermek için yeni bir sorgu penceresinde aşağıdaki iki komutu yürütme</span><span class="sxs-lookup"><span data-stu-id="154a5-174">To grant these permissions to the newly created user, execute the following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="154a5-175">Yeni kullanıcılar oluşturma gibi yönetici görevleri çalıştırmak gerekli olmadıkça, veritabanına bağlanmak için veritabanı düzeyinde bu yönetici olmayan bir hesap oluşturmak için en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="154a5-175">It is best practice to create these non-administrator accounts at the database level to connect to your database unless you need to execute administrator tasks like creating new users.</span></span> <span data-ttu-id="154a5-176">Lütfen gözden [Azure Active Directory öğretici](./sql-database-aad-authentication-configure.md) Azure Active Directory'yi kullanarak kimlik doğrulaması yapmayı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="154a5-176">Please review the [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how to authenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="154a5-177">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="154a5-177">Protect your data with encryption</span></span>

<span data-ttu-id="154a5-178">Azure SQL veritabanında saydam veri şifreleme (TDE) şifrelenmiş veritabanına erişen uygulama herhangi bir değişiklik gerektirmeden verilerinizi REST, otomatik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="154a5-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes to the application accessing the encrypted database.</span></span> <span data-ttu-id="154a5-179">Yeni oluşturulan veritabanları için TDE varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="154a5-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="154a5-180">Veritabanınız için TDE etkinleştirmek ya da TDE açık olduğunu doğrulamak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="154a5-180">To enable TDE for your database or to verify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="154a5-181">Seçin **SQL veritabanları** sol taraftaki menüden ve veritabanınızı tıklayın **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="154a5-181">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="154a5-182">Tıklayın **saydam veri şifreleme** TDE için yapılandırma sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="154a5-182">Click on **Transparent data encryption** to open the configuration page for TDE.</span></span>

    ![Saydam Veri Şifrelemesi](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="154a5-184">Gerekirse, ayarlamak **veri şifreleme** on tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="154a5-184">If necessary, set **Data encryption** to ON and click **Save**.</span></span>

<span data-ttu-id="154a5-185">Şifreleme işlemi arka planda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="154a5-185">The encryption process starts in the background.</span></span> <span data-ttu-id="154a5-186">SQL veritabanı için kullanılacak bağlanarak ilerleme durumunu izleyebilirsiniz [SQL Server Management Studio](./sql-database-connect-query-ssms.md) encryption_state sütunu sorgulamak `sys.dm_database_encryption_keys` görünümü.</span><span class="sxs-lookup"><span data-stu-id="154a5-186">You can monitor the progress by connecting to SQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying the encryption_state column of the `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="154a5-187">SQL veritabanı denetimi, gerekirse etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="154a5-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="154a5-188">Azure SQL veritabanı denetimi veritabanı olaylarını ve Azure depolama hesabınızdaki bunları Denetim günlüğüne yazar izler.</span><span class="sxs-lookup"><span data-stu-id="154a5-188">Azure SQL Database Auditing tracks database events and writes them to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="154a5-189">Denetim, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve olası güvenlik ihlallerini gösterebilir anormallikleri kavramanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="154a5-190">Denetim İlkesi SQL veritabanınız için bir varsayılan oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="154a5-190">Follow these steps to create a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="154a5-191">Seçin **SQL veritabanları** sol taraftaki menüden ve veritabanınızı tıklayın **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="154a5-191">Select **SQL databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 

2. <span data-ttu-id="154a5-192">Ayarlar dikey penceresinde seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="154a5-192">In the Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="154a5-193">Bildirim olduğunu ve sunucu düzeyi denetimi devre: bir **sunucu ayarlarını görüntüleyin** bağlantı görüntülemek veya sunucunun denetim ayarları'nı bu bağlamından değiştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you to view or modify the server auditing settings from this context.</span></span>

    ![Denetim dikey penceresi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="154a5-195">Bir denetim türü (veya konum?) etkinleştirmeyi tercih ediyorsanız olandan farklı sunucu düzeyinde belirtilen, kapatma **ON** denetleme ve **Blob** denetim türü.</span><span class="sxs-lookup"><span data-stu-id="154a5-195">If you prefer to enable an Audit type (or location?) different from the one specified at the server level, turn **ON** Auditing, and choose the **Blob** Auditing Type.</span></span> <span data-ttu-id="154a5-196">Sunucu Blob denetimi etkinse, yapılandırılmış veritabanı denetimi yan yana sunucu Blob denetim yer alır.</span><span class="sxs-lookup"><span data-stu-id="154a5-196">If server Blob auditing is enabled, the database configured audit will exist side by side with the server Blob audit.</span></span>

    ![Denetim Aç](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="154a5-198">Seçin **depolama ayrıntıları** denetim günlüklerini depolama dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="154a5-198">Select **Storage Details** to open the Audit Logs Storage Blade.</span></span> <span data-ttu-id="154a5-199">Burada günlüklerine kaydedilir ve daha sonra eski günlükleri silinecek, saklama dönemi, ardından Azure depolama hesabı seçin **Tamam** altındaki.</span><span class="sxs-lookup"><span data-stu-id="154a5-199">Select the Azure storage account where logs will be saved, and the retention period, after which the old logs will be deleted, then click **OK** at the bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="154a5-200">En iyi denetim raporları şablonları almak için tüm denetlenen veritabanları için aynı depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="154a5-200">Use the same storage account for all audited databases to get the most out of the auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="154a5-201">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="154a5-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="154a5-202">Denetlenen olayları özelleştirmek istiyorsanız, PowerShell veya REST API - bunu yapabilirsiniz bkz [Otomasyon (PowerShell / REST API)](sql-database-auditing.md#subheading-7) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="154a5-202">If you want to customize the audited events, you can do this via PowerShell or REST API - see the [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="154a5-203">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="154a5-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="154a5-204">Tehdit algılama, müşterilerin algılamak ve anormal etkinlikler güvenlik uyarıları sağlayarak göründüklerinde olası risklere yanıt sağlayan bir güvenlik yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-204">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="154a5-205">Kullanıcılar, bunlar erişim, ihlal ya da veritabanındaki verileri yararlanma girişimi sonucu olmadığını belirlemek için SQL veritabanı denetimi kullanarak şüpheli olayları gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="154a5-205">Users can explore the suspicious events using SQL Database Auditing to determine if they result from an attempt to access, breach or exploit data in the database.</span></span> <span data-ttu-id="154a5-206">Tehdit algılama, veritabanına Uzman güvenlik olması veya sistemleri izleme Gelişmiş Güvenlik yönetmek zorunda kalmadan adresi olası tehditlere kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="154a5-206">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="154a5-207">Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="154a5-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="154a5-208">SQL ekleme veri güdümlü uygulamaları saldırmak için kullanılıyorsa Internet üzerinde ortak Web uygulaması güvenlik sorunlarını biridir.</span><span class="sxs-lookup"><span data-stu-id="154a5-208">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="154a5-209">Saldırganlar ihlal veya veritabanındaki verileri değiştirmek için uygulama giriş alanları, kötü amaçlı SQL deyimleri eklemesine uygulama güvenlik açıkları yararlanın.</span><span class="sxs-lookup"><span data-stu-id="154a5-209">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

1. <span data-ttu-id="154a5-210">İzlemek istediğiniz SQL veritabanı yapılandırma dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="154a5-210">Navigate to the configuration blade of the SQL database you want to monitor.</span></span> <span data-ttu-id="154a5-211">Ayarlar dikey penceresinde seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="154a5-211">In the Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="154a5-213">İçinde **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler tehdit algılama ayarlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-213">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the threat detection settings.</span></span>

3. <span data-ttu-id="154a5-214">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="154a5-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="154a5-215">Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="154a5-215">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="154a5-216">Tıklatın **kaydetmek** içinde **denetim ve tehdit algılama** yeni veya güncelleştirilmiş denetim kaydedin ve tehdit algılama İlkesi dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="154a5-216">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection policy.</span></span>

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="154a5-218">Anormal veritabanı etkinliklerini algılanmazsa, anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="154a5-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="154a5-219">E-posta anormal etkinlikler, veritabanı adı, sunucu adını ve olay süresi yapısını dahil olmak üzere şüpheli güvenlik olayı üzerinde bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="154a5-219">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="154a5-220">Ayrıca, olası nedenler bilgileri sağlarız ve önerilen eylemleri araştırmak ve veritabanına olası tehdidi azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="154a5-220">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span> <span data-ttu-id="154a5-221">Sonraki adımlarda size yol yapmanız gerekenler aracılığıyla gibi e-posta almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="154a5-221">The next steps walk you through what to do should you receive such an email:</span></span>

    ![Tehdit algılama e-posta](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="154a5-223">E-posta ile tıklayın **Azure SQL denetim günlüğü** bağlantı, hangi Azure Portalı'nı başlatın ve ilgili denetim kayıtları şüpheli olay sırada geçici gösterir.</span><span class="sxs-lookup"><span data-stu-id="154a5-223">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure portal and show the relevant auditing records around the time of the suspicious event.</span></span>

    ![Denetim kaydı](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="154a5-225">Denetim kayıtlarının SQL deyimini gibi şüpheli veritabanı etkinlikleri hakkında daha fazla ayrıntı görüntülemek için tıklatın başarısızlık nedeni ve istemci IP.</span><span class="sxs-lookup"><span data-stu-id="154a5-225">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Kayıt ayrıntıları](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="154a5-227">Denetim kayıtlarının dikey penceresinde tıklayın **Excel'de açın** açmak için önceden yapılandırılmış excel almak ve daha derin denetim günlüğü şüpheli olay sırada geçici analizini çalıştırmak için şablon.</span><span class="sxs-lookup"><span data-stu-id="154a5-227">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="154a5-228">Excel 2010 veya üzeri, güç sorgu ve **hızlı Birleştir** ayarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="154a5-228">In Excel 2010 or later, Power Query and the **Fast Combine** setting is required.</span></span>

    ![Kayıtları Excel'de Aç](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="154a5-230">Yapılandırmak için **hızlı Birleştir** - ayarlamayı **POWER QUERY** Şerit sekmesi, select **seçenekleri** Seçenekleri iletişim kutusunu görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="154a5-230">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="154a5-231">Gizlilik bölümünü seçin ve ikinci seçeneği 'Gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' - belirtin:</span><span class="sxs-lookup"><span data-stu-id="154a5-231">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>

    ![Excel hızlı Birleştir](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="154a5-233">SQL denetim günlüklerini yüklemek için sekme doğru ayarlandığından ve 'Data' Şerit'i seçin ve 'Tümünü Yenile' düğmesini tıklatın ayarlarını parametrelerinde emin olun.</span><span class="sxs-lookup"><span data-stu-id="154a5-233">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>

    ![Excel parametreleri](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="154a5-235">Sonuçları görünür **SQL denetim günlüklerini** algılandı anormal etkinlikler daha derin çözümlenmesi çalıştırın ve güvenlik olay uygulamanızda etkisini olanak tanıyan sayfası.</span><span class="sxs-lookup"><span data-stu-id="154a5-235">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="154a5-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="154a5-236">Next steps</span></span>
<span data-ttu-id="154a5-237">Veritabanınızı kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı koruma artırabilir.</span><span class="sxs-lookup"><span data-stu-id="154a5-237">You can improve the protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="154a5-238">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="154a5-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="154a5-239">Sunucu ve veya veritabanı için güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="154a5-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="154a5-240">Güvenli bağlantı dizesi kullanarak veritabanınıza bağlanmak</span><span class="sxs-lookup"><span data-stu-id="154a5-240">Connect to your database using a secure connection string</span></span>
> * <span data-ttu-id="154a5-241">Kullanıcı erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="154a5-241">Manage user access</span></span>
> * <span data-ttu-id="154a5-242">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="154a5-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="154a5-243">SQL veritabanı denetimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="154a5-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="154a5-244">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="154a5-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="154a5-245">SQL Veritabanı performansını iyileştirme</span><span class="sxs-lookup"><span data-stu-id="154a5-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

