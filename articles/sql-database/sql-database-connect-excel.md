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
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Excel tooan Azure SQL veritabanına bağlanmak ve rapor oluşturma

Merhaba bulutta Excel tooa SQL veritabanına bağlanmak ve veri içeri aktarın ve tablolar ve grafikler hello veritabanındaki değerlere göre oluşturun. Bu öğreticide, Excel ve bir veritabanı tablosu arasındaki hello bağlantı ayarlayacaksınız Excel için veri ve hello bağlantı bilgilerini depolayan hello dosyasını kaydedin ve veritabanı değerlerini'da hello Özet Grafik oluşturma.

Başlayabilmek için Azure'da bir SQL veritabanınızın olması gerekir. Yoksa, bkz: [ilk SQL veritabanınızı oluşturma](sql-database-get-started-portal.md) tooget bir veritabanı örnek verilerle birkaç dakika içinde çalışır. Bu makalede, ilgili makaleden Excel'e örnek veriler aktaracaksınız ancak kendi verilerinizle benzer adımları izleyebilirsiniz.

Ayrıca, bir Excel kopyanızın olması gerekir. Bu makalede [Microsoft Excel 2016](https://products.office.com/) kullanılmıştır.

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Excel tooa SQL veritabanına bağlama ve odc dosyası oluşturma
1. tooconnect Excel tooSQL veritabanı Excel'i açın ve ardından yeni bir çalışma kitabı oluşturun veya varolan bir Excel çalışma kitabı açın.
2. Merhaba sayfanın üst kısmındaki hello hello menü çubuğunda tıklatın **veri**, tıklatın **diğer kaynaklardan**ve ardından **SQL Server'dan**.
   
   ![Veri kaynağını seçin: Excel tooSQL veritabanına bağlanın.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Merhaba Veri Bağlantı Sihirbazı açılır.
3. Merhaba, **tooDatabase sunucu bağlanmak** iletişim kutusu, SQL veritabanı türü hello **sunucu adı** tooconnect tooin hello form istediğiniz <*servername* > **. database.windows.net**. Örneğin, **adworkserver.database.windows.net**.
4. Altında **oturum açma kimlik bilgileri**, tıklatın **kullanıcı adı ve parola aşağıdaki kullanım hello**, türü hello **kullanıcı adı** ve **parola** için ayarlanmış oluşturduğunuz sırada Hello SQL veritabanı sunucusu ve ardından **sonraki**.
   
   ![Merhaba sunucu adını ve oturum açma kimlik bilgilerini yazın](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Ağ ortamınıza bağlı olarak mümkün tooconnect olmayabilir veya hello SQL veritabanı sunucusu, istemci IP adresinden gelen trafiğine izin vermiyorsa hello bağlantınız kesilebilir. Toohello Git [Azure portal](https://portal.azure.com/), SQL Server'ı tıklatın, sunucunuzun'ı tıklatın, güvenlik duvarı ayarları altında ve istemci IP adresinizi ekleyin. Bkz: [nasıl tooconfigure Güvenlik Duvarı ayarları](sql-database-configure-firewall-settings.md) Ayrıntılar için.
   > 
   > 
5. Merhaba, **veritabanı ve Tablo Seç** iletişim, ile toowork hello listeden istediğiniz ve hello tabloları veya görünümleri ile toowork istediğiniz ardından select hello veritabanı (seçtik **vGetAllCategories**) ve ardından tıklatın **sonraki**.
   
    ![Bir veritabanı ve tablo seçin.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Merhaba **veri bağlantısı dosyasını Kaydet ve Tamamla** iletişim kutusunu açar, burada, Excel'in kullandığı hello Office veritabanı bağlantısı (*.odc) dosyası hakkında bilgi sağlar. Merhaba Varsayılanları bırakabilir veya kendi seçimlerinizi özelleştirebilirsiniz.
6. Not hello ancak hello Varsayılanları bırakabilirsiniz **dosya adı** özellikle. A **açıklama**, **kolay ad**, ve **arama anahtar sözcükleri** yardımcı olur ve diğer kullanıcıların bağlantı kurduğunuz unutmayın tooand hello bağlantı bulunamıyor. Tıklatın **her zaman bu dosya toorefresh verileri toouse denemesi** tooit bağlanın ve ardından güncelleştirebilmesi için hello odc dosyasında depolanan bağlantı bilgilerinin isteyip istemediğinizi **son**.
   
    ![ODC dosyasını kaydetme](./media/sql-database-connect-excel/save-odc-file.png)
   
    Merhaba **veri içeri aktarma** iletişim kutusu görüntülenir.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Merhaba verileri Excel'e aktarmak ve Özet Grafik oluşturma
Merhaba bağlantısı ve veri ve bağlantı bilgilerini oluşturulan hello dosyasıyla belirlediğinize göre tooimport hello verileri okuma.

1. Merhaba, **veri içeri aktarma** iletişim kutusunda, verilerinizi hello çalışma sayfasında nasıl sunmak istediğiniz hello seçeneğini tıklatın ve ardından **Tamam**. Biz **PivotChart** seçeneğini belirledik. Toocreate de seçebilirsiniz bir **yeni çalışma sayfası** veya çok**bu veri tooa veri modeli ekleme**. Veri Modelleri hakkında daha fazla bilgi için bkz. [Excel'de veri modeli oluşturma](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Tıklatın **özellikleri** tooexplore bilgilerini oluşturduğunuz Seçenekleri'nde hello veri yenileme hello önceki adım ve toochoose hello odc dosyası.
   
    ![Excel'de veri için Hello biçimi seçme](./media/sql-database-connect-excel/import-data.png)
   
    Merhaba çalışma şimdi bir boş Özet grafiği ve grafik var.
2. Altında **PivotTable alanları**, tooview istediğiniz alanları hello tüm hello onay kutularını seçin.
   
    ![Veritabanı raporunu yapılandırın.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Diğer Excel çalışma kitaplarını ve çalışma toohello veritabanı tooconnect istiyorsanız, **veri**, tıklatın **bağlantıları**, tıklatın **Ekle**, oluşturduğunuz hello bağlantısı seçin Merhaba listesi ve ardından **açık**.
> ![Başka bir çalışma kitabından bağlantı açma](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[tooSQL veritabanı SQL Server Management Studio ile bağlanma](sql-database-connect-query-ssms.md) gelişmiş sorgulama ve analiz için.
* Merhaba avantajları hakkında bilgi edinin [esnek havuzlar](sql-database-elastic-pool.md).
* Nasıl çok öğrenin[tooSQL veritabanı hello arka uçta bağlanan bir web uygulaması oluşturma](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

