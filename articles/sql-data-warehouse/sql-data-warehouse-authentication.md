---
title: "Azure SQL veri ambarı için kimlik doğrulaması | Microsoft Docs"
description: "Azure Active Directory (AAD) ve SQL Server kimlik doğrulaması Azure SQL veri ambarı."
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="b751e-103">Azure SQL Veri Ambarı’nda kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="b751e-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b751e-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="b751e-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b751e-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b751e-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b751e-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="b751e-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b751e-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="b751e-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="b751e-108">SQL veri ambarı'na bağlanmak için kimlik doğrulama amacıyla güvenlik kimlik bilgilerini geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b751e-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="b751e-109">Bağlantı kurulduktan sonra belirli bağlantı ayarları, sorgu oturumu bir parçası olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b751e-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="b751e-110">Güvenlik ve veri ambarınız için bağlantıları etkinleştirme hakkında daha fazla bilgi için bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b751e-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="b751e-111">SQL kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b751e-111">SQL authentication</span></span>
<span data-ttu-id="b751e-112">SQL veri ambarı'na bağlanmak için aşağıdaki bilgileri sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b751e-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="b751e-113">Tam servername</span><span class="sxs-lookup"><span data-stu-id="b751e-113">Fully qualified servername</span></span>
* <span data-ttu-id="b751e-114">SQL kimlik doğrulaması belirtin</span><span class="sxs-lookup"><span data-stu-id="b751e-114">Specify SQL authentication</span></span>
* <span data-ttu-id="b751e-115">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="b751e-115">Username</span></span>
* <span data-ttu-id="b751e-116">Parola</span><span class="sxs-lookup"><span data-stu-id="b751e-116">Password</span></span>
* <span data-ttu-id="b751e-117">Varsayılan veritabanı (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="b751e-117">Default database (optional)</span></span>

<span data-ttu-id="b751e-118">Varsayılan olarak, bağlantınızı bağlandığı *ana* veritabanı ile değil, kullanıcı veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b751e-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="b751e-119">Kullanıcı veritabanına bağlanmak için ikisinden birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b751e-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="b751e-120">Varsayılan veritabanı sunucunuz SQL Server Nesne Gezgini SSDT, SSMS, veya uygulama bağlantı dizenizi kaydedilirken belirtin.</span><span class="sxs-lookup"><span data-stu-id="b751e-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="b751e-121">Örneğin, bir ODBC bağlantı için InitialCatalog parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b751e-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="b751e-122">Kullanıcı veritabanı oturumu içinde SSDT oluşturmadan önce vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="b751e-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="b751e-123">Transact-SQL deyimini **kullanım Veritabanım;** bir bağlantı için veritabanını değiştirmek için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b751e-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="b751e-124">SSDT ile SQL Data Warehouse'a bağlanma yönergeler için bkz [sorgu Visual Studio ile] [ Query with Visual Studio] makalesi.</span><span class="sxs-lookup"><span data-stu-id="b751e-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="b751e-125">Azure Active Directory (AAD) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b751e-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="b751e-126">[Azure Active Directory] [ What is Azure Active Directory] kimlik doğrulama mekanizmasıdır Microsoft Azure SQL Data Warehouse için Azure Active Directory (Azure AD) kullanarak kimlikleri bağlayan bir.</span><span class="sxs-lookup"><span data-stu-id="b751e-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b751e-127">Azure Active Directory kimlik doğrulaması ile veritabanı kullanıcıları kimlikleri ve diğer Microsoft Hizmetleri tek bir merkezi konumda merkezi olarak yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="b751e-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="b751e-128">Merkezi kimlik yönetimi, SQL Data Warehouse kullanıcıları yönetmek için tek bir yer sağlar ve izin Yönetimi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="b751e-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="b751e-129">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="b751e-129">Benefits</span></span>
<span data-ttu-id="b751e-130">Azure Active Directory yararlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b751e-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="b751e-131">SQL Server kimlik doğrulaması için bir alternatif sunar.</span><span class="sxs-lookup"><span data-stu-id="b751e-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="b751e-132">Yardımcı veritabanı sunucuları arasında kullanıcı kimlikleri artışı durdurun.</span><span class="sxs-lookup"><span data-stu-id="b751e-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="b751e-133">Tek bir yerde parola döndürme sağlar</span><span class="sxs-lookup"><span data-stu-id="b751e-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="b751e-134">Dış (AAD) gruplarını kullanarak veritabanı izinleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="b751e-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="b751e-135">Depolama parolalar, tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b751e-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="b751e-136">Veritabanı düzeyinde kimlikleri doğrulamak için veritabanı kullanıcıları bulunan kullanır.</span><span class="sxs-lookup"><span data-stu-id="b751e-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="b751e-137">SQL veri ambarı'na bağlanan uygulamalar için belirteç tabanlı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="b751e-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="b751e-138">Active Directory Evrensel kimlik doğrulaması aracılığıyla çok faktörlü kimlik doğrulaması için SQL Server Management Studio destekler.</span><span class="sxs-lookup"><span data-stu-id="b751e-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="b751e-139">Çok faktörlü kimlik doğrulaması açıklaması için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b751e-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b751e-140">Azure Active Directory hala yeni ve bazı sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="b751e-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="b751e-141">Azure Active Directory ortamınız için uygun olmanın olduğundan emin olmak için bkz: [Azure AD özelliklerini ve sınırlamalarını][Azure AD features and limitations], özellikle ek hususlar.</span><span class="sxs-lookup"><span data-stu-id="b751e-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="b751e-142">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="b751e-142">Configuration steps</span></span>
<span data-ttu-id="b751e-143">Azure Active Directory kimlik doğrulamasını yapılandırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b751e-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="b751e-144">Oluşturma ve Azure Active Directory doldurma</span><span class="sxs-lookup"><span data-stu-id="b751e-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="b751e-145">İsteğe bağlı: İlişkilendir ya da şu anda Azure aboneliğinizle ilişkili olan active directory değiştirme</span><span class="sxs-lookup"><span data-stu-id="b751e-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="b751e-146">Azure SQL Data Warehouse için Azure Active Directory yönetici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b751e-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="b751e-147">İstemci bilgisayarları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b751e-147">Configure your client computers</span></span>
5. <span data-ttu-id="b751e-148">Azure AD kimlikleri eşlenen veritabanınızdaki kapsanan veritabanı kullanıcıları oluşturun</span><span class="sxs-lookup"><span data-stu-id="b751e-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="b751e-149">Azure AD kimlik kullanarak, veri ambarına bağlama</span><span class="sxs-lookup"><span data-stu-id="b751e-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="b751e-150">Şu anda Azure Active Directory Kullanıcıları SSDT nesne Gezgini'nde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="b751e-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="b751e-151">Geçici bir çözüm olarak, kullanıcılar görüntülemek [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="b751e-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="b751e-152">Ayrıntılarını bulun</span><span class="sxs-lookup"><span data-stu-id="b751e-152">Find the details</span></span>
* <span data-ttu-id="b751e-153">Adımları yapılandırmak ve Azure Active Directory kimlik doğrulaması kullanmak için Azure SQL Database ve Azure SQL Data Warehouse için neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b751e-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b751e-154">Konusunda ayrıntılı adımları [SQL Database'e veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması için bağlanma](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b751e-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="b751e-155">Özel veritabanı rolleri oluşturun ve kullanıcıları rollere ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b751e-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="b751e-156">Ardından rollere ayrıntılı izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="b751e-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="b751e-157">Daha fazla bilgi için bkz: [veritabanı altyapısı izinleri ile çalışmaya başlama](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="b751e-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b751e-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b751e-158">Next steps</span></span>
<span data-ttu-id="b751e-159">Visual Studio ve diğer uygulamalarla veri ambarınız sorgulama başlatmak için bkz: [sorgu Visual Studio ile][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b751e-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
