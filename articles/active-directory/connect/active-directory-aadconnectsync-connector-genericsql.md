---
title: "aaaGeneric SQL bağlayıcı | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure Microsoft'un Genel SQL bağlayıcı."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Genel SQL bağlayıcı Teknik Başvurusu
Bu makalede hello Genel SQL bağlayıcı açıklanmaktadır. Merhaba makale ürünleri aşağıdaki toohello geçerlidir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Düzeltme 4.1.3671.0 kullanmanız gerekir ya da daha sonra [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 ve FIM2010R2 için hello bağlayıcı olarak hello Merkezi'nden kullanılabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee eylem, bu bağlayıcı bkz hello [Genel SQL bağlayıcı adım adım](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) makalesi.

## <a name="overview-of-hello-generic-sql-connector"></a>Merhaba Genel SQL Connector genel bakış
Merhaba Genel SQL bağlayıcı toointegrate hello eşitleme hizmeti bir veritabanı sistemiyle ODBC bağlantı sunar sağlar.  

Üst düzey açısından bakıldığında, özellikler aşağıdaki hello hello sürümü geçerli hello bağlayıcı tarafından desteklenir:

| Özellik | Destek |
| --- | --- |
| Bağlı veri kaynağı |Merhaba bağlayıcı tüm 64-bit ODBC sürücüleri ile desteklenir. Merhaba aşağıdakilerle sınanmıştır: <li>Microsoft SQL Server ve SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 ve 11 g</li><li>MySQL 5.x</li> |
| Senaryolar |<li>Nesne yaşam döngüsü yönetimi</li><li>Parola Yönetimi</li> |
| İşlemler |<li>Tam içeri aktarma ve Delta içeri aktarma, dışarı aktarma</li><li>Dışarı aktarma: Eklemek, güncelleştirme, silme ve değiştirme</li><li>Parola, parola değiştirme</li> |
| Şema |<li>Nesneler ve özniteliklerin dinamik bulma</li> |

### <a name="prerequisites"></a>Ön koşullar
Merhaba bağlayıcı kullanmadan önce hello eşitleme sunucusunda hello şunlara sahip olmanız emin olun:

* 4.5.2 Microsoft .NET Framework veya daha yenisi
* 64-bit ODBC istemci sürücüleri

### <a name="permissions-in-connected-data-source"></a>Bağlı veri kaynağı izinleri
toocreate veya desteklenen hello görevlerden herhangi birini Genel SQL Connector'daki gerçekleştirmek, sahip olmanız gerekir:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Bağlantı noktalarını ve protokolleri
Merhaba ODBC sürücüsü toowork için gereken hello bağlantı noktaları için hello veritabanı satıcısının belgelerine başvurun.

## <a name="create-a-new-connector"></a>Yeni bir bağlayıcı oluşturun
tooCreate Genel SQL bağlayıcı, **eşitleme hizmeti** seçin **yönetim Aracısı** ve **oluşturma**. Select hello **Genel SQL (Microsoft)** bağlayıcı.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Bağlantı
Merhaba bağlayıcı bağlantısı için bir ODBC DSN dosyası kullanır. Merhaba DSN dosyası kullanarak oluşturmak **ODBC veri kaynakları** hello Başlat menüsü altında bulunan **Yönetimsel Araçlar**. Merhaba Yönetim Aracı'nda oluşturma bir **dosya DSN** toohello bağlayıcı sağlanabilir şekilde.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

Yeni Genel SQL Bağlayıcısı oluşturduğunuzda hello bağlantı ekran hello ilk olur. Önce aşağıdaki bilgilerle tooprovide hello gerekir:

* DSN dosyası yolu
* Kimlik Doğrulaması
  * User Name
  * Parola

Merhaba veritabanı bu kimlik doğrulama yöntemlerini birini desteklemelidir:

* **Windows kimlik doğrulaması**: veritabanı kimlik doğrulaması hello hello Windows kimlik tooverify hello kullanıcı kullanır. Kullanıcı adı/parola Hello belirtilen hello veritabanı ile kullanılan tooauthenticate ' dir. Bu hesap izinleri toohello veritabanı olmalıdır.
* **SQL kimlik doğrulaması**: veritabanı kullanan hello kullanıcı adı/parola kimlik doğrulaması hello tanımlı bir hello bağlantı ekran tooconnect toohello veritabanı. Merhaba DSN dosyasında hello kullanıcı adı/parolanın depolarsanız hello bağlantı ekranda sağlanan hello kimlik önceliğe sahiptir.
* **Azure SQL veritabanı kimlik doğrulaması**: daha fazla bilgi için bkz: [tooSQL veritabanı tarafından kullanarak Azure Active Directory kimlik doğrulaması bağlanmak](../../sql-database/sql-database-aad-authentication.md).

**DN olan bağlantı**: Bu seçeneği belirlerseniz, hello DN hello bağlantı özniteliği olarak da kullanılır. Basit bir uygulama için kullanılabilir ancak sınırlaması aşağıdaki hello de vardır:

* Bağlayıcı, yalnızca bir nesne türünü destekler. Bu nedenle öznitelikleri yalnızca başvurabilir herhangi bir referans hello aynı nesne türü.

**Dışarı aktarma türü: Nesne Değiştir**: dışa aktarma sırasında yalnızca bazı öznitelikleri değiştiğinde tüm öznitelikleri olan tüm nesne hello aktarılır ve değiştirir hello varolan nesne.

### <a name="schema-1-detect-object-types"></a>Şema 1 (Algıla nesne türleri)
Bu sayfada tooconfigure kalacaklarını hello bağlayıcı giderek toofind hello farklı nesne türleri hello veritabanında nasıl olduğu.

Her nesne türü bir bölümü olarak sunulan ve yapılandırılmış hakkında daha fazla **yapılandırma bölümleri ve hiyerarşileri**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Nesne türü algılama yöntemi**: hello bağlayıcı, bu nesne türü algılama yöntemleri destekler.

* **Sabit değer**: hello listesiyle nesne türlerini virgülle ayrılmış bir liste sağlar. Örneğin: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Tablo/görünüm/saklı yordam**: hello hello tablo/görünüm/saklı yordamın adını ve ardından nesne türlerini hello listesini sağlar hello sütun adı sağlayın. Saklı yordam kullanırsanız, sonra da parametreleri hello biçiminde sağlayan **[Name]: [Yön]: [değer]**. Her bir parametreyi ayrı bir satırda (Ctrl + Enter tooget yeni bir satır kullanın) sağlayın.  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **SQL sorgusu**: Bu seçenek, tooprovide nesne türleri ile tek bir sütun örneğin döndüren bir SQL sorgusu tanır `SELECT [Column Name] FROM TABLENAME`. Merhaba sütunu (varchar) dize türünden olmalıdır döndürdü.

### <a name="schema-2-detect-attribute-types"></a>Şema 2 (Algıla öznitelik türlerini)
Bu sayfada tooconfigure nasıl hello öznitelik adları ve türlerini algılanan toobe kalacaklarını adımıdır. Merhaba yapılandırma seçenekleri hello önceki sayfada algılanan her nesne türü için listelenir.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Öznitelik türü algılama yöntemi**: hello bağlayıcı Şeması 1 ekranında bu öznitelik türü algılama yöntemleri her algılanan nesne türü ile destekler.

* **Tablo/görünüm/saklı yordam**: hello kullanılan toofind hello öznitelik adları olması gereken hello tablo/görünüm/saklı yordamın adını sağlayın. Saklı yordam kullanırsanız, sonra da parametreleri hello biçiminde sağlayan **[Name]: [Yön]: [değer]**. Her bir parametreyi ayrı bir satırda (Ctrl + Enter tooget yeni bir satır kullanın) sağlayın. birden çok değerli bir öznitelik toodetect hello öznitelik adları tabloları veya görünümleri virgülle ayrılmış listesini sağlayın. Birden çok değerli senaryoları desteklenmez üst ve alt tablo aynı sütun adları olduğunda.
* **SQL sorgusu**: Bu seçenek, tooprovide öznitelik adları ile tek bir sütun örneğin döndüren bir SQL sorgusu tanır `SELECT [Column Name] FROM TABLENAME`. Merhaba sütunu (varchar) dize türünden olmalıdır döndürdü.

### <a name="schema-3-define-anchor-and-dn"></a>Şema 3 (tanımla bağlantı ve DN)
Bu sayfa, tooconfigure bağlantı ve DN özniteliği her algılanan nesne türü için sağlar. Birden çok öznitelikleri toomake hello bağlantı benzersiz seçebilirsiniz.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Birden çok değerli ve Boolean öznitelikleri listelenmez.
* Aynı öznitelik kullanamaz DN ve bağlayıcı, sürece **DN olan bağlantı** hello bağlantı sayfasında seçilidir.
* Varsa **DN olan bağlantı** seçili hello bağlantı sayfasında bu sayfa yalnızca hello DN özniteliği gerektiriyor. Bu öznitelik hello bağlantı özniteliği olarak da kullanılır.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Şema 4 (tanımla öznitelik türü, başvuru ve yön)
Bu sayfa, tamsayı, ikili, veya Boolean ve her bir öznitelik için yönü gibi tooconfigure hello öznitelik türü sağlar. Tüm öznitelikleri sayfasından **şema 2** birden çok değerli öznitelikler dahil olmak üzere listelenir.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Veri türü**: hello eşitleme altyapısı tarafından bilinen toomap hello öznitelik türü toothose türleri kullanılır. aynı hello SQL şemasında algılanan type toouse hello Hello varsayılandır ancak DateTime ve başvuru kolayca algılanamaz. Toospecify olanlar için ihtiyacınız **DateTime** veya **başvuru**.
* **Yön**: hello özniteliği yönü tooImport, dışa aktarma veya ImportExport ayarlayabilirsiniz. ImportExport varsayılandır.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Notlar:

* Bir öznitelik türü hello bağlayıcı tarafından algılanamayan değilse hello dize veri türü kullanır.
* **İç içe tablolar** tek sütunluk veritabanı tablolarını kabul edilebilir. Oracle hello satırları iç içe tablonun belirli bir sırada depolar. Ancak, bir PL/SQL değişkene hello iç içe tablo aldığınızda hello satır 1'den başlayarak ardışık indisleri verilir. Bu, dizi benzeri erişim tooindividual satırları sağlar.
* **VARRYS** hello Bağlayıcısı desteklenmez.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Şema 5 (başvuru öznitelikleri için bölüm tanımlayın)
Bu sayfada, hangi bölümünü (nesne türü) için bir öznitelik başvuran tüm başvuru öznitelikleri için yapılandırın.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Kullanırsanız **DN olan bağlantı**, aynı nesne türü bir gelen başvurduğunuz hello gibi hello kullanmanız gerekir. Başka bir nesne türü başvuramaz.

>[!NOTE]
Şimdi bir seçenek olan hello Mart 2017 güncelleştirme Başlangıç "*" Bu seçenek seçilen sonra tüm olası üye türleri olduğunda alınacak.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 Mayıs 2017 itibariyle hello "*" aka **herhangi bir seçenek** değiştirildi toosupport alma ve akış verme. Bu seçenek toouse istiyorsanız, birden çok değerli tablo/görünüm hello nesne türünü içeren bir öznitelik olmalıdır.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> "*" Merhaba nesne türü ile Merhaba sütunun hello adı de belirtilmelidir sonra seçilir.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

İçeri aktarma işleminden sonra aşağıdaki benzeri toohello görüntü görürsünüz:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Genel Parametreler
Merhaba genel parametreleri sayfası olduğu kullanılan tooconfigure Delta içeri aktarma, tarih/saat biçimi ve parola yöntemi.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Merhaba Genel SQL bağlayıcı yöntemleri Delta alma için aşağıdaki hello destekler:

* **Tetikleyici**: bkz [Tetikleyicileri kullanarak Delta görünümleri oluşturma](https://technet.microsoft.com/library/cc708665.aspx).
* **Filigran**: herhangi bir veritabanı ile kullanılan genel bir yaklaşım. Merhaba Filigran sorgu hello veritabanı satıcıya göre önceden doldurulur. Filigran sütun her tablo/kullanılan görünüm mevcut olması gerekir. Bu sütun olarak ekler ve güncelleştirmeleri toohello tablolar ve bağımlı izlemelidir (birden çok değerli veya alt) tablo. Eşitleme hizmeti ile Merhaba veritabanı sunucusu arasındaki Hello saatler eşitlenmelidir. Aksi durumda, bazı girdilerin hello delta içeri aktarma devre dışı bırakılacak.  
  Sınırlama:
  * Filigran stratejisi değil destek silinmiş nesneler eşleşmiyor.
* **Anlık Görüntü**: (yalnızca Microsoft SQL Server ile birlikte çalışır) [anlık görüntülerini kullanarak Delta görünümler oluşturma](https://technet.microsoft.com/library/cc720640.aspx)
* **Değişiklik izleme**: (yalnızca Microsoft SQL Server ile birlikte çalışır) [değişiklik izleme hakkında](https://msdn.microsoft.com/library/bb933875.aspx)  
  Sınırlamaları:
  * Bağlantı & DN özniteliği hello tablosundaki hello seçili nesne için birincil anahtarın parçası olması gerekir.
  * SQL sorgusu sırasında içeri ve dışarı aktarma değişiklik izleme desteklenmiyor.

**Ek parametreler**: hello veritabanı sunucunuz bulunduğu belirten veritabanı sunucusu saat dilimini belirtin. Bu değer kullanılır toosupport hello tarih ve saat özniteliklerin çeşitli biçimleri.

Merhaba bağlayıcı her zaman tarih ve tarih-saat UTC biçiminde depolar. toobe mümkün toocorrectly dönüştürme hello tarih ve saatleri, hello veritabanı sunucusu ve kullanılan hello biçimi hello saat dilimini belirtilmesi gerekir. Merhaba biçimi .net biçiminde ifade edilmelidir.

Dışa aktarma sırasında her bir tarih saat özniteliği toohello bağlayıcı UTC saat biçiminde sağlanması gerekir.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Parola yapılandırma**: hello bağlayıcı parola eşitleme özellikleri sağlar ve ayarlamak ve parola değiştirme destekler.

Merhaba bağlayıcı toosupport parola eşitleme için iki yöntem sunar:

* **Saklı yordam**: Bu yöntem iki saklı yordamlar toosupport kümesi & Parola Değiştir gerektirir. Tür Ekle için tüm parametreleri ve hello parola işlemde değiştirin **ayarlamak parola SP** ve **değiştirme parola SP** örnek aşağıdaki parametrelerin sırasıyla göre.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Parola uzantısı**: Bu yöntem parola uzantı DLL'si gerektirir (tooprovide hello hello uygulama uzantı DLL adı gereksinim [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) arabirimi). Böylece Hello bağlayıcı hello DLL çalışma zamanında yükleyebilir parola uzantı derlemesi uzantısı klasörüne yerleştirilmelidir.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

Merhaba üzerinde tooenable hello parola yönetimi de **yapılandırmanız uzantı** sayfası.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Bölümleri ve hiyerarşileri Yapılandır
Merhaba bölümleri ve hiyerarşileri sayfasında tüm nesne türlerini seçin. Her nesne türü kendi bölümdür.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

Merhaba üzerinde tanımlanan hello değerleri geçersiz kılabilirsiniz **bağlantı** veya **genel parametreleri** sayfası.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Yer işaretlerini Yapılandır
Merhaba bağlantı zaten tanımlı olduğundan bu sayfayı salt okunurdur. Merhaba Seçili bağlayıcı öznitelik her zaman eklenir hello nesne türü tooensure ile nesne türleri arasında benzersiz kalır.

![tutturucular](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Çalışma adımı parametre yapılandırma
Bu adımları hello bağlayıcı üzerinde çalıştırma profilleri hello yapılandırılır. Bu yapılandırmalar içeri ve dışarı aktarma veri gerçek iş hello.

### <a name="full-and-delta-import"></a>Tam ve Delta içeri aktarma
Genel SQL bağlayıcı desteği tam ve Delta içeri aktarma bu yöntemleri kullanarak:

* Tablo
* Görünüm
* Saklı Yordam
* SQL sorgusu

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Tablo/görünüm**  
tooimport birden çok değerli öznitelikleri bir nesne için tooprovide hello virgülle ayrılmış tablosu/görünümü adınızı elinizde **adı, birden çok değerli tablo/Görünüm** ve ilgili birleştirme koşulları hello içinde **katılma koşulu**hello üst tabloyla.

Örnek: Tooimport hello çalışan nesne ve tüm birden çok değerli öznitelikleri istiyor. Çalışan (ana tablo) ve departman (birden çok değerli) adlı iki tablo vardır.
Aşağıdaki hello:

* Tür **çalışan** içinde **tablo/görünüm/SP**.
* Türü departmanında **adı, birden çok değerli tablo/Görünüm**.
* Yazın hello birleştirme koşulunun çalışan & departmanında arasındaki **birleştirme koşulunun**, örneğin `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Saklı yordamlar**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Fazla veriniz varsa, saklı yordamlar ile tooimplement sayfalandırma önerilir.
* Saklı yordam toosupport sayfalandırma için tooprovide dizin başlangıç ve bitiş dizini gerekir. Bkz: [verimli bir şekilde büyük miktarlarda verinin disk belleği](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndexve @EndIndex yürütme sırasında yapılandırılan ilgili sayfa boyutu değeri ile değiştirilir **yapılandırma adımı** sayfası. Örneğin, ilk sayfa ve hello sayfa boyutu hello bağlayıcı zaman alır 500, böyle bir durumda ayarlanır @StartIndex 1 olur ve @EndIndex 500. Bu değerler bağlayıcı sonraki sayfalarda aldığında artırmak ve hello değiştirme @StartIndex & @EndIndex değeri.
* tooexecute parametreli saklı yordamı, hello parametrelerinde sağlayın `[Name]:[Direction]:[Value]` biçimi. Her bir parametreyi ayrı bir satırda (kullanımı Ctrl + Enter tooget yeni bir satır) girin.
* Genel SQL bağlayıcı, Microsoft SQL Server'da bağlı sunuculardan içeri aktarma işlemi de destekler. Bilgi bağlantılı sunucu tabloda nereden alınacağını, tablo hello biçiminde verilmesi:`[ServerName].[Database].[Schema].[TableName]`
* Genel SQL bağlayıcı bilgileri ve şeması algılama adımlarını çalıştırmak benzer yapıya (hem diğer adı ve veri türü) arasında sahip nesneleri destekler. Merhaba seçtiyseniz, şema ve çalışma adımı sırasında sağlanan bilgiler nesnesinden farklıdır ve ardından SQL Bağlayıcıdır oluşturulamıyor toosupport senaryolar bu tür.

**SQL sorgusu**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Birden çok sonuç desteklenmiyor sorguları ayarlar.
* Merhaba sayfalandırma ve başlangıç sağlamak destekler SQL sorgusu dizin ve değişken toosupport sayfalandırma olarak bitiş dizini.

### <a name="delta-import"></a>Delta içeri aktarma
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

Delta içeri aktarma yapılandırma tam içeri aktarma ile karşılaştırıldığında daha fazla miktar yapılandırma gerektirir.

* Tootrack delta değişiklikleri hello tetikleyici veya anlık görüntü yaklaşımı seçerseniz, geçmiş tablosu veya anlık görüntü veritabanında sağlamak **geçmiş tablosu veya anlık görüntü veritabanı adı** kutusu.
* Ayrıca tooprovide birleştirme koşulunun geçmiş tablosu üst tablo arasındaki örneğin gerekir`Employee.ID=History.EmployeeID`
* tootrack hello işlem hello geçmişi tablodan hello üst tablo üzerinde hello işlemi bilgileri (ekleme/güncelleştirme/silme) içeren hello sütun adı sağlamanız gerekir.
* Delta değişiklikleri Filigran tootrack seçerseniz, hello işlemi bilgileri içeren hello sütun adı sağlayın **su işareti sütun adı**.
* Merhaba **türü özniteliği değiştirmek** sütun hello değişiklik türü için gereklidir. Bu sütunu hello birincil tabloda oluşan bir değişiklik eşler veya birden çok değerli tablo tooa hello delta görünümünde türünü değiştirin. Bu sütun hello Modify_Attribute değişiklik türü için öznitelik düzeyi değiştirme veya ekleme, değiştirme, içerebilir veya Delete türü bir nesne düzeyinde değişiklik türü için değiştirin. Dışında bir şey olması durumunda varsayılan değer ekleme, değiştirme, hello veya silin, sonra bu seçeneği kullanarak bu değerleri tanımlayabilirsiniz.

### <a name="export"></a>Dışarı Aktarma
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

Genel SQL bağlayıcı desteği gibi dört desteklenen yöntemleri kullanarak verme:

* Tablo
* Görünüm
* Saklı Yordam
* SQL sorgusu

**Tablo/görünüm**  
Merhaba tablo/görünüm seçeneği seçerseniz, hello bağlayıcı hello ilgili sorgular toodo hello verme oluşturur.

**Saklı yordamlar**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Merhaba saklı yordam seçeneği belirlerseniz, dışa aktarma üç farklı saklı yordamları tooperform ekleme/güncelleştirme/silme işlemlerini gerektirir.

* **SP adı eklemek**: herhangi bir nesne ekleme hello ilgili tablodaki tooconnector geliyorsa bu SP çalıştırır.
* **Güncelleştirme SP adı**: herhangi bir nesne tooconnector hello ilgili tablodaki güncelleştirmesi geliyorsa bu SP çalıştırır.
* **SP adı silmek**: tooconnector hello ilgili tablodaki silme işlemi için herhangi bir nesne geliyorsa, bu SP çalıştırır.
* Bir parametre değeri toohello depolanmış yordam kullanılan hello şemasından seçili özniteliği. Örneğin, `EmployeeName: INPUT: @EmployeeName` (EmployeeName hello bağlayıcı şemada seçili ve hello bağlayıcı dışarı aktarma yaparken hello ilgili değer yerini alır)
* toorun parametreli saklı yordam, parametreleri sağlamak `[Name]:[Direction]:[Value]` biçimi. Her bir parametreyi ayrı bir satırda (kullanımı Ctrl + Enter tooget yeni bir satır) girin.

**SQL sorgusu**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Merhaba SQL sorgu seçeneği seçerseniz, üç farklı tooperform ekleme/güncelleştirme/silme işlemleri sorgular verme gerektirir.

* **Sorguyu eklemek**: herhangi bir nesne ekleme hello ilgili tablodaki tooconnector geliyorsa, bu sorguyu çalıştırır.
* **Güncelleştirme sorgusu**: herhangi bir nesne tooconnector hello ilgili tablodaki güncelleştirmesi geliyorsa, bu sorguyu çalıştırır.
* **Sorguyu silmek**: tooconnector hello ilgili tablodaki silme işlemi için herhangi bir nesne geliyorsa, bu sorguyu çalıştırır.
* Örneğin bir parametre değeri toohello sorgu olarak kullanılan hello şemadan seçili özniteliği`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Sorun giderme
* Merhaba nasıl tooenable günlük tootroubleshoot hello Bağlayıcısı hakkında daha fazla bilgi için bkz [nasıl tooEnable ETW İzleme bağlayıcıların](http://go.microsoft.com/fwlink/?LinkId=335731).
