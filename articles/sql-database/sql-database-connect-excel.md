---
title: "aaaConnect Excel tooSQL veritabanı | Microsoft Docs"
description: "Nasıl tooconnect Microsoft Excel tooAzure SQL veritabanı hello bulutta öğrenin. Raporlama ve veri araştırması için Excel'e veri aktarın."
services: sql-database
keywords: "Connect toosql excel, veri tooexcel İçeri Aktar"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="d30e2-105">Excel tooan Azure SQL veritabanına bağlanmak ve rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="d30e2-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="d30e2-106">Merhaba bulutta Excel tooa SQL veritabanına bağlanmak ve veri içeri aktarın ve tablolar ve grafikler hello veritabanındaki değerlere göre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d30e2-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="d30e2-107">Bu öğreticide, Excel ve bir veritabanı tablosu arasındaki hello bağlantı ayarlayacaksınız Excel için veri ve hello bağlantı bilgilerini depolayan hello dosyasını kaydedin ve veritabanı değerlerini'da hello Özet Grafik oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d30e2-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="d30e2-108">Başlayabilmek için Azure'da bir SQL veritabanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d30e2-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="d30e2-109">Yoksa, bkz: [ilk SQL veritabanınızı oluşturma](sql-database-get-started-portal.md) tooget bir veritabanı örnek verilerle birkaç dakika içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d30e2-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="d30e2-110">Bu makalede, ilgili makaleden Excel'e örnek veriler aktaracaksınız ancak kendi verilerinizle benzer adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d30e2-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="d30e2-111">Ayrıca, bir Excel kopyanızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d30e2-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="d30e2-112">Bu makalede [Microsoft Excel 2016](https://products.office.com/) kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d30e2-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="d30e2-113">Excel tooa SQL veritabanına bağlama ve odc dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d30e2-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="d30e2-114">tooconnect Excel tooSQL veritabanı Excel'i açın ve ardından yeni bir çalışma kitabı oluşturun veya varolan bir Excel çalışma kitabı açın.</span><span class="sxs-lookup"><span data-stu-id="d30e2-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="d30e2-115">Merhaba sayfanın üst kısmındaki hello hello menü çubuğunda tıklatın **veri**, tıklatın **diğer kaynaklardan**ve ardından **SQL Server'dan**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Veri kaynağını seçin: Excel tooSQL veritabanına bağlanın.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="d30e2-117">Merhaba Veri Bağlantı Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="d30e2-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="d30e2-118">Merhaba, **tooDatabase sunucu bağlanmak** iletişim kutusu, SQL veritabanı türü hello **sunucu adı** tooconnect tooin hello form istediğiniz <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="d30e2-119">Örneğin, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="d30e2-120">Altında **oturum açma kimlik bilgileri**, tıklatın **kullanıcı adı ve parola aşağıdaki kullanım hello**, türü hello **kullanıcı adı** ve **parola** için ayarlanmış oluşturduğunuz sırada Hello SQL veritabanı sunucusu ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Merhaba sunucu adını ve oturum açma kimlik bilgilerini yazın](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="d30e2-122">Ağ ortamınıza bağlı olarak mümkün tooconnect olmayabilir veya hello SQL veritabanı sunucusu, istemci IP adresinden gelen trafiğine izin vermiyorsa hello bağlantınız kesilebilir.</span><span class="sxs-lookup"><span data-stu-id="d30e2-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="d30e2-123">Toohello Git [Azure portal](https://portal.azure.com/), SQL Server'ı tıklatın, sunucunuzun'ı tıklatın, güvenlik duvarı ayarları altında ve istemci IP adresinizi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d30e2-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="d30e2-124">Bkz: [nasıl tooconfigure Güvenlik Duvarı ayarları](sql-database-configure-firewall-settings.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d30e2-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="d30e2-125">Merhaba, **veritabanı ve Tablo Seç** iletişim, ile toowork hello listeden istediğiniz ve hello tabloları veya görünümleri ile toowork istediğiniz ardından select hello veritabanı (seçtik **vGetAllCategories**) ve ardından tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Bir veritabanı ve tablo seçin.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="d30e2-127">Merhaba **veri bağlantısı dosyasını Kaydet ve Tamamla** iletişim kutusunu açar, burada, Excel'in kullandığı hello Office veritabanı bağlantısı (*.odc) dosyası hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d30e2-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="d30e2-128">Merhaba Varsayılanları bırakabilir veya kendi seçimlerinizi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d30e2-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="d30e2-129">Not hello ancak hello Varsayılanları bırakabilirsiniz **dosya adı** özellikle.</span><span class="sxs-lookup"><span data-stu-id="d30e2-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="d30e2-130">A **açıklama**, **kolay ad**, ve **arama anahtar sözcükleri** yardımcı olur ve diğer kullanıcıların bağlantı kurduğunuz unutmayın tooand hello bağlantı bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="d30e2-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="d30e2-131">Tıklatın **her zaman bu dosya toorefresh verileri toouse denemesi** tooit bağlanın ve ardından güncelleştirebilmesi için hello odc dosyasında depolanan bağlantı bilgilerinin isteyip istemediğinizi **son**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![ODC dosyasını kaydetme](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="d30e2-133">Merhaba **veri içeri aktarma** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d30e2-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="d30e2-134">Merhaba verileri Excel'e aktarmak ve Özet Grafik oluşturma</span><span class="sxs-lookup"><span data-stu-id="d30e2-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="d30e2-135">Merhaba bağlantısı ve veri ve bağlantı bilgilerini oluşturulan hello dosyasıyla belirlediğinize göre tooimport hello verileri okuma.</span><span class="sxs-lookup"><span data-stu-id="d30e2-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="d30e2-136">Merhaba, **veri içeri aktarma** iletişim kutusunda, verilerinizi hello çalışma sayfasında nasıl sunmak istediğiniz hello seçeneğini tıklatın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="d30e2-137">Biz **PivotChart** seçeneğini belirledik.</span><span class="sxs-lookup"><span data-stu-id="d30e2-137">We chose **PivotChart**.</span></span> <span data-ttu-id="d30e2-138">Toocreate de seçebilirsiniz bir **yeni çalışma sayfası** veya çok**bu veri tooa veri modeli ekleme**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="d30e2-139">Veri Modelleri hakkında daha fazla bilgi için bkz. [Excel'de veri modeli oluşturma](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="d30e2-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="d30e2-140">Tıklatın **özellikleri** tooexplore bilgilerini oluşturduğunuz Seçenekleri'nde hello veri yenileme hello önceki adım ve toochoose hello odc dosyası.</span><span class="sxs-lookup"><span data-stu-id="d30e2-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Excel'de veri için Hello biçimi seçme](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="d30e2-142">Merhaba çalışma şimdi bir boş Özet grafiği ve grafik var.</span><span class="sxs-lookup"><span data-stu-id="d30e2-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="d30e2-143">Altında **PivotTable alanları**, tooview istediğiniz alanları hello tüm hello onay kutularını seçin.</span><span class="sxs-lookup"><span data-stu-id="d30e2-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Veritabanı raporunu yapılandırın.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="d30e2-145">Diğer Excel çalışma kitaplarını ve çalışma toohello veritabanı tooconnect istiyorsanız, **veri**, tıklatın **bağlantıları**, tıklatın **Ekle**, oluşturduğunuz hello bağlantısı seçin Merhaba listesi ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="d30e2-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="d30e2-146">![Başka bir çalışma kitabından bağlantı açma](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="d30e2-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d30e2-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d30e2-147">Next steps</span></span>
* <span data-ttu-id="d30e2-148">Nasıl çok öğrenin[tooSQL veritabanı SQL Server Management Studio ile bağlanma](sql-database-connect-query-ssms.md) gelişmiş sorgulama ve analiz için.</span><span class="sxs-lookup"><span data-stu-id="d30e2-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="d30e2-149">Merhaba avantajları hakkında bilgi edinin [esnek havuzlar](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="d30e2-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="d30e2-150">Nasıl çok öğrenin[tooSQL veritabanı hello arka uçta bağlanan bir web uygulaması oluşturma](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d30e2-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

