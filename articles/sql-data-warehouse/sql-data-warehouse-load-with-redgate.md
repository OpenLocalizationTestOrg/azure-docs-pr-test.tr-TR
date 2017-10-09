---
title: "aaaUse Redgate tooload veri tooyour Azure veri ambarı | Microsoft Docs"
description: "Bilgi nasıl toouse Redgate'nın veri platformu Studio veri depolama senaryolarında için."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Redgate Data Platform Studio ile veri yükleme
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

Bu öğretici şunların nasıl yapıldığını gösterir toouse [Redgate'nın veri platformu Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) bir şirket içi SQL Server tooAzure SQL veri ambarı (DPS) toomove verileri. Veri Platformu Studio hello en uygun uyumluluk düzeltmeleri uygular ve bu nedenle en iyi duruma getirme, hello hızlı şekilde tooget SQL Data Warehouse ile başlatıldı.

> [!NOTE]
> [Redgate](http://www.red-gate.com) çeşitli SQL Server araçları sunan uzun süreli bir Microsoft ortağıdır. Data Platform Studio’daki bu özellik hem ticari hem de ticari olmayan kullanımlar için ücretsiz olarak sunulmuştur.
> 
> 

## <a name="before-you-begin"></a>Başlamadan önce
### <a name="create-or-identify-resources"></a>Kaynak oluşturma veya tanımlama
Bu öğreticiye başlamadan önce toohave gerekir:

* **Şirket içi SQL Server veritabanı**: Merhaba tooimport tooSQL veri ambarı gereken bir şirket içi SQL Server'dan toocome istediğiniz verileri (sürüm 2008R2 veya üstü). Data Platform Studio, verileri bir Azure SQL Veritabanından veya metin dosyalarından doğrudan aktaramaz.
* **Azure depolama hesabı**: SQL Data Warehouse'a yüklemeden önce veri platformu Studio hello verileri Azure Blob Depolama aşamaları. Merhaba depolama hesabı hello "Klasik" dağıtım modeli yerine hello "Resource Manager" dağıtım modeli (Merhaba varsayılan) kullanmanız gerekir. Depolama hesabınız yoksa, bilgi nasıl tooCreate bir depolama hesabı. 
* **SQL veri ambarı**: toohave gerekir böylece Bu öğretici hello verileri şirket içi SQL Server tooSQL veri ambarı, çevrimiçi bir veri ambarı taşır. Veri ambarı zaten yoksa öğrenin nasıl tooCreate Azure SQL Data Warehouse.

> [!NOTE]
> Merhaba depolama hesabı ve hello veri ambarı hello aynı oluşturulmuş olması durumunda performans geliştirildi bölgesi.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>1. adım: tooData Platform Studio Azure hesabınızla oturum
Web tarayıcınızı açın ve toohello gidin [veri platformu Studio](https://www.dataplatformstudio.com/) Web sitesi. Oturum açma ile aynı Azure hesabı bu, kullanılan toocreate hello depolama hesabı ve veri ambarı hello. E-posta adresinizi bir iş veya Okul hesabı ve bir Microsoft hesabı ile ilişkili ise, erişim tooyour kaynaklara sahip emin toochoose hello hesabı olması.

> [!NOTE]
> Bu veri platformu Studio kullanarak ilk kez ise olduğunuz Azure kaynaklarınızı toogrant hello uygulama izni toomanage istedi.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>2. adım: hello İçeri Aktarma Sihirbazı'nı Başlat
Merhaba DPS ana ekranından, hello alma tooAzure SQL veri ambarı bağlantı toostart hello İçeri Aktarma Sihirbazı seçin.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>3. adım: hello veri platformu Studio ağ geçidi yükleme
tooconnect tooyour şirket içi SQL Server veritabanı tooinstall hello DPS ağ geçidi gerekir. Merhaba ağ geçidi erişim tooyour şirket içi ortamına hello verileri ayıklar ve tooyour depolama hesabı yükler sağlayan bir istemci aracısıdır. Verileriniz hiçbir zaman Redgate sunucularından geçmez. tooinstall hello ağ geçidi:

1. Merhaba tıklatın **ağ geçidi Oluştur** bağlantı
2. İndirme ve yükleme hello ağ geçidini kullanarak sağlanan yükleyici hello

![][2]

> [!NOTE]
> Merhaba ağ geçidi, ağ erişim toohello kaynak SQL Server veritabanı ile herhangi bir makinede yüklenebilir. Merhaba hello geçerli kullanıcı kimlik bilgileriyle Windows kimlik doğrulaması kullanarak hello SQL Server veritabanına erişir.
> 
> 

Yüklendikten sonra ağ geçidi durumu değişiklikleri tooConnected hello ve sonraki seçebilirsiniz.

## <a name="step-4-identify-hello-source-database"></a>4. adım: hello kaynak veritabanı tanımlayın
Merhaba, *sunucu adı girin* metin kutusuna, hello veritabanınızı barındıran hello sunucu adını girin ve **sonraki**. Ardından, hello açılır menüsünden tooimport verileri istediğiniz hello veritabanını seçin.

![][3]

DPS hello seçili veritabanı tabloları tooimport için olup olmadığını denetler. Varsayılan olarak, dağıtım noktaları hello veritabanındaki tüm hello tabloların alır. Tüm tabloları bağlantı hello genişleterek tabloları seçimini kaldırın veya seçin. Merhaba İleri düğmesi toomove İleri seçin.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>5. adım: depolama hesabı toostage hello veri seçin
Dağıtım noktaları için konum toostage hello verileri ister. Aboneliğinizde var olan bir depolama hesabı seçin ve **İleri**’yi seçin.

> [!NOTE]
> DPS depolama hesabı seçilen hello yeni blob kapsayıcı oluşturun ve her alma için ayrı bir klasör kullanın.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>6. Adım: Veri ambarı seçin
Ardından, bir çevrimiçi seçtiğiniz [Azure SQL Data Warehouse](http://aka.ms/sqldw) veritabanı tooimport hello verileri. Veritabanınızı seçtikten sonra tooenter hello kimlik bilgilerini tooconnect toohello gereken veritabanı ve seçin **sonraki**.

![][5]

> [!NOTE]
> DPS hello kaynak veri tabloları hello veri ambarına birleştirir. Dağıtım noktaları, hello tablo adı, var olan tabloları hello veri ambarı toooverwrite gerektirip gerektirmediğini sizi uyarır. İsteğe bağlı olarak hello veri ambarındaki mevcut tüm nesneleri silme ticking tarafından içe aktarma işleminden önce varolan tüm nesneler silebilir.
> 
> 

## <a name="step-7-import-hello-data"></a>7. adım: Hello Veri Al
DPS tooimport hello veri istediğiniz onaylar. Merhaba başlangıç İçe Aktar düğmesi toobegin hello veri alma tıklamanız yeterlidir.

![][6]

DPS ayıklanması ve hello şirket içi SQL Server ve hello ilerlemesini SQL Data Warehouse hello içe hello verileri karşıya hello ilerleme durumunu gösteren bir görsel öğe görüntüler.

![][7]

Merhaba alma işlemi tamamlandıktan sonra dağıtım noktaları hello veri alma özetini ve gerçekleştirilmiş hello uyumluluk düzeltmeleri değişiklik raporunu görüntüler.

![][8]

## <a name="next-steps"></a>Sonraki adımlar
Verilerinizi SQL Data warehouse'da tooexplore görüntüleyerek başlatın:

* [Azure SQL Veri Ambarı'nı (Visual Studio) Sorgulama][Query Azure SQL Data Warehouse (Visual Studio)]
* [Power BI ile verileri görselleştirme][Visualize data with Power BI]

toolearn Redgate'nın veri platformu Studio hakkında daha fazla bilgi:

* [Merhaba DPS giriş sayfasını ziyaret edin](http://www.dataplatformstudio.com/)
* [DPS Channel9 gösterimini izleyin](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Diğer yolları toomigrate ve Yük genel bakış için SQL Data Warehouse verilerinizi bakın:

* [Çözüm tooSQL veri ambarına geçirme][Migrate your solution tooSQL Data Warehouse]
* [Azure SQL Veri Ambarı’na veri yükleme](sql-data-warehouse-overview-load.md)

Daha fazla geliştirme ipuçları için bkz: Merhaba [SQL Data Warehouse geliştirmeye genel bakış](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
