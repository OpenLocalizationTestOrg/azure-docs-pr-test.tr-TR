---
title: "aaaSecure Azure SQL veritabanınızı | Microsoft Docs"
description: "Azure SQL veritabanınızı teknikler ve Özellikler toosecure hakkında bilgi edinin."
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
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a><span data-ttu-id="c4b42-103">Azure SQL veritabanınızı güvenli</span><span class="sxs-lookup"><span data-stu-id="c4b42-103">Secure your Azure SQL Database</span></span>

<span data-ttu-id="c4b42-104">SQL veritabanı güvenlik duvarı kuralları, kullanıcıların tooprove kendi kimlik ve yetkilendirme toodata üyeliklerini rol tabanlı ve izinleri aracılığıyla yanı sıra aracılığıyla gerektiren kimlik doğrulama mekanizmaları kullanarak erişim tooyour veritabanı sınırlandırarak verilerinizi korur satır düzeyi güvenlik ve dinamik veri maskeleme.</span><span class="sxs-lookup"><span data-stu-id="c4b42-104">SQL Database secures your data by limiting access tooyour database using firewall rules, authentication mechanisms requiring users tooprove their identity, and authorization toodata through role-based memberships and permissions, as well as through row-level security and dynamic data masking.</span></span>

<span data-ttu-id="c4b42-105">Kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı veritabanınızın hello koruma artırabilir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-105">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="c4b42-106">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-106">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c4b42-107">Sunucunuzdaki hello Azure portal için sunucu düzeyinde güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c4b42-107">Set up server-level firewall rules for your server in hello Azure portal</span></span>
> * <span data-ttu-id="c4b42-108">SSMS kullanarak, veritabanı için veritabanı düzeyinde güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c4b42-108">Set up database-level firewall rules for your database using SSMS</span></span>
> * <span data-ttu-id="c4b42-109">Güvenli bağlantı dizesi kullanarak tooyour veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="c4b42-109">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="c4b42-110">Kullanıcı erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="c4b42-110">Manage user access</span></span>
> * <span data-ttu-id="c4b42-111">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="c4b42-111">Protect your data with encryption</span></span>
> * <span data-ttu-id="c4b42-112">SQL veritabanı denetimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c4b42-112">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="c4b42-113">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c4b42-113">Enable SQL Database threat detection</span></span>

<span data-ttu-id="c4b42-114">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="c4b42-114">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b42-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c4b42-115">Prerequisites</span></span>

<span data-ttu-id="c4b42-116">toocomplete Bu öğretici, yapma emin aşağıdaki hello sahip:</span><span class="sxs-lookup"><span data-stu-id="c4b42-116">toocomplete this tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="c4b42-117">Yüklü hello en yeni sürümünü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="c4b42-117">Installed hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> 
- <span data-ttu-id="c4b42-118">Yüklü Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="c4b42-118">Installed Microsoft Excel</span></span>
- <span data-ttu-id="c4b42-119">Bir Azure SQL server ve veritabanı - oluşturulan bkz [hello Azure portalında bir Azure SQL veritabanı oluşturma](sql-database-get-started-portal.md), [hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma](sql-database-get-started-cli.md), ve [tek bir Azure SQL oluşturma PowerShell kullanarak veritabanı](sql-database-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c4b42-119">Created an Azure SQL server and database - See [Create an Azure SQL database in hello Azure portal](sql-database-get-started-portal.md), [Create a single Azure SQL database using hello Azure CLI](sql-database-get-started-cli.md), and [Create a single Azure SQL database using PowerShell](sql-database-get-started-powershell.md).</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="c4b42-120">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="c4b42-120">Log in toohello Azure portal</span></span>

<span data-ttu-id="c4b42-121">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4b42-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="c4b42-122">Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4b42-122">Create a server-level firewall rule in hello Azure portal</span></span>

<span data-ttu-id="c4b42-123">SQL veritabanları Azure güvenlik duvarı tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="c4b42-123">SQL databases are protected by a firewall in Azure.</span></span> <span data-ttu-id="c4b42-124">Varsayılan olarak, diğer Azure hizmetleriyle bağlantılarından hariç tüm bağlantıları toohello sunucusu ve hello veritabanları hello Sunucusu'ndaki reddedilir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-124">By default, all connections toohello server and hello databases inside hello server are rejected except for connections from other Azure services.</span></span> <span data-ttu-id="c4b42-125">Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c4b42-125">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="c4b42-126">Merhaba en güvenli tooset 'tooAzure Hizmetleri erişime izin ver' tooOFF yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-126">hello most secure configuration is tooset 'Allow access tooAzure services' tooOFF.</span></span> <span data-ttu-id="c4b42-127">Bir Azure VM veya Bulut hizmeti tooconnect toohello veritabanından gerekiyorsa, oluşturmalısınız bir [ayrılmış IP](../virtual-network/virtual-networks-reserved-public-ip.md) ve yalnızca hello ayrılmış IP adresi erişim hello güvenlik duvarı aracılığıyla izin verin.</span><span class="sxs-lookup"><span data-stu-id="c4b42-127">If you need tooconnect toohello database from an Azure VM or cloud service, you should create a [Reserved IP](../virtual-network/virtual-networks-reserved-public-ip.md) and allow only hello reserved IP address access through hello firewall.</span></span> 

<span data-ttu-id="c4b42-128">Bu adımları toocreate izleyin bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) belirli bir IP adresi, sunucu tooallow bağlantıları için.</span><span class="sxs-lookup"><span data-stu-id="c4b42-128">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server tooallow connections from a specific IP address.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4b42-129">Azure'da hello önceki öğreticiler veya quickstarts ve misiniz birini kullanarak bir örnek veritabanı oluşturduysanız hello olan bir bilgisayarda bu öğreticiyi gerçekleştirmeden aynı IP adresi, BT'nin sahip şekilde bu öğreticileri gitti aldığında sahip, bu adımı atlayabilirsiniz zaten bir sunucu düzeyinde güvenlik duvarı kuralı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="c4b42-129">If you have created a sample database in Azure using one of hello previous tutorials or quickstarts and are performing this tutorial on a computer with hello same IP address that it had when you walked through those tutorials, you can skip this step as you will have already created a server-level firewall rule.</span></span>
>

1. <span data-ttu-id="c4b42-130">Tıklatın **SQL veritabanları** hello sol menüsüne ve ardından hello veritabanından tooconfigure hello güvenlik duvarı kuralı için başlangıç istediğiniz **SQL veritabanları** sayfa.</span><span class="sxs-lookup"><span data-stu-id="c4b42-130">Click **SQL databases** from hello left-hand menu and click hello database you would like tooconfigure hello firewall rule for on hello **SQL databases** page.</span></span> <span data-ttu-id="c4b42-131">Merhaba hello tam olarak gösteren, veritabanı açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver 20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-131">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![sunucu güvenlik duvarı kuralı](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. <span data-ttu-id="c4b42-133">Tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello önceki görüntüde gösterildiği gibi hello araç.</span><span class="sxs-lookup"><span data-stu-id="c4b42-133">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="c4b42-134">Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-134">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

3. <span data-ttu-id="c4b42-135">Tıklatın **istemci IP'si Ekle** üzerinde hello araç tooadd hello genel IP adresi hello bilgisayar bağlı toohello portalıyla veya hello güvenlik duvarı kuralı el ile girin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-135">Click **Add client IP** on hello toolbar tooadd hello public IP address of hello computer connected toohello portal with or enter hello firewall rule manually and then click **Save**.</span></span>

      ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. <span data-ttu-id="c4b42-137">Tıklatın **Tamam** ve hello ardından **X** tooclose hello **Güvenlik Duvarı ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-137">Click **OK** and then click hello **X** tooclose hello **Firewall settings** page.</span></span>

<span data-ttu-id="c4b42-138">Belirtilen hello ile Merhaba Server'daki tooany veritabanı artık bağlanabilir IP adresi veya IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="c4b42-138">You can now connect tooany database in hello server with hello specified IP address or IP address range.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b42-139">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-139">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="c4b42-140">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="c4b42-140">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c4b42-141">Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="c4b42-141">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a><span data-ttu-id="c4b42-142">SSMS kullanarak bir veritabanı düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4b42-142">Create a database-level firewall rule using SSMS</span></span>

<span data-ttu-id="c4b42-143">Veritabanı düzeyinde güvenlik duvarı kuralları aynı mantıksal sunucu ve toocreate güvenlik duvarı kuralları, taşınabilir - takip etmeleri sırasında hello veritabanı anlamı hello içinde farklı veritabanları için toocreate farklı bir güvenlik duvarı ayarlarını etkinleştir bir [yük devretme ](sql-database-geo-replication-overview.md) hello SQL sunucusunda depolanıp depolanmadığı yerine.</span><span class="sxs-lookup"><span data-stu-id="c4b42-143">Database-level firewall rules enable you toocreate different firewall settings for different databases within hello same logical server and toocreate firewall rules that are portable - meaning that they follow hello database during a [failover](sql-database-geo-replication-overview.md) rather than being stored on hello SQL server.</span></span> <span data-ttu-id="c4b42-144">Merhaba ilk sunucu düzeyinde güvenlik duvarı kuralını yapılandırdıktan sonra veritabanı düzeyinde güvenlik duvarı kuralları yalnızca Transact-SQL deyimi kullanarak yapılandırılmış ve yalnızca olabilir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-144">Database-level firewall rules can only be configured by using Transact-SQL statements and only after you have configured hello first server-level firewall rule.</span></span> <span data-ttu-id="c4b42-145">Daha fazla bilgi için bkz: [Azure SQL veritabanı sunucusu ve veritabanı düzeyi güvenlik duvarı kuralları](sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c4b42-145">For more information, see [Azure SQL Database server-level and database-level firewall rules](sql-database-firewall-configure.md).</span></span>

<span data-ttu-id="c4b42-146">Bu adımları toocreate bir veritabanı özel güvenlik duvarı kuralı izler.</span><span class="sxs-lookup"><span data-stu-id="c4b42-146">Follows these steps toocreate a database-specific firewall rule.</span></span>

1. <span data-ttu-id="c4b42-147">Örneğin kullanarak tooyour veritabanı bağlantı [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="c4b42-147">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md).</span></span>

2. <span data-ttu-id="c4b42-148">Bir güvenlik duvarı için kural ve tıklatın tooadd istediğiniz hello veritabanında nesne Gezgini'nde sağ **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-148">In Object Explorer, right-click on hello database you want tooadd a firewall rule for and click **New Query**.</span></span> <span data-ttu-id="c4b42-149">Boş sorgu penceresi bağlı tooyour veritabanını başka bir deyişle açar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-149">A blank query window opens that is connected tooyour database.</span></span>

3. <span data-ttu-id="c4b42-150">Merhaba sorgu penceresinde hello IP adresi tooyour ortak IP adresini değiştirmek ve sorgu aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="c4b42-150">In hello query window, modify hello IP address tooyour public IP address and then execute hello following query:</span></span>

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. <span data-ttu-id="c4b42-151">Merhaba araç çubuğundan, **yürütme** toocreate hello güvenlik duvarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="c4b42-151">On hello toolbar, click **Execute** toocreate hello firewall rule.</span></span>

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a><span data-ttu-id="c4b42-152">Bir uygulama tooyour tooconnect nasıl veritabanı güvenli bağlantı dizesi kullanarak görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c4b42-152">View how tooconnect an application tooyour database using a secure connection string</span></span>

<span data-ttu-id="c4b42-153">tooensure bir istemci uygulaması ve SQL veritabanı arasında güvenli, şifreli bir bağlantı, hello bağlantı dizesi için yapılandırılmış toobe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c4b42-153">tooensure a secure, encrypted connection between a client application and SQL Database, hello connection string has toobe configured to:</span></span>

- <span data-ttu-id="c4b42-154">Şifreli bir bağlantı isteği ve</span><span class="sxs-lookup"><span data-stu-id="c4b42-154">Request an encrypted connection, and</span></span>
- <span data-ttu-id="c4b42-155">toonot güven hello sunucu sertifikası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-155">toonot trust hello server certificate.</span></span> 

<span data-ttu-id="c4b42-156">Bu Aktarım Katmanı Güvenliği (TLS) kullanarak bağlantı kurar ve man-in--middle saldırıları hello riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-156">This establishes a connection using Transport Layer Security (TLS) and reduces hello risk of man-in-the-middle attacks.</span></span> <span data-ttu-id="c4b42-157">Doğru yapılandırılmış bağlantı dizeleri desteklenen istemci için SQL veritabanınızın sürücüleri hello Azure portal ' ADO.net için bu ekran görüntüsünde gösterildiği gibi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4b42-157">You can obtain correctly configured connection strings for your SQL Database for supported client drivers from hello Azure portal as shown for ADO.net in this screenshot.</span></span>

1. <span data-ttu-id="c4b42-158">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-158">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span>

2. <span data-ttu-id="c4b42-159">Merhaba üzerinde **genel bakış** sayfasında veritabanınız için **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-159">On hello **Overview** page for your database, click **Show database connection strings**.</span></span>

3. <span data-ttu-id="c4b42-160">Gözden geçirme hello tam **ADO.NET** bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="c4b42-160">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET bağlantı dizesi](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a><span data-ttu-id="c4b42-162">Veritabanı kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4b42-162">Creating database users</span></span>

<span data-ttu-id="c4b42-163">Herhangi bir kullanıcı oluşturmadan önce ilk Azure SQL veritabanı tarafından desteklenen iki kimlik doğrulama türleri birini seçmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4b42-163">Before creating any users, you must first choose from one of two authentication types supported by Azure SQL Database:</span></span> 

<span data-ttu-id="c4b42-164">**SQL kimlik doğrulaması**kullanan kullanıcı adı ve parola oturumları için ve yalnızca, geçerli olan kullanıcılar bir mantıksal sunucu içinde belirli bir veritabanı bağlamında hello.</span><span class="sxs-lookup"><span data-stu-id="c4b42-164">**SQL Authentication**, which uses username and password for logins and users that are valid only in hello context of a specific database within a logical server.</span></span> 

<span data-ttu-id="c4b42-165">**Azure Active Directory kimlik doğrulaması**, Azure Active Directory tarafından yönetilen kimlikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-165">**Azure Active Directory Authentication**, which uses identities managed by Azure Active Directory.</span></span> 

<span data-ttu-id="c4b42-166">Toouse istiyorsanız [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate SQL veritabanında doldurulan bir Azure Active Directory devam etmeden önce bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-166">If you want toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate against SQL Database, a populated Azure Active Directory must exist before you can proceed.</span></span>

<span data-ttu-id="c4b42-167">Bu adımları toocreate SQL kimlik doğrulaması kullanan bir kullanıcının izleyin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-167">Follow these steps toocreate a user using SQL Authentication:</span></span>

1. <span data-ttu-id="c4b42-168">Örneğin kullanarak tooyour veritabanı bağlantı [SQL Server Management Studio](./sql-database-connect-query-ssms.md) server yönetici kimlik bilgilerinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c4b42-168">Connect tooyour database, for example using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) using your server admin credentials.</span></span>

2. <span data-ttu-id="c4b42-169">Nesne Gezgini'nde üzerinde üzerinde yeni bir kullanıcı tooadd istediğiniz hello veritabanını sağ tıklatın **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-169">In Object Explorer, right-click on hello database you want tooadd a new user on and click **New Query**.</span></span> <span data-ttu-id="c4b42-170">Boş sorgu penceresi, diğer bir deyişle bağlı toohello seçili veritabanı açılır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-170">A blank query window opens that is connected toohello selected database.</span></span>

3. <span data-ttu-id="c4b42-171">Merhaba sorgu penceresinde, sorgu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-171">In hello query window, enter hello following query:</span></span>

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. <span data-ttu-id="c4b42-172">Merhaba araç çubuğundan, **yürütme** toocreate hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c4b42-172">On hello toolbar, click **Execute** toocreate hello user.</span></span>

5. <span data-ttu-id="c4b42-173">Varsayılan olarak, hello kullanıcı toohello veritabanı bağlanabilirsiniz, ancak izinleri tooread veya yazma veri yok.</span><span class="sxs-lookup"><span data-stu-id="c4b42-173">By default, hello user can connect toohello database, but has no permissions tooread or write data.</span></span> <span data-ttu-id="c4b42-174">toogrant bu izinleri toohello yeni oluşturulan kullanıcı, aşağıdaki iki komutu yeni bir sorgu penceresinde hello yürütme</span><span class="sxs-lookup"><span data-stu-id="c4b42-174">toogrant these permissions toohello newly created user, execute hello following two commands in a new query window</span></span>

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

<span data-ttu-id="c4b42-175">Bu yönetici olmayan hesaplar hello veritabanı düzeyi tooconnect tooyour en yeni kullanıcılar oluşturma gibi tooexecute yönetici görevleri gerekmedikçe veritabanı en iyi yöntem toocreate olur.</span><span class="sxs-lookup"><span data-stu-id="c4b42-175">It is best practice toocreate these non-administrator accounts at hello database level tooconnect tooyour database unless you need tooexecute administrator tasks like creating new users.</span></span> <span data-ttu-id="c4b42-176">Lütfen hello gözden [Azure Active Directory öğretici](./sql-database-aad-authentication-configure.md) nasıl Azure Active Directory'yi kullanarak tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="c4b42-176">Please review hello [Azure Active Directory tutorial](./sql-database-aad-authentication-configure.md) on how tooauthenticate using Azure Active Directory.</span></span>


## <a name="protect-your-data-with-encryption"></a><span data-ttu-id="c4b42-177">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="c4b42-177">Protect your data with encryption</span></span>

<span data-ttu-id="c4b42-178">Azure SQL veritabanında saydam veri şifreleme (TDE) tüm değişiklikleri toohello uygulama hello şifrelenmiş veritabanı erişimi gerek kalmadan, rest, verileri otomatik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="c4b42-178">Azure SQL Database transparent data encryption (TDE) automatically encrypts your data at rest, without requiring any changes toohello application accessing hello encrypted database.</span></span> <span data-ttu-id="c4b42-179">Yeni oluşturulan veritabanları için TDE varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-179">For newly created databases, TDE is on by default.</span></span> <span data-ttu-id="c4b42-180">tooenable TDE veritabanı veya TDE açıktır tooverify için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-180">tooenable TDE for your database or tooverify that TDE is on, follow these steps:</span></span>

1. <span data-ttu-id="c4b42-181">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-181">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="c4b42-182">Tıklayın **saydam veri şifreleme** TDE için tooopen hello yapılandırma sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-182">Click on **Transparent data encryption** tooopen hello configuration page for TDE.</span></span>

    ![Saydam Veri Şifrelemesi](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. <span data-ttu-id="c4b42-184">Gerekirse, ayarlamak **veri şifreleme** tooON tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-184">If necessary, set **Data encryption** tooON and click **Save**.</span></span>

<span data-ttu-id="c4b42-185">Merhaba arka planda Hello şifreleme işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-185">hello encryption process starts in hello background.</span></span> <span data-ttu-id="c4b42-186">Bağlantı tooSQL veritabanını kullanarak hello ilerlemesini izleyebilirsiniz [SQL Server Management Studio](./sql-database-connect-query-ssms.md) hello hello encryption_state sütunu sorgulamak `sys.dm_database_encryption_keys` görünümü.</span><span class="sxs-lookup"><span data-stu-id="c4b42-186">You can monitor hello progress by connecting tooSQL Database using [SQL Server Management Studio](./sql-database-connect-query-ssms.md) by querying hello encryption_state column of hello `sys.dm_database_encryption_keys` view.</span></span>

## <a name="enable-sql-database-auditing-if-necessary"></a><span data-ttu-id="c4b42-187">SQL veritabanı denetimi, gerekirse etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c4b42-187">Enable SQL Database auditing, if necessary</span></span>

<span data-ttu-id="c4b42-188">Azure SQL veritabanı denetimi veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-188">Azure SQL Database Auditing tracks database events and writes them tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="c4b42-189">Denetim, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve olası güvenlik ihlallerini gösterebilir anormallikleri kavramanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-189">Auditing can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate potential security violations.</span></span> <span data-ttu-id="c4b42-190">Bu adımları toocreate SQL veritabanınız için varsayılan bir denetim ilkesini izleyin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-190">Follow these steps toocreate a default auditing policy for your SQL database:</span></span>

1. <span data-ttu-id="c4b42-191">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-191">Select **SQL databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

2. <span data-ttu-id="c4b42-192">Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-192">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> <span data-ttu-id="c4b42-193">Bildirim olduğunu ve sunucu düzeyi denetimi devre: bir **sunucu ayarlarını görüntüleyin** bağlantıyı tooview sağlar veya bu bağlamından hello sunucu denetim ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c4b42-193">Notice that sever-level auditing is diabled and that there is a **View server settings** link that allows you tooview or modify hello server auditing settings from this context.</span></span>

    ![Denetim dikey penceresi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. <span data-ttu-id="c4b42-195">Tooenable bir denetim türü (veya konum?) tercih ederseniz hello bir hello sunucu düzeyinde belirtilen farklı Aç **ON** denetleme ve hello seçin **Blob** denetim türü.</span><span class="sxs-lookup"><span data-stu-id="c4b42-195">If you prefer tooenable an Audit type (or location?) different from hello one specified at hello server level, turn **ON** Auditing, and choose hello **Blob** Auditing Type.</span></span> <span data-ttu-id="c4b42-196">Sunucu Blob denetimi etkinse hello yapılandırılmış veritabanı denetimi hello sunucu Blob denetim yan yana yer alır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-196">If server Blob auditing is enabled, hello database configured audit will exist side by side with hello server Blob audit.</span></span>

    ![Denetim Aç](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. <span data-ttu-id="c4b42-198">Seçin **depolama ayrıntıları** tooopen hello denetim günlüklerini depolama dikey.</span><span class="sxs-lookup"><span data-stu-id="c4b42-198">Select **Storage Details** tooopen hello Audit Logs Storage Blade.</span></span> <span data-ttu-id="c4b42-199">Burada günlükleri kaydedilecek select hello Azure depolama hesabı ve hello saklama dönemi, hangi hello sonra eski günlükleri silinecek, ardından **Tamam** hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="c4b42-199">Select hello Azure storage account where logs will be saved, and hello retention period, after which hello old logs will be deleted, then click **OK** at hello bottom.</span></span> 

   > [!TIP]
   > <span data-ttu-id="c4b42-200">Kullanım hello aynı depolama hesabı en hello denetimi dışında tüm denetlenen veritabanları tooget hello için raporları şablonları.</span><span class="sxs-lookup"><span data-stu-id="c4b42-200">Use hello same storage account for all audited databases tooget hello most out of hello auditing reports templates.</span></span>
   > 

5. <span data-ttu-id="c4b42-201">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4b42-201">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4b42-202">Toocustomize denetlenen hello olayları istiyorsanız, PowerShell veya REST API - bunu yapabilirsiniz hello bkz [Otomasyon (PowerShell / REST API)](sql-database-auditing.md#subheading-7) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="c4b42-202">If you want toocustomize hello audited events, you can do this via PowerShell or REST API - see hello [Automation (PowerShell / REST API)](sql-database-auditing.md#subheading-7) section for more details.</span></span>
>

## <a name="enable-sql-database-threat-detection"></a><span data-ttu-id="c4b42-203">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c4b42-203">Enable SQL Database threat detection</span></span>

<span data-ttu-id="c4b42-204">Tehdit algılama müşteriler toodetect sağlar ve güvenlik uyarıları anormal etkinlikler sağlayarak göründüklerinde toopotential tehditlerine yanıt güvenliği, yeni bir katman sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-204">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="c4b42-205">Kullanıcılar bir girişim tooaccess, ihlali neden veya hello veritabanındaki verileri yararlanma SQL veritabanı denetimi toodetermine kullanarak hello şüpheli olayları gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4b42-205">Users can explore hello suspicious events using SQL Database Auditing toodetermine if they result from an attempt tooaccess, breach or exploit data in hello database.</span></span> <span data-ttu-id="c4b42-206">Tehdit algılama basit tooaddress olası tehditler toohello veritabanı hello gerek toobe güvenlik Uzman olmadan kolaylaştırır veya sistemleri izleme Gelişmiş Güvenlik yönetin.</span><span class="sxs-lookup"><span data-stu-id="c4b42-206">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>
<span data-ttu-id="c4b42-207">Örneğin, tehdit algılama olası SQL ekleme girişimlerini gösteren belirli anormal veritabanı etkinliklerini algılar.</span><span class="sxs-lookup"><span data-stu-id="c4b42-207">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="c4b42-208">SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-208">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="c4b42-209">Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini ihlal veya hello veritabanındaki verileri değiştirmek için uygulama giriş alanları içine yararlanın.</span><span class="sxs-lookup"><span data-stu-id="c4b42-209">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

1. <span data-ttu-id="c4b42-210">Merhaba toomonitor istediğiniz SQL veritabanını toohello yapılandırma dikey gidin.</span><span class="sxs-lookup"><span data-stu-id="c4b42-210">Navigate toohello configuration blade of hello SQL database you want toomonitor.</span></span> <span data-ttu-id="c4b42-211">Hello ayarları dikey penceresinde, seçin **denetim ve tehdit algılama**.</span><span class="sxs-lookup"><span data-stu-id="c4b42-211">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. <span data-ttu-id="c4b42-213">Merhaba, **denetim ve tehdit algılama** yapılandırma dikey Aç **ON** denetleme, hangi görüntüler hello tehdit algılama ayarları.</span><span class="sxs-lookup"><span data-stu-id="c4b42-213">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello threat detection settings.</span></span>

3. <span data-ttu-id="c4b42-214">Kapatma **ON** tehdit algılama.</span><span class="sxs-lookup"><span data-stu-id="c4b42-214">Turn **ON** threat detection.</span></span>

4. <span data-ttu-id="c4b42-215">Güvenlik Uyarıları anormal veritabanı etkinliklerini algılandığında alacak e-postaları Hello listesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c4b42-215">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>

5. <span data-ttu-id="c4b42-216">Tıklatın **kaydetmek** hello içinde **denetim ve tehdit algılama** dikey toosave hello yeni veya güncelleştirilmiş denetim ve tehdit algılama ilkesi.</span><span class="sxs-lookup"><span data-stu-id="c4b42-216">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection policy.</span></span>

    ![Gezinti Bölmesi](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    <span data-ttu-id="c4b42-218">Anormal veritabanı etkinliklerini algılanmazsa, anormal veritabanı etkinliklerini algılandığında bir e-posta bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4b42-218">If anomalous database activities are detected, you will receive an email notification upon detection of anomalous database activities.</span></span> <span data-ttu-id="c4b42-219">Merhaba e-posta hello şüpheli güvenlik olayı hello yapısını hello anormal etkinlikler, veritabanı adı, sunucu adını ve hello olay zaman dahil olmak üzere bilgileri sağlarız.</span><span class="sxs-lookup"><span data-stu-id="c4b42-219">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="c4b42-220">Ayrıca, olası nedenler bilgileri sağlarız Eylemler tooinvestigate önerilen ve hello olası tehdit toohello veritabanı etkisini azaltır.</span><span class="sxs-lookup"><span data-stu-id="c4b42-220">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span> <span data-ttu-id="c4b42-221">Merhaba hangi toodo size gereken sonraki adımları ilerlemesi gibi e-posta alırsınız:</span><span class="sxs-lookup"><span data-stu-id="c4b42-221">hello next steps walk you through what toodo should you receive such an email:</span></span>

    ![Tehdit algılama e-posta](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. <span data-ttu-id="c4b42-223">Hello postada hello üzerinde tıklatın **Azure SQL denetim günlüğü** hello Azure portal'ı başlatın ve hello ilgili denetim kayıtları hello şüpheli olay hello sırada geçici Göster bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c4b42-223">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure portal and show hello relevant auditing records around hello time of hello suspicious event.</span></span>

    ![Denetim kaydı](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. <span data-ttu-id="c4b42-225">SQL deyimi gibi hello veritabanı kuşkulu etkinlikleri hakkında daha fazla ayrıntı Hello denetim kayıtları tooview üzerinde tıklatın başarısızlık nedeni ve istemci IP.</span><span class="sxs-lookup"><span data-stu-id="c4b42-225">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>

    ![Kayıt ayrıntıları](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. <span data-ttu-id="c4b42-227">Merhaba denetimi kayıtları dikey penceresinde tıklayın **Excel'de Aç** tooopen önceden yapılandırılmış excel şablonu tooimport ve hello denetim günlüğü hello şüpheli olay hello sırada geçici çalışma daha derin çözümlenmesi.</span><span class="sxs-lookup"><span data-stu-id="c4b42-227">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4b42-228">Excel 2010 veya üzeri, Power Query ve hello **hızlı Birleştir** ayarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-228">In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required.</span></span>

    ![Kayıtları Excel'de Aç](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. <span data-ttu-id="c4b42-230">tooconfigure hello **hızlı Birleştir** ayarında - hello **POWER QUERY** Şerit sekmesi, select **seçenekleri** toodisplay hello Seçenekleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="c4b42-230">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="c4b42-231">Merhaba gizlilik bölümünü seçin ve 'Hello gizlilik düzeylerini yoksayın ve potansiyel performansı geliştirin' hello ikinci seçeneği - belirtin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-231">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>

    ![Excel hızlı Birleştir](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. <span data-ttu-id="c4b42-233">tooload SQL denetim günlüklerini hello parametreleri hello Ayarlar sekmesinde doğru ayarlandığından ve ardından hello 'Verileri' Şerit'i seçin ve hello 'Tümünü Yenile' düğmesini tıklatın emin olun.</span><span class="sxs-lookup"><span data-stu-id="c4b42-233">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>

    ![Excel parametreleri](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. <span data-ttu-id="c4b42-235">Merhaba sonuçları görünen hello **SQL denetim günlüklerini** toorun daha derin algılanan ve uygulamanızda hello güvenlik olayı hello etkisini hello anormal etkinlikler analizini sağlayan sayfası.</span><span class="sxs-lookup"><span data-stu-id="c4b42-235">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c4b42-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4b42-236">Next steps</span></span>
<span data-ttu-id="c4b42-237">Kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı veritabanınızın hello koruma artırabilir.</span><span class="sxs-lookup"><span data-stu-id="c4b42-237">You can improve hello protection of your database against malicious users or unauthorized access with just a few simple steps.</span></span> <span data-ttu-id="c4b42-238">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="c4b42-238">In this tutorial you learn to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c4b42-239">Sunucu ve veya veritabanı için güvenlik duvarı kuralları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c4b42-239">Set up firewall rules for your sever and or database</span></span>
> * <span data-ttu-id="c4b42-240">Güvenli bağlantı dizesi kullanarak tooyour veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="c4b42-240">Connect tooyour database using a secure connection string</span></span>
> * <span data-ttu-id="c4b42-241">Kullanıcı erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="c4b42-241">Manage user access</span></span>
> * <span data-ttu-id="c4b42-242">Şifreleme ile verilerinizi koruma</span><span class="sxs-lookup"><span data-stu-id="c4b42-242">Protect your data with encryption</span></span>
> * <span data-ttu-id="c4b42-243">SQL veritabanı denetimi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c4b42-243">Enable SQL Database auditing</span></span>
> * <span data-ttu-id="c4b42-244">SQL veritabanı tehdit algılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c4b42-244">Enable SQL Database threat detection</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c4b42-245">SQL Veritabanı performansını iyileştirme</span><span class="sxs-lookup"><span data-stu-id="c4b42-245">Improve SQL Database performance</span></span>](sql-database-performance-tutorial.md)

