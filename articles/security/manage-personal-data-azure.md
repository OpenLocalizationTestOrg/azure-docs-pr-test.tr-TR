---
title: "aaaManage kişisel verileri Microsoft Azure | Microsoft Docs"
description: "yönergeler nasıl toocorrect, güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="fb147-103">Microsoft Azure kişisel verileri yönetmek</span><span class="sxs-lookup"><span data-stu-id="fb147-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="fb147-104">Bu makalede nasıl toocorrect, güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma yönergeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb147-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="fb147-105">Senaryo</span><span class="sxs-lookup"><span data-stu-id="fb147-105">Scenario</span></span>

<span data-ttu-id="fb147-106">Üst uç hedef Düğünler İrlanda ve hem de bir yerel ve uluslararası müşteri tabanı için Merhaba Dünya için tek adrestir alışveriş Dublin tabanlı şirket sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb147-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="fb147-107">Ofisleri, müşteriler, çalışanların ve satıcıların bunlar sunar hello world toofully hizmet hello görebildikleri bulunan sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="fb147-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="fb147-108">Diğer birçok öğeler arasında hello şirket yemek Alerjiler ve dietary Tercihler dahil LCV'ler izler.</span><span class="sxs-lookup"><span data-stu-id="fb147-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="fb147-109">Evlilik konuklar arabası, horseback gözatan, bot gibi üstündeçalýþan, vb. için çeşitli etkinlikleri kaydetmek ve hatta birbiriyle merkezi bir web sayfasında toohello olay baştaki hello ay sırasında etkileşim.</span><span class="sxs-lookup"><span data-stu-id="fb147-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="fb147-110">Merhaba şirket, çalışanlar, satıcılar, müşteriler ve Evlilik konuklar kişisel bilgileri toplar.</span><span class="sxs-lookup"><span data-stu-id="fb147-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="fb147-111">Hello nedeniyle hello iş hello şirket uluslararası yapısını düzenleme birden çok düzeyi ile uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fb147-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="fb147-112">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="fb147-112">Problem statement</span></span>

- <span data-ttu-id="fb147-113">Veri admins mümkün toocorrect yanlış kişisel bilgi ve güncelleştirme eksik ya da değişen kişisel bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb147-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="fb147-114">Veri admins gerek mümkün toodelete bir veri konunun hello istek üzerine kişisel bilgileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb147-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="fb147-115">Veri admins tooexport verilere ihtiyaç ve tooa veri konu bilgilendirilmesine istek üzerine ortak, yapılandırılmış bir biçimde sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fb147-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="fb147-116">Şirketin hedeflerine</span><span class="sxs-lookup"><span data-stu-id="fb147-116">Company goals</span></span>

- <span data-ttu-id="fb147-117">Yanlış veya tamamlanmamış müşteri, Evlilik konuk, çalışan ve satıcı kişisel bilgileri düzeltildi veya gerekir Azure Active Directory ve Azure SQL veritabanı güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="fb147-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="fb147-118">Kişisel bilgiler Azure Active Directory ve Azure SQL veritabanı veri konu hello istek üzerine silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb147-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="fb147-119">Kişisel veriler ortak, yapılandırılmış bir biçimde bir veri konunun hello istek üzerine aktarılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb147-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="fb147-120">Çözümler</span><span class="sxs-lookup"><span data-stu-id="fb147-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="fb147-121">Azure Active Directory: yanlış veya tamamlanmamış kişisel verileri düzeltmek/düzeltin ve silme/kişisel veri/kullanıcı profillerini Sil</span><span class="sxs-lookup"><span data-stu-id="fb147-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="fb147-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) Microsoft'un bulut tabanlı, çok kiracılı dizin ve kimlik yönetimi hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="fb147-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="fb147-123">Düzeltin, güncelleştirmek veya müşteri ve çalışan kullanıcı profilleri ve bir kullanıcının adını, iş başlığı, adresi veya telefon numarası gibi kişisel verileri içerdiğini kullanıcı iş bilgilerini silmek, [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) hello kullanarak ortam [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fb147-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="fb147-124">Merhaba dizin için genel yönetici olan bir hesapla oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb147-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="fb147-125">Nasıl düzeltin veya kullanıcı profili ve iş güncelleştirme bilgileri Azure Active Directory'de?</span><span class="sxs-lookup"><span data-stu-id="fb147-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="fb147-126">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="fb147-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="fb147-127">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fb147-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![Medya/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="fb147-129">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fb147-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="fb147-131">Merhaba üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde hello listeden bir kullanıcı seçin ve sonra hello dikey penceresinde hello seçilen kullanıcı,'i seçin **profil** düzeltildi toobe gereken tooview hello kullanıcı profili bilgileri veya güncelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="fb147-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![Medya/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="fb147-133">Düzeltin veya güncelleştirme hello bilgileri ve hello komut çubuğunda, ardından **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fb147-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="fb147-134">Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **iş bilgisi** toobe gereken tooview kullanıcı iş bilgilerini düzeltildi veya güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fb147-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![Medya/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="fb147-136">Düzeltin veya hello kullanıcı iş bilgilerini güncelleştirmek ve hello komut çubuğunda, ardından **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fb147-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="fb147-137">Azure Active Directory'de bir kullanıcı profili nasıl silebilirim?</span><span class="sxs-lookup"><span data-stu-id="fb147-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="fb147-138">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="fb147-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="fb147-139">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fb147-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="fb147-140">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fb147-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="fb147-142">Merhaba üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde, kullanıcı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="fb147-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![Medya/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="fb147-144">Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **genel bakış**ve hello komut çubuğunda, ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="fb147-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="fb147-145">SQL veritabanı: düzeltin ve düzeltmek yanlış veya tamamlanmamış kişisel veri; Kişisel verileri silme veya silme; Kişisel verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="fb147-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="fb147-146">[Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) yapı ve uygulamalarını geliştiriciler yardımcı olan bir bulut veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="fb147-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="fb147-147">Kişisel veriler güncelleştirilebilir [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) standart SQL sorguları kullanılarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="fb147-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="fb147-148">Ayrıca, kişisel verileri çeşitli hello Azure SQL Server içeri ve Dışarı Aktarma Sihirbazı'nı dahil olmak üzere yöntemleri ve biçimleri, bir BACPAC dosyası dahil olmak üzere çeşitli kullanarak SQL veritabanından dışa aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb147-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="fb147-149">Nasıl düzeltin, güncelleştirme veya SQL veritabanında kişisel verileri silme?</span><span class="sxs-lookup"><span data-stu-id="fb147-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="fb147-150">toolearn nasıl toocorrect veya güncelleştirme kişisel verileri SQL veritabanında ziyaret hello [güncelleştirme (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [güncelleştirme metin](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [güncelleştirme ile ortak tablo ifadesinin](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), veya [ Metni Yaz güncelleştirme](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fb147-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="fb147-151">toolearn nasıl toodelete kişisel veriler SQL veritabanında ziyaret hello [(Transact-SQL) Delete](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fb147-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="fb147-152">Kişisel veri tooa BACPAC SQL veritabanı dosyasında nasıl dışarı?</span><span class="sxs-lookup"><span data-stu-id="fb147-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="fb147-153">Bir BACPAC dosya hello SQL veritabanı veri ve meta verileri içerir ve bir BACPAC uzantılı bir zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="fb147-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="fb147-154">Bu yapılabilir hello kullanarak [Azure portal](https://portal.azure.com/), SQLPackage komut satırı yardımcı programı, SQL Server Management Studio (SSMS) veya PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="fb147-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="fb147-155">toolearn nasıl tooexport veri tooa BACPAC dosyası, ziyaret hello [bir Azure SQL veritabanı tooa BACPAC dosyasını dışarı](https://docs.microsoft.com/azure/sql-database/sql-database-export) sayfasında, yukarıda listelenen her bir yöntemin ayrıntılı yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="fb147-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="fb147-156">Kişisel veriler nasıl SQL veritabanıyla hello SQL Server içeri ve Dışarı Aktarma Sihirbazı verme?</span><span class="sxs-lookup"><span data-stu-id="fb147-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="fb147-157">Bu sihirbaz bir kaynak tooa hedef veri kopyalamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fb147-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="fb147-158">Bir giriş toohello Sihirbazı için nasıl tooget, izinleri bilgiler ve nasıl tooget yardımcı hello aracıyla ziyaret dahil olmak üzere hello [içeri aktarma ve dışarı aktarma veri ile Merhaba SQL Server içeri ve Dışarı Aktarma Sihirbazı](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web sayfası.</span><span class="sxs-lookup"><span data-stu-id="fb147-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="fb147-159">Merhaba hello Sihirbazı için adımlara genel bakış için ziyaret [hello SQL Server içeri ve Dışarı Aktarma Sihirbazı'ndaki adımları](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web sayfası.</span><span class="sxs-lookup"><span data-stu-id="fb147-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb147-160">Sonraki Adımlar:</span><span class="sxs-lookup"><span data-stu-id="fb147-160">Next Steps:</span></span>

[<span data-ttu-id="fb147-161">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="fb147-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="fb147-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb147-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

