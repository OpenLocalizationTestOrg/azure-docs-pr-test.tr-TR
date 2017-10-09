---
title: "SQL Server'dan Azure SQL veri ambarı (SSIS) içine aaaLoad veri | Microsoft Docs"
description: "Toocreate çok çeşitli verileri bir SQL Server Integration Services (SSIS) paketi toomove verilerinden tooSQL veri ambarına nasıl kaynakları gösterir."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>SQL Server'dan Azure SQL veri ambarı (SSIS) içine veri yükleme
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

SQL Server Integration Services (SSIS) paket tooload verileri SQL Server'dan Azure SQL Data Warehouse'a oluşturun. İsteğe bağlı olarak, yapılandırmayı, dönüştürme ve hello SSIS veri akışı geçerken hello verilerini temizlemek.

Bu öğreticide şunları yapacaksınız:

* Visual Studio'da yeni bir Integration Services projesi oluşturun.
* (Kaynak) olarak SQL Server ve SQL Data Warehouse (hedef) olarak da dahil olmak üzere toodata kaynaklar bağlayın.
* Merhaba hedefe hello kaynaktan verileri yükler bir SSIS paketi tasarlayın.
* Merhaba SSIS paketi tooload hello veri çalıştırın.

Bu öğretici, SQL Server hello veri kaynağı olarak kullanır. SQL Server, şirket içinde veya bir Azure sanal makinesi çalışıyor.

## <a name="basic-concepts"></a>Temel kavramlar
Merhaba paket hello SSIS iş birimidir. İlişkili paketleri projelerinde gruplandırılır. SQL Server veri araçları ile Visual Studio'da projeler ve tasarım paketler oluşturun. işlem, sürükleyip bileşenleri hello araç toohello tasarım yüzeyden bir görsel işlemidir hello tasarım bunları bağlamak ve özelliklerini ayarlayın. Paketinizi tamamladıktan sonra isteğe bağlı olarak tooSQL sunucu kapsamlı yönetim, izleme ve güvenlik dağıtabilirsiniz.

## <a name="options-for-loading-data-with-ssis"></a>SSIS ile veri yükleme seçenekleri
SQL Server Integration Services (SSIS) bağlanan ve bu verileri SQL Data Warehouse'a, yükleme için çeşitli seçenekler sağlayan esnek araçlar kümesidir.

1. ADO NET hedef tooconnect tooSQL veri ambarı kullanın. En az yapılandırma seçenekleri hello içerdiğinden Bu öğretici bir ADO NET hedef kullanır.
2. OLE DB hedef tooconnect tooSQL veri ambarı kullanın. Bu seçenek hello ADO NET hedef daha biraz daha iyi performans sağlayabilir.
3. Hello Azure Blob karşıya yükleme görev toostage hello verileri Azure Blob depolama alanına kullanın. Daha sonra hello SSIS SQL Yürüt görev toolaunch hello verileri SQL Data Warehouse'a yükler Polybase komut dosyası kullanın. Bu seçenek, burada listelenen hello üç seçenekten birini hello en iyi performans sağlar. tooget hello görev, Azure Blob karşıya yükle hello [Microsoft SQL Server 2016 tümleştirme hizmetleri özellik paketi Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. Polybase, hakkında daha fazla toolearn bkz [PolyBase Kılavuzu][PolyBase Guide].

## <a name="before-you-start"></a>Başlamadan önce
toostep Bu öğreticide, aşağıdakiler gerekir:

1. **SQL Server Integration Services (SSIS)**. SSIS SQL Server'ın bir bileşenidir ve bir değerlendirme sürümü veya SQL Server'ın lisanslı bir sürüm gerektirir. tooget SQL Server 2016 Önizleme'nin değerlendirme sürümünü bkz [SQL Server değerlendirme][SQL Server Evaluations].
2. **Visual Studio**. tooget ücretsiz Visual Studio Community Edition Merhaba, bkz: [Visual Studio Community][Visual Studio Community].
3. **SQL Server veri araçları Visual Studio (SSDT) için**. tooget SQL Server veri araçları Visual Studio için bkz: [karşıdan SQL Server veri Araçları'nı (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Örnek veri**. Bu öğretici, SQL Server'da SQL Data Warehouse'a yüklenen kaynak veri toobe hello gibi hello AdventureWorks örnek veritabanında depolanan örnek verileri kullanır. tooget hello AdventureWorks örnek veritabanı bkz [AdventureWorks 2014 örnek veritabanları][AdventureWorks 2014 Sample Databases].
5. **SQL veri ambarı veritabanı ve izinleri**. Bu öğretici tooa SQL Data Warehouse örneğine bağlanır ve verileri içine yükler. Bir tablo ve tooload veri toohave izinleri toocreate var.
6. **Bir güvenlik duvarı kuralı**. SQL veri ambarı veri toohello karşıya yüklemeden önce toocreate bir güvenlik duvarı kuralı SQL Data Warehouse, yerel bilgisayarınızın başlangıç IP adresi ile sahip.

## <a name="step-1-create-a-new-integration-services-project"></a>1. adım: yeni bir Integration Services projesi oluşturma
1. Visual Studio'yu başlatın.
2. Merhaba üzerinde **dosya** menüsünde, select **yeni | Proje**.
3. Toohello gidin **yüklü | Şablonları | İş Zekası | Integration Services** proje türleri.
4. Seçin **Integration Services proje**. İçin değerler sağlayın **adı** ve **konumu**ve ardından **Tamam**.

Visual Studio açar ve yeni bir Integration Services (SSIS) projesi oluşturur. Ardından Visual Studio hello projesinde hello Tasarımcısı hello tek yeni SSIS paketi için (Package.dtsx) açar. Ekran alanları aşağıdaki hello bakın:

* Merhaba solda hello **araç** SSIS bileşenlerinin.
* Merhaba ortadaki birden çok sekmelerle tasarım yüzeyi hello. Genellikle en az kullandığınız hello **akış denetimi** ve hello **veri akışını** sekmeleri.
* Sağ Hello üzerinde hello **Çözüm Gezgini** ve hello **özellikleri** bölmeleri.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>2. adım: hello temel veri akışı oluşturma
1. Bir veri akış görevi hello araç toohello merkezinden hello tasarım yüzeyine sürükleyin (Merhaba üzerinde **akış denetimi** sekmesi).
   
    ![][02]
2. Merhaba veri akış görevi tooswitch toohello veri akışı sekmesini çift tıklatın.
3. Merhaba diğer kaynakları listesinde hello araç kutusu, bir ADO.NET kaynak toohello tasarım yüzeyine sürükleyin. Halen seçili hello kaynak bağdaştırıcısıyla çok adını değiştirin**SQL Server Kaynak** hello içinde **özellikleri** bölmesi.
4. Merhaba diğer hedefler listesinden hello araç kutusu içinde hello ADO.NET kaynak altında bir ADO.NET hedef toohello tasarım yüzeyine sürükleyin. Halen seçili hello hedef bağdaştırıcısıyla çok adını değiştirin**SQL DW hedef** hello içinde **özellikleri** bölmesi.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>3. adım: hello kaynak bağdaştırıcısını yapılandırın
1. Merhaba kaynak bağdaştırıcısı tooopen hello çift **ADO.NET Kaynak Düzenleyici**.
   
    ![][03]
2. Merhaba üzerinde **Bağlantı Yöneticisi** hello sekmesinde **ADO.NET Kaynak Düzenleyici**, hello tıklatın **yeni** düğmesine bir sonraki toohello **ADO.NET Bağlantı Yöneticisi**listesi tooopen hello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusuna ve bu öğreticinin yükler veri hello SQL Server veritabanı için bağlantı ayarlarını oluşturun.
   
    ![][04]
3. Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırmak** iletişim kutusunda, hello **yeni** düğmesi tooopen hello **Bağlantı Yöneticisi** iletişim kutusuna ve yeni bir veri bağlantısı oluştur.
   
    ![][05]
4. Merhaba, **Bağlantı Yöneticisi** iletişim kutusunda, öğeleri hello.
   
   1. İçin **sağlayıcısı**, hello SqlClient veri sağlayıcısı seçin.
   2. İçin **sunucu adı**, hello SQL Server adı girin.
   3. Merhaba, **toohello sunucuda oturum** bölümünde, seçin veya kimlik doğrulama bilgilerini girin.
   4. Merhaba, **Bağlan tooa veritabanı** bölümünde, hello AdventureWorks örnek veritabanını seçin.
   5. Tıklatın **Bağlantıyı Sına**.
      
       ![][06]
   6. Merhaba hello bağlantı testi sonuçlarını raporlar hello iletişim kutusunda, tıklatın **Tamam** tooreturn toohello **Bağlantı Yöneticisi** iletişim kutusu.
   7. Merhaba, **Bağlantı Yöneticisi** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu.
5. Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Kaynak Düzenleyici**.
6. Merhaba, **ADO.NET Kaynak Düzenleyici**, hello içinde **Merhaba tablonun veya hello Görünüm adı** listesi, select hello **Sales.SalesOrderDetail** tablo.
   
    ![][07]
7. Tıklatın **Önizleme** toosee hello hello hello kaynak tablodaki veri ilk 200 satırı **Önizleme sorgu sonuçları** iletişim kutusu.
   
    ![][08]
8. Merhaba, **Önizleme sorgu sonuçları** iletişim kutusu, tıklatın **Kapat** tooreturn toohello **ADO.NET Kaynak Düzenleyici**.
9. Merhaba, **ADO.NET Kaynak Düzenleyici**, tıklatın **Tamam** toofinish hello veri kaynağını yapılandırma.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>4. adım: hello kaynak bağdaştırıcısı toohello hedef bağdaştırıcı bağlanma
1. Merhaba kaynak hello tasarım yüzeyi bağdaştırıcısında seçin.
2. Merhaba kaynağı bağdaştırıcısından genişletir hello mavi oku seçin ve yerine tutturur kadar toohello hedef Düzenleyicisi sürükleyin.
   
    ![][10]
   
    Tipik bir SSIS paketi diğer bileşenlerini hello SSIS araç hello kaynak ve hedef toorestructure Merhaba, dönüştürme arasında bir sayı kullanın ve hello SSIS veri akışı geçerken verilerinizi temizler. tookeep kadar basit Bu örnekte, biz bağlandığınız hello kaynak doğrudan toohello hedef.

## <a name="step-5-configure-hello-destination-adapter"></a>5. adım: hello hedef bağdaştırıcısını yapılandırın
1. Merhaba hedef bağdaştırıcı tooopen hello çift **ADO.NET hedef Düzenleyicisi**.
   
    ![][11]
2. Merhaba üzerinde **Bağlantı Yöneticisi** hello sekmesinde **ADO.NET hedef Düzenleyicisi**, hello tıklatın **yeni** düğmesine bir sonraki toohello **Bağlantı Yöneticisi**listesi tooopen hello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusuna ve bu öğreticinin veri yükler hello Azure SQL veri ambarı veritabanı için bağlantı ayarlarını oluşturun.
3. Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırmak** iletişim kutusunda, hello **yeni** düğmesi tooopen hello **Bağlantı Yöneticisi** iletişim kutusuna ve yeni bir veri bağlantısı oluştur.
4. Merhaba, **Bağlantı Yöneticisi** iletişim kutusunda, öğeleri hello.
   1. İçin **sağlayıcısı**, hello SqlClient veri sağlayıcısı seçin.
   2. İçin **sunucu adı**, hello SQL veri ambarı adını girin.
   3. Merhaba, **toohello sunucuda oturum** bölümünde, select **kullanım SQL Server kimlik doğrulaması** ve kimlik doğrulama bilgilerini girin.
   4. Merhaba, **Bağlan tooa veritabanı** bölümünde, var olan bir SQL veri ambarı veritabanını seçin.
   5. Tıklatın **Bağlantıyı Sına**.
   6. Merhaba hello bağlantı testi sonuçlarını raporlar hello iletişim kutusunda, tıklatın **Tamam** tooreturn toohello **Bağlantı Yöneticisi** iletişim kutusu.
   7. Merhaba, **Bağlantı Yöneticisi** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu.
5. Merhaba, **ADO.NET Bağlantı Yöneticisi'ni yapılandırma** iletişim kutusu, tıklatın **Tamam** tooreturn toohello **ADO.NET hedef Düzenleyicisi**.
6. Merhaba, **ADO.NET hedef Düzenleyicisi**, tıklatın **yeni** sonraki toohello **tablo veya görünüm kullanın** listesi tooopen hello **Create Table** iletişim kutusu toocreate hello kaynak tablosu ile eşleşen bir sütun listesi ile yeni bir hedef tablo.
   
    ![][12a]
7. Merhaba, **Create Table** iletişim kutusunda, öğeleri hello.
   
   1. Merhaba hello hedef tablo adını da değiştirmem**satış siparişi ayrıntısını**.
   2. Merhaba kaldırmak **ROWGUID** sütun. Merhaba **uniqueidentifier** veri türü, SQL veri ambarı'nda desteklenmiyor.
   3. Merhaba hello veri türünü değiştirmek **LineTotal** sütun çok**para**. Merhaba **ondalık** veri türü, SQL veri ambarı'nda desteklenmiyor. Desteklenen veri türleri hakkında daha fazla bilgi için bkz: [CREATE TABLE (Azure SQL Data Warehouse, paralel veri ambarı)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Tıklatın **Tamam** toocreate hello tablo ve return toohello **ADO.NET hedef Düzenleyicisi**.
8. Merhaba, **ADO.NET hedef Düzenleyicisi**seçin hello **eşlemeleri** toosee sekmesinde nasıl hello kaynağındaki sütunları hello hedef toocolumns eşlendi.
   
    ![][13]
9. Tıklatın **Tamam** toofinish hello veri kaynağını yapılandırma.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>6. adım: hello paket tooload hello verileri çalıştırma
Merhaba tıklatarak çalışma hello paket **Başlat** düğmesi hello araç çubuğunda veya hello birini seçerek **çalıştırmak** hello seçenekleri **hata ayıklama** menüsü.

Merhaba paket toorun başladığında, o ana kadarki işlenen satır sayısı hello yanı sıra sarı dönen Tekerlek tooindicate etkinlik bakın.

![][14]

Merhaba paket çalışması sona erdiğinde, yeşil onay işareti tooindicate başarı bkz yanı sıra hello kaynak toohello hedef yüklenen veri satırı toplam sayısı hello.

![][15]

Tebrikler! SQL Server Integration Services tooload verileri Azure SQL Data Warehouse'a başarıyla kullandığınız.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba SSIS veri akışı hakkında daha fazla bilgi edinin. Buradan başlayın: [veri akışını][Data Flow].
* Bilgi nasıl toodebug ve paketleri hak hello tasarım ortamında sorun giderme. Buradan başlayın: [paket geliştirme için sorun giderme araçları][Troubleshooting Tools for Package Development].
* Nasıl toodeploy, SSIS projeleri ve paketleri öğrenin tooIntegration Hizmetleri sunucusu veya tooanother depolama konumu. Buradan başlayın: [, dağıtım projeleri ve paketleri][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
