---
title: "aaaGet veri Kataloğu ile çalışmaya | Microsoft Docs"
description: "Azure veri Kataloğu'nun Hello senaryolarını ve özelliklerini sunan uçtan uca öğretici."
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 7652918b5a8254f5cff9e32d77b1fd3e1bf59d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-catalog"></a>Azure Veri Kataloğu ile çalışmaya başlama
Azure Veri Kataloğu kurumsal veri varlıkları için bir kayıt sistemi ve bulma sistemi olarak görev yapan tam yönetilen bir bulut hizmetidir. Ayrıntılı bir genel bakış için bkz. [Azure Veri Kataloğu nedir](data-catalog-what-is-data-catalog.md).

Bu öğretici Azure Veri Kataloğu ile çalışmaya başlamanıza yardımcı olur. Bu öğreticide yordamları izleyerek hello gerçekleştirin:

| Yordam | Açıklama |
|:--- |:--- |
| [Veri kataloğu sağlama](#provision-data-catalog) |Bu yordamda Azure Veri Kataloğu hizmetini hazırlar veya ayarlarsınız. Yalnızca hello katalog önce ayarlanmış olan değil, bu adımı uygulayın. Azure hesabınızla ilişkili birden fazla abonelik olsa bile bir kuruluş (Microsoft Azure Active Directory etki alanı) için yalnızca bir veri kataloğunuz olabilir. |
| [Veri varlıklarını kaydetme](#register-data-assets) |Bu yordamda hello veri Kataloğu ile Merhaba AdventureWorks2014 örnek veritabanından veri varlıklarını kaydetme. Kayıt, ayıklanan anahtar yapısal meta verilerin adlar, türler ve konumlar hello veri kaynağı ve o meta veri toohello Kataloğu kopyalama gibi hello işlemidir. Merhaba veri kaynağı ve veri varlıkları olduğu oldukları kalır, ancak hello meta verileri hello katalog toomake tarafından kullanılan onları daha kolay bulunabilir ve anlaşılabilir. |
| [Veri varlıklarını bulma](#discover-data-assets) |Bu yordamda hello önceki adımda kaydedilen hello Azure veri Kataloğu portalı toodiscover veri varlıklarını kullanın. Azure veri Kataloğu ile veri kaynağı kaydedildikten sonra böylece kullanıcılar için ihtiyaç duydukları hello verileri kolayca arayabilir meta verilerini hello hizmeti tarafından dizine alınır. |
| [Veri varlıklarına not ekleme](#annotate-data-assets) |Bu yordamda veri varlıklarını hello için ek açıklamalar (açıklamalar, etiketler, belge veya uzmanlar gibi bilgiler) sağlayın. Bu bilgiler hello veri kaynağından ayıklanan hello meta verileri tamamlayan ve daha fazla anlaşılabilir toomore kişiler toomake hello veri kaynağı. |
| [Toodata varlıklar Bağlan](#connect-to-data-assets) |Bu yordamda veri varlıklarını tümleşik istemci araçlarında (Excel ve SQL Server Veri Araçları gibi) ve tümleşik olmayan bir araçta (SQL Server Management Studio) açarsınız. |
| [Veri varlıklarını yönetme](#manage-data-assets) |Bu yordamda veri varlıklarınız için güvenliği ayarlarsınız. Veri Kataloğu kullanıcılara erişim toohello verilerin kendisini sağlamaz. Merhaba sahibi hello veri kaynağının veri erişimi denetler. <br/><br/> Veri Kataloğu ile veri kaynakları ve görünüm hello bulabilir **meta veri** ilgili toohello kaynakları hello kataloğa kayıtlı. Veri kaynakları görünür yalnızca toospecific kullanıcılara veya belirli grupların toomembers olması gereken yerde durumlar olabilir. Bu senaryolar için veri Kataloğu tootake hello kataloğu ve denetim hello sahip olduğunuz hello varlıklarının görünürlüğünü içindeki kayıtlı veri kaynaklarının sahipliğini kullanabilirsiniz. |
| [Veri varlıklarını kaldırma](#remove-data-assets) |Bu yordamda, veri kataloğu nasıl tooremove veri varlıklarından hello öğrenin. |

## <a name="tutorial-prerequisites"></a>Öğretici önkoşulları
### <a name="azure-subscription"></a>Azure aboneliği
tooset Azure veri Kataloğu, hello sahibi veya bir Azure aboneliğinin ortak sahibi olmalıdır.

Azure abonelikleri Azure veri Kataloğu gibi toocloud hizmet kaynaklara erişmek düzenlemenize yardımcı olur. Ayrıca kaynak kullanımının nasıl raporlandığını, faturalandırıldığını ve ödendiği denetlemenize yardımcı olur. Her abonelik farklı bir faturalandırma ve ödeme ayarına sahip olabilir, bu nedenle departmana, projeye, bölgesel ofise vb. göre farklı abonelikleriniz ve farklı planlarınız olabilir. Her bir bulut hizmeti tooa aboneliği aittir ve toohave Azure veri Kataloğu'nu ayarlamadan önce bir abonelik gerekiyor. toolearn daha, fazla [hesapları, abonelikleri ve yönetici rollerini yönetme](../active-directory/active-directory-how-subscriptions-associated-directory.md).

Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).

### <a name="azure-active-directory"></a>Azure Active Directory
tooset Azure veri Kataloğu, bir Azure Active Directory (Azure AD) kullanıcı hesabıyla oturum açmanız gerekir. Merhaba sahibi veya bir Azure aboneliğinin ortak sahibi olmalıdır.  

Azure AD iş toomanage kimlik ve erişim, hem de hello Bulut ve şirket içi için kolay bir yol sağlar. Şirket içi web uygulaması veya tek bir iş veya Okul hesabı toosign tooany bulutta kullanabilirsiniz. Azure AD tooauthenticate oturum açma Azure veri kataloğu kullanır. toolearn daha, fazla [Azure Active Directory nedir](../active-directory/active-directory-whatis.md).

### <a name="azure-active-directory-policy-configuration"></a>Azure Active Directory ilke yapılandırması
Toohello Azure veri Kataloğu portalında oturum açabildiğiniz, ancak toohello veri kaynağı kayıt aracını toosign çalıştığınızda bir durum karşılaşabilirsiniz, açmasını engelleyen bir hata iletisiyle karşılaşırsınız. Merhaba şirket ağına veya dış hello şirket ağdan ne zaman bağlanan olduğunda bu hata oluşabilir.

Merhaba kayıt aracını kullanarak *form kimlik doğrulaması* toovalidate kullanıcı oturum açtığını Azure Active Directory. Başarılı oturum açma için Azure Active Directory yönetici hello form kimlik doğrulamasını etkinleştirmeniz gerekir *genel kimlik doğrulama İlkesi*.

Merhaba genel kimlik doğrulama İlkesi ile hello görüntü aşağıdaki gösterildiği gibi kimlik doğrulamasını intranet ve extranet bağlantıları için ayrı ayrı etkinleştirebilirsiniz. Bağlantı kurduğunuz hello ağ için form kimlik doğrulaması etkin değilse oturum açma hataları oluşabilir.

 ![Azure Active Directory genel kimlik doğrulama ilkesi](./media/data-catalog-prerequisites/global-auth-policy.png)

Daha fazla bilgi için bkz. [Kimlik doğrulama ilkelerini yapılandırma](https://technet.microsoft.com/library/dn486781.aspx).

## <a name="provision-data-catalog"></a>Veri kataloğu hazırlama
Bir kuruluş (Azure Active Directory etki alanı) için yalnızca bir tane veri kataloğu hazırlayabilirsiniz. Merhaba sahibi veya bir Azure aboneliği toothis Azure Active Directory etki alanına ait ortak sahibi zaten bir katalog oluşturmuşsa, birden fazla Azure aboneliğine sahip olsa bile bu nedenle, mümkün toocreate katalog yeniden olmaz. tootest, Azure Active Directory etki alanındaki bir kullanıcı tarafından veri Kataloğu oluşturulup oluşturulmadığını toohello Git [Azure veri Kataloğu giriş sayfasına](http://azuredatacatalog.com) ve hello Kataloğu görüp görmediğinizi doğrulayın. Bir katalog zaten sizin için oluşturulduysa, yordam ve Git toohello sonraki bölümde aşağıdaki hello atlayın.    

1. Toohello Git [veri Kataloğu hizmet sayfasına](https://azure.microsoft.com/services/data-catalog) tıklatıp **başlama**.
   
    ![Azure Veri Kataloğu--pazarlama giriş sayfası](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. Merhaba sahibi veya bir Azure aboneliğinin ortak sahibi olan bir kullanıcı hesabıyla oturum açın. Oturum açtıktan sonra sayfa aşağıdaki hello bakın.
   
    ![Azure Veri Kataloğu--veri kataloğu hazırlama](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. Belirtin bir **adı** hello veri kataloğu için hello **abonelik** toouse istediğiniz ve hello **konumu** hello katalog için.
4. **Fiyatlandırma** seçeneğini genişletin ve bir Azure Veri Kataloğu **sürümü** (Ücretsiz veya Standart) seçin.
    ![Azure Veri Kataloğu--sürüm seçme](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)
5. Genişletme **katalog kullanıcıları** tıklatıp **Ekle** tooadd kullanıcılar hello veri kataloğu için. Toothis Grup otomatik olarak eklenir.
    ![Azure Veri Kataloğu--kullanıcılar](media/data-catalog-get-started/data-catalog-add-catalog-user.png)
6. Genişletme **katalog yöneticilerinin** tıklatıp **Ekle** tooadd ek Yöneticiler hello veri kataloğu için. Toothis Grup otomatik olarak eklenir.
    ![Azure Veri Kataloğu--yöneticiler](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)
7. Tıklatın **Katalog Oluştur** toocreate hello veri Kataloğu, kuruluşunuz için. Oluşturulduktan sonra hello veri kataloğu için hello giriş sayfasına bakın.
    ![Azure Veri Kataloğu--oluşturuldu](media/data-catalog-get-started/data-catalog-created.png)    

### <a name="find-a-data-catalog-in-hello-azure-portal"></a>Veri Kataloğu hello Azure portal Bul
1. Ayrı bir sekmede hello web tarayıcısında veya ayrı bir web tarayıcısı penceresinde, toohello Git [Azure portal](https://portal.azure.com) ve bu, kullanılan toocreate hello veri Kataloğu hello önceki adımda oturum ile Merhaba aynı hesabı.
2. **Gözat**’ı seçin ve ardından **Veri Kataloğu**’na tıklayın.
   
    ![Azure veri Kataloğu--Azure'a göz atın](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) oluşturduğunuz katalog hello veri bakın.
   
    ![Azure Veri Kataloğu--kataloğu listede görüntüleme](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. Oluşturduğunuz hello kataloğa tıklayın. Merhaba gördüğünüz **veri Kataloğu** dikey penceresinde hello portal.
   
   ![Azure Veri Kataloğu--portaldaki dikey pencere ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. Merhaba veri Kataloğu özelliklerini görüntülemek ve bunları güncelleştirin. Örneğin, **fiyatlandırma katmanı** ve hello sürümü değiştirin.
   
    ![Azure Veri Kataloğu--fiyatlandırma katmanı](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a>Adventure Works örnek veritabanı
Bu öğreticide hello AdventureWorks2014 örnek veritabanından hello SQL Server veritabanı altyapısı için veri kaynaklarını (tablolar) kaydedebilirsiniz, ancak bildiğiniz ve rolünüzle ilgili tooyour rol verilerle toowork tercih ederseniz, herhangi bir desteklenen veri kaynağını kullanabilirsiniz. Desteklenen veri kaynaklarının listesi için bkz. [Desteklenen veri kaynakları](data-catalog-dsr.md).

### <a name="install-hello-adventure-works-2014-oltp-database"></a>Merhaba Adventure Works 2014 OLTP veritabanını yükleme
Merhaba Adventure Works veritabanı; ürünler, satış ve satın alma içeren bir kurgusal bir bisiklet üreticisine (Adventure Works Cycles), standart çevrimiçi işlem gerçekleştirme senaryolarını destekler. Bu öğreticide ürünlerle ilgili bilgileri Azure Veri Kataloğu'na kaydedersiniz.

tooinstall hello Adventure Works örnek veritabanını:

1. CodePlex üzerinde [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) dosyasını indirin.
2. toorestore hello veritabanını makinenize, hello yönergeleri izleyin [SQL Server Management Studio'yu kullanarak bir veritabanı yedeklemesini geri](http://msdn.microsoft.com/library/ms177429.aspx), veya şu adımları izleyin:
   1. SQL Server Management Studio'yu açın ve SQL Server veritabanı altyapısı toohello bağlanın.
   2. **Veritabanları**’na sağ tıklayın ve **Veritabanını Geri Yükle**’ye tıklayın.
   3. Altında **Restore Database**, hello tıklatın **aygıt** seçenek için **kaynak** tıklatıp **Gözat**.
   4. **Yedekleme cihazları seç** altında **Ekle**’ye tıklayın.
   5. Merhaba olduğu gidin toohello klasörü **AdventureWorks2014.bak** dosya, select hello dosya ve tıklatın **Tamam** tooclose hello **yedek dosyayı** iletişim kutusu.
   6. Tıklatın **Tamam** tooclose hello **yedekleme cihazları Seç** iletişim kutusu.    
   7. Tıklatın **Tamam** tooclose hello **Restore Database** iletişim kutusu.

Artık Azure veri kataloğu kullanarak hello Adventure Works örnek veritabanından veri varlıklarını kaydedebilirsiniz.

## <a name="register-data-assets"></a>Veri varlıklarını kaydetme
Bu alıştırmada, hello Kataloğu ile Merhaba Adventure Works veritabanından hello kayıt aracı tooregister veri varlıklarını kullanın. Kayıt hello veri kaynağı ve içerdiği hello varlıklara ait adlar, türler ve konumlar gibi önemli yapısal meta verilerin ayıklanması ve meta veri toohello Kataloğu kopyalama hello işlemidir. Merhaba veri kaynağı ve veri varlıkları olduğu oldukları kalır, ancak hello meta verileri hello katalog toomake tarafından kullanılan onları daha kolay bulunabilir ve anlaşılabilir.

### <a name="register-a-data-source"></a>Veri kaynağını kaydetme
1. Toohello Git [Azure veri Kataloğu giriş sayfasına](http://azuredatacatalog.com) tıklatıp **verileri Yayımla**.
   
   ![Azure Veri Kataloğu--Verileri Yayımla düğmesi](media/data-catalog-get-started/data-catalog-publish-data.png)
2. Tıklatın **uygulama Başlat** toodownload, yükleme ve çalıştırma hello kayıt aracı, bilgisayarınızdaki.
   
   ![Azure Veri Kataloğu--Başlat düğmesi](media/data-catalog-get-started/data-catalog-launch-application.png)
3. Merhaba üzerinde **Hoş Geldiniz** sayfasında, **oturum** ve kimlik bilgilerinizi girin.     
   
    ![Azure Veri Kataloğu--Hoş geldiniz sayfası](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. Merhaba üzerinde **Microsoft Azure veri Kataloğu** sayfasında, **SQL Server** ve **sonraki**.
   
    ![Azure Veri Kataloğu--veri kaynakları](media/data-catalog-get-started/data-catalog-data-sources.png)
5. Merhaba SQL Server bağlantı özelliklerini girin **AdventureWorks2014** (Merhaba aşağıdaki örneğine bakın) tıklatıp **BAĞLAN**.
   
   ![Azure Veri Kataloğu--SQL Server bağlantı ayarları](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. Merhaba meta veri varlığınızın kaydedin. Bu örnekte, kaydettiğiniz **üretim/ürün** hello AdventureWorks üretimi ad alanındaki nesneler:
   
   1. Merhaba, **sunucusu hiyerarşisi** ağaç, genişletin **AdventureWorks2014** tıklatıp **üretim**.
   2. Ctrl tuşuna basıp tıklayarak **Product**, **ProductCategory**, **ProductDescription** ve **ProductPhoto** seçimini yapın.
   3. Merhaba tıklatın **seçili oku Taşı** (**>**). Bu eylem seçilen tüm nesneler hello taşır **kayıtlı nesneler toobe** listesi.
      
      ![Azure Veri Kataloğu öğreticisi--nesnelere göz atma ve seçme](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. Seçin **Önizleme ekleme** tooinclude hello verilerin bir anlık görüntü önizlemesini. Merhaba kataloğa kopyalanır ve Hello anlık görüntü her tablodan too20 kayıtları yukarı içerir.
   5. Seçin **dahil veri profili** tooinclude hello hello veri profili için nesne istatistiklerinin bir anlık görüntü (örneğin: bir sütuna, satır sayısı için en az, en fazla ve ortalama değerler).
   6. Merhaba, **Etiket Ekle** alanına, **adventure works, döngüleri**. Bu eylem söz konusu veri varlıklarına arama etiketleri ekler. Etiketleri, kayıtlı bir veri kaynağını toohelp kullanıcılarından harika bir yoludur.
   7. Merhaba adını belirtin bir **Uzman** bu veriler (isteğe bağlı).
      
      ![Azure veri Kataloğu Öğreticisi--kayıtlı nesneler toobe](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. **KAYDET**'e tıklayın. Azure Veri Kataloğu seçtiğiniz nesneleri kaydeder. Bu alıştırmada, Adventure Works'ten seçilen hello nesneler kaydedilir. Merhaba kayıt aracı hello veri varlığından meta verileri ayıklar ve bu verileri hello Azure veri Kataloğu hizmetine kopyalar. Burada o anda bulunduğu ve hello denetimi hello Yöneticiler ve hello geçerli sistem ilkelerini altında kaldığı hello veri kalır.
      
      ![Azure Veri Kataloğu--kayıtlı nesneler](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. kayıtlı veri kaynağı nesnelerinizi toosee tıklatın **portalı görüntüle**. Hello Azure veri Kataloğu Portalı'nda tüm dört tablonun ve hello veritabanı hello ızgara görünümünde gördüğünüzü onaylayın.
      
      ![Hello Azure veri Kataloğu portalındaki nesneler ](media/data-catalog-get-started/data-catalog-view-portal.png)

Bu alıştırmada, böylece kolayca kullanıcılar tarafından kuruluşunuz genelinde bulunabilmeleri hello Adventure Works örnek veritabanını nesneleri kaydettiniz. Merhaba sonraki alıştırmada, kayıtlı veri varlıklarını nasıl toodiscover öğrenin.

## <a name="discover-data-assets"></a>Veri varlıklarını bulma
Azure Veri Kataloğu’nda bulma işlemi iki birincil mekanizmayı kullanır: arama ve filtreleme.

Arama hem sezgisel hem de güçlü tasarlanmış toobe olur. Varsayılan olarak, arama terimleri kullanıcı tarafından ek açıklamalar dahil olmak üzere hello kataloğunda herhangi bir özellikle eşleştirilir.

Filtreleme tasarlanmıştır toocomplement arama. Toomatching varlıklar etiketleri tooview eşleşen veri varlıklarını ve tooconstrain arama sonuçları ve uzmanlar, veri kaynağı türü, nesne türü gibi belirli özellikleri seçebilirsiniz.

Arama ve filtreleme, bir birleşimini kullanarak, kayıtlı Azure veri Kataloğu toodiscover hello veri varlıklarını ihtiyacınız hello veri kaynaklarına hızlıca gidebilirsiniz.

Bu alıştırmada, hello önceki alıştırmada kaydettiğiniz hello Azure veri Kataloğu portalı toodiscover veri varlıklarını kullanın. Arama söz dizimiyle ilgili ayrıntılar için bkz. [Veri Kataloğu Arama söz dizimi başvurusu](https://msdn.microsoft.com/library/azure/mt267594.aspx).

Merhaba katalogdaki veri varlıklarını bulmaya yönelik birkaç örnek verilmiştir.  

### <a name="discover-data-assets-with-basic-search"></a>Basit arama ile veri varlıklarını bulma
Basit arama bir veya daha fazla arama terimi kullanarak bir katalogda arama yapmanıza yardımcı olur. Sonuçları bir veya daha fazla hello koşulları belirtilen herhangi bir özellikte eşleşen tüm varlıkları içerir.

1. Tıklatın **giriş** hello Azure veri Kataloğu portalında. Merhaba web tarayıcısını kapattıysanız toohello Git [Azure veri Kataloğu giriş sayfasına](https://www.azuredatacatalog.com).
2. Merhaba arama kutusuna `cycles` ve basın **ENTER**.
   
    ![Azure Veri Kataloğu--basit metin araması](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. Tüm dört tablonun ve hello sonuçlarında hello veritabanını (AdventureWorks2014) gördüğünüzü onaylayın. Arasında geçiş yapabilirsiniz **Izgara Görünümü** ve **liste görünümü** hello görüntü aşağıdaki gösterildiği gibi hello araç çubuğundaki düğmeler tıklatılarak. Bu hello arama anahtar sözcüğü çünkü hello arama sonuçlarında vurgulanır fark hello **vurgulayın** seçenek **ON**. Merhaba sayısını da belirtebilirsiniz **sayfa başına sonuç** arama sonuçlarında.
   
    ![Azure Veri Kataloğu--basit metin araması sonuçları](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    Hello **aramaları** panosudur sol hello ve hello **özellikleri** hello sağ panosudur. Merhaba üzerinde **aramaları** paneli, arama ölçütlerini değiştirebilir ve sonuçları filtreleyebilirsiniz. Merhaba **özellikleri** paneli hello ızgara veya liste görünümünde seçili nesnenin özelliklerini görüntüler.
4. Tıklatın **ürün** hello arama sonuçlarında. Merhaba tıklatın **Önizleme**, **sütunları**, **veri profili**, ve **belgelerine** sekmeler veya hello ok tooexpand hello alt bölme'ı tıklatın.  
   
    ![Azure Veri Kataloğu--alt bölme](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    Merhaba üzerinde **Önizleme** sekmesinde hello hello verilerin bir önizlemesini görmek **ürün** tablo.  
5. Merhaba tıklatın **sütunları** sekmesinde sütunlara ilişkin toofind ayrıntıları (gibi **adı** ve **veri türü**) hello veri varlığının içinde.
6. Merhaba tıklatın **veri profili** toosee verilerin hello profil sekmesinde (örneğin: satır sayısı verileri veya bir sütundaki en küçük değer boyutu) hello veri varlığının içinde.
7. Filtre Hello sonuçları kullanarak **filtreleri** hello soldaki. Örneğin, **tablo** için **nesne türü**, ve veritabanı hello değil, yalnızca hello dört tabloları bakın.
   
    ![Azure Veri Kataloğu--arama sonuçlarını filtreleme](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a>Özellik kapsamı ile veri varlıklarını bulma
Belirtilen özelliğin özellik kapsamı hello arama terimi ile Merhaba burada eşleştirildiği veri varlıklarını bulma yardımcı olur.

1. Clear hello **tablo** altında filtre **nesne türü** içinde **filtreleri**.  
2. Merhaba arama kutusuna `tags:cycles` ve basın **ENTER**. Bkz: [veri kataloğu arama söz dizimi başvurusu](https://msdn.microsoft.com/library/azure/mt267594.aspx) tüm hello veri kataloğu arama için kullanabileceğiniz özellikleri hello için.
3. Tüm dört tablonun ve hello sonuçlarında hello veritabanını (AdventureWorks2014) gördüğünüzü onaylayın.  
   
    ![Veri Kataloğu--özellik kapsamı arama sonuçları](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-hello-search"></a>Merhaba aramayı kaydetme
1. Hello içinde **aramaları** hello bölmesinde **geçerli arama** bölümünde hello arama için bir ad girin ve tıklatın **kaydetmek**.
   
    ![Azure Veri Kataloğu--aramayı kaydetme](media/data-catalog-get-started/data-catalog-save-search.png)
2. Altında hello kaydedilen arama görüntülenir onaylayın **kayıtlı aramaları**.
   
    ![Azure Veri Kataloğu--kayıtlı aramalar](media/data-catalog-get-started/data-catalog-saved-search.png)
3. Hello kayıtlı arama üzerinde gerçekleştirebileceğiniz hello eylemlerden birini seçin (**yeniden adlandırma**, **silmek**, **varsayılan olarak Kaydet** arama).
   
    ![Azure Veri Kataloğu--kayıtlı arama seçenekleri](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a>Boole işleçleri
Aramanızı Boole işleçleriyle genişletebilir veya daraltabilirsiniz.

1. Merhaba arama kutusuna `tags:cycles AND objectType:table`ve basın **ENTER**.
2. Yalnızca tabloları (Merhaba veritabanını değil) hello sonuçlarında gördüğünüzü onaylayın.  
   
    ![Azure Veri Kataloğu--aramada Boole işleci](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a>Parantezler ile gruplandırma
Parantezler ile gruplandırma yaparak hello sorgu tooachieve mantıksal ayırma, özellikle Boole işleçleri ile birlikte bölümlerini gruplandırabilirsiniz.

1. Merhaba arama kutusuna `name:product AND (tags:cycles AND objectType:table)` ve basın **ENTER**.
2. Yalnızca hello gördüğünüzü onaylayın **ürün** hello arama sonuçlarında tablo.
   
    ![Azure Veri Kataloğu--gruplandırma araması](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a>Karşılaştırma işleçleri
Karşılaştırma işleçleri ile sayısal ve tarih veri türlerine sahip özellikler için eşitlik dışındaki karşılaştırmaları kullanabilirsiniz.

1. Merhaba arama kutusuna `lastRegisteredTime:>"06/09/2016"`.
2. Clear hello **tablo** altında filtre **nesne türü**.
3. **ENTER**'a basın.
4. Merhaba gördüğünüzü onaylayın **ürün**, **ProductCategory**, **ProductDescription**, ve **ProductPhoto** tablolar ve hello Arama sonuçlarında kaydettiğiniz AdventureWorks2014 veritabanını.
   
    ![Azure Veri Kataloğu--karşılaştırma arama sonuçları](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

Bkz: [nasıl toodiscover veri varlıklarını](data-catalog-how-to-discover.md) veri varlıklarını bulma hakkında ayrıntılı bilgi için ve [veri kataloğu arama söz dizimi başvurusu](https://msdn.microsoft.com/library/azure/mt267594.aspx) arama söz dizimi için.

## <a name="annotate-data-assets"></a>Veri varlıklarına açıklama ekleme
Bu alıştırmada, hello Azure veri Kataloğu portalı tooannotate kullanın (açıklamalar, etiketler veya uzmanlar gibi bilgileri ekleme), daha önce kaydettiğiniz hello Kataloğu'nda veri varlıklarının. Hello ek açıklamaları tamamlayacak kayıt sırasında hello veri kaynağından ayıklanan hello yapısal meta verileri destekleyip geliştirecek ve çok daha kolay toodiscover hello veri varlıklarını yapar ve anlama.

Bu alıştırmada tek bir veri varlığına (ProductPhoto) açıklama eklersiniz. Kolay bir ad ve açıklama toohello ProductPhoto veri varlığına ekleyin.  

1. Toohello Git [Azure veri Kataloğu giriş sayfasına](https://www.azuredatacatalog.com) ve ile arama `tags:cycles` toofind hello veri varlıklarını kayıtlı.  
2. Arama sonuçlarında **ProductPhoto** öğesine tıklayın.  
3. Girin **ürün görüntüleri** için **kolay ad** ve **pazarlama malzemeleri için ürün fotoğrafları** hello için **açıklama**.
   
    ![Azure Veri Kataloğu--ProductPhoto açıklaması](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    Merhaba **açıklama** başkalarının bulmak ve neden ve nasıl toouse hello veri varlığına seçtiğini anlamasına yardımcı olur. Ayrıca daha fazla etiket ekleyebilir ve sütunları görüntüleyebilirsiniz. Arama ve filtreleme toodiscover veri varlıklarını hello açıklayıcı meta verileri kullanarak deneyebilirsiniz artık toohello katalog ekledik.

Ayrıca yapabilirsiniz bu sayfada aşağıdaki hello:

* Merhaba veri varlığı için uzmanlar ekleyin. Tıklatın **Ekle** hello içinde **uzmanlar** alanı.
* Merhaba veri kümesi düzeyinde etiketler ekleyin. Tıklatın **Ekle** hello içinde **etiketleri** alanı. Etiket bir kullanıcı etiketi veya bir sözlük etiketi olabilir. Merhaba, veri Kataloğu standart sürümü, katalog yöneticilerinin merkezi bir iş sınıflandırması tanımlamasına yardımcı olan bir iş sözlüğü içerir. Böylece katalog kullanıcıları, sözlük terimlerini veri varlıklarına ek açıklama olarak dahil edebilir. Daha fazla bilgi için bkz: [nasıl tooset yukarı hello iş sözlüğünü yönetilen etiketleme için](data-catalog-how-to-business-glossary.md)
* Merhaba sütun düzeyinde etiketler ekleyin. Tıklatın **Ekle** altında **etiketleri** hello sütunu için tooannotate istiyor.
* Merhaba sütun düzeyinde açıklama ekleyin. Sütun için **Açıklama** girin. Merhaba veri kaynağından ayıklanan hello açıklama meta verileri de görüntüleyebilirsiniz.
* Ekleme **erişim isteği** kullanıcılar toorequest erişim nasıl toohello veri varlığına gösterir bilgi.
  
    ![Azure Veri Kataloğu--etiket, açıklama ekleme](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* Merhaba seçin **belgelerine** sekmesinde ve hello veri varlığı için belgeleri belirtin. Azure veri Kataloğu belgeleri ile veri kataloğunuzu bir içerik deposu toocreate veri varlıklarınız varlıklarınızın tam bir açıklamasını kullanabilirsiniz.
  
    ![Azure Veri Kataloğu--Belgeler sekmesi](media/data-catalog-get-started/data-catalog-documentation.png)

Bir ek açıklama toomultiple veri varlıklarını de ekleyebilirsiniz. Örneğin, kaydettiğiniz tüm hello veri varlıklarını seçebilir ve bunlar için bir uzman belirtin.

![Azure Veri Kataloğu--birden fazla veri varlığına açıklama ekleme](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

Azure veri Kataloğu yönelik kitle kaynak yaklaşımı tooannotations destekler. Bir veri varlığına ve kullanımına açısı olan herhangi bir kullanıcı, yakalanan Perspektif ve kullanılabilir tooother kullanıcılar böylece herhangi bir veri Kataloğu kullanıcısı etiketler (kullanıcı veya sözlük), açıklamalar ve diğer meta verileri ekleyebilirsiniz.

Bkz: [nasıl tooannotate veri varlıklarını](data-catalog-how-to-annotate.md) veri varlıklarına açıklama hakkında ayrıntılı bilgi.

## <a name="connect-toodata-assets"></a>Toodata varlıklar Bağlan
Bu alıştırmada bağlantı bilgilerini kullanarak veri varlıklarını tümleşik bir istemci aracında (Excel) ve tümleşik olmayan bir araçta (SQL Server Management Studio) açarsınız.

> [!NOTE]
> Azure veri Kataloğu, vermediğinin tooremember toohello gerçek veri kaynağına erişim önemlidir — yalnızca sizin için toodiscover kolaylaştırır ve onu anladığınızdan emin olun. Tooa veri kaynağına bağlandığınızda, Windows kimlik bilgileri veya gerektiğinde kimlik bilgilerini ister kullanır seçtiğiniz istemci uygulaması hello. Daha önce erişim toohello veri kaynağı verilmemiş, toobe bağlanabilmesi için önce erişim izni gerekir.
> 
> 

### <a name="connect-tooa-data-asset-from-excel"></a>Excel'den tooa veri varlığına bağlanma
1. Arama sonuçlarından **Ürün**’ü seçin. Tıklatın **Aç** hello araç ve tıklatın **Excel**.
   
    ![Azure veri Kataloğu--toodata varlık Bağlan](media/data-catalog-get-started/data-catalog-connect1.png)
2. Tıklatın **açık** hello indirme açılır penceresinde. Bu deneyim hello tarayıcıya bağlı olarak değişebilir.
   
    ![Azure Veri Kataloğu--indirilen Excel bağlantı dosyası](media/data-catalog-get-started/data-catalog-download-open.png)
3. Merhaba, **Microsoft Excel Güvenlik Bildirimi** penceresinde tıklatın **etkinleştirmek**.
   
    ![Azure Veri Kataloğu--Excel güvenlik açılır penceresi](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. Hello Hello Varsayılanları tutun **veri içeri aktarma** iletişim kutusu ve tıklatın **Tamam**.
   
    ![Azure Veri Kataloğu--Excel ile verileri içeri aktarma](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. Excel'de hello veri kaynağı görüntüle.
   
    ![Azure Veri Kataloğu--Excel’deki ürün tablosu](media/data-catalog-get-started/data-catalog-connect2.png)

Bu alıştırmada Azure veri kataloğu kullanarak bulunan toodata varlıklar bağlı. Hello Azure veri Kataloğu portalı ile Merhaba tümleştirilmiş hello istemci uygulamalarını kullanarak doğrudan bağlanabilir **Aç** menüsü. Merhaba hello varlık meta verilerinde bulunan bağlantı konumu bilgilerini kullanarak seçtiğiniz herhangi bir uygulamayla bağlanabilir. Örneğin, bu öğreticide kaydedilen hello veri varlıklarını SQL Server Management Studio tooconnect toohello AdventureWorks2014 veritabanını tooaccess hello veri kullanabilirsiniz.

1. **SQL Server Management Studio**’yu açın.
2. Merhaba, **tooServer bağlanmak** iletişim kutusunda, hello hello sunucu adı girin **özellikleri** hello Azure veri Kataloğu portalındaki bölmesinde.
3. Uygun kimlik doğrulama ve kimlik bilgilerini tooaccess hello veri varlığına kullanın. Erişimi yoksa, bilgileri hello kullanın **istek erişimi** alan tooget onu.
   
    ![Azure Veri Kataloğu--erişim isteği](media/data-catalog-get-started/data-catalog-request-access.png)

Tıklatın **bağlantı dizelerini görüntüle** tooview ve kopyalama ADF.NET, ODBC ve OLEDB bağlantı dizeleri toohello Pano, uygulamanızda kullanmak için.

## <a name="manage-data-assets"></a>Veri varlıklarını yönetme
Bu adımda, gördüğünüz nasıl tooset veri varlıklarınız için güvenliği. Veri Kataloğu kullanıcılara erişim toohello verilerin kendisini sağlamaz. Merhaba sahibi hello veri kaynağının veri erişimi denetler.

Veri Kataloğu kullanabilirsiniz toodiscover veri kaynakları ve tooview hello meta verileri ilgili hello kataloğa kayıtlı toohello kaynakları. Burada veri kaynakları yalnızca görünür toospecific kullanıcılara veya belirli grupların toomembers olmalıdır durumlar olabilir. Bu senaryolar için veri Kataloğu tootake hello katalog içindeki kayıtlı veri kaynaklarının sahipliğini ve toothen denetim hello sahip olduğunuz hello varlıklarının görünürlüğünü kullanabilirsiniz.

> [!NOTE]
> Bu alıştırmada tanımlanan hello yönetim özellikleri yalnızca hello, Azure veri Kataloğu standart sürümü kullanılabilen, hello ücretsiz sürüm içinde değil.
> Azure veri Kataloğu'nda veri varlıklarının sahipliğini, ikincil sahip toodata varlıklar ekleyin ve hello veri varlıklarının görünürlüğünü ayarlayabilirsiniz.
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a>Veri varlıklarının sahipliğini alma ve görünürlüğü kısıtlama
1. Toohello Git [Azure veri Kataloğu giriş sayfasına](https://www.azuredatacatalog.com). Merhaba, **arama** metin kutusuna `tags:cycles` ve basın **ENTER**.
2. Merhaba sonuç listesindeki bir öğeyi tıklatın ve'ı tıklatın **Sahipliği Al** hello araç.
3. Merhaba, **Yönetim** hello bölümünü **özellikleri** öğesine tıklayın **Sahipliği Al**.
   
    ![Azure Veri Kataloğu--sahipliği alma](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. toorestrict görünürlük seçin **sahipler ve bu kullanıcılar** hello içinde **görünürlük** 'ye tıklayın **Ekle**. Kullanıcı e-posta adreslerini girin hello metin kutusu ve tuşuna **ENTER**.
   
    ![Azure Veri Kataloğu--erişimi kısıtlama](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a>Veri varlıklarını kaldırma
Bu alıştırmada hello Azure veri Kataloğu portalı tooremove Önizleme verilerini kayıtlı veri varlıklarını gelen kullanın ve veri varlıklarını hello Kataloğu'ndan silin.

Azure Veri Kataloğu'nda tek bir varlığı veya birden çok varlığı silebilirsiniz.

1. Toohello Git [Azure veri Kataloğu giriş sayfasına](https://www.azuredatacatalog.com).
2. Merhaba, **arama** metin kutusuna `tags:cycles` tıklatıp **ENTER**.
3. Merhaba sonuç listesinden bir öğe seçin ve tıklatın **silmek** hello görüntü aşağıdaki gösterildiği gibi hello araç çubuğunda:
   
    ![Azure Veri Kataloğu--ızgara öğesini silme](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    Merhaba liste görünümünü kullanıyorsanız, hello onay kutusunu hello görüntü aşağıdaki gösterildiği gibi hello öğesinin toohello sol olur:
   
    ![Azure Veri Kataloğu--liste öğesini silme](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    Ayrıca, birden fazla veri varlığına seçip hello görüntü aşağıdaki gösterildiği gibi silebilirsiniz:
   
    ![Azure Veri Kataloğu--birden fazla veri varlığını silme](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> Merhaba hello kataloğun varsayılan davranışı tooallow tüm kullanıcı tooregister herhangi olduğundan veri kaynağı ve tooallow tüm kullanıcı toodelete kayıtlı herhangi bir veri varlığını. Merhaba, Azure veri Kataloğu standart sürümü dahil hello yönetim özellikleri varlıklar silebilirsiniz sahipliği varlıklar bulabilmesi için kısıtlama ve kısıtlama varlıkları alma için ek seçenekler sağlar.
> 
> 

## <a name="summary"></a>Özet
Bu öğreticide, kurumsal veri varlıklarını kaydetme, bulma, yönetme ve bunlara ek açıklama ekleme de dahil olmak üzere Azure Veri Kataloğu'nun temel özelliklerini incelediniz. Merhaba öğreticiyi tamamladığınıza göre zamanı tooget başlatıldı. Sizin ve ekibinizin bağlı hello veri kaynaklarını kaydederek ve iş arkadaşlarınızı toouse hello katalog davet hemen başlayabilirsiniz.

## <a name="references"></a>Başvurular
* [Nasıl tooregister veri varlıklarını](data-catalog-how-to-register.md)
* [Nasıl toodiscover veri varlıklarını](data-catalog-how-to-discover.md)
* [Nasıl tooannotate veri varlıklarını](data-catalog-how-to-annotate.md)
* [Nasıl toodocument veri varlıklarını](data-catalog-how-to-documentation.md)
* [Nasıl tooconnect toodata varlıklar](data-catalog-how-to-connect.md)
* [Nasıl toomanage veri varlıklarını](data-catalog-how-to-manage.md)

