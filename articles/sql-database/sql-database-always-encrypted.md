---
title: "Her zaman şifreli: Azure SQL veritabanı - Windows sertifika deposunda | Microsoft Docs"
description: "Bu makalede, her zaman şifreli Sihirbazı SQL Server Management Studio (SSMS) kullanarak veritabanı şifreleme ile bir SQL veritabanında toosecure hassas verileri nasıl hello gösterir. Ayrıca, nasıl toostore hello Windows sertifika, şifreleme anahtarlarını saklamak gösterir."
keywords: "her zaman şifreli verileri, sql şifrelemesi, veritabanı şifreleme, hassas verileri şifrelemek"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="24ca3-105">Her zaman şifreli: SQL veritabanındaki hassas verileri korumak ve şifreleme anahtarlarınızı hello Windows sertifika deposunda depola</span><span class="sxs-lookup"><span data-stu-id="24ca3-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="24ca3-106">Bu makalede nasıl hello kullanarak toosecure hassas verileri bir SQL veritabanı şifreleme ile veritabanı gösterilmektedir [her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx) içinde [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="24ca3-107">Ayrıca, nasıl toostore hello Windows sertifika, şifreleme anahtarlarını saklamak gösterir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="24ca3-108">Her zaman şifreli bir yeni veri şifreleme Azure SQL veritabanındaki bir teknolojidir ve yardımcı olan bir SQL Server istemci ve sunucu arasında hareket sırasında rest hello sunucusunda hassas verileri korumak ve hello veri kullanımdayken bu hassas verileri asla sağlayarak olarak görünür düz metin hello veritabanı sistem içinde.</span><span class="sxs-lookup"><span data-stu-id="24ca3-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="24ca3-109">Veri şifrelemek sonra yalnızca istemci uygulamaları ya da erişim toohello anahtarlara sahip uygulama sunucuları düz metin verilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="24ca3-110">Ayrıntılı bilgi için bkz: [(veritabanı altyapısı)'her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="24ca3-111">Merhaba veritabanı toouse her zaman şifreli yapılandırdıktan sonra C# Visual Studio toowork hello şifrelenmiş verilerle birlikte bir istemci uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="24ca3-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="24ca3-112">Bu makale toolearn Hello adımları nasıl izleyin bir Azure SQL veritabanı için her zaman şifreli yukarı tooset.</span><span class="sxs-lookup"><span data-stu-id="24ca3-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="24ca3-113">Bu makalede, nasıl tooperform hello aşağıdaki görevleri öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="24ca3-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="24ca3-114">Kullanım hello her zaman şifreli sihirbazında SSMS toocreate [her zaman şifreli anahtarları](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="24ca3-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="24ca3-115">Oluşturma bir [sütun ana anahtar (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="24ca3-116">Oluşturma bir [sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="24ca3-117">Bir veritabanı tablosu oluşturmak ve sütunları şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="24ca3-118">Ekler, seçer ve şifrelenmiş hello sütunları verileri görüntüleyen bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24ca3-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ca3-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="24ca3-119">Prerequisites</span></span>
<span data-ttu-id="24ca3-120">Bu öğretici için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="24ca3-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="24ca3-121">Bir Azure hesabı ve aboneliği</span><span class="sxs-lookup"><span data-stu-id="24ca3-121">An Azure account and subscription.</span></span> <span data-ttu-id="24ca3-122">Yoksa, kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24ca3-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="24ca3-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) sürüm 13.0.700.242 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="24ca3-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="24ca3-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) veya üstünü (Merhaba istemci bilgisayarda).</span><span class="sxs-lookup"><span data-stu-id="24ca3-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="24ca3-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="24ca3-126">Boş bir SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24ca3-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="24ca3-127">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="24ca3-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="24ca3-128">Tıklatın **yeni** > **veri + depolama** > **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="24ca3-129">Oluşturma bir **boş** adlı veritabanı **Clinic** yeni veya var olan bir sunucuda.</span><span class="sxs-lookup"><span data-stu-id="24ca3-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="24ca3-130">Hello Azure portalında bir veritabanı oluşturma hakkında ayrıntılı yönergeler için bkz: [ilk Azure SQL veritabanınızı](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24ca3-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Boş veritabanı oluşturma](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="24ca3-132">Daha sonra hello öğreticide hello bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="24ca3-133">Merhaba veritabanı oluşturulduktan sonra toohello yeni Clinic veritabanı ve kopyalama hello bağlantı dizesi gidin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="24ca3-134">Herhangi bir zamanda hello bağlantı dizesi elde edebilirsiniz, ancak bunu kolay toocopy onu hello Azure portal olduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="24ca3-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="24ca3-135">Tıklatın **SQL veritabanları** > **Clinic** > **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="24ca3-136">Merhaba bağlantı dizesini kopyalayın **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="24ca3-138">SSMS ile toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="24ca3-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="24ca3-139">SSMS açın ve toohello sunucu hello Clinic veritabanıyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="24ca3-140">SSMS açın.</span><span class="sxs-lookup"><span data-stu-id="24ca3-140">Open SSMS.</span></span> <span data-ttu-id="24ca3-141">(Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresi açık değilse).</span><span class="sxs-lookup"><span data-stu-id="24ca3-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="24ca3-142">Sunucu adı ve kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-142">Enter your server name and credentials.</span></span> <span data-ttu-id="24ca3-143">Merhaba sunucu adı hello SQL veritabanı dikey bulunabilir ve daha önce kopyaladığınız hello bağlantı dizesinde.</span><span class="sxs-lookup"><span data-stu-id="24ca3-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="24ca3-144">Türü hello tam sunucu adını içeren *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="24ca3-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="24ca3-146">Merhaba, **yeni güvenlik duvarı kuralı** penceresi açılır oturum içinde tooAzure ve let SSMS sizin için yeni bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24ca3-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="24ca3-147">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="24ca3-147">Create a table</span></span>
<span data-ttu-id="24ca3-148">Bu bölümde, bir tablo toohold Hasta verileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24ca3-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="24ca3-149">Bu normal bir tablo başlangıçta--olacaktır şifreleme hello sonraki bölümde yapılandıracak.</span><span class="sxs-lookup"><span data-stu-id="24ca3-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="24ca3-150">Genişletme **veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="24ca3-151">Sağ hello **Clinic** veritabanı ve tıklatın **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="24ca3-152">Transact-SQL (T-SQL) hello yeni sorgu penceresine aşağıdaki Yapıştır hello ve **yürütme** onu.</span><span class="sxs-lookup"><span data-stu-id="24ca3-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="24ca3-153">(Her zaman şifreli yapılandırma) sütunları şifrele</span><span class="sxs-lookup"><span data-stu-id="24ca3-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="24ca3-154">SSMS sağlayan bir sihirbaz tooeasily yapılandırma ayarlayarak hello CMK, CEK ve şifrelenmiş sütunlar, her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="24ca3-155">Genişletme **veritabanları** > **Clinic** > **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="24ca3-156">Sağ hello **hastalar** tablo ve seçin **şifrelemek sütunları** tooopen hello her zaman şifreli Sihirbazı:</span><span class="sxs-lookup"><span data-stu-id="24ca3-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Sütunları şifrele](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="24ca3-158">Merhaba her zaman şifreli Sihirbazı'nı içerir bölümleri aşağıdaki hello: **sütun seçimi**, **ana anahtar yapılandırma** (CMK) **doğrulama**, ve  **Özet**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="24ca3-159">Sütun Seçimi</span><span class="sxs-lookup"><span data-stu-id="24ca3-159">Column Selection</span></span>
<span data-ttu-id="24ca3-160">Tıklatın **sonraki** hello üzerinde **giriş** sayfa tooopen hello **sütun seçimi** sayfası.</span><span class="sxs-lookup"><span data-stu-id="24ca3-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="24ca3-161">Bu sayfada, hangi sütunların seçecektir tooencrypt, istediğiniz [hello şifreleme türünü ve hangi sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="24ca3-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="24ca3-162">Şifreleme **SSN** ve **doğum tarihi** bilgi için her bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="24ca3-163">Merhaba **SSN** sütun eşitlik aramaları, birleştirmeler ve Grupla destekleyen belirleyici şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="24ca3-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="24ca3-164">Merhaba **doğum tarihi** sütun işlemlerini desteklemeyen rastgele şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="24ca3-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="24ca3-165">Set hello **şifreleme türü** hello için **SSN** sütun çok**Deterministic** ve hello **doğum tarihi** sütun çok **Rastgele**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="24ca3-166">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="24ca3-166">Click **Next**.</span></span>

![Sütunları şifrele](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="24ca3-168">Ana anahtar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24ca3-168">Master Key Configuration</span></span>
<span data-ttu-id="24ca3-169">Merhaba **ana anahtar yapılandırma** sayfasıdır CMK ve select hello anahtar depolama sağlayıcısı hello CMK depolanacağı ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="24ca3-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="24ca3-170">Şu anda bir CMK hello Windows sertifika deposu, Azure anahtar kasası veya bir donanım güvenlik modülü (HSM) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="24ca3-171">Bu öğretici nasıl toostore anahtarlarınızı hello Windows sertifika depolamak gösterir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="24ca3-172">Doğrulayın **Windows sertifika deposunda** seçilir ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Ana anahtar yapılandırma](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="24ca3-174">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="24ca3-174">Validation</span></span>
<span data-ttu-id="24ca3-175">Merhaba sütunları şifrelemek veya bir PowerShell komut dosyası toorun daha sonra kaydedin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="24ca3-176">Bu öğretici için seçin **toofinish şimdi devam** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="24ca3-177">Özet</span><span class="sxs-lookup"><span data-stu-id="24ca3-177">Summary</span></span>
<span data-ttu-id="24ca3-178">Hello ayarlarının doğru olduğunu tıklatın emin olun ve **son** toocomplete hello kurulumu için her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Özet](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="24ca3-180">Merhaba sihirbazın Eylemler doğrulayın</span><span class="sxs-lookup"><span data-stu-id="24ca3-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="24ca3-181">Merhaba Sihirbaz tamamlandıktan sonra veritabanı her zaman şifreli için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="24ca3-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="24ca3-182">Merhaba gerçekleştirilen Sihirbazı hello aşağıdaki eylemler:</span><span class="sxs-lookup"><span data-stu-id="24ca3-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="24ca3-183">Bir CMK oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24ca3-183">Created a CMK.</span></span>
* <span data-ttu-id="24ca3-184">Bir CEK oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24ca3-184">Created a CEK.</span></span>
* <span data-ttu-id="24ca3-185">Seçili sütunları şifreleme için yapılandırılmış hello.</span><span class="sxs-lookup"><span data-stu-id="24ca3-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="24ca3-186">**Hastalar** tablosunda şu anda hiçbir veri var, ancak mevcut verileri hello seçili sütunlardaki şimdi şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="24ca3-187">Çok giderek SSMS hello anahtarlarında hello oluşturulmasını doğrulayabilirsiniz**Clinic** > **güvenlik** > **her zaman şifreli anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="24ca3-188">Sihirbaz sizin için oluşturulan hello hello yeni anahtarlar artık görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="24ca3-189">Şifrelenmiş hello verilerle çalışan istemci uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="24ca3-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="24ca3-190">Her zaman şifreli ayarlamak, gerçekleştiren bir uygulama oluşturabilirsiniz *ekler* ve *seçer* sütunlar üzerinde hello şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="24ca3-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="24ca3-191">Merhaba örnek uygulamayı çalıştırın toosuccessfully çalıştırılmalıdır üzerinde hello hello Sihirbazı'nı her zaman şifreli çalıştığı aynı bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="24ca3-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="24ca3-192">toorun hello uygulama başka bir bilgisayarda hello istemci uygulamasını çalıştıran her zaman şifreli sertifikaları toohello bilgisayarınızın dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="24ca3-193">Uygulamanızı kullanmalısınız [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) nesneleri düz metin veri toohello sunucusu her zaman şifreli sütunlarla geçirilirken.</span><span class="sxs-lookup"><span data-stu-id="24ca3-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="24ca3-194">Değişmez değerler SqlParameter nesnelerini kullanmadan geçirme bir özel durum neden olur.</span><span class="sxs-lookup"><span data-stu-id="24ca3-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="24ca3-195">Visual Studio'yu açın ve yeni bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24ca3-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="24ca3-196">Projenizi çok ayarlandığından emin olun**.NET Framework 4.6** veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="24ca3-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="24ca3-197">Ad hello proje **AlwaysEncryptedConsoleApp** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Yeni konsol uygulaması](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="24ca3-199">Bağlantı dizesi tooenable her zaman şifreli değiştirme</span><span class="sxs-lookup"><span data-stu-id="24ca3-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="24ca3-200">Bu bölümde nasıl tooenable veritabanı bağlantı dizenizi her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="24ca3-201">Merhaba konsol uygulaması "Örnek konsol uygulaması her zaman şifrelenir." Merhaba sonraki bölümde, az önce oluşturduğunuz değiştirir</span><span class="sxs-lookup"><span data-stu-id="24ca3-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="24ca3-202">tooenable her zaman şifreli, gereksinim duyduğunuz tooadd hello **sütun şifreleme ayarı** anahtar sözcüğü tooyour bağlantı dizesi ve çok ayarlayın**etkin**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="24ca3-203">Bu doğrudan hello bağlantı dizesinde ayarlayabilirsiniz veya kullanarak ayarlayabilirsiniz bir [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="24ca3-204">Merhaba Hello örnek uygulama sonraki bölüm gösterir nasıl toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="24ca3-205">Bu bir istemci uygulama belirli tooAlways içinde şifrelenmiş gerekli hello yalnızca değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="24ca3-206">Harici olarak kendi bağlantı dizesi depolar var olan bir uygulamanız varsa, (diğer bir deyişle, bir yapılandırma dosyasında), herhangi bir kod değiştirmeden mümkün tooenable her zaman şifreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="24ca3-207">Her zaman şifreli hello bağlantı dizesinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="24ca3-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="24ca3-208">Anahtar sözcüğü tooyour bağlantı dizesi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="24ca3-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="24ca3-209">Her zaman bir SqlConnectionStringBuilder ile şifrelenmiş etkinleştir</span><span class="sxs-lookup"><span data-stu-id="24ca3-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="24ca3-210">Merhaba aşağıdaki kod nasıl ayarlayarak tooenable her zaman şifreli hello gösterir [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) çok[etkin](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="24ca3-211">Her zaman şifreli örnek konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="24ca3-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="24ca3-212">Bu örnek gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="24ca3-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="24ca3-213">Bağlantı dizesi tooenable her zaman şifreli değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="24ca3-214">Veriler şifrelenmiş hello sütunlara ekleyin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="24ca3-215">Bir kayıt şifrelenmiş sütununda belirli bir değeri filtreleyerek seçin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="24ca3-216">Merhaba Değiştir **Program.cs** koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="24ca3-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="24ca3-217">Hello bağlantı dizesi hello genel connectionString değişken hello satır hello Main yönteminin doğrudan üstü için hello Azure portal, geçerli bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24ca3-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="24ca3-218">Bu toomake toothis kodu gerekli hello yalnızca değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="24ca3-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="24ca3-219">Merhaba uygulama toosee her zaman şifreli eylemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24ca3-219">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="24ca3-220">Merhaba verilerin şifrelendiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="24ca3-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="24ca3-221">Merhaba sorgulayarak hello sunucuda hello gerçek veri şifrelenir hızlı bir şekilde denetleyebilirsiniz **hastalar** SSMS ile verileri.</span><span class="sxs-lookup"><span data-stu-id="24ca3-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="24ca3-222">(Burada hello sütun şifreleme ayarı henüz etkinleştirilmedi geçerli bağlantınızı kullanın.)</span><span class="sxs-lookup"><span data-stu-id="24ca3-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="24ca3-223">Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24ca3-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="24ca3-224">Herhangi bir düz metin veri içermemesi hello şifrelenmiş sütunlar görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="24ca3-226">toouse SSMS tooaccess düz metin veri Merhaba, hello ekleyebilirsiniz **sütun şifreleme ayarı = etkin** parametresi toohello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="24ca3-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="24ca3-227">SSMS, sunucunuzun sağ **Object Explorer**ve ardından **Bağlantıyı Kes**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="24ca3-228">Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresi ve ardından **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="24ca3-229">Tıklatın **ek bağlantı parametrelerini** ve türü **sütun şifreleme ayarı = etkin**.</span><span class="sxs-lookup"><span data-stu-id="24ca3-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="24ca3-231">Çalışma hello hello bir sorguyu aşağıdaki **Clinic** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="24ca3-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="24ca3-232">Şimdi şifrelenmiş hello sütunlardaki hello düz metin verileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="24ca3-234">Farklı bir bilgisayardan SSMS (veya herhangi bir istemci) ile bağlanıyorsanız, erişim toohello şifreleme anahtarları olmaz ve mümkün toodecrypt hello veri olmaz.</span><span class="sxs-lookup"><span data-stu-id="24ca3-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="24ca3-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24ca3-235">Next steps</span></span>
<span data-ttu-id="24ca3-236">Her zaman şifreli kullanan bir veritabanı oluşturduktan sonra toodo hello aşağıdaki isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24ca3-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="24ca3-237">Bu örnek, farklı bir bilgisayardan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24ca3-237">Run this sample from a different computer.</span></span> <span data-ttu-id="24ca3-238">Böylece erişim toohello düz metin veri olmaz ve başarılı bir şekilde çalışmaz erişim toohello şifreleme anahtarları, olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="24ca3-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="24ca3-239">[Döndürün ve anahtarlarınızı Temizleme](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="24ca3-240">[Zaten her zaman şifreli ile şifrelenmiş veri geçişi](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ca3-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="24ca3-241">[Her zaman şifreli sertifikaları tooother istemci makineleri dağıtmak](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (Merhaba "sertifikalar kullanılabilir tooApplications ve kullanıcıların hale" bölümüne bakın).</span><span class="sxs-lookup"><span data-stu-id="24ca3-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="24ca3-242">İlgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="24ca3-242">Related information</span></span>
* [<span data-ttu-id="24ca3-243">Her zaman şifreli (istemci geliştirme)</span><span class="sxs-lookup"><span data-stu-id="24ca3-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="24ca3-244">Saydam veri şifreleme</span><span class="sxs-lookup"><span data-stu-id="24ca3-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="24ca3-245">SQL Server şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="24ca3-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="24ca3-246">Her zaman şifreli Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="24ca3-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="24ca3-247">Her zaman şifreli blogu</span><span class="sxs-lookup"><span data-stu-id="24ca3-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

