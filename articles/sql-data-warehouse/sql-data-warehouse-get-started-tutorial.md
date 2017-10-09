---
title: "SQL veri ambarı - aaaAzure Başlarken Öğreticisi | Microsoft Docs"
description: "Bu öğretici nasıl öğretilmektedir tooprovision ve yük verileri Azure SQL veri ambarında. Ayrıca hello temelleri ölçeklendirme, duraklatma ve ayarlama hakkında bilgi edineceksiniz."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="5cd10-104">SQL Veri Ambarı'nı kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="5cd10-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="5cd10-105">Bu öğreticide gösterilmiştir nasıl tooprovision ve yük verileri Azure SQL veri ambarında.</span><span class="sxs-lookup"><span data-stu-id="5cd10-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="5cd10-106">Ayrıca hello temelleri ölçeklendirme, duraklatma ve ayarlama hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="5cd10-107">İşlemi tamamladığınızda, hazır tooquery olması ve veri ambarınız keşfedin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="5cd10-108">**Zaman toocomplete tahmini:** hello önkoşulları karşıladığınızı sonra yaklaşık 30 dakika toocomplete geçen örnek kod ile uçtan uca öğretici budur.</span><span class="sxs-lookup"><span data-stu-id="5cd10-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5cd10-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5cd10-109">Prerequisites</span></span>

<span data-ttu-id="5cd10-110">Başlangıç Öğreticisi SQL veri ambarı temel kavramları hakkında bilgi sahibi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="5cd10-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="5cd10-111">Bir tanıtım gerekirse bkz. [SQL Veri Ambarı nedir?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="5cd10-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="5cd10-112">Microsoft Azure’a kaydolun</span><span class="sxs-lookup"><span data-stu-id="5cd10-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="5cd10-113">Zaten bir Microsoft Azure hesabınız yoksa, bu hizmet için bir toouse toosign gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="5cd10-114">Zaten bir hesabınız varsa, bu adımı geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="5cd10-115">Toohello hesabı sayfalarında gezinmek [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="5cd10-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="5cd10-116">Ücretsiz bir Azure hesabı oluşturun veya bir hesap satın alın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="5cd10-117">Merhaba yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="5cd10-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="5cd10-118">Uygun SQL istemci sürücülerini ve araçlarını yükleyin</span><span class="sxs-lookup"><span data-stu-id="5cd10-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="5cd10-119">Çoğu SQL istemci araçları JDBC, ODBC veya ADO.NET kullanarak tooSQL veri ambarına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="5cd10-120">Toohello çok sayıda SQL Data Warehouse destekleyen T-SQL özelliklerini, bazı istemci uygulamaları ile SQL veri ambarı tamamen uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="5cd10-121">Bir Windows işletim sistemi çalıştırıyorsanız [Visual Studio] veya [SQL Server Management Studio] kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="5cd10-122">SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cd10-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="5cd10-123">SQL Veri Ambarı, yüksek düzeyde paralel işleme için tasarlanmış özel bir veritabanı türüdür.</span><span class="sxs-lookup"><span data-stu-id="5cd10-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="5cd10-124">Merhaba veritabanı birden çok düğümüne dağıtılmış ve paralel sorgular işler.</span><span class="sxs-lookup"><span data-stu-id="5cd10-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="5cd10-125">SQL veri ambarı tüm hello düğümleri hello etkinliklerini düzenler bir denetim düğümü vardır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="5cd10-126">Merhaba düğümlerin kendilerini SQL veritabanı toomanage verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="5cd10-127">SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="5cd10-128">Ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="5cd10-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="5cd10-129">Veri ambarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cd10-129">Create a data warehouse</span></span>

1. <span data-ttu-id="5cd10-130">Merhaba içine oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5cd10-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5cd10-131">**Yeni** > **Veritabanları** > **SQL Veri Ambarı** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="5cd10-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="5cd10-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="5cd10-133">Dağıtım ayrıntılarını doldurun</span><span class="sxs-lookup"><span data-stu-id="5cd10-133">Fill out deployment details</span></span>

    <span data-ttu-id="5cd10-134">**Veritabanı Adı**: İstediğiniz bir adı seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="5cd10-135">Birden çok veri ambarlarında varsa adları dahil hello bölge, ortam, örneğin gibi ayrıntıları önerilir *westus 1 test mydw*.</span><span class="sxs-lookup"><span data-stu-id="5cd10-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="5cd10-136">**Abonelik**: Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="5cd10-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="5cd10-137">**Kaynak Grubu**: Bir kaynak grubu oluşturun veya mevcut bir kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="5cd10-138">Kaynak grupları, kapsam erişim denetimi ve şablonlu dağıtım gibi kaynak yönetimi için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="5cd10-139">Azure kaynak grupları ve en iyi uygulamalar hakkında daha fazla bilgiyi [burada](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5cd10-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="5cd10-140">**Kaynak**: Boş Veritabanı</span><span class="sxs-lookup"><span data-stu-id="5cd10-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="5cd10-141">**Sunucu**: oluşturduğunuz Select hello sunucu [önkoşulları].</span><span class="sxs-lookup"><span data-stu-id="5cd10-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="5cd10-142">**Harmanlama**: hello varsayılan harmanlama sql_latin1_general_cp1_cı_as bırakın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="5cd10-143">**Performans seçin**: hello standart 400DWU ile başlayan öneririz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="5cd10-144">Seçin **PIN toodashboard** ![PIN tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="5cd10-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="5cd10-145">Arkanıza yaslanın ve, veri ambarı toodeploy için bekleyin!</span><span class="sxs-lookup"><span data-stu-id="5cd10-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="5cd10-146">Birkaç dakika için bu işlemi tootake normaldir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="5cd10-147">veri ambarınız hazır toouse olduğunda hello portal size bildirir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="5cd10-148">TooSQL veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="5cd10-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="5cd10-149">Bu öğretici, SQL Server Management Studio (SSMS) tooconnect toohello veri ambarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="5cd10-150">Bu desteklenen bağlayıcılar tooSQL veri ambarına bağlanabilir: ADO.NET, JDBC, ODBC ve PHP.</span><span class="sxs-lookup"><span data-stu-id="5cd10-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="5cd10-151">Microsoft tarafından desteklenmeyen araçlar için işlevselliğin sınırlı olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="5cd10-152">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="5cd10-152">Get connection information</span></span>

<span data-ttu-id="5cd10-153">tooconnect tooyour veri ambarı, gereksinim duyduğunuz hello oluşturduğunuz mantıksal SQL sunucusu üzerinden tooconnect [önkoşulları].</span><span class="sxs-lookup"><span data-stu-id="5cd10-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="5cd10-154">Veri ambarınız hello Pano veya kaynaklarınız için bu aramada seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![SQL Veri Ambarı Panosu](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="5cd10-156">Merhaba mantıksal SQL sunucusu için tam ad Hello bulun.</span><span class="sxs-lookup"><span data-stu-id="5cd10-156">Find hello full name for hello logical SQL server.</span></span>

    ![Sunucu Adını seçin](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="5cd10-158">SSMS açıp Nesne Gezgini tooconnect toothis sunucusu oluşturduğunuz hello server yönetici kimlik bilgileriyle kullanmak [önkoşulları]</span><span class="sxs-lookup"><span data-stu-id="5cd10-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![SSMS ile bağlanma](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="5cd10-160">Tüm kalırsa doğru artık bağlı tooyour mantıksal SQL sunucusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="5cd10-161">Sunucu Yöneticisi hello gibi oturum bu yana hello ana veritabanı da dahil, hello sunucu tarafından barındırılan tooany veritabanının bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="5cd10-162">Yalnızca bir sunucu yönetici hesabı ve hello herhangi bir kullanıcı çoğu ayrıcalıklarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="5cd10-163">Dikkatli olun değil tooallow kuruluş tooknow hello Yönetici parolanızı çok fazla kişilere.</span><span class="sxs-lookup"><span data-stu-id="5cd10-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="5cd10-164">Bir Azure active directory yönetici hesabına da sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="5cd10-165">Merhaba ayrıntıları buraya sunuyoruz yok.</span><span class="sxs-lookup"><span data-stu-id="5cd10-165">We don't provide hello details here.</span></span> <span data-ttu-id="5cd10-166">Azure Active Directory kimlik doğrulaması kullanma hakkında daha fazla toolearn istiyorsanız, bkz: [Azure AD kimlik doğrulaması](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="5cd10-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="5cd10-167">Ardından, ek oturumlar ve kullanıcılar oluşturma hakkında bilgi verilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="5cd10-168">Veritabanı kullanıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cd10-168">Create a database user</span></span>

<span data-ttu-id="5cd10-169">Bu adımda, bir kullanıcı hesabı tooaccess veri ambarınız oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cd10-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="5cd10-170">Ayrıca toogive o kullanıcı hello özelliği toorun büyük miktarda bellek ve CPU kaynaklarını ile nasıl sorgular gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="5cd10-171">Kaynakları tooqueries ayırma için kaynak sınıfları ile ilgili notlar</span><span class="sxs-lookup"><span data-stu-id="5cd10-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="5cd10-172">tookeep verilerinizi güvenli, üretim veritabanlarınızı hello server yönetim toorun sorguları kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="5cd10-173">Merhaba herhangi bir kullanıcı çoğu ayrıcalıklarına sahip ve tooperform kullanarak kullanıcı verilerine operations yerleştirir verileriniz risk altında.</span><span class="sxs-lookup"><span data-stu-id="5cd10-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="5cd10-174">Hello Sunucu Yöneticisi tooperform yönetim işlemlerini tasarlanmıştır olduğundan, ayrıca, dosya işlemleri bellek ve CPU kaynaklarını yalnızca küçük bir ayırma ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="5cd10-175">SQL veri ambarı adlı kaynak sınıfları, bellek, CPU kaynaklarını ve eşzamanlılık yuvaları toousers farklı miktarlarda tooallocate önceden tanımlanmış veritabanı rollerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="5cd10-176">Her kullanıcı tooa küçük, Orta, büyük veya çok büyük bir kaynak sınıfı ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="5cd10-177">Merhaba kullanıcının kaynak sınıfı hello kaynakları hello kullanıcının sahip toorun sorguları belirler ve yükleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="5cd10-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="5cd10-178">En iyi veri sıkıştırma için hello kullanıcı tooload büyük veya çok büyük kaynak ayırma gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="5cd10-179">Kaynak sınıfları hakkında daha fazla bilgiyi [burada](./sql-data-warehouse-develop-concurrency.md#resource-classes) bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5cd10-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="5cd10-180">Veritabanını denetleyebilen bir hesap oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cd10-180">Create an account that can control a database</span></span>

<span data-ttu-id="5cd10-181">Sunucu Yöneticisi Merhaba, oturum açmış olduğunuz olduğundan izinleri toocreate oturumları ve kullanıcıları sahip.</span><span class="sxs-lookup"><span data-stu-id="5cd10-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="5cd10-182">SSMS veya başka bir sorgu istemcisini kullanarak **ana** için yeni bir sorgu açın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Asıl’da Yeni Sorgu](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Asıl1’de Yeni Sorgu](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="5cd10-185">Merhaba sorgu penceresinde, bu T-SQL komut toocreate MedRCLogin adlı oturum açma ve kullanıcı LoadingUser adlı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="5cd10-186">Bu oturum açma toohello mantıksal SQL sunucusuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="5cd10-187">Şimdi hello sorgulama *SQL Data Warehouse veritabanı*, temel bir veritabanı kullanıcısı oluşturmalıdır hello tooaccess oluşturulan oturum açma ve hello veritabanı işlemleri.</span><span class="sxs-lookup"><span data-stu-id="5cd10-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="5cd10-188">Merhaba veritabanı kullanıcı denetimi izinleri toohello veritabanı NYT adlı verin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="5cd10-189">Veritabanı adınız kısa çizgi varsa, emin toowrap olması köşeli ayraçlar içinde!</span><span class="sxs-lookup"><span data-stu-id="5cd10-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="5cd10-190">Merhaba kullanıcı orta kaynak ayırma verin</span><span class="sxs-lookup"><span data-stu-id="5cd10-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="5cd10-191">Bu T-SQL komut toomake çalıştırmak üyesi mediumrc adlı hello Orta kaynak sınıfı, bir BT.</span><span class="sxs-lookup"><span data-stu-id="5cd10-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="5cd10-192">Tıklatın [burada](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn eşzamanlılık ve kaynak sınıfları hakkında daha fazla!</span><span class="sxs-lookup"><span data-stu-id="5cd10-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="5cd10-193">Toohello mantıksal sunucu hello yeni kimlik bilgilerinizle bağlanmak</span><span class="sxs-lookup"><span data-stu-id="5cd10-193">Connect toohello logical server with hello new credentials</span></span>

    ![Yeni Oturum Bilgileriyle oturum açın](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="5cd10-195">Azure blob depolamadan veri yükleme</span><span class="sxs-lookup"><span data-stu-id="5cd10-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="5cd10-196">Artık hazır tooload verileri veri ambarınıza bulunur.</span><span class="sxs-lookup"><span data-stu-id="5cd10-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="5cd10-197">Bu adım nasıl ortak bir Azure depolama biriminden tooload New York şehrinde ücreti cab verileri blob gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="5cd10-198">SQL veri ambarı tooload verisine toofirst olan yaygın bir yolu hello veri tooAzure blob depolama taşıyın ve veri ambarına yük.</span><span class="sxs-lookup"><span data-stu-id="5cd10-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="5cd10-199">toomake bunu daha kolay toounderstand nasıl tooload, New York ücreti cab veri zaten bir ortak Azure storage blobu barındırılan sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="5cd10-200">Gelecekte başvurmak, toolearn nasıl tooget veri tooAzure blob depolama veya doğrudan kaynağınızdan SQL veri ambarında, bkz: tooload hello [yüklemeye genel bakış](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="5cd10-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="5cd10-201">Dış veri tanımlama</span><span class="sxs-lookup"><span data-stu-id="5cd10-201">Define external data</span></span>

1. <span data-ttu-id="5cd10-202">Bir ana anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cd10-202">Create a master key.</span></span> <span data-ttu-id="5cd10-203">Yalnızca toocreate her veritabanı için bir kez bir ana anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="5cd10-204">Merhaba hello ücreti cab verileri içeren Azure blob Hello konumunu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="5cd10-205">Merhaba dış dosya biçimleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5cd10-205">Define hello external file formats</span></span>

    <span data-ttu-id="5cd10-206">Merhaba ```CREATE EXTERNAL FILE FORMAT``` komuttur kullanılan toospecify hello dış veri içeren dosyaları biçimi.</span><span class="sxs-lookup"><span data-stu-id="5cd10-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="5cd10-207">Sınırlayıcı adlı bir veya daha fazla karakter ile ayrılmış metinler içerir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="5cd10-208">Tanıtım amacıyla hello ücreti cab verileri hem de sıkıştırılmamış veri gzip sıkıştırılmış veri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="5cd10-209">Bunları çalıştırmak T-SQL toodefine iki farklı biçimlerde komutlar: sıkıştırılmamış ve sıkıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="5cd10-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="5cd10-210">Dış dosya biçiminiz için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cd10-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="5cd10-211">Merhaba dış tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cd10-211">Create hello external tables.</span></span> <span data-ttu-id="5cd10-212">Bu tablolar Azure blob depolamada saklanan verilere başvurur.</span><span class="sxs-lookup"><span data-stu-id="5cd10-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="5cd10-213">T-SQL komutlarını toocreate aşağıdaki hello tüm noktası toohello Azure blob biz önceden bizim dış veri kaynağında tanımlanan birkaç dış tablolara çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="5cd10-214">Merhaba verileri Azure blob depolama alanından içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="5cd10-215">SQL Veri Ambarı, CREATE TABLE AS SELECT (CTAS) adlı bir anahtar deyimini destekler.</span><span class="sxs-lookup"><span data-stu-id="5cd10-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="5cd10-216">Bu deyim bir select deyimi hello sonuçlarına dayalı yeni bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5cd10-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="5cd10-217">Merhaba yeni tablolu hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri.</span><span class="sxs-lookup"><span data-stu-id="5cd10-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="5cd10-218">Bu bir Azure blob depolama alanına SQL Data Warehouse zarif bir şekilde tooimport verilerdir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="5cd10-219">Bu komut dosyası tooimport verilerinizi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="5cd10-220">Verilerinizi yüklenirken görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-220">View your data as it loads.</span></span>

   <span data-ttu-id="5cd10-221">Birkaç GB veri yüklüyorsunuz ve yüksek performanslı kümelenmiş columnstore dizinlerine sıkıştırıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="5cd10-222">Merhaba yük dinamik yönetim görünümlerini (Dmv'leri) tooshow hello durumunu kullanan sorgu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="5cd10-223">SQL Data Warehouse bazı ağır lifting desteklemiyor sırada hello sorgu başlattıktan sonra bir kahve ve bir yemek alın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="5cd10-224">Tüm sistem sorgularını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="5cd10-225">Azure SQL Veri Ambarı’nıza verilerinizin sorunsuz şekilde yüklenmesinin keyfini çıkarın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Yüklenen Verilere bakın](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="5cd10-227">Sorgu performansını artırma</span><span class="sxs-lookup"><span data-stu-id="5cd10-227">Improve query performance</span></span>

<span data-ttu-id="5cd10-228">SQL veri ambarı tooachieve hello yüksek performans tooprovide tasarlanmış ve çeşitli yolları tooimprove sorgu performansı vardır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="5cd10-229">Merhaba etkisini sorgu performansına ölçeklendirme bakın</span><span class="sxs-lookup"><span data-stu-id="5cd10-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="5cd10-230">Tek yönlü tooimprove sorgu performansı veri ambarınız için hello DWU hizmet düzeyi değiştirerek tooscale kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="5cd10-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="5cd10-231">Her hizmet düzeyi daha fazla maliyet getirir, ancak dilediğiniz zaman kaynakların ölçeğini azaltabilir veya kaynakları duraklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="5cd10-232">Bu adımda, iki farklı DWU ayarında performansı karşılaştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="5cd10-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="5cd10-233">İlk olarak, biz nasıl bir işlem düğümünde hakkında bir fikir sınıflandırıp DWU gerçekleştirebileceğiniz, kendi too100 aşağı hello boyutlandırma şimdi ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="5cd10-234">Toohello portal gidin ve SQL veri ambarı seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="5cd10-235">Ölçek hello SQL Data Warehouse dikey penceresinde seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Portaldan Ölçek DW](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="5cd10-237">Merhaba performans too100 DWU çubuğu ölçeğini ve Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Ölçek ve kayıt](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="5cd10-239">Ölçek işlemi toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5cd10-240">Sorguları hello ölçek değiştirilirken çalıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="5cd10-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="5cd10-241">Ölçeklendirme, o anda çalışmakta olan sorgularınızı **sonlandırır**.</span><span class="sxs-lookup"><span data-stu-id="5cd10-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="5cd10-242">Merhaba işlem sona erdiğinde bunları yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="5cd10-243">Merhaba üst milyon girişleri tüm hello sütunlar için seçerek hello seyahat veri üzerinde bir tarama işlemi yapın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="5cd10-244">İstekli toomove hızla girdiğinizi, ücretsiz tooselect daha az sayıda satır hissedilmesini.</span><span class="sxs-lookup"><span data-stu-id="5cd10-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="5cd10-245">Bu işlem toorun geçen hello süreyi not edin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="5cd10-246">Veri ambarınız ölçeklendirme too400 DWU yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="5cd10-247">Her 100 DWU başka bir işlem düğümü tooyour Azure SQL Data Warehouse eklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="5cd10-248">Merhaba sorguyu yeniden çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="5cd10-248">Run hello query again!</span></span> <span data-ttu-id="5cd10-249">Önemli bir fark dikkat göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5cd10-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="5cd10-250">Hello sorgu çok miktarda veri döndürdüğünden hello bant genişliği kullanılabilirliğini SSMS çalışan hello makinenin performans düşüklüğü olabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="5cd10-251">Bu da herhangi bir performans artışıyla karşılaşmamanıza yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="5cd10-252">SQL Veri Ambarı, yüksek düzeyde paralel işleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="5cd10-253">Tarama veya milyonlarca satır analitik işlevleri gerçekleştirmek sorguları hello true Azure SQL Data Warehouse gücünü karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="5cd10-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="5cd10-254">Sorgu performans istatistikleri Hello etkisini görmek</span><span class="sxs-lookup"><span data-stu-id="5cd10-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="5cd10-255">Birleştirmeler tarih tablosu hello seyahat tabloyla hello sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5cd10-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="5cd10-256">Merhaba birleştirme gerçekleştirmeden önce SQL veri ambarı tooshuffle veri içerdiğinden bu sorguyu biraz uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="5cd10-257">Birleştirmeler yok tooshuffle veri hello tasarlanmış toojoin verilerde olmaları durumunda aynı şekilde bu dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="5cd10-258">Bu daha derin bir konudur.</span><span class="sxs-lookup"><span data-stu-id="5cd10-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="5cd10-259">İstatistikler fark yaratır.</span><span class="sxs-lookup"><span data-stu-id="5cd10-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="5cd10-260">Bu deyim toocreate istatistikleri hello birleştirme sütunu üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="5cd10-261">SQL DW istatistikleri sizin için otomatik olarak yönetmez.</span><span class="sxs-lookup"><span data-stu-id="5cd10-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="5cd10-262">İstatistikleri sorgu performansı için önemlidir ve istatistikleri oluşturmanız ve güncelleştirmeniz önemle tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="5cd10-263">**Çoğu avantajı sütunlarda söz konusu birleşimlerde GROUP BY yan tümcesi ve sütun bulundu hello kullanılan sütun istatistikleri sağlayarak hello kazanır.**</span><span class="sxs-lookup"><span data-stu-id="5cd10-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="5cd10-264">Önkoşulları Hello sorguyu yeniden çalıştırın ve tüm performans farklar inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="5cd10-265">Sorgu performansı Hello farklılıkları ölçeklendirmeyi olarak olarak keskin olmaz olsa da, bir faturalamak dikkat etmelidir.</span><span class="sxs-lookup"><span data-stu-id="5cd10-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5cd10-266">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cd10-266">Next steps</span></span>

<span data-ttu-id="5cd10-267">Şimdi hazır tooquery olduğunuz ve keşfedin.</span><span class="sxs-lookup"><span data-stu-id="5cd10-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="5cd10-268">En iyi yöntemlerimize veya ipuçlarımıza bakın.</span><span class="sxs-lookup"><span data-stu-id="5cd10-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="5cd10-269">İşiniz bittiğinde, örneğinizi olun emin toopause hello gün için keşfetme!</span><span class="sxs-lookup"><span data-stu-id="5cd10-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="5cd10-270">Üretimde muazzam tasarrufları duraklatma ve ölçeklendirme toomeet yaşayabilirsiniz iş gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="5cd10-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Duraklat](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="5cd10-272">Yararlı okumalar</span><span class="sxs-lookup"><span data-stu-id="5cd10-272">Useful readings</span></span>

<span data-ttu-id="5cd10-273">[Eşzamanlılık ve İş Yükü Yönetimi][]</span><span class="sxs-lookup"><span data-stu-id="5cd10-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="5cd10-274">[Azure SQL Veri Ambarı için en iyi yöntemler][]</span><span class="sxs-lookup"><span data-stu-id="5cd10-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="5cd10-275">[Sorgu İzleme][]</span><span class="sxs-lookup"><span data-stu-id="5cd10-275">[Query Monitoring][]</span></span>

<span data-ttu-id="5cd10-276">[Büyük Ölçekli İlişkisel Veri Ambarı Oluşturmaya Yönelik En İyi 10 Yöntem][]</span><span class="sxs-lookup"><span data-stu-id="5cd10-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="5cd10-277">[Geçirme verilerini tooAzure SQL veri ambarı][]</span><span class="sxs-lookup"><span data-stu-id="5cd10-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Eşzamanlılık ve İş Yükü Yönetimi]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL Veri Ambarı için en iyi yöntemler]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Sorgu İzleme]: sql-data-warehouse-manage-monitor.md
[Büyük Ölçekli İlişkisel Veri Ambarı Oluşturmaya Yönelik En İyi 10 Yöntem]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Geçirme verilerini tooAzure SQL veri ambarı]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[önkoşulları]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
