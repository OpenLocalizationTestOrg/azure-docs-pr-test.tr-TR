---
title: "Machine Learning Studio çevrimiçi veri kaynaklarından aaaImport verisine | Microsoft Docs"
description: "Nasıl tooimport eğitim verilerinizi Azure Machine Learning Studio çevrimiçi çeşitli kaynaklardan."
keywords: "veriler, veri biçimi, veri türleri, veri kaynakları, eğitim verilerini içeri aktarma"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Azure Machine Learning Studio hello veri içeri aktarma modülü ile çeşitli çevrimiçi veri kaynaklarından veri aktarın
Bu makalede hello desteği verileri çevrimiçi çeşitli kaynaklardan içeri aktarma ve hello bilgiler bu kaynaklardan gelen toomove verileri bir Azure Machine Learning deneme gerekli.

> [!NOTE]
> Bu makalede hello hakkında genel bilgi sağlar [veri içeri aktarma] [ import-data] modülü. Merhaba erişebileceğiniz veri türleri hakkında daha ayrıntılı bilgi için biçimleri, parametreleri ve yanıtları toocommon sorular, hello hello modülü başvurusu konuya bakın [veri içeri aktarma] [ import-data] modülü.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Giriş
Hello kullanarak [veri içeri aktarma] [ import-data] modül erişebileceğiniz veri birkaç çevrimiçi veri kaynaklarından biri denemenizi çalışırken [Azure Machine Learning Studio](https://studio.azureml.net/Home):

* HTTP kullanarak bir Web URL'si
* Hadoop HiveQL kullanma
* Azure blob depolama
* Azure tablo
* Azure SQL veritabanına veya Azure VM'de SQL Server
* Şirket içi SQL Server veritabanı
* Sağlayıcı, şu anda OData veri akışı
* Azure CosmosDB (daha önce DocumentDB denir)

Studio denemenizi tooaccess çevrimiçi veri kaynaklarında eklemek hello [veri içeri aktarma] [ import-data] modülü tooyour, select hello **veri kaynağı**ve ardından gerekli hello parametreleri belirtin tooaccess hello verileri. desteklenen hello çevrimiçi veri kaynakları hello aşağıdaki tabloda listelenmektedir. Bu tablo da desteklenen dosya biçimleri hello özetler ve kullanılan tooaccess parametre veri hello.

Bu eğitim verileri denemenizi çalışırken erişildiği için yalnızca bu deneme kullanılabilir olduğunu unutmayın. Karşılaştırma, bir veri kümesi modülünde depolanan çalışma alanınızdaki kullanılabilir tooany deneme verilerdir.

> [!IMPORTANT]
> Şu anda hello [veri içeri aktarma] [ import-data] ve [verileri dışa aktar] [ export-data] modülleri okuma ve yalnızca hello kullanılarak oluşturulan Azure Storage'dan veri yazma Klasik dağıtım modeli. Diğer bir deyişle, sık erişimli depolama erişim katmanı sunar yeni Azure Blob Depolama hesabı türü hello veya seyrek erişimli depolama erişim katmanı henüz desteklenmiyor. 
> 
> Genellikle tüm Azure depolama hesapları bu hizmeti seçeneği kullanılabilir olmadan önce oluşturmuş olabileceğiniz olduğunu etkilenmez. 
> Yeni bir hesap toocreate gereksinim duyarsanız, seçin **Klasik** hello dağıtım için modeli veya Kaynak Yöneticisi'ni kullanın ve seçin **genel amaçlı** yerine **Blob storage** için **Tür hesap**. 
> 
> Daha fazla bilgi için bkz: [Azure Blob Storage: sık erişimli ve seyrek erişimli depolama katmanları](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Çevrimiçi veri kaynaklarında desteklenmemektedir
Azure Machine Learning **veri içeri aktarma** Modülü aşağıdaki veri kaynaklar hello destekler:

| Veri kaynağı | Açıklama | Parametreler |
| --- | --- | --- |
| HTTP üzerinden Web URL'si |Verileri virgülle ayrılmış değerler (CSV), sekmeyle ayrılmış değerler (TSV), öznitelik-ilişki dosyası biçimi (ARFF) ve Destek vektör makineler (SVM-light) biçimleri, HTTP kullanan tüm web URL'den okur |<b>URL</b>: hello hello site URL'si ve hello herhangi uzantılı dosya adı dahil olmak üzere hello dosyasının tam adı belirtir. <br/><br/><b>Veri biçimi</b>: desteklenen hello veri birini biçimleri belirtir: CSV, TSV, ARFF veya SVM açık. Merhaba veri başlık satırı varsa, kullanılan tooassign sütun adları olur. |
| Hadoop/HDFS |Hadoop dağıtılmış depolama alanından verileri okur. HiveQL, bir SQL benzeri sorgu dili kullanarak istediğiniz hello verileri belirtin. HiveQL da kullanılan tooaggregate veriler ve hello veri tooMachine Learning Studio eklemeden önce filtreleme verilerini gerçekleştirin. |<b>Veritabanı sorgusu hive</b>: hello Hive sorgusu kullanılan toogenerate hello veri belirtir.<br/><br/><b>HCatalog sunucusu URI </b> : Belirtilen hello hello biçimi kullanılarak, küme adını  *&lt;küme adınızı&gt;. azurehdinsight.net.*<br/><br/><b>Hadoop kullanıcı hesabı adı</b>: kullanılan tooprovision hello küme adı hello Hadoop kullanıcı hesabını belirtir.<br/><br/><b>Hadoop kullanıcı hesabı parolasını</b> : belirtir hello hello küme hazırlama sırasında kullanılan kimlik bilgileri. Daha fazla bilgi için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Çıktı verilerini konumunu</b>: hello verileri Hadoop dağıtılmış dosya sistemi (HDFS) veya Azure depolanan belirtir. <br/><ul>Çıktı verilerini HDFS'de depolamak hello HDFS sunucusu URI belirtin. (Emin toouse hello Hdınsight küme adı hello HTTPS:// öneki olmadan olabilir). <br/><br/>Azure'da, çıktı verilerini depolarsanız hello Azure depolama hesabı adı, depolama erişim tuşu ve depolama kapsayıcısı adı belirtmeniz gerekir.</ul> |
| SQL veritabanı |Bir Azure SQL veritabanında veya bir Azure sanal makine üzerinde çalışan bir SQL Server veritabanında depolanan verileri okur. |<b>Veritabanı sunucusu adı</b>: hello hangi hello üzerinde veritabanı çalıştığı hello sunucusunun adını belirtir.<br/><ul>Azure SQL veritabanı durumunda oluşturulur hello sunucu adı girin. Genellikle hello form sahip  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>Azure sanal bir makinede barındırılan bir SQL server durumunda girin *tcp:&lt;sanal makinenin DNS adı&gt;, 1433*</ul><br/><b>Veritabanı adı </b>: hello sunucuda hello hello veritabanı adını belirtir. <br/><br/><b>Sunucu kullanıcı hesabı adı</b>: hello veritabanı için erişim izinlerine sahip bir hesap için kullanıcı adını belirtir. <br/><br/><b>Sunucu kullanıcı hesabı parolasını</b>: hello hello kullanıcı hesabının parolasını belirtir.<br/><br/><b>Herhangi bir sunucu sertifikayı kabul</b>: tooskip verilerinizi okumadan önce hello site sertifikası gözden geçirmek istiyorsanız (daha az güvenli) bu seçeneği kullanın.<br/><br/><b>Veritabanı sorgusu</b>: tooread istediğiniz hello verileri tanımlayan bir SQL deyimi girin. |
| Şirket içi SQL veritabanı |Bir şirket içi SQL veritabanında depolanan verileri okur. |<b>Veri ağ geçidi</b>: hello veri yönetimi ağ geçidi burada da erişebilir, SQL Server veritabanınızın bir bilgisayarda yüklü hello adını belirtir. Merhaba ağ geçidi ayarlama hakkında daha fazla bilgi için bkz: [bir şirket içi SQL server verilerini kullanarak Azure Machine Learning ile gelişmiş analizler gerçekleştirme](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Veritabanı sunucusu adı</b>: hello hangi hello üzerinde veritabanı çalıştığı hello sunucusunun adını belirtir.<br/><br/><b>Veritabanı adı </b>: hello sunucuda hello hello veritabanı adını belirtir. <br/><br/><b>Sunucu kullanıcı hesabı adı</b>: hello veritabanı için erişim izinlerine sahip bir hesap için kullanıcı adını belirtir. <br/><br/><b>Kullanıcı adı ve parola</b>: tıklatın <b>değerleri girin</b> tooenter veritabanı kimlik bilgileri. Windows tümleşik kimlik doğrulaması veya SQL Server şirket içi SQL Server'ınızdaki nasıl yapılandırıldığına bağlı olarak kimlik doğrulaması kullanabilirsiniz.<br/><br/><b>Veritabanı sorgusu</b>: tooread istediğiniz hello verileri tanımlayan bir SQL deyimi girin. |
| Azure tablo |Hello Azure Storage tablo hizmeti verileri okur.<br/><br/>Büyük miktarlarda verinin seyrek okuma hello Azure tablo hizmeti kullanın. Esnek, sağlar ilişkisel olmayan (NoSQL), yüksek düzeyde ölçeklenebilir, ucuz ve yüksek oranda kullanılabilir bir depolama çözümü. |Merhaba hello seçeneklerinde **veri içeri aktarma** , ortak bilgi veya oturum açma kimlik bilgileri gerektiren bir özel depolama hesabına erişme bağlı olarak değiştirin. Bu hello tarafından belirlenir <b>kimlik doğrulama türü</b> "PublicOrSAS" veya "Hesap" değeri her biri kendi parametrelerinin sahip olabilir. <br/><br/><b>Ortak veya paylaşılan erişim imzası (SAS) URI</b>: hello Parametreler:<br/><br/><ul><b>Tablo URI</b>: hello tablosu için hello ortak ya da SAS URL'yi belirtir.<br/><br/><b>Özellik adları için Hello satırları tooscan belirtir</b>: hello değerler <i>TopN</i> tooscan hello satır sayısı, belirtilen veya <i>ScanAll</i> tooget tüm satırları hello tablosunda. <br/><br/>Merhaba veri homojen ve tahmin edilebilir ise, seçtiğiniz önerilir *TopN* ve N. için bir sayı girin Büyük tablolar için bu daha hızlı okuma kez neden olabilir.<br/><br/>Merhaba verileri hello derinliği ve Merhaba tablonun konuma göre farklılık özelliklerinin kümeleriyle yapılandırıldıysa hello seçin *ScanAll* tüm satırları tooscan seçeneği. Bu, sonuçta elde edilen özelliği ve meta veri dönüştürme hello bütünlüğü sağlar.<br/><br/></ul><b>Özel depolama hesabı</b>: hello Parametreler: <br/><br/><ul><b>Hesap adı</b>: hello hello tablo tooread içeren hello hesabının adını belirtir.<br/><br/><b>Hesap anahtarı</b>: hello hesabıyla ilişkilendirilmiş hello depolama anahtarını belirtir.<br/><br/><b>Tablo adı</b> : hello hello veri tooread içeren Merhaba tablonun adını belirtir.<br/><br/><b>Özellik adları için satır tooscan</b>: hello değerler <i>TopN</i> tooscan hello satır sayısı, belirtilen veya <i>ScanAll</i> tooget tüm satırları hello tablosunda.<br/><br/>Merhaba veri homojen ve tahmin edilebilir ise, seçtiğiniz öneririz *TopN* ve N. için bir sayı girin Büyük tablolar için bu daha hızlı okuma kez neden olabilir.<br/><br/>Merhaba verileri hello derinliği ve Merhaba tablonun konuma göre farklılık özelliklerinin kümeleriyle yapılandırıldıysa hello seçin *ScanAll* tüm satırları tooscan seçeneği. Bu, sonuçta elde edilen özelliği ve meta veri dönüştürme hello bütünlüğü sağlar.<br/><br/> |
| Azure Blob Depolama |Resimler, yapılandırılmamış metin veya ikili veriler dahil olmak üzere Azure Storage hello Blob hizmetinde depolanan verileri okur.<br/><br/>Merhaba Blob hizmeti toopublicly sunmaya verilerini veya tooprivately deposu uygulama verilerini kullanabilirsiniz. Verilerinizi yerden erişebilirsiniz HTTP veya HTTPS bağlantıları kullanarak. |Merhaba hello seçeneklerinde **veri içeri aktarma** ortak bilgi ya da oturum açma kimlik bilgileri gerektiren özel depolama hesabı erişmeye çalıştığınız bağlı olarak modülü Değiştir. Bu hello tarafından belirlenir <b>kimlik doğrulama türü</b> "PublicOrSAS" veya "Hesap" bir değer olabilir.<br/><br/><b>Ortak veya paylaşılan erişim imzası (SAS) URI</b>: hello Parametreler:<br/><br/><ul><b>URI</b>: hello depolama blobu hello ortak ya da SAS URL'yi belirtir.<br/><br/><b>Dosya biçimi</b>: hello Blob hizmeti hello veri hello biçimini belirtir. desteklenen hello biçimleri, CSV, TSV ve ARFF olacaktır.<br/><br/></ul><b>Özel depolama hesabı</b>: hello Parametreler: <br/><br/><ul><b>Hesap adı</b>: Merhaba tooread istediğiniz hello blob'un bulunduğu hello hesabının adını belirtir.<br/><br/><b>Hesap anahtarı</b>: hello hesabıyla ilişkilendirilmiş hello depolama anahtarını belirtir.<br/><br/><b>Yol toocontainer, dizin veya blob </b> : hello veri tooread içeren hello blob hello adını belirtir.<br/><br/><b>BLOB dosya biçimi</b>: hello blob hizmetinde hello veri hello biçimini belirtir. Merhaba desteklenen veri biçimleri CSV, TSV, ARFF, CSV belirtilen kodlama ve Excel olacaktır. <br/><br/><ul>Merhaba biçimi CSV veya TSV hello dosya üstbilgisi satır içerip içermediğini emin tooindicate olması.<br/><br/>Excel çalışma kitaplarından hello Excel seçeneği tooread verilerini kullanabilirsiniz. Merhaba, <i>Excel veri biçimi</i> seçeneği, belirtmek hello verileri bir Excel çalışma sayfası aralığı veya bir Excel tablosu olup. Merhaba, <i>Excel sayfası veya katıştırılmış tablo </i>seçeneği, hello hello sayfası veya gelen tooread istediğiniz tablo adını belirtin.</ul><br/> |
| Veri akış sağlayıcısı |Desteklenen bir akış Sağlayıcısı'ndan verileri okur. Şu anda yalnızca hello açık veri Protokolü (OData) biçiminde desteklenir. |<b>Veri içerik türü</b>: hello OData biçimi belirtir.<br/><br/><b>Kaynak URL</b>: hello veri akışının hello tam URL'sini belirtir. <br/>Örneğin, URL okuma hello Northwind örnek veritabanı'ndaki aşağıdaki hello: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Sonraki adımlar

[Veri alma ve verileri dışarı aktarma modülleri kullanan Azure ML web hizmetleri dağıtma](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
