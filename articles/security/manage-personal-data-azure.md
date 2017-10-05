---
title: "Microsoft Azure kişisel verileri yönetmek | Microsoft Docs"
description: "Kılavuzu nasıl düzeltileceğine güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma"
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
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="fde6a-103">Microsoft Azure kişisel verileri yönetmek</span><span class="sxs-lookup"><span data-stu-id="fde6a-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="fde6a-104">Bu makale, düzeltin, güncelleştirme, silme ve Azure Active Directory ve Azure SQL veritabanı kişisel verileri dışarı aktarma konusunda rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="fde6a-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="fde6a-105">Senaryo</span><span class="sxs-lookup"><span data-stu-id="fde6a-105">Scenario</span></span>

<span data-ttu-id="fde6a-106">Üst uç hedef Düğünler İrlanda ve dünyanın her iki bir yerel ve uluslararası müşteri için temel için tek adrestir alışveriş Dublin tabanlı şirket sağlar.</span><span class="sxs-lookup"><span data-stu-id="fde6a-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="fde6a-107">Ofisleri, müşteriler, çalışanlar ve bunlar sunar görebildikleri tam olarak hizmet vermek için Satıcılar tüm dünyada bulunan sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="fde6a-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="fde6a-108">Diğer birçok öğeler arasında şirket yemek Alerjiler ve dietary Tercihler dahil LCV'ler izler.</span><span class="sxs-lookup"><span data-stu-id="fde6a-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="fde6a-109">Evlilik konuklar arabası, horseback gözatan, bot gibi üstündeçalýþan, vb. için çeşitli etkinlikleri kaydetmek ve hatta birbiriyle merkezi bir web sayfasında olayla ay sırasında etkileşim.</span><span class="sxs-lookup"><span data-stu-id="fde6a-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="fde6a-110">Şirket, çalışanlar, satıcılar, müşteriler ve Evlilik konuklar kişisel bilgileri toplar.</span><span class="sxs-lookup"><span data-stu-id="fde6a-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="fde6a-111">İş uluslararası yapısı nedeniyle şirket düzenleme birden çok düzeyi ile uyumlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fde6a-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="fde6a-112">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="fde6a-112">Problem statement</span></span>

- <span data-ttu-id="fde6a-113">Veri admins doğru yanlış kişisel bilgileri ve güncelleştirme eksik ya da değişen kişisel bilgilere sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="fde6a-114">Veri admins gerek veri konu istek üzerine kişisel bilgileri silmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="fde6a-115">Verileri dışarı aktarma ve veri konu ortak, yapılandırılmış bir biçimde bilgilendirilmesine istek üzerine sağlamak veri admins gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="fde6a-116">Şirketin hedeflerine</span><span class="sxs-lookup"><span data-stu-id="fde6a-116">Company goals</span></span>

- <span data-ttu-id="fde6a-117">Yanlış veya tamamlanmamış müşteri, Evlilik konuk, çalışan ve satıcı kişisel bilgileri düzeltildi veya gerekir Azure Active Directory ve Azure SQL veritabanı güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="fde6a-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="fde6a-118">Kişisel bilgiler Azure Active Directory ve Azure SQL veritabanı veri konu istek üzerine silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="fde6a-119">Kişisel veriler ortak, yapılandırılmış bir biçimde bir veri konu istek üzerine aktarılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="fde6a-120">Çözümler</span><span class="sxs-lookup"><span data-stu-id="fde6a-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="fde6a-121">Azure Active Directory: yanlış veya tamamlanmamış kişisel verileri düzeltmek/düzeltin ve silme/kişisel veri/kullanıcı profillerini Sil</span><span class="sxs-lookup"><span data-stu-id="fde6a-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="fde6a-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) Microsoft'un bulut tabanlı, çok kiracılı dizin ve kimlik yönetimi hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="fde6a-123">Düzeltin, güncelleştirmek veya müşteri ve çalışan kullanıcı profilleri ve bir kullanıcının adını, iş başlığı, adresi veya telefon numarası gibi kişisel verileri içerdiğini kullanıcı iş bilgilerini silmek, [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) kullanarak ortam [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fde6a-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="fde6a-124">Dizin için genel yönetici olan bir hesapla oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="fde6a-125">Nasıl düzeltin veya kullanıcı profili ve iş güncelleştirme bilgileri Azure Active Directory'de?</span><span class="sxs-lookup"><span data-stu-id="fde6a-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="fde6a-126">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="fde6a-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="fde6a-127">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fde6a-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![Medya/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="fde6a-129">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fde6a-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="fde6a-131">Üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde, listeden bir kullanıcı seçin ve ardından dikey penceresinde seçili kullanıcı, seçin **profil** düzeltildi veya güncelleştirilmesi için gereken kullanıcı profili bilgilerini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fde6a-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![Medya/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="fde6a-133">Düzeltin veya bilgileri güncelleştirmek ve ardından komut çubuğunda seçin **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fde6a-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="fde6a-134">Seçilen kullanıcı için dikey seçin **iş bilgisi** düzeltildi veya güncelleştirilmesi için gereken kullanıcı iş bilgilerini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fde6a-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![Medya/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="fde6a-136">Düzeltin veya kullanıcı iş bilgilerini güncelleştirin ve ardından komut çubuğunda seçin **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="fde6a-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="fde6a-137">Azure Active Directory'de bir kullanıcı profili nasıl silebilirim?</span><span class="sxs-lookup"><span data-stu-id="fde6a-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="fde6a-138">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="fde6a-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="fde6a-139">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fde6a-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="fde6a-140">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="fde6a-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![Medya/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="fde6a-142">**Kullanıcılar ve gruplar - Kullanıcılar** dikey penceresinde, listeden bir kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="fde6a-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![Medya/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="fde6a-144">Seçilen kullanıcı için dikey seçin **genel bakış**ve ardından komut çubuğunda **silmek**.</span><span class="sxs-lookup"><span data-stu-id="fde6a-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="fde6a-145">SQL veritabanı: düzeltin ve düzeltmek yanlış veya tamamlanmamış kişisel veri; Kişisel verileri silme veya silme; Kişisel verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="fde6a-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="fde6a-146">[Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) yapı ve uygulamalarını geliştiriciler yardımcı olan bir bulut veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="fde6a-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="fde6a-147">Kişisel veriler güncelleştirilebilir [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) standart SQL sorguları kullanılarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="fde6a-148">Ayrıca, kişisel verileri içeri ve Dışarı Aktarma Sihirbazı çeşitli yöntemler, Azure SQL Server dahil olmak üzere SQL veritabanı kullanma ve biçimleri, bir BACPAC dosyası dahil olmak üzere çeşitli aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="fde6a-149">Nasıl düzeltin, güncelleştirme veya SQL veritabanında kişisel verileri silme?</span><span class="sxs-lookup"><span data-stu-id="fde6a-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="fde6a-150">Düzeltmek veya kişisel verileri SQL veritabanında güncelleştirmek öğrenmek için ziyaret [güncelleştirme (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [güncelleştirme metin](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [güncelleştirme ile ortak tablo ifadesinin](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), veya [Güncelleştirme metni yaz](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fde6a-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="fde6a-151">SQL veritabanı kişisel verileri silme hakkında bilgi için [(Transact-SQL) Delete](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fde6a-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="fde6a-152">Nasıl ı kişisel verileri SQL veritabanındaki bir BACPAC dosyası dışarı?</span><span class="sxs-lookup"><span data-stu-id="fde6a-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="fde6a-153">Bir BACPAC dosya SQL veritabanı veri ve meta verileri içerir ve bir BACPAC uzantılı bir zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="fde6a-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="fde6a-154">Bu yapılabilir kullanarak [Azure portal](https://portal.azure.com/), SQLPackage komut satırı yardımcı programı, SQL Server Management Studio (SSMS) veya PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fde6a-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="fde6a-155">Verilerini bir BACPAC dosyasına verme konusunda bilgi almak için şurayı ziyaret edin [bir Azure SQL veritabanı BACPAC dosyaya](https://docs.microsoft.com/azure/sql-database/sql-database-export) sayfasında, yukarıda listelenen her bir yöntemin ayrıntılı yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="fde6a-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="fde6a-156">Nasıl ı kişisel verileri SQL veritabanı SQL Server içeri ve Dışarı Aktarma Sihirbazı ile verilecek?</span><span class="sxs-lookup"><span data-stu-id="fde6a-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="fde6a-157">Bu sihirbaz verileri bir kaynaktan bir hedefe kopyalamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fde6a-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="fde6a-158">Alma Sihirbazı'na giriş için de dahil olmak üzere izin bilgileri ve aracı ile ilgili Yardım almak için ziyaret nasıl [içeri ve dışarı aktarma veri SQL Server içeri ve Dışarı Aktarma Sihirbazı ile](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web sayfası.</span><span class="sxs-lookup"><span data-stu-id="fde6a-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="fde6a-159">Sihirbazın adımlarını genel bakış için ziyaret [SQL Server içeri ve Dışarı Aktarma Sihirbazı'nda adımları](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web sayfası.</span><span class="sxs-lookup"><span data-stu-id="fde6a-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fde6a-160">Sonraki Adımlar:</span><span class="sxs-lookup"><span data-stu-id="fde6a-160">Next Steps:</span></span>

[<span data-ttu-id="fde6a-161">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="fde6a-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="fde6a-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fde6a-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

