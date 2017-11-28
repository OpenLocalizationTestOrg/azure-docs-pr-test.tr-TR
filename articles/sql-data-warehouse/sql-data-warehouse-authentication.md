---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: "Azure Active Directory (AAD) ve SQL Server kimlik doğrulama tooAzure SQL veri ambarı."
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
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="bc391-103">Kimlik doğrulama tooAzure SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="bc391-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc391-104">Güvenlik genel bakış</span><span class="sxs-lookup"><span data-stu-id="bc391-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="bc391-105">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bc391-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="bc391-106">Şifreleme (Portal)</span><span class="sxs-lookup"><span data-stu-id="bc391-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="bc391-107">Şifreleme (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="bc391-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="bc391-108">tooconnect tooSQL veri ambarı, kimlik doğrulama amacıyla güvenlik kimlik bilgilerini geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc391-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="bc391-109">Bağlantı kurulduktan sonra belirli bağlantı ayarları, sorgu oturumu bir parçası olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="bc391-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="bc391-110">Güvenlik hakkında daha fazla bilgi ve nasıl tooenable bağlantıları tooyour veri ambarı, bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="bc391-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="bc391-111">SQL kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bc391-111">SQL authentication</span></span>
<span data-ttu-id="bc391-112">tooconnect tooSQL veri ambarı, aşağıdaki bilgilerle hello sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc391-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="bc391-113">Tam servername</span><span class="sxs-lookup"><span data-stu-id="bc391-113">Fully qualified servername</span></span>
* <span data-ttu-id="bc391-114">SQL kimlik doğrulaması belirtin</span><span class="sxs-lookup"><span data-stu-id="bc391-114">Specify SQL authentication</span></span>
* <span data-ttu-id="bc391-115">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="bc391-115">Username</span></span>
* <span data-ttu-id="bc391-116">Parola</span><span class="sxs-lookup"><span data-stu-id="bc391-116">Password</span></span>
* <span data-ttu-id="bc391-117">Varsayılan veritabanı (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="bc391-117">Default database (optional)</span></span>

<span data-ttu-id="bc391-118">Varsayılan olarak, bağlantı toohello bağlar *ana* veritabanı ve, kullanıcı veritabanını değil.</span><span class="sxs-lookup"><span data-stu-id="bc391-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="bc391-119">tooconnect tooyour kullanıcı veritabanı toodo ikisinden birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc391-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="bc391-120">Merhaba varsayılan veritabanı sunucunuz hello SQL Server Nesne Gezgini SSDT, SSMS, veya uygulama bağlantı dizenizi kaydedilirken belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc391-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="bc391-121">Örneğin, bir ODBC bağlantı için hello InitialCatalog parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bc391-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="bc391-122">Bir oturum SSDT oluşturmadan önce Hello kullanıcı veritabanı vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="bc391-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="bc391-123">Transact-SQL deyimini hello **kullanım Veritabanım;** hello veritabanı bağlantı değiştirilmesi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bc391-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="bc391-124">SSDT ile tooSQL veri ambarına bağlanma rehberlik için toohello başvuran [sorgu Visual Studio ile] [ Query with Visual Studio] makale.</span><span class="sxs-lookup"><span data-stu-id="bc391-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="bc391-125">Azure Active Directory (AAD) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="bc391-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="bc391-126">[Azure Active Directory] [ What is Azure Active Directory] kimlik doğrulama mekanizmasıdır Azure Active Directory (Azure AD) kullanarak kimlikleri tooMicrosoft Azure SQL Data Warehouse bağlayan bir.</span><span class="sxs-lookup"><span data-stu-id="bc391-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bc391-127">Azure Active Directory kimlik doğrulaması ile veritabanı kullanıcıları hello kimlikleri ve diğer Microsoft Hizmetleri tek bir merkezi konumda merkezi olarak yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="bc391-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="bc391-128">Merkezi kimlik yönetimi toomanage SQL Data Warehouse kullanıcılar tek bir yer sağlar ve izin yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="bc391-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="bc391-129">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="bc391-129">Benefits</span></span>
<span data-ttu-id="bc391-130">Azure Active Directory yararlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bc391-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="bc391-131">Bir alternatif tooSQL sunucu kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc391-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="bc391-132">Yardımcı veritabanı sunucuları arasında kullanıcı kimlikleri hello artışı durdurun.</span><span class="sxs-lookup"><span data-stu-id="bc391-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="bc391-133">Tek bir yerde parola döndürme sağlar</span><span class="sxs-lookup"><span data-stu-id="bc391-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="bc391-134">Dış (AAD) gruplarını kullanarak veritabanı izinleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc391-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="bc391-135">Depolama parolalar, tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bc391-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="bc391-136">Kullanır, veritabanı kullanıcıları tooauthenticate kimlikleri hello veritabanı düzeyinde içeriyor.</span><span class="sxs-lookup"><span data-stu-id="bc391-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="bc391-137">Belirteç tabanlı kimlik doğrulaması için tooSQL veri ambarına bağlanan uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="bc391-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="bc391-138">Active Directory Evrensel kimlik doğrulaması aracılığıyla çok faktörlü kimlik doğrulaması için SQL Server Management Studio destekler.</span><span class="sxs-lookup"><span data-stu-id="bc391-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="bc391-139">Çok faktörlü kimlik doğrulaması açıklaması için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bc391-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc391-140">Azure Active Directory hala yeni ve bazı sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="bc391-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="bc391-141">Azure Active Directory ortamınız için uygun olmanın olduğunu tooensure bkz [Azure AD özelliklerini ve sınırlamalarını][Azure AD features and limitations], özellikle dikkat edilecek diğer noktalar hello.</span><span class="sxs-lookup"><span data-stu-id="bc391-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="bc391-142">Yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="bc391-142">Configuration steps</span></span>
<span data-ttu-id="bc391-143">Bu adımları tooconfigure Azure Active Directory kimlik doğrulaması izleyin.</span><span class="sxs-lookup"><span data-stu-id="bc391-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="bc391-144">Oluşturma ve Azure Active Directory doldurma</span><span class="sxs-lookup"><span data-stu-id="bc391-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="bc391-145">İsteğe bağlı: İlişkilendir ya da şu anda Azure aboneliğinizle ilişkili hello active directory değiştirme</span><span class="sxs-lookup"><span data-stu-id="bc391-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="bc391-146">Azure SQL Data Warehouse için Azure Active Directory yönetici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc391-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="bc391-147">İstemci bilgisayarları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bc391-147">Configure your client computers</span></span>
5. <span data-ttu-id="bc391-148">Kapsanan veritabanı kullanıcıları, eşlenen veritabanı tooAzure AD kimlikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc391-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="bc391-149">Azure AD kimlikleri kullanarak tooyour veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="bc391-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="bc391-150">Şu anda Azure Active Directory Kullanıcıları SSDT nesne Gezgini'nde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="bc391-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="bc391-151">Geçici bir çözüm olarak hello kullanıcılar görüntülemek [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc391-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="bc391-152">Merhaba ayrıntılarını bulun</span><span class="sxs-lookup"><span data-stu-id="bc391-152">Find hello details</span></span>
* <span data-ttu-id="bc391-153">Merhaba adımları tooconfigure ve kullanım Azure Active Directory kimlik doğrulaması Azure SQL Database ve Azure SQL Data Warehouse için neredeyse aynı.</span><span class="sxs-lookup"><span data-stu-id="bc391-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bc391-154">İzleyin hello ayrıntılı hello konudaki adımları [bağlanıyor tooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bc391-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="bc391-155">Özel veritabanı rolleri oluşturun ve kullanıcıların toohello roller ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bc391-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="bc391-156">Ardından toohello rolleri ayrıntılı izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="bc391-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="bc391-157">Daha fazla bilgi için bkz: [veritabanı altyapısı izinleri ile çalışmaya başlama](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc391-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc391-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc391-158">Next steps</span></span>
<span data-ttu-id="bc391-159">Visual Studio ve diğer uygulamalar, veri Ambarınızı sorgulama toostart bkz [sorgu Visual Studio ile][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="bc391-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
