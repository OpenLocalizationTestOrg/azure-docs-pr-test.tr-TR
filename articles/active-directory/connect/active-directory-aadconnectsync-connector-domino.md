---
title: "aaaLotus Domino Bağlayıcısı | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure Microsoft'un Lotus Domino Bağlayıcısı."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Lotus Domino Bağlayıcısı Teknik Başvurusu
Bu makalede hello Lotus Domino Bağlayıcısı açıklanmaktadır. Merhaba makale ürünleri aşağıdaki toohello geçerlidir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Düzeltme 4.1.3671.0 kullanmanız gerekir ya da daha sonra [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 ve FIM2010R2 için hello bağlayıcı olarak hello Merkezi'nden kullanılabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Merhaba Lotus Domino Bağlayıcısı genel bakış
Merhaba Lotus Domino Bağlayıcısı toointegrate hello eşitleme hizmeti IBM'in Lotus Domino sunucusuyla sağlar.

Üst düzey açısından bakıldığında, özellikler aşağıdaki hello hello sürümü geçerli hello bağlayıcı tarafından desteklenir:

| Özellik | Destek |
| --- | --- |
| Bağlı veri kaynağı |Sunucu: <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>İstemci:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Senaryolar |<li>Nesne yaşam döngüsü yönetimi</li><li>Grup Yönetimi</li><li>Parola Yönetimi</li> |
| İşlemler |<li>Tam ve Delta içeri aktarma</li><li>Dışarı Aktarma</li><li>Ayarlayın ve HTTP parola parolasını değiştirme</li> |
| Şema |<li>Kişi (gezici kullanıcı, kişi (kişiler sertifika ile))</li><li>Grup</li><li>Kaynak (kaynak, yer, çevrimiçi toplantı)</li><li>Posta veritabanı</li><li>Desteklenen nesnelerinin öznitelikleri dinamik bulma</li> |

Merhaba Lotus Domino Bağlayıcısı hello Lotus Notes istemci toocommunicate Lotus Domino sunucusuyla kullanır. Bu bağımlılık gruplarındaki sonucu olarak, desteklenen Lotus Notes istemcisi hello eşitleme sunucusuna yüklenmesi gerekir. Merhaba istemci hello sunucusu arasında Hello iletişimi hello Lotus Notes .NET birlikte çalışabilirliği (Interop.domino.dll) arabirimi aracılığıyla uygulanır. Bu arabirim hello hello Microsoft.NET platform ve Lotus Notes istemci arasındaki iletişimi kolaylaştırır ve erişim tooLotus Domino belgeler ve görünümler destekler. Delta içeri aktarma için de bu hello C++ yerel arabirim (delta alma yöntemine bağlı olarak seçilen hello) kullanılır mümkündür.

### <a name="prerequisites"></a>Ön koşullar
Merhaba bağlayıcı kullanmadan önce önkoşul hello eşitleme sunucusunda aşağıdaki hello sahip emin olun:

* 4.5.2 Microsoft .NET Framework veya daha yenisi
* Merhaba Lotus Notes istemci eşitleme sunucunuzda yüklenmelidir
* Merhaba Lotus Domino Bağlayıcısı hello varsayılan Lotus Domino LDAP şema veritabanı (schema.nsf) toobe hello Domino dizin sunucusunda mevcut gerektirir. Mevcut değilse, çalışan veya hello Domino sunucuda hello LDAP hizmetini yeniden yükleyebilirsiniz.

### <a name="connected-data-source-permissions"></a>Bağlı veri kaynağı izinleri
tooperform Lotus Domino Bağlayıcısı hello hiçbirini desteklenen görevleri, aşağıdaki grupların bir üyesi olmanız gerekir:

* Tam erişim yöneticileri
* Yöneticiler
* Veritabanı Yöneticileri

Merhaba aşağıdaki tabloda her işlem için gerekli olan hello izinleri listelenmektedir:

| İşlem | Erişim hakları |
| --- | --- |
| İçeri Aktarma |<li>Ortak belgeler okuma</li><li> Tam Erişim Yöneticisi (tam erişim Yöneticiler grubunun üyesi olduğunda otomatik olarak hello etkili erişim tooin ACL vardır.)</li> |
| Dışarı aktarma ve parola ayarlama |Etkili erişim: <li>Belgeleri oluşturma</li><li>Belgeleri silme</li><li>Ortak belgeler okuma</li><li>Ortak belgeler yazma</li><li>Replicate veya Kopyala belgeler</li>Verme işlemleri için rolleri aşağıdaki hello de gerekir: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Doğrudan işlemler ve AdminP
İşlemler doğrudan toohello Domino dizinine gidin veya AdminP hello işlem. Merhaba aşağıdaki tablolarda listelenmektedir tüm desteklenen nesneleri, operations ve uygunsa, uygulama yöntemi hello ilgili:

**Birincil adres defteri**

| Nesne | Oluştur | Güncelleştirme | Sil |
| --- | --- | --- | --- |
| Kişi |AdminP |Doğrudan |AdminP |
| Grup |AdminP |Doğrudan |AdminP |
| MailInDB |Doğrudan |Doğrudan |Doğrudan |
| Kaynak |AdminP |Doğrudan |AdminP |

**İkincil adres defteri**

| Nesne | Oluştur | Güncelleştirme | Sil |
| --- | --- | --- | --- |
| Kişi |Yok |Doğrudan |Doğrudan |
| Grup |Doğrudan |Doğrudan |Doğrudan |
| MailInDB |Doğrudan |Doğrudan |Doğrudan |
| Kaynak |Yok |Yok |Yok |

Bir kaynak oluşturulduğunda, notlar belge oluşturulur. Benzer şekilde, bir kaynak silindiğinde, hello notları belge silinir.

### <a name="ports-and-protocols"></a>Bağlantı noktalarını ve protokolleri
IBM Lotus Notes istemcisi ve Domino sunucuları notları uzak yordam çağrısı (NRPC TCP/IP'yi burada kullanması gereken NRPC) kullanarak iletişim kurar. Merhaba varsayılan bağlantı noktası numarası 1352 olmakla birlikte, hello Domino Yöneticisi tarafından değiştirilebilir.

### <a name="not-supported"></a>Desteklenmiyor
aşağıdaki işlemleri hello hello sürümü geçerli hello Lotus Domino Bağlayıcısı tarafından desteklenmez:

* Posta kutusu sunucuları arasında taşıyın.

## <a name="create-a-new-connector"></a>Yeni bir bağlayıcı oluşturun
### <a name="client-software-installation-and-configuration"></a>İstemci yazılımı yükleme ve yapılandırma
Lotus Notes hello sunucusunda yüklü olması **önce** hello Bağlayıcısı yüklenir.

Yükleme sırasında yaptığınızdan emin olun bir **tek kullanıcılı yükleme**. Merhaba varsayılan **çok kullanıcı yükleme** çalışmıyor.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Lotus Notes özellikleri Hello gerekli yalnızca hello özellikleri sayfasında, yüklemek ve **istemci tek oturum açma**. Çoklu oturum açma hello bağlayıcı toobe mümkün toolog toohello Domino sunucusunda gereklidir.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Not:** hello üzerinde bulunan bir kullanıcı ile aynı sunucuya hello hesap sonra Başlangıç Lotus Notes bağlayıcı'nın hizmet hesabı hello olarak kullanın. Ayrıca emin tooclose hello Lotus Notes istemci hello sunucuda olun. İşletim sistemiyle çalıştırılamaz hello tooconnect toohello Domino sunucusu aynı saat hello bağlayıcı çalışır.

### <a name="create-connector"></a>Bağlayıcı oluşturma
Lotus Domino Bağlayıcısı tooCreate, **eşitleme hizmeti** seçin **yönetim Aracısı** ve **oluşturma**. Select hello **Lotus Domino (Microsoft)** bağlayıcı.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Eşitleme hizmeti sürümünüz hello özelliği tooconfigure sağlayıp **mimarisi**, hello bağlayıcı tooits varsayılan değeri toorun ayarlandığından emin olun **işlem**.

### <a name="connectivity"></a>Bağlantı
Merhaba bağlantı sayfasında hello Lotus Domino sunucu adı belirtin ve hello oturum açma kimlik bilgilerini girin.  
![Bağlantı](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Merhaba Domino sunucu özelliği hello sunucusu adı için iki biçim destekler:

* serverName
* ServerName/DirectoryName

Merhaba **ServerName/DirectoryName** biçimi olduğundan bu öznitelik için tercih edilen biçim hello hello bağlayıcı kişiler Domino sunucusu hello olduğunda daha hızlı yanıt sağlar.

Merhaba, USERID dosya hello eşitleme hizmetinin hello yapılandırma veritabanı'nda depolanır sağlanır.

İçin **Delta içeri aktarma** Bu seçenekler vardır:

* **None**. Merhaba bağlayıcı herhangi delta içeri aktarmalar yapmaz.
* **Ekleme/güncelleştirme**. Merhaba bağlayıcı mu delta içeri aktarma ekleme ve güncelleştirme işlemlerinde. Silme için bir **tam içeri aktarma** işlemi gereklidir. Bu işlem hello .net birlikte çalışabilirliği kullanıyor.
* **Ekleme/güncelleştirme/silme**. Hello bağlayıcı mu delta içeri aktarma ekleme, güncelleştirme ve silme işlemleri. Bu işlem hello yerel C++ arabirimleri kullanıyor.

İçinde **şema seçenekleri** seçenekleri aşağıdaki hello vardır:

* **Varsayılan şema**. Merhaba bağlayıcı hello şema hello Domino sunucusundan algılar. Bu seçim hello varsayılan seçenektir.
* **DSML şema**. Merhaba Domino sunucusu hello şema imkanı sunmuyorsa yalnızca kullanılır. Ardından hello şemasıyla DSML dosyası oluşturabilir ve bunun yerine alabilirsiniz. DSML hakkında daha fazla bilgi için bkz: [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

İleri'yi tıklattığınızda hello kullanıcı kimliği ve parola yapılandırma parametreleri doğrulanır.

### <a name="global-parameters"></a>Genel Parametreler
Hello genel parametreleri sayfasında, hello saat dilimi ve hello alma yapılandırın ve işlemi seçeneği verin.  
![Genel Parametreler](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Merhaba **Domino sunucu saat dilimi** parametre Domino sunucunuz hello konumunu tanımlar.

Bu yapılandırma seçeneği gerekli toosupport olan **delta içeri aktarma** işlemleri hello eşitleme hizmeti, sağladığından hello son iki içeri aktarmalar arasındaki değişiklikleri belirleme.

>[!Note]
Merhaba Mart 2017 güncelleştirme hello genel parametreleri ekranında başlangıç hello seçeneği toodelete hello kullanıcının posta veritabanı hello kullanıcının silinirken içerir.

![Kullanıcının posta Sil](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>İçeri aktarma ayarları, yöntemi
Merhaba **tam içeri aktarma gerçekleştirmek tarafından aktar** Bu seçenekler vardır:

* Arama
* Görünüm (önerilir)

**Arama** olan Domino ancak bu dizin kullanarak hello dizinleri değil gerçek zamanlı olarak güncelleştirilir ve hello sunucusundan döndürülen hello veriler her zaman doğru değil ortak. Birden çok değişikliği bir sistem, bu seçenek genellikle iyi çalışmaz ve bazı durumlarda yanlış siler sağlar. Ancak, **arama** hızlıdır **Görünüm**.

**Görünüm** hello seçeneği önerilir, bu çünkü hello doğru veri durumunu sağlar. Arama biraz daha yavaş çalışıyor.

#### <a name="creation-of-virtual-contact-objects"></a>Sanal bağlantı nesnelerini oluşturma
Merhaba **etkinleştirmek oluşturulmasını \_kişi nesnesi** Bu seçenekler vardır:

* None
* Başvuru olmayan değerleri
* Başvuru ve başvuru olmayan değerleri

Domino içinde başvuru öznitelikleri birçok farklı biçimlerde tooreference diğer nesnelerini içerebilir. toobe mümkün toorepresent farklı Çeşitlemeler, bağlayıcı Implements hello \_nesneleri, kişi olarak da bilinen **sanal kişiler** (VC). Bu nesneler tooexisting MV nesneleri katılmanız için oluşturulan veya yeni nesneler olarak öngörülen. Bu şekilde, öznitelik başvuruları korunabilir.

Bu ayarı etkinleştirerek ve bir başvuru özniteliği Merhaba içeriğine DN biçiminde değilse, bir \_ilgili kişi nesnesi oluşturulur. Örneğin, bir grubun üyesi özniteliği SMTP adresi içerebilir. Aynı zamanda olası toohave kısaad olan ve diğer öznitelikleri başvurusu öznitelikleri sunar. Bu senaryo için seçin **olmayan başvuru değerlerini**. Bu yapılandırma hello en yaygın Domino uygulamaları için bir ayardır.

Lotus Domino yapılandırılmış toohave ayrı adres defterleri olduğunda ayırt edici farklı adlara sahip aynı nesne Merhaba temsil eden, kendi olası tooalso oluşturma \_nesneleri için bir adres defteri içinde bulunan tüm başvuru değerleri başvurun. Bu senaryo için hello seçin **başvurusu ve başvuru olmayan değerleri** seçeneği.

Merhaba özniteliği birden çok değer varsa **FullName** başvuruları çözümlenebilir şekilde Domino içinde sonra da sanal kişiler tooenable hello oluşturma isteyebilirsiniz. Örneğin, bu öznitelik bir marriage veya divorce sonra birden çok değer olabilir. Merhaba onay kutusunu seçin **etkinleştir... FullName sahip birden çok değer** bu senaryo için.

Merhaba doğru özniteliklerinde birleştirerek hello \_kişi nesneleri birleştirilmiş toohello MV nesne olacaktır.

Bu nesneler VC sahiptir =\_ilgili kişi tootheir DN eklediniz.

#### <a name="import-settings-conflict-object"></a>Ayarları içeri aktarmak, nesne çakışıyor
**Çakışma nesne Dışla**

Büyük bir Domino uygulamasında birden fazla nesne sahip Merhaba, aynı DN tooreplication sorunları nedeniyle mümkündür. Bu durumlarda, iki farklı UniversalIDs ancak aynı DN nesneleriyle hello bağlayıcı görür. Bu çakışma hello bağlayıcı alanı oluşturulan geçici bir nesne neden olur. Merhaba bağlayıcı Domino içinde çoğaltma kurbana seçilen hello nesneleri yoksayabilirsiniz. Merhaba, bu onay kutusunun seçili tookeep önerilir.

#### <a name="export-settings"></a>Dışa aktarma ayarları
Merhaba, seçenek **AdminP başvurularını güncelleştirme için kullanmak** üyesi gibi başvuru öznitelikleri verilmesini doğrudan çağrısı ve hello AdminP işlemi kullanmıyor seçildiyse. Yalnızca AdminP yapılandırılmış toomaintain başvuru bütünlüğü ayarlanmadı olduğunda bu seçeneği kullanın.

#### <a name="routing-information"></a>Yönlendirme bilgileri
Domino içinde bir başvuru özniteliği soneki toohello DN ekli yönlendirme bilgileri olduğunu mümkündür. Örneğin, bir grup üyesi özniteliğinde hello içerebilir **CN =example/organization@ABC**. Merhaba soneki @ABC hello yönlendirme bilgileri. Merhaba yönlendirme bilgileri, farklı bir kuruluşta bir sistem olabilir Domino toosend e-postaları toohello doğru Domino sistemi tarafından kullanılır. Merhaba yönlendirme bilgi alanında hello sonekleri yönlendirme hello kuruluşunuzda hello bağlayıcı, kapsam içinde kullanılan belirtebilirsiniz. Bir başvuru özniteliği şu değerlerden biri sonek olarak bulunursa, hello yönlendirme bilgilerini hello başvurusundan kaldırılır. Merhaba yönlendirme son ekini başvuru değeri belirtilen, bu değerlerin eşleşen tooone olamazsa bir \_ilgili kişi nesnesi oluşturulur. Bunlar \_kişi nesneleri ile oluşturulan **RO = @<RoutingSuffix>**  DN hello eklenen. Bu \_öznitelikleri aşağıdaki hello olan de kişi nesneler eklenen tooa gerçek nesne gerekiyorsa birleştirmek tooallow: \_routingName, \_contactName, \_displayName ve UniversalID.

#### <a name="additional-address-books"></a>Ek adres defterleri
Sahip değilse **directory Yardım** yüklü, ikincil adres defterleri hello adını sağlayan ve ardından bu adres defterleri el ile girebilirsiniz.

#### <a name="multivalued-transformation"></a>Birden çok değerli dönüştürme
Lotus Domino birçok öznitelikte birden çok değerli. Merhaba karşılık gelen meta veri deposu öznitelikleri genellikle tek değerli. Merhaba alma ve hello dışa aktarma işlemi seçeneği yapılandırarak, etkilenen hello özniteliklerin gerekli hello çeviri ile Merhaba bağlayıcı toohelp etkinleştirin.

**Dışarı aktarma**  
Merhaba dışa aktarma işlemi seçeneği iki modlarını destekler:

* Öğe Ekle
* Öğeyi değiştirin

**Maddesini** – bu seçenek, her zaman hello bağlayıcı Kaldır hello geçerli değerlerini hello özniteliği içinde Domino seçin ve sağlanan hello değerlerle değiştirin. sağlanan hello değerli tek değerli veya birden çok değerli olabilir.

Örnek: Merhaba Yardımcısı nesnesinin özniteliği olan bir kişi değerleri aşağıdaki hello sahiptir:

* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Adlı yeni bir yardımcı varsa **David Alexander** olan toothis kişi nesnesi atanmış, hello oluşur:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**Öğe ekleme** – bu seçeneği işaretlediğinizde hello bağlayıcı hello varolan Domino ve INSERT yeni değerleri hello veri listesi hello üstündeki hello öznitelik değerlerine korur.

Örnek: Merhaba Yardımcısı nesnesinin özniteliği olan bir kişi değerleri aşağıdaki hello sahiptir:

* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Adlı yeni bir yardımcı varsa **David Alexander** olan toothis kişi nesnesi atanmış, hello oluşur:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**İçeri Aktarma**  
Merhaba alma işlemi seçeneği iki modlarını destekler:

* Varsayılan
* Birden çok değerli tooSingle değeri

**Varsayılan** –, öznitelikler alınır tüm hello tüm değerlerin hello varsayılan seçeneği seçin.

**Birden çok değerli tooSingle değeri** – bu seçeneği işaretlediğinizde birden çok değerli özniteliği tek değerli bir özniteliğe dönüştürülür. Birden fazla değer varsa, (Bu değer genellikle de hello son sayısıdır) hello üstte hello değeri kullanılır.

Örnek: Merhaba Yardımcısı nesnesinin özniteliği olan bir kişi değerleri aşağıdaki hello sahiptir:

* CN = David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN = Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN = John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Merhaba en son güncelleştirme toothis özniteliktir **David Alexander**. Merhaba alma işlemi seçeneği tooMultivalued tooSingle değeri ayarlandığından Bağlayıcısı yalnızca alır **David Alexander** hello bağlayıcı alanına.

Merhaba mantığı tooconvert birden çok değerli öznitelikler tek değerli öznitelikler toohello grup üyesi ve toohello kişi fullname özniteliklerini uygulanmaz.

Bu da olası tooconfigure içeri ve dışarı aktarma dönüştürme kuralları, öznitelik başına birden çok değerli öznitelikler için bir özel durum toohello genel kural olarak. tooconfigure bu seçeneği, [objecttype] girin. [attributename] hello içinde **dışlama öznitelik listesi alma** ve **dışlama öznitelik listesi verme** metin kutuları. Örneğin, Person.Assistant girin ve hello genel bayrağını tooimport tüm değerler, yalnızca hello ilk değer ise hello Yardımcısı için içe aktarılan.

#### <a name="certifiers"></a>Certifiers
Tüm kuruluşun/kuruluş birimlerini hello bağlayıcı tarafından listelenir. toobe mümkün tooexport kişi nesneleri toohello birincil adres defteri, kendi parola ile certifier gereklidir.

Tüm certifiers varsa aynı parolayı hello hello **tüm Certifers parolasını** kullanılabilir. Ardından hello parolayı buraya girin ve yalnızca hello certifier dosyası belirtin.

Ardından, yalnızca içe aktarırsanız, toospecify herhangi certifiers yok.

### <a name="configure-provisioning-hierarchy"></a>Sağlama hiyerarşisini Yapılandır
Merhaba Lotus Domino Bağlayıcısı yapılandırdığınızda, bu iletişim sayfasını atlayın. sağlama hiyerarşisini başlangıç Lotus Domino Bağlayıcısı desteklemez.  
![Hiyerarşi sağlama](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Bölümleri ve hiyerarşileri Yapılandır
Bölümleri ve hiyerarşileri yapılandırdığınızda NAB=names.nsf adlı hello birincil adres defteri seçmeniz gerekir. Ayrıca toohello birincil adres defteri varsa ikincil adres defterleri seçebilirsiniz.  
![Bölümler](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Öznitelikleri seçin
Öznitelikler yapılandırdığınızda ile önek tüm öznitelikleri seçmelisiniz  **\_MMS\_**. Yeni nesneleri tooLotus Domino sağlarken bu öznitelikler gereklidir

![Öznitelikler](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Nesne yaşam döngüsü yönetimi
Bu bölümde Domino hello farklı nesneler genel bir bakış sağlar.

### <a name="person-objects"></a>Kişi nesneleri
Merhaba kişi nesnesi kuruluş ve kuruluş birimleri kullanıcıları temsil eder. Ayrıca toohello varsayılan öznitelik Merhaba Domino yönetici özel öznitelikler tooa kişi nesnesi ekleyebilirsiniz. En az bir kişi nesnesi tüm zorunlu öznitelikler eklemeniz gerekir. Zorunlu öznitelikler tam bir listesi için bkz: [Lotus Notes özellikleri](#lotus-notes-properties). tooregister bir kişi nesnesi, Önkoşullar aşağıdaki hello karşılanmalıdır:

* Merhaba adres defteri (names.nsf) tanımlanmalıdır ve hello birincil adres defteri olması gerekir.
* Belirli bir kullanıcının hello kuruluş hello O/OU certifier kimliği ve hello parola tooregister olmalıdır / kuruluş birimi.
* Lotus Notes özellikleri bir kişi nesnesi için belirli bir dizi ayarlamanız gerekir. Bu özellikler hello kişi nesnesi sağlamak için kullanılır. Daha fazla bilgi için bkz: adlı hello bölüm [Lotus Notes özellikleri](#lotus-notes-properties) bu belgenin devamındaki.
* bir kişi Hello ilk HTTP parolası, sağlama işlemi sırasında bir öznitelik ve kümesi değil.
* Merhaba kişi nesnesi şu üç desteklenen türlerini hello biri olmalıdır:
  1. Posta dosyası ve bir kullanıcı kimliği dosyası olan normal kullanıcı
  2. Gezici kullanıcı (Normal gezici tüm veritabanı dosyaları içeren kullanıcı)
  3. Kişiler (herhangi bir kimliği dosyası olan kullanıcı)

Kişiler (dışında kişiler) daha fazla gruplandırılabilir BİZE ve uluslararası kullanıcılar hello hello değeri tarafından tanımlandığı şekilde \_MMS\_IDRegType özelliği. Bu kişiler, notlar kimliği ve bir kişinin belgeyi hello notları istemci tooaccess Lotus Domino sunucuları kullanın. Notlar posta kullanıyorsanız, sonra da posta dosyası sahiptirler. Merhaba kullanıcının kayıtlı toobecome etkin olması gerekir. Daha fazla bilgi için bkz.

* [Notlar kullanıcıları ayarlama](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Kullanıcı kaydı](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Kullanıcıları yönetme](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Kullanıcıların yeniden adlandırma](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Bu işlemler Lotus Domino gerçekleştirilen ve hello eşitleme hizmetinde içeri aktarıldı.

### <a name="resources-and-rooms"></a>Kaynakları ve odaları
Lotus Domino veritabanında başka türde bir kaynaktır. Kaynakları konferans odaları ekipmanının projektörler gibi çeşitli türleriyle olabilir. Hello kaynak türü özniteliği tarafından tanımlanan Lotus Domino Bağlayıcısı tarafından desteklenen kaynakların alt türleri şunlardır:

| Kaynak türü | Kaynak türü özniteliği |
| --- | --- |
| Yer |1 |
| Kaynak (diğer) |2 |
| Çevrimiçi toplantı |3 |

Merhaba kaynak nesne türü toowork için hello aşağıdakiler gereklidir:

* Kaynak ayırma veritabanını bağlı hello Domino Server'da zaten mevcut olmalıdır
* Merhaba site kaynak hello için zaten tanımlandı

Merhaba kaynak ayırma veritabanı belgeleri üç tür içerir:

* Site profili
* Kaynak
* Rezervasyon

Kaynak ayırma veritabanı ayarlama ile ilgili daha fazla bilgi için bkz: [hello kaynak ayırmaları veritabanı kurma](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**, Güncelleştirme, oluşturma ve kaynakları silme**  
Merhaba oluşturma, güncelleştirme ve silme işlemleri hello kaynak ayırma veritabanında hello Lotus Domino Bağlayıcısı tarafından gerçekleştirilir. Kaynaklar, belge Names.nsf (diğer bir deyişle, hello birincil adres defteri) olarak oluşturulur. Düzenleme ve kaynakları silme hakkında daha fazla bilgi için bkz: [düzenleme ve kaynak belgeleri silme](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html).

**İçeri ve dışarı aktarma işlemi kaynaklar için**  
Merhaba kaynakları herhangi bir nesne türünün gibi hello eşitleme hizmetinden dışarı alınan tooand olabilir. Yapılandırma sırasında SELECT hello nesne türü kaynak olarak. Başarılı dışarı aktarma işlemine ilişkin ayrıntılar için kaynak türü, konferans veritabanı ve Site adı olmalıdır.

### <a name="mail-in-databases"></a>Posta veritabanları
Bir posta veritabanı tasarlanmış tooreceive postalar olan bir veritabanıdır. Tüm özel Lotus Domino kullanıcı hesabıyla ilişkilendirilmemiş bir Lotus Domino posta kutusudur (diğer bir deyişle, kendi kimlik dosyasını ve parolası yok). Bir posta veritabanı ve kendi e-posta adresi ile ilişkili benzersiz bir kimliği ("kısa adı") sahiptir.

Farklı bir posta kutusu farklı kullanıcılar arasında paylaşılabilen kendi e-posta adresi olan bir gereksinimi varsa (örneğin, group@contoso.com), bir posta veritabanı oluşturulur. Merhaba erişim toothis posta kutusu, erişim denetim listesi (tooopen hello posta kutusu izin hello notları kullanıcıların hello adlarını içeren ACL aracılığıyla), denetlenir.

Adlı hello bölüm hello gerekli öznitelikler listesi için bkz [zorunlu öznitelikler](#mandatory-attributes) bu makalenin ilerisinde yer.

Bir veritabanı tasarlanmış tooreceive posta olduğunda, bir posta veritabanı belge Lotus Domino oluşturulur. Bu belge hello veritabanının bir kopyasını depolar her sunucunun Domino dizininde olması gerekir. Veritabanı posta belgesi oluşturma hakkında daha ayrıntılı bir açıklaması için bkz: [bir posta veritabanı belge oluşturma](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html).

Bir posta veritabanı oluşturmadan önce hello veritabanı zaten var olmalıdır (Lotus yönetici tarafından oluşturulmuş olmalıdır) hello Domino sunucusunda.

### <a name="group-management"></a>Grup Yönetimi
Kaynakları aşağıdaki hello hello Lotus Domino Grup Yönetimi ayrıntılı bir genel bakış elde edebilirsiniz:

* [Grupları kullanma](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Grup oluşturma](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Oluşturma ve grupları değiştirme](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Grupları yönetme](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Bir grubu yeniden adlandırma](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Parola Yönetimi
Kayıtlı bir Lotus Domino kullanıcı için parola iki tür vardır:

1. Kullanıcı parolası (User.ID dosyasında depolanan)
2. Internet / HTTP parola

Merhaba Lotus Domino Bağlayıcısı, yalnızca HTTP parolayla işlemleri destekler.

tooperform parola yönetimi hello yönetim aracı Tasarımcısı hello Bağlayıcısı için parola yönetimini etkinleştirmeniz gerekir. tooenable parola yönetimi, select **parola yönetimini etkinleştirin** hello üzerinde **uzantıları Yapılandır** iletişim sayfası.  
![Uzantıları Yapılandır](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Internet parola işlemleri aşağıdaki hello Lotus Domino Bağlayıcısı desteği:

* Parola ayarlama: Parola ayarlama Domino hello kullanıcı yeni bir HTTP/Internet parola koyar. Varsayılan olarak hello hesabı da kilitli değil. Merhaba kilidini bayrağı hello WMI arabiriminde hello eşitleme altyapısı sunulur.
* Parolayı Değiştir: Bu senaryoda, bir kullanıcı toochange hello parola isteyebilirsiniz veya belirtilen bir süre sonra istendiğinde toochange paroladır. Bu işlemi tootake bağlantısı için hem (Merhaba eski ve yeni parolayı hello) zorunludur. Değiştirilen sonra hello yeni parola Lotus Domino güncelleştirilir.

Daha fazla bilgi için bkz.

* [Merhaba Internet kilitleme özelliğini kullanma](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Internet parolaları yönetme](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Başvuru bilgileri
Bu bölümde, öznitelik tanımlarını ve hello Lotus Domino Bağlayıcısı için öznitelik gereksinimleri gibi listelenir.

### <a name="lotus-notes-properties"></a>Lotus Notes özellikleri
Kişi nesneleri tooyour Lotus Domino dizin sağladığınızda nesnelerinizi doldurulan belirli değerleri belirli bir özellikler kümesi olmalıdır. Bu değerleri yalnızca için gereken işlemleri oluşturun.

Merhaba aşağıdaki tabloda bu özellikleri listeler ve bunları bir açıklamasını sağlar.

| Özellik | Açıklama |
| --- | --- |
| \_MMS_AltFullName |Merhaba alternatif kullanıcının tam adını. |
| \_MMS_AltFullNameLanguage |Merhaba dil toobe Hello alternatif kullanıcının tam adını belirtmek için kullanılır. |
| \_MMS_CertDaysToExpire |Merhaba itibaren kaç gün hello geçerli tarihten önce hello sertifika süresi dolar. Belirtilmezse, hello varsayılan iki yıl hello geçerli tarih tarihidir. |
| \_MMS_Certifier |Merhaba kuruluş hiyerarşisi hello certifier adını içeren özellik. Örneğin: OU = OrganizationUnit, O = Org, C = ülke =. |
| \_MMS_IDPath |Merhaba özelliği boşsa, herhangi bir kullanıcı kimliği dosyası hello eşitleme sunucusu üzerinde yerel olarak oluşturulur. Merhaba özellik bir dosya adı içeriyorsa, bir kullanıcı kimliği dosyası hello madata klasöründe oluşturulur. Hello özelliği, tam bir yol da içerebilir. |
| \_MMS_IDRegType |Kişi, kişiler, BİZE kullanıcılar ve uluslararası kullanıcılar sınıflandırılabilir. Merhaba aşağıdaki tabloda hello olası değerler listelenmektedir: <li>0 - başvurun</li><li>1 - ABD kullanıcı</li><li>2 - uluslararası kullanıcı</li> |
| \_MMS_IDStoreType |ABD ve uluslararası kullanıcılar için gerekli özellik. Merhaba özelliği hello kullanıcı kimliği iliştirerek hello notları adres defteri veya hello kişinin posta dosyasında depolanan olup olmadığını belirten bir tamsayı değeri içerir. Merhaba kullanıcı kimliği dosya eki hello adres defterinde ise, bu isteğe bağlı olarak bir dosya olarak oluşturulabilir \_MMS_IDPath. <li>Boş - depolama kimliği dosya kimliği kasadaki (kişiler için kullanılır) tanımlama dosyası yok.</li><li> 1 - hello notları adres defteri eki. Merhaba \_ekleri olan kullanıcı kimliği dosyaları için MMS_Password özelliğini ayarlayın</li><li>2 - kimliği kişinin posta dosyasında depolar. Merhaba \_MMS_UseAdminP toofalse toolet hello posta ayarlanmalıdır dosya hello kişi kayıt sırasında oluşturulabilir. Merhaba \_MMS_Password özelliği, kullanıcı kimliği dosyaları için ayarlanmış olması gerekir.</li> |
| \_MMS_MailQuotaSizeLimit |Merhaba hello e-posta dosya veritabanı için izin verilen megabayt sayısı. |
| \_MMS_MailQuotaWarningThreshold |bir uyarı verilmeden önce hello e-posta dosya veritabanı için izin verilen megabayt cinsinden Hello sayısı. |
| \_MMS_MailTemplateName |kullanılan toocreate hello kullanıcının e-posta dosyası hello e-posta şablon dosyası. Bir şablonu belirtilmediği takdirde, hello belirtilen şablonu kullanarak hello posta dosyası oluşturulur. Hiçbir Şablon belirtilmişse hello varsayılan şablon dosyası kullanılan toocreate hello dosyasıdır. |
| \_MMS_OU |Merhaba OU adı hello certifier altında isteğe bağlı özellik. Bu özellik, kişiler için boş olmalıdır. |
| \_MMS_Password |Kullanıcılar için gerekli özellik. Merhaba özelliği hello tanımlama dosyası hello nesnesinin hello parolası içerir. |
| \_MMS_UseAdminP |Merhaba Domino sunucusundaki (zaman uyumsuz toohello dışa aktarma işlemi) hello AdminP işlemi tarafından Hello posta dosyası oluşturduysanız, bu özellik kümesi tootrue olmalıdır. Özelliğini toofalse ayarlarsanız hello posta dosyası ile Merhaba Domino kullanıcı (Merhaba dışa aktarma işlemi, zaman uyumlu) oluşturulur. |

Bir ilişkili tanımlama dosyası ile bir kullanıcı için hello \_MMS_Password özelliği, bir değer bulunmalıdır. Merhaba MailServer ve bir kullanıcının MailFile özelliklerini hello Lotus Notes istemcisi aracılığıyla e-posta erişimi için bir değer içermesi gerekir.

bir Web tarayıcısı üzerinden tooaccess e-posta aşağıdaki özelliklere hello değerler içermesi gerekir:

* MailFile - hello posta dosyasının depolandığı hello Lotus Domino sunucusundaki hello yol içerir gerekli özelliği'ni tıklatın.
* MailServer - hello hello Lotus Domino sunucusu adını içeren gerekli özelliği'ni tıklatın. Merhaba Domino sunucusunda hello Lotus posta dosyası oluşturduğunuzda bu değer hello adı toouse olur.
* HTTPPassword - hello Web erişim hello nesnesinin parolasını içeren isteğe bağlı özellik.

tooaccess Domino sunucusu posta yetenek olmadan Merhaba, hello HTTPPassword özelliği bir değer içermelidir. MailFile özelliği hello ve hello MailServer özelliği boş olamaz.

İle \_MMS_ IDStoreType = 2 (depolama kimliği) posta dosyasındaki hello NotesRegistrationclass MailSystem özelliği tooREG_MAILSYSTEM_INOTES (3) ayarlayın.

### <a name="mandatory-attributes"></a>Zorunlu öznitelikler
Merhaba Lotus Domino Bağlayıcısı çoğunlukla bu tür nesneleri (belge türleri) destekler:

* Grup
* Posta veritabanı
* Kişi
* Kişi (hiçbir certifier kişiyle)
* Kaynak

Bu bölümde her desteklenen nesne tooexport tooa Domino sunucusu için zorunlu hello öznitelikler listelenir.

| Nesne türü | Zorunlu öznitelikler |
| --- | --- |
| Grup |<li>ListName</li> |
| Ana veritabanı |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Kişi |<li>Soyadı</li><li>MailFile</li><li>Kısaad</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Kişi (hiçbir certifier kişiyle) |<li>\_MMS_IDRegType</li> |
| Kaynak |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Site</li><li>Görünen adı</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Ortak sorunlar ve sorular
### <a name="schema-detection-does-not-work"></a>Şema algılama çalışmıyor
toobe mümkün toodetect hello şema, bu hello schema.nsf dosya hello Domino sunucusunda mevcut gereklidir. LDAP hello sunucuda yüklüyse, bu dosya yalnızca görünür. Merhaba şema algılanamaz değilse hello şunları doğrulayın:

* Merhaba dosya schema.nsf hello Domino sunucusu, kök klasörde hello yok
* Merhaba kullanıcının izinleri toosee hello schema.nsf dosyası vardır.
* Merhaba LDAP sunucunun yeniden başlatılmasını zorlar. Açık **Lotus Domino konsol** ve **söyleyin LDAP ReloadSchema** komutu tooreload hello şema.

### <a name="not-all-secondary-address-books-are-visible"></a>Tüm İkincil adres defterleri görülebilir
Merhaba Domino Bağlayıcısı dayanır hello özelliğini **Directory Yardım** toobe mümkün toofind hello ikincil adres defterleri. Merhaba ikincil adres defterleri eksikse doğrulayıp [Directory Yardım](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) etkin ve hello Domino sunucu üzerinde yapılandırılmış.

### <a name="custom-attributes-in-domino"></a>Domino özel öznitelikler
Birkaç yolu vardır Domino tooextend hello şemada bağlayıcı hello tarafından tüketilebilir özel öznitelik olarak göründüğü şekilde.

**Yaklaşım 1: Lotus Domino şemasını genişletme**

1. Domino Directory şablonu {PUBNAMES. bir kopyasını oluşturun NTF} izleyerek [adımları](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (uygulamasını hello varsayılan IBM Lotus Domino dizini şablonunu özelleştirmeniz gerekir değil):
2. Açık hello kopyalama, Domino directory şablonu {CONTOSO. Domino Tasarımcısı'nda oluşturuldu ve bu adımları NTF} şablonu:
   * Paylaşılan öğelerini tıklatın ve alt genişletin
   * ${ObjectName} InheritableSchema alt çift tıklayın (burada {ObjectName} adıdır hello hello varsayılan yapısal nesne sınıfı, örneğin: kişi).
   * {MyPersonAtrribute} şemasına tooadd istediğiniz hello özniteliği ve ilgili toothat özniteliği olarak adlandırın. Bir alan seçin hello tarafından oluşturma **oluşturma** menüsüne ve ardından **alan** menüsünde.
   * Merhaba eklenen alanında türünü, stili, boyutu, yazı tipi ve diğer ilgili parametreleri alan özellikleri penceresinde seçerek özelliklerini ayarlayın.
   * Varsayılan olarak bu öznitelik için verilen hello adı aynı değer tutma hello özniteliği (Merhaba hello varsayılan değeri öznitelik adı MyPersonAttribute ise, örneğin, tutmak aynı adı).
   * Merhaba ${ObjectName} InheritableSchema alt güncelleştirilmiş değerlerle kaydedin.
3. Merhaba Domino Directory şablonu {PUBNAMES. değiştirin NTF} hello yeni özelleştirilmiş şablonuyla {CONTOSO. NTF} izleyerek [adımları](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Domino yönetici kapatın ve Domino konsol toorestart hello LDAP hizmeti ve tooReload hello LDAP şema açın:
   * Merhaba komutu altında Domino konsolunda Ekle **Domino komutu** toorestart hello LDAP Hizmeti - Dosyalanan metin [yeniden görev LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * tooreload LDAP şema söyleyin LDAP ReloadSchema söyleyin LDAP komutu - kullanın
5. Açık Domino yönetici ve select kişiler ve Gruplar sekmesinde toosee özniteliği domino Ekle kişi yansıtılır eklendi.
6. Gelen Schema.nsf açmak **dosyaları** sekmesinde ve eklenen öznitelik dominoPerson LDAP nesne sınıfına yansıtılan bakın.

**Yaklaşım 2: bir auxClass ile özel bir öznitelik oluşturma ve hello nesne sınıfı ile ilişkilendirme**

1. Domino Directory şablonu {PUBNAMES. bir kopyasını oluşturun NTF} izleyerek [adımları](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (hiçbir zaman hello varsayılan IBM Lotus Domino dizini şablonu özelleştirme):
2. Açık hello kopyalama, Domino directory şablonu {CONTOSO. Domino Tasarımcısı'nda oluşturulan NTF} şablonu.
3. Merhaba sol bölmede, paylaşılan kod ve alt formlar seçin.
4. Yeni alt'ı tıklatın
5. Merhaba yeni alt toospecify hello özelliklerini aşağıdaki hello:
   * Merhaba yeni alt açıkken, tasarım - alt Özellikler'i seçin.
   * Sonraki toohello Name özelliği hello yardımcı nesne sınıfı--Örneğin, TestSubform için bir ad girin.
   * "Insert alt... iletişim seçili dahil" Merhaba seçenekleri özelliği tutun
   * "İşle geçirmek notları HTML'de aracılığıyla." Merhaba seçenekleri özellik seçimini kaldırın
   * Bırakın hello diğer özellikleri aynı hello ve hello alt özellikleri kutusunu kapatın.
   * Kaydedin ve hello yeni alt kapatın.
6. Bir alan toodefine hello yardımcı nesnesi sınıfı tooadd hello:
   * Oluşturduğunuz hello alt açın.
   * Seçin oluşturma - alan.
   * Sonraki tooName hello alan iletişim kutusunun hello temelleri sekmesinde belirtin herhangi bir ad, örneğin: {MyPersonTestAttribute}.
   * Merhaba eklenen alanında tür, stil, boyutu, yazı tipi ve ilgili özellikleri seçerek özelliklerini ayarlayın.
   * Varsayılan olarak bu öznitelik için verilen hello adı aynı değer tutma hello özniteliği (Merhaba hello varsayılan değeri öznitelik adı MyPersonTestAttribute ise, örneğin, tutmak aynı adı).
   * Güncelleştirilmiş değerlerle Hello alt kaydedin ve aşağıdaki hello:
     * Paylaşılan kod ve alt formlar Hello sol bölmesinde seçin
     * Merhaba yeni alt seçin ve tasarım - tasarım özellikleri seçin.
     * Merhaba soldan Hello üçüncü sekmesini tıklatın ve seçin **bu Yasak tasarım değişikliğini yayılması**.
7. ${ObjectName} ExtensibleSchema alt, (burada {ObjectName} hello hello varsayılan yapısal nesne sınıfı, örneğin – kişi adıdır) açın.
8. Kaynak Ekle ve hello (oluşturduğunuz, örneğin – TestSubform) alt seçin ve hello ${ObjectName} ExtensibleSchema alt kaydedin.
9. Merhaba Domino Directory şablonu {PUBNAMES. değiştirin NTF} hello yeni özelleştirilmiş şablonuyla {CONTOSO. NTF} izleyerek [adımları](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Domino yönetici kapatın ve Domino konsol toorestart hello LDAP hizmeti ve tooReload hello LDAP şema açın:
    * Merhaba komutu altında Domino konsolunda Ekle **Domino komutu** toorestart hello LDAP Hizmeti - Dosyalanan metin [yeniden görev LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * tooreload LDAP şemayı kullanan söyleyin LDAP komutu **söyleyin LDAP ReloadSchema**.
11. Açık Domino yönetici ve select kişiler ve Gruplar sekmesinde toosee eklenen öznitelik domino Ekle kişi yansıtılır (diğerlerinin altında sekmesinde).
12. Gelen Schema.nsf açmak **dosyaları** sekmesinde ve eklenen öznitelik TestSubform LDAP yardımcı nesne sınıfı altında yansıtılır bakın.

**Yaklaşım 3: hello özel öznitelik toohello ExtensibleObject sınıfı ekleme**

1. Merhaba kök dizinine yerleştirilen {Schema.nsf} dosyasını aç
2. Altında hello sol menüden LDAP nesne sınıfları seçin **tüm şema belgeleri** tıklatıp **eklemek nesne sınıfı** düğmesi:
3. LDAP adı biçiminde (burada zzz hello hello varsayılan yapısal nesne sınıfı, örneğin kişi adıdır) hello {zzzExtensibleSchema} sağlar. Örneğin, tooextend hello şema kişi nesne sınıfı için LDAP ad {PersonExtensibleSchema} sağlayın.
4. Tooextend hello şema istediğiniz üst nesne sınıfı adı sağlayın. Örneğin, tooextend hello şema kişi nesne sınıfı için üst nesne sınıfı adı {dominoPerson} sağlar:
5. Geçerli bir OID karşılık gelen toohello nesne sınıfı sağlar.
6. Zorunlu veya isteğe bağlı öznitelik türlerini alanları hello gereksinim göredir altında genişletilmiş/özel öznitelikleri seçin:
7. Gerekli ekleme toohello ExtensibleObjectClass öznitelikleri sonra tıklayın **Kaydet ve Kapat**.
8. Bir ExtensibleObjectClass genişletilmiş öznitelikleri olan ilgili varsayılan nesne sınıfı için oluşturulur.

## <a name="troubleshooting"></a>Sorun giderme
* Merhaba nasıl tooenable günlük tootroubleshoot hello Bağlayıcısı hakkında daha fazla bilgi için bkz [nasıl tooEnable ETW İzleme bağlayıcıların](http://go.microsoft.com/fwlink/?LinkId=335731).
