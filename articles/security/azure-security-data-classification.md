---
title: "Azure için sınıflandırma aaaData | Microsoft Docs"
description: "Bu makalede, bir giriş toohello veri sınıflandırması temelleri sağlar ve özellikle bağlamında hello bilgi işlem ve Microsoft Azure kullanarak bulut değerini vurgular"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Azure veri sınıflandırması
Bu makale, bir giriş toohello veri sınıflandırması temelleri sağlar ve özellikle bağlamında hello bilgi işlem ve Microsoft Azure kullanarak bulut değerini vurgular. 

## <a name="data-classification-fundamentals"></a>Veri sınıflandırması temelleri
Bir kuruluştaki başarılı veri sınıflandırması, kuruluşunuzun gereksinimlerini geniş hakkında farkındalık ve veri varlıklarınız bulunduğu, kapsamlı olarak anlamayı gerektirir.  

Veri üç temel durumdan birinde bulunur: 

* Bekleyen 
* İşlemde 
* Aktarım sırasında 

Veri sınıflandırması için benzersiz teknik çözümler tüm üç durumdan gerektirir, ancak hello veri sınıflandırma uygulanan ilkeler olması hello aynı her biri için. Gizli olarak sınıflandırılmış verilerin toostay gizli REST işleminde hem de Aktarım sırasında gerekir. 

Veriler de yapılandırılmış veya yapılandırılmamış olabilir. Hello için tipik sınıflandırma işlemlerini yapısal veritabanlarında bulunan verileri ve elektronik belgeleri, kaynak kodu ve e-posta gibi yapılandırılmamış veriler için olandan daha az karmaşık ve zaman alıcı toomanage değildir. 

> [!TIP]
> Azure işlevlerini ve veri şifrelemesi için en iyi uygulamalar hakkında daha fazla bilgi için okumaya devam [Azure veri şifreleme en iyi uygulamalar](azure-security-data-encryption-best-practices.md)
> 
> 

Genel olarak, kuruluşlar daha fazla olacaktır yapılandırılmış veri daha yapılandırılmamış veriler. Veri yapılandırılmış veya yapılandırılmamış olmasına bakılmaksızın, toomanage veri duyarlılık için önemlidir. Düzgün şekilde uygulandığında, veri sınıflandırması genel ya da boş toodistribute kabul edilen veri varlıklarını daha büyük gözetim ile yönetilen varlıklar, hassas veya gizli verileri sağlamaya yardımcı olur. 

### <a name="controlling-access-toodata"></a>Erişim toodata denetleme
Kimlik doğrulama ve Yetkilendirme genellikle birbiriyle yanıltıcı olmaktadır ve rollerine yanlış. Gerçekte oldukları hello aşağıdaki şekilde gösterildiği gibi oldukça farklı olabilir.  

![Veri erişim ve Denetim](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Kimlik Doğrulaması
Kimlik doğrulaması genellikle en az iki bölümden oluşur: bir kullanıcı adı veya kullanıcı kimliği tooidentify kullanıcı ve parola, kullanıcı adı kimlik bilgisi hello tooconfirm gibi belirteci geçerli değil. Merhaba işlem hello kimliği doğrulanmış kullanıcının erişimini tooany öğeleri veya hizmetlerle sağlamaz; Merhaba kullanıcının kim olduklarını söyleyin doğrular.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) tooauthenticate izin ver ve Kullanıcıları yetkilendirmek kimlik bulut tabanlı hizmetler sağlar. 
> 
> 

### <a name="authorization"></a>Yetkilendirme
Yetkilendirme, bir uygulama, veri kümesi, veri dosyası veya başka bir nesne kimliği doğrulanmış kullanıcının hello özelliği tooaccess sağlama hello işlemidir. Kimliği doğrulanmış kullanıcılar hello hakları toouse atama değiştirebilir veya erişebilecekleri öğeleri silme dikkat toodata sınıflandırma gerektirir. 

Başarılı yetkilendirme tooaccess dosyaları ve bilgileri rolü, güvenlik ilkesi ve risk ilke konuları bir bileşimine dayalı bir mekanizma toovalidate ayrı kullanıcıların uygulaması gereken gerektirir. Örneğin, belirli satır iş kolu (LOB) uygulamaları verilerden tüm çalışanlar tarafından erişilen toobe gerekmeyebilir ve yalnızca küçük bir alt çalışanların büyük olasılıkla toohuman kaynakları (HR) dosyaları erişecek. Ancak, kuruluşlar toocontrol için kimin ne zaman ve nasıl olarak, kullanıcıların kimlik doğrulaması için geçerli bir sistem karşılanması gereken olarak, verilere erişebilir. 

> [!TIP]
> Microsoft Azure'da, kullanıcıların işlerini tooperform gerektiğini emin tooleverage Azure rol tabanlı erişim denetimi (RBAC) toogrant yalnızca hello erişim miktarını olun. Okuma [rol atamalarını toomanage erişim tooyour Azure Active Directory kaynaklarını kullanmak](../active-directory/role-based-access-control-configure.md) daha fazla bilgi için. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Rolleri ve sorumlulukları bulut
Bulut sağlayıcıları riskleri yönetmeye yardımcı olabilen, müşteriler, bu veri sınıflandırma yönetimi tooensure gerekir ve zorlama düzgün uygulanır ancak tooprovide uygun düzeyde bir veri Yönetimi Hizmetleri hello.  

Veri sınıflandırması sorumlulukları değişir hangi bulut hizmeti modeli yerinde üzerinde hello aşağıdaki şekilde gösterildiği gibi dayanır. Merhaba üç birincil bulut hizmeti modeli olarak bir hizmet (Iaas), platform (PaaS) hizmet olarak yazılım (SaaS) hizmet olarak altyapı ' dir. Veri sınıflandırması mekanizmalar uygulaması hello bağımlılık ve hello bulut sağlayıcısı beklentilerini göre değişir. 

![Roller](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Verilerinizi sınıflandırmak için sorumlu olmasına rağmen bulut sağlayıcılarının nasıl güvenli ve bulut içinde depolanan hello Müşteri verilerinin hello gizliliğini hakkında yazılı taahhüt olmalısınız.  

* **Iaas sağlayıcıları** gereksinimleri sınırlı veri sınıflandırma özelliklerinin ve müşteri uyumluluk gereksinimleri sanal ortam hello tooensuring uyum. Yalnızca müşteri verilerini uyumluluk gereksinimlerini ele tooensure gerektiğinden Iaas sağlayıcıları daha küçük bir rol veri sınıflandırması özelliği yoktur. Ancak, sağlayıcıları hala sanal ortamlarını veri merkezlerine veri sınıflandırma gereksinimlerine ek toosecuring içinde adres emin olmalısınız.
* **PaaS sağlayıcıları** sorumlulukları karma, hello platform için bir sınıflandırma aracı bir katmanlı yaklaşımın tooprovide güvenlik kullanılabileceği için. PaaS sağlayıcıları kimlik doğrulama ve yetkilendirme kuralları büyük olasılıkla bazı sorumlu olabilir ve güvenlik ve veri sınıflandırma özellikleri tootheir uygulama katmanı sağlamanız gerekir. Çok Iaas sağlayıcıları gibi tüm ilgili veri sınıflandırma gereksinimlerine kendi platform karşılar tooensure PaaS sağlayıcıları gerekir.
* **SaaS sağlayıcısı** sık bir yetkilendirme zinciri bir parçası olarak kabul edilir ve hello SaaS uygulamada depolanan verileri hello tooensure sınıflandırma türüne göre denetlenebilir. SaaS uygulamaları LOB uygulamaları için kullanılabilir ve kendi yapısı gereği tooprovide anlamına gelir tooauthenticate hello ve kullanılan ve depolanan veri yetkilendirin. 

## <a name="classification-process"></a>Sınıflandırma işlemi
Merhaba anlamak birçok kuruluş, veri sınıflandırması için gereken ve temel bir sınama yüz tooimplement istediğiniz: Burada toobegin?

Tooimplement veri sınıflandırması toouse hello planı olan bir etkili ve en basit yolu onay, ACT gelen model yapın [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). Merhaba aşağıdakilerden grafikleri gerekli toosuccessfully uygulama veri sınıflandırması Bu modelde hello görevler şekil.  

1. **PLAN**. Veri varlıklarını, bir veri koruyucu toodeploy hello sınıflandırma programı belirleyin ve koruma profilleri geliştirin. 
2. **YAPMAK**. Veri sınıflandırma ilkeleri varılan sonra hello program dağıtın ve zorlama teknolojileri için gizli verileri gerektiği gibi uygulayın.  
3. **DENETLEME**. Denetleyin ve hello araçları ve kullanılan yöntemleri etkili bir şekilde adresleme tooensure hello sınıflandırma ilkeleri raporları doğrulayın. 
4. **ACT**. Veri erişimi Hello durumunu gözden geçirin ve dosyaları ve bir sınıflama ve düzeltme Metodoloji tooadopt değişiklikleri ve tooaddress yeni riskleri kullanarak gözden geçirme gerektiren verileri gözden geçirin.  

![Planlama, denetleme hareket,](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Gereksinimlerinize adresleri terminolojisi modelini seçin
El ile işlemleri, bir kullanıcının veya sistemin konumu, uygulama tabanlı işlemler veritabanına özel sınıflandırma gibi temel alır ve otomatik verileri sınıflandırmak konum temelli işlemleri dahil verileri sınıflandırmak için çeşitli işlemler var bazıları hello "gizli verileri korumak" bölümünde bu makalenin sonraki bölümlerinde açıklanan çeşitli teknolojiler tarafından kullanılan işlemleri.  

Bu makale iyi kullanılan ve endüstri dikkate modellerinde tabanlı iki genelleştirilmiş terminolojisi modeli sunar. Her ikisi de, üç düzeyde sınıflandırma duyarlılık sağlamak, bu terimleri modeller aşağıdaki tablonun hello gösterilir.  

> [!NOTE]
> bir dosya veya kaynak genellikle farklı düzeylerde hello yüksek düzey bir sınıflandırmaya mevcut sınıflandırılmış veri kurmalısınız birleştirir genel sınıflandırma hello sınıflandırma olduğunda. Örneğin, hassas ve kısıtlı verileri içeren bir dosyayı sınıflandırılmalıdır olarak kısıtlı.  
> 
> 

| **Duyarlılık** | **1 terminolojisi modeli** | **Terminolojisi modeli 2** |
| --- | --- | --- |
| Yüksek |Gizli |Sınırlı |
| Orta |Yalnızca dahili kullanım |Hassas |
| Düşük |Genel |Sınırsız |

#### <a name="confidential-restricted"></a>Gizli (sınırlı)
Gizli veya kısıtlanmış olarak sınıflandırılmış bilgileri yıkıcı tooone veya daha fazla kişiler ve/veya kayıp ya da güvenliği aşılmış, kuruluşların olabilir verileri içerir. Gibi bilgileri sık bir "gerek tooknow" temelde sağlanır ve şunlar olabilir: 

* Sosyal Güvenlik veya Ulusal Kimlik numaraları, passport numaraları, kredi kartı numaraları, sürücünün lisans sayıları, tıbbi kaydeder ve sağlık sigortası ilkesi kimlik numaraları gibi kişisel bilgiler dahil olmak üzere kişisel veriler.  
* Denetimi gibi finansal hesap numarası veya yatırım hesap numaraları gibi finansal kaydeder. 
* Belgeler veya benzersiz veya belirli fikri mülkiyet veriler gibi iş malzemeler.  
* Olası avukata ayrıcalıklı malzeme gibi yasal veriler. 
* Özel şifreleme anahtarları, kullanıcı adı parola çiftleri veya biyometrik özel anahtar dosyaları gibi diğer kimlik sıraları dahil olmak üzere, kimlik doğrulama verileri. 

Gizli olarak sık sınıflandırılır verileri içeren yasal ve veri işleme için uyumluluk gereksinimleri. 

#### <a name="for-internal-use-only-sensitive"></a>Dahili kullanım yalnızca (hassas)
Orta duyarlılığını olacak şekilde sınıflandırılır bilgi dosyaları ve bir kişi ve/veya kuruluş üzerinde ciddi bir etkisi kaybolur veya yok olması gereken olmayan verileri içerir. Gibi bilgileri içerebilir: 

* E-posta, çoğunu silinmiş ya da (Merhaba gizli sınıflandırmasında tanımlanan kişilerin posta kutuları veya e-posta hariç) kriz neden olmadan dağıtılmış.  
* Belgeler ve gizli verileri içermez dosyaları.

Genellikle, bu sınıflandırma, gizli olmayan bir şey içerir. Bu Sınıflandırma, yönetilen veya günlük kullanılan çoğu dosyaları gizli olarak sınıflandırılmış çünkü çoğu işletme verilerini dahil edebilirsiniz. Genel kullanıma açılmadan veya gizli verileri Hello özel durum ile bir iş kuruluş içindeki tüm veriler hassas olarak varsayılan olarak sınıflandırılabilir. 

#### <a name="public-unrestricted"></a>Public (sınırsız)
Genel olarak sınıflandırılır bilgiler, veri ve kritik toobusiness gereksinimlerini veya işlemleri olmayan dosyaları içerir. Bu sınıflandırma malzeme veya basın duyuruları pazarlama gibi bunların kullanılması için ortak yayımlanan toohello kasıtlı olarak daha eski verileri de içerir. Ayrıca, bu sınıflandırma, bir e-posta hizmeti tarafından depolanan istenmeyen e-posta iletileri gibi verileri içerebilir. 

### <a name="define-data-ownership"></a>Veri sahipliği tanımlayın
Önemli tooestablish tüm veri varlıklarının sahipliğini temizleyin custodial zinciri var. Merhaba aşağıdaki tabloda farklı veri sahipliği rolleri veri sınıflandırma çabaları ve ilgili haklarını tanımlar.  

| **Rol** | **Oluşturma** | **Değiştirme/silme** | **Temsilci** | **Okuma** | **Arşiv/geri yükleme** |
| --- | --- | --- | --- | --- | --- |
| Sahip |X |X |X |X |X |
| Koruyucu | | |X | | |
| Yönetici | | | | |X |
| Kullanıcı\* | |X | |X | |

**Kullanıcıları düzenleme ve bir koruyucu tarafından silme gibi ek haklar verilebilir* 

> [!NOTE]
> Bu tablo, roller ve haklar, ancak yalnızca temsili bir örnek kapsamlı bir listesi sağlamaz. 
> 
> 

Merhaba **veri varlık sahibi** kimlerin temsilci sahipliği ve bir koruyucu atamak hello veri hello özgün Oluşturucu. Bir dosya oluşturulurken hello sahibi mümkün tooassign sorumluluk toounderstand gizli olarak sınıflandırılmış toobe ihtiyaç duyduğu sahip oldukları anlamına gelir, kuruluşun ilkelerine bağlı olarak bir sınıflandırması olması gerekir. Sahip veya gizli (sınırlı) veri türleri oluşturma sorumlu edilmedikleri sürece tüm veri varlık sahibinin verileri dahili kullanım yalnızca (duyarlı olduğu gibi) otomatik olarak sınıflandırılan olabilir. Sık sık hello sahibinin rol Hello veri sınıflandırılır sonra değiştirilir. Örneğin, hello sahibi bir sınıflandırılmış bilgilerinin veritabanı oluşturma ve bunların haklarını toohello veri koruyucu teknisyene.  

> [!NOTE]
> Veri varlık sahipleri genellikle Hizmetleri, aygıtları ve bazıları da kişisel ve bazıları toohello kuruluş ait medya karışımını kullanın. Clear kuruluş ilkesi, dizüstü bilgisayarlar gibi ve akıllı aygıtlar kullanımını veri sınıflandırma yönergelerine uygun olduğundan emin olun yardımcı olabilir.  
> 
> 

Merhaba **veri varlık koruyucu** hello varlık sahibi (veya kendi temsilci) toomanage hello varlık according tooagreements hello varlık sahibi olan veya uygulanabilir ilke gereksinimlere uygun atanır. İdeal olarak, otomatik bir sistemde hello koruyucu rol uygulanabilir. Bir varlık koruyucusu gerekli erişim denetimleri sağlanır ve yönetilmesinden sorumludur ve varlıkların korunması tootheir dikkatli temsilci sağlar. Merhaba varlık koruyucu Hello sorumluluklarını dahil olabilir:  

* Merhaba varlık hello varlık sahibinin yönü uygun olarak veya hello varlık sahibi belirlendiği koruma 
* Sınıflandırma ilkeleri ile uyum emin olma 
* Herhangi bir varlık sahiplerini bildiren değiştirir tooagreed-denetimleri ve/veya koruma yordamları önceki toothose değişiklikler etkili alma bağlı 
* Değişiklikleri tooor hello varlık koruyucu'nın sorumlulukları kaldırılması hakkında raporlama toohello varlık sahibi 
* Bir **yönetici** bütünlüğü saklanır, ancak veri varlık sahibi, koruyucu veya kullanıcı olmadıkları sağlamak için sorumlu kullanıcıyı temsil eder. Aslında, çok sayıda yönetici rolleri toohello verilere erişmek zorunda kalmadan veri kapsayıcısı Yönetim Hizmetleri sağlar. Hello yöneticisi rolü yedekleme ve geri yükleme hello varlıklar kayıtlarının bakımı hello verilerin içerir ve seçme, alınırken ve işletim aygıtlar ve depolama, ev hello varlıklar hello. 
* Merhaba varlık kullanıcı erişimi toodata veya bir dosya izni olan herkes içerir. Erişim atama genellikle hello sahibi toohello varlık koruyucusu tarafından temsilci.  

### <a name="implementation"></a>Uygulama
Yönetim değerlendirmeleri tooall sınıflandırma yöntemleri uygulayın. Bu noktalar kim tooinclude ayrıntılarını gereksinim ne, nerede, ne zaman ve neden bir veri varlığına kullanılan, erişilen, değiştirilen veya silinen. Tüm varlık yönetimi nasıl bir kuruluş kendi riskleri görünümleri ile ilgili bir anlama yapılması gerekir, ancak basit bir Metodoloji hello veri sınıflandırma işleminde tanımlanan uygulanabilir. Veri sınıflandırması için ek hususlar yeni uygulamaları ve araçları ve sınıflandırma yöntemi uygulandıktan sonra değişikliği yönetme hello giriş içerir.  

### <a name="reclassification"></a>Sınıflama
Yeniden sınıflama veya bir veri varlığına hello sınıflandırma durumunu değiştirme riski profili değişti ya da bir kullanıcı veya sistem bu hello veri varlığın önem belirler yapılacak toobe gerekir. Bu çalışmaların hello sınıflandırma durum toobe geçerli devam etmesini sağlamaya yönelik önemli ve geçerli. El ile sınıflandırılmaz çoğu içerik otomatik olarak sınıflandırılmış veya bir veri koruyucu veya veri sahibi tarafından kullanıma dayalı. 

### <a name="manual-data-reclassification"></a>El ile veri Sınıflama
İdeal olarak, bu çalışmaların bir değişiklik hello ayrıntılarını yakalanan ve denetlenen olduğundan emin olun. el ile yeniden sınıflandırma en olası nedeni Hello duyarlılık nedenlerinden ya da kağıt biçimi veya başlangıçta bildireceğinizi bir gereksinimi tooreview veri tutulan kayıtlar için olacaktır. Bu raporda veri sınıflandırması ve taşıma veri toohello bulut algıladığından, el ile yeniden sınıflandırma çaba olay temelinde dikkat gerektiren ve risk yönetimi İnceleme ideal tooaddress sınıflandırma gereksinimlerini olacaktır. Genellikle, böyle bir çaba sınıflandırılmış toobe gerekenler hakkında hello kuruluşun ilkesine göz önünde bulundurun, varsayılan sınıflandırma durumu (tüm verileri ve hassas ancak gizli olan dosyaları) hello ve yüksek riskli veri özel durumlarını uygulayın. 

### <a name="automatic-data-reclassification"></a>Otomatik veri Sınıflama
Otomatik veri Sınıflama hello aynı genel kural elle sınıflandırma kullanır. Merhaba otomatik çözümleri kurallarını izleyen ve gerektiğinde uygulanan sağlayabilirsiniz istisnadır. Veri sınıflandırması, verilerin Kullanımdaki ve yetkilendirme teknolojisini kullanarak Aktarımdaki depolandığında zorunlu tutulabilir olan bir veri Sınıflandırma zorlama İlkesi, bir parçası olarak yapılabilir.

* Uygulama tabanlı. Bazı uygulamalar varsayılan olarak kullanarak bir sınıflandırma düzeyini ayarlar. Örneğin, müşteri ilişkileri yönetimi (CRM) yazılımı, İK ve sistem durumu kayıt yönetimi araçları verilerini varsayılan olarak gizlidir. 
* Konum temelli. Veri konumu, veri duyarlılık tanımlamaya yardımcı olabilir. Örneğin, bir HR veya Finans departmanı tarafından depolanan veriler büyük olasılıkla toobe doğası gereği gizli olur.  

### <a name="data-retention-recovery-and-disposal"></a>Veri bekletme, kurtarma ve çıkarma
Veri kurtarma ve veri Sınıflama gibi elden veri varlıklarını yönetme önemli bir durum değil. Merhaba ilkeleri veri kurtarma ve elden için bir veri bekletme ilkesi tarafından tanımlanan ve hello aynı zorlanan veri Sınıflama; şekilde Bu tür bir çaba işbirliğine dayalı bir görev olarak hello koruyucusu ve yönetici rolleri tarafından gerçekleştirilen.  

Hata toohave veri bekletme ilkesi kurallar ve yasal bulgu gereksinimleri ile veri kaybı veya hata toocomply anlamına gelir. Açıkça tanımlanmış veri bekletme ilkesine sahip olmayan çoğu kuruluş toouse varsayılan "her şeyi tut" bekletme ilkesi eğilimlidir. Ancak, bu tür bir bekletme ilkesi bulut Hizmetleri senaryolarda ek risk vardır. 

Örneğin, (Merhaba veriler korunur için hello hizmet ödenen sürece) bulut hizmeti sağlayıcıları için bir veri Bekletme İlkesi "Merhaba süresi hello abonelik için olduğu gibi" düşünülebilir. Bu tür bir bekletme için ödeme sözleşmesi Kurumsal veya yasal bekletme ilkeleri adresi değil. Gizli veriler için bir ilke tanımlama veriler depolanır ve en iyi uygulamalar hakkında temel kaldırılan emin olabilirsiniz. Ayrıca, hangi verilerle ilgili anlaşılması atıldı, tooformalize arşivleme İlkesi oluşturulabilir ve ne zaman. 

Veri bekletme ilkesi gerekli hello ilgilenmelidir yasal düzenleme ve uyumluluk gereksinimleri, hem de şirket yasal tutma gereksinimleri. Sınıflandırılmış veri tutma süresi ve özel durumları zamandır depolanmış veriler için bir sağlayıcı ile ilgili sorular yol açabilirsiniz; Bu tür sorular için doğru bir şekilde Sınıflandırılmamış verileri daha yüksektir. 

> [!TIP]
> Azure veri bekletme ilkeleri vb. hello okuyarak hakkında daha fazla bilgi [Microsoft çevrimiçi Abonelik Sözleşmesi](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Gizli verileri koruma
Veri sınıflandırması sonra bulma ve yolları tooprotect gizli verileri uygulama hiçbir veri koruma dağıtım stratejisini ayrılmaz bir parçası olur. Gizli verileri korumak ek dikkat toohow veriler depolanır ve hello bulut olduğu gibi da geleneksel mimarilerindeki aktarılan gerektirir. 

Bu bölümde toohelp gizli olarak sınıflandırılmış verileri korumak zorlama çaba otomatikleştirebilirsiniz bazı teknolojiler hakkında temel bilgiler sağlar. 

Aşağıdaki şekil gösterir hello, bu teknolojiler şirket içi veya bulut tabanlı çözümlerle dağıtılabilir — veya onlara dağıtılan şirket içi bazıları ve bazı hello bulutta bir karma şekilde. (Şifreleme ve hak yönetimi gibi bazı teknolojiler de toouser aygıtları genişletir.)  

![Teknolojileri](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Hak Yönetimi yazılımı
Veri kaybını engellemek için bir hak yönetimi yazılımı çözümüdür. Bir kuruluştaki çıkış noktalarda bilgi toointerrupt hello akışını denemesi yaklaşımlardan farklı olarak, hak yönetimi yazılımı veri depolama teknolojileri içindeki derin düzeylerde çalışır. Belgeler şifrelenir ve kimin bunların şifrelerini çözmek üzerinde denetim bir dizin hizmeti gibi bir kimlik doğrulama denetimi çözümde tanımlanan erişim denetimlerini kullanır.  

> [!TIP]
> Merhaba bilgi koruma çözümü tooprotect veri farklı senaryolar olarak Azure Rights Management (Azure RMS) kullanabilirsiniz. Okuma [Azure Rights Management nedir?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) Azure Bu çözüm hakkında daha fazla bilgi için.
> 
> 

Hak Yönetimi yazılımı hello avantajlarından bazıları şunlardır: 

* Hassas bilgileri korunması. Kullanıcıların rights management özellikli uygulamalar kullanarak doğrudan verilerini koruyabilir. Başka adım gerekli değildir — belgeleri yazma, e-posta göndermek ve veri yayımlama tutarlı veri koruma deneyimi sunar. 
* Koruma hello verilerle dolaşır. Müşteriler tootheir verilere erişmek, bulutta hello olup olmadığını, var olan BT altyapısı veya hello kullanıcının masaüstü olanların denetim kalır. Kuruluşlar tooencrypt verilerini seçin ve tootheir iş gereksinimlerinize göre erişimi kısıtlayabilirsiniz. 
* Varsayılan bilgi koruma ilkeleri. Yöneticiler ve kullanıcılar "Şirket Gizli – Read Only" ve "İletmeyin." gibi çok sayıda yaygın iş senaryolar için standart ilkelerini kullanabilirsiniz Zengin bir kullanım hakları, okuma, kopyalama, yazdırma, kaydetme, düzenleme ve iletme tooallow esneklik özel kullanım hakları tanımlama gibi desteklenir. 

> [!TIP]
> Azure depolama biriminde bulunan verilere kullanarak koruyabilirsiniz [Azure depolama hizmeti şifrelemesi](../storage/storage-service-encryption.md) bekleyen veri için. Aynı zamanda [Azure Disk şifrelemesi](azure-security-disk-encryption.md) toohelp Azure sanal makineler için kullanılan sanal diskler üzerinde yer alan verilerini korur.
> 
> 

### <a name="encryption-gateways"></a>Şifreleme ağ geçitleri
Şifreleme ağ geçitleri kendi katmanları tooprovide şifreleme Hizmetleri'nde tüm erişim toocloud tabanlı veri yeniden yönlendirilmesine çalışır. Bu yaklaşım, sanal özel ağ (VPN) ile karıştırılmamalıdır. Şifreleme ağ geçitleri tasarlanmış tooprovide saydam olan katman toocloud tabanlı çözümler.   

Şifreleme ağ geçitleri yol toomanage ve gizli olarak Aktarım hello verileri ve aynı zamanda kalan verileri şifreleyerek sınıflandırılmış güvenli veri sağlar.  

Şifreleme ağ geçitleri hello kullanıcı aygıtları arasındaki veri akışını içine yerleştirilir ve uygulama verilerini tooprovide şifreleme/şifre çözme hizmetleri merkezlerinin. Bu çözümler, VPN gibi daha şirket içi çözümdür. Tasarlanmış tooprovide bir üçüncü taraf şifreleme anahtarları, yardımcı olan hello veri ve anahtar yönetimi sağlayıcısı ile yerleştirme hello riskini azaltmak denetime sahip oldukları. Bu tür çözümler, çok şifreleme gibi toowork sorunsuz ve şeffaf bir şekilde kullanıcılar ve hello hizmeti arasındaki tasarlanmıştır. 

> [!TIP]
> adanmış özel bağlantı hello Microsoft bulutunu şirket içi ağlarınız Azure ExpressRoute tooextend kullanabilirsiniz. Okuma [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md) bu özelliği hakkında daha fazla bilgi için. Başka seçenekler için şirket içi ağınız arasında bağlantı arası ve [Azure olan bir siteden siteye VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Veri kaybını önleme
Veri kaybı (bazen başvurulan tooas veri sızıntısını) önemli bir konudur ve kötü amaçlı ve yanlışlıkla Insider aracılığıyla dış veri kaybı önleme hello çoğu kuruluş için en önemli.  

Veri kaybı önleme (DLP) teknolojilerini çözümleri e-posta hizmetleri gibi gizli olarak sınıflandırılmış veri iletme sağlanmasına yardımcı olur. Kuruluşlar yararlanabilirsiniz toohelp var olan ürünler DLP özelliklerin veri kaybını önleme. Bu özellikler baştan ya da hello yazılım sağlayıcısı tarafından sağlanan bir şablon kullanarak kolayca oluşturulabilir ilkelerini kullanın.  

DLP teknolojileri anahtar sözcük eşleştirmeleri, sözlük eşleştirmeleri, normal ifade hesaplaması ve kuruluş DLP ilkeleri ihlal diğer içerik incelemelerini kullanarak toodetect içeriği derin içerik çözümlemesi gerçekleştirebilirsiniz. Örneğin, DLP veri türleri aşağıdaki hello hello kaybetmemek yardımcı olabilir: 

* Sosyal Güvenlik ve Ulusal Kimlik numaraları 
* Bankacılık bilgilerini 
* Kredi kartı numaraları  
* IP adresleri 

(Örneğin, bir kuruluşun tootransmit sosyal güvenlik numarası bilgileri tooa Bordro işlemci gerektiriyorsa) bazı DLP teknolojileri de hello özelliği toooverride hello DLP yapılandırmasını sağlar. Ayrıca, böylece bunlar bile değil iletilmesi hassas bilgiler toosend denemeden önce kullanıcılara bildirim gönderilip olası tooconfigure DLP olur. 

> [!TIP]
> belgelerinizi Office 365 DLP yetenekleri tooprotect kullanabilirsiniz. Okuma [Office 365 uyumluluk denetimleri: veri kaybını önleme](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) daha fazla bilgi için.
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure veri şifreleme en iyi uygulamalar](azure-security-data-encryption-best-practices.md)
* [En iyi güvenlik uygulamaları Azure kimlik yönetimi ve erişim denetimi](azure-security-identity-management-best-practices.md)
* [Azure Güvenlik Ekibi Blogu](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft Güvenlik Yanıt Merkezi](https://technet.microsoft.com/library/dn440717.aspx)

