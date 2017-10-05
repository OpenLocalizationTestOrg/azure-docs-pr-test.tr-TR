---
title: "Azure için veri sınıflandırma | Microsoft Docs"
description: "Bu makalede, veri sınıflandırması ile ilgili temel bilgileri bir giriş sağlar ve bilgi işlem ve Microsoft Azure kullanarak bulut bağlamında özellikle değerini vurgular"
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
ms.openlocfilehash: e5d8841c47f91b27131fcf5066bfd3805b5670f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="data-classification-for-azure"></a>Azure veri sınıflandırması
Bu makalede, veri sınıflandırması ile ilgili temel bilgileri bir giriş sağlar ve bilgi işlem ve Microsoft Azure kullanarak bulut bağlamında özellikle değerini vurgular. 

## <a name="data-classification-fundamentals"></a>Veri sınıflandırması temelleri
Bir kuruluştaki başarılı veri sınıflandırması, kuruluşunuzun gereksinimlerini geniş hakkında farkındalık ve veri varlıklarınız bulunduğu, kapsamlı olarak anlamayı gerektirir.  

Veri üç temel durumdan birinde bulunur: 

* Bekleyen 
* İşlemde 
* Aktarım sırasında 

Veri sınıflandırması için benzersiz teknik çözümler tüm üç durumdan gerektirir, ancak veri sınıflandırması uygulanan ilkeler her için aynı olması gerekir. REST işleminde hem de Aktarım sırasında gizli kalmasını gizli olarak sınıflandırılmış veri gerekir. 

Veriler de yapılandırılmış veya yapılandırılmamış olabilir. Tipik sınıflandırma işlemlerini veritabanları ve tablolar bulunan yapılandırılmış veriler için daha az karmaşık ve zaman alıcı belgeler, kaynak kodu ve e-posta gibi yapılandırılmamış veriler için olandan yönetin. 

> [!TIP]
> Azure işlevlerini ve veri şifrelemesi için en iyi uygulamalar hakkında daha fazla bilgi için okumaya devam [Azure veri şifreleme en iyi uygulamalar](azure-security-data-encryption-best-practices.md)
> 
> 

Genel olarak, kuruluşlar daha fazla olacaktır yapılandırılmış veri daha yapılandırılmamış veriler. Veri yapılandırılmış veya yapılandırılmamış olmasına bakılmaksızın, veri duyarlılık yönetmek için önemlidir. Düzgün şekilde uygulandığında, veri sınıflandırması, genel veya dağıtmak ücretsiz olarak kabul edilir veri varlıklarını daha büyük gözetim ile yönetilen varlıklar, hassas veya gizli verileri sağlamaya yardımcı olur. 

### <a name="controlling-access-to-data"></a>Veri erişimi denetleme
Kimlik doğrulama ve Yetkilendirme genellikle birbiriyle yanıltıcı olmaktadır ve rollerine yanlış. Gerçekte, aşağıdaki çizimde gösterildiği gibi oldukça farklı olabilir.  

![Veri erişim ve Denetim](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Kimlik Doğrulaması
Kimlik doğrulaması genellikle en az iki bölümden oluşur: bir kullanıcı ve bir parola gibi bir belirteç kullanıcı adı kimlik bilgisinin geçerli olduğunu onaylamak için tanımlamak için bir kullanıcı adı veya kullanıcı kimliği. İşlem kimliği doğrulanmış kullanıcının herhangi bir öğe veya hizmetleri için erişim sağlamaz; Bu, kullanıcının kim olduklarını söyleyin olduğunu doğrular.   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md) kimliğini doğrulamak ve kullanıcılara yetki vermek izin bulut tabanlı kimlik hizmetleri sağlar. 
> 
> 

### <a name="authorization"></a>Yetkilendirme
Yetkilendirme kimliği doğrulanmış bir kullanıcı bir uygulama, veri kümesi, veri dosyası veya başka bir nesne erişim olanağı sağlama işlemidir. Kimliği doğrulanmış kullanıcılar atama haklarını kullanmak için değiştirmek veya erişebilecekleri öğeleri silme veri sınıflandırması dikkat gerektirir. 

Dosyaları ve bilgileri erişmek için tek tek kullanıcıların ihtiyaçlarını doğrulamak için bir mekanizma birleşimi rol, güvenlik ilkesi ve risk ilkesine konuları temel başarılı kimlik doğrulaması gerektirir. Örneğin, belirli satır iş kolu (LOB) uygulamaları verilerden tüm çalışanlar tarafından erişilecek gerekmeyebilir ve yalnızca küçük bir alt çalışanların olasılıkla İnsan Kaynakları (HR) dosyalara erişimi gerekir. Ancak kuruluşlar denetlemek için kimin ne zaman ve nasıl olarak, kullanıcıların kimlik doğrulaması için geçerli bir sistem karşılanması gereken olarak, verilere erişebilir. 

> [!TIP]
> Microsoft Azure'da Azure rol tabanlı erişim denetimi (RBAC), kullanıcıların işlerini yapmak için gereksinim duyduğu erişim miktarını yalnızca vermek için yararlanan emin olun. Okuma [Azure Active Directory kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md) daha fazla bilgi için. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Rolleri ve sorumlulukları bulut
Riskleri yönetme bulut sağlayıcıları yardımcı olmakla birlikte, müşteriler, veri sınıflandırma yönetimi sağlamak zorunda ve zorlama düzgün uygun düzeyde bir veri yönetimi hizmetleri sağlamak için uygulanır.  

Veri sınıflandırması sorumlulukları göre hangi bulut hizmeti modeli, bulunduğundan aşağıdaki resimde gösterildiği gibi değişir. Üç birincil bulut hizmeti modeli olarak bir hizmet (Iaas), platform (PaaS) hizmet olarak yazılım (SaaS) hizmet olarak altyapı ' dir. Veri sınıflandırması mekanizmalar uygulaması bağımlılık ve bulut sağlayıcısı beklentilerini göre değişir. 

![Roller](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Verilerinizi sınıflandırmak için sorumlu olmasına rağmen bulut sağlayıcılarının nasıl güvenli ve bulut içinde depolanan müşteri verileri gizliliğini hakkında yazılı taahhüt olmalısınız.  

* **Iaas sağlayıcıları** sanal ortam veri sınıflandırma özelliklerinin ve müşteri uyumluluk gereksinimleri barındırabilecek sağlamak için gereksinimleri sınırlıdır. Yalnızca müşteri verilerini uyumluluk gereksinimlerini ele emin olmak ihtiyaç duydukları olduğundan Iaas sağlayıcıları daha küçük bir rol veri sınıflandırması özelliği yoktur. Ancak, sağlayıcıları hala sanal ortamlarını veri merkezlerine güvenliğini sağlama yanı sıra veri sınıflandırma gereksinimlerini karşılayacak emin olmalısınız.
* **PaaS sağlayıcıları** sorumlulukları karma, platform katmanlı bir yaklaşım sınıflandırma aracı için güvenlik sağlamak için kullanılabilir olduğundan. PaaS sağlayıcıları kimlik doğrulama ve yetkilendirme kuralları büyük olasılıkla bazı sorumlu olabilir ve güvenlik ve kendi uygulama katmanı için veri sınıflandırma özelliklerinin sağlamanız gerekir. Çok Iaas sağlayıcıları gibi PaaS sağlayıcıları kendi platform tüm ilgili veri sınıflandırma gereksinimleriyle uyumlu emin olmanız gerekir.
* **SaaS sağlayıcısı** sık bir yetkilendirme zinciri bir parçası olarak kabul edilir ve SaaS uygulamada depolanan veri sınıflandırma türüne göre denetlenebilir emin olmak gerekir. SaaS uygulamaları, LOB uygulamaları için ve bunların çok yapısı gerek tarafından kimlik doğrulaması ve yetkilendirme kullanılan ve depolanan veri bulunmasını sağlamak için kullanılabilir. 

## <a name="classification-process"></a>Sınıflandırma işlemi
Veri sınıflandırması gereksinimini anlamak ve uygulamak istediğiniz çoğu kuruluş bir temel güçlükle karşı karşıya kalıyor: başlamak nerede?

Veri sınıflandırması uygulamak için bir etkili ve basit yoludur planı, iş, denetimi kullanmak için listeden bir model hareket [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). Aşağıdaki şekil, başarıyla veri sınıflandırması Bu modelde uygulamak için gereken görevleri grafikleri.  

1. **PLAN**. Veri varlıklarını sınıflandırma program dağıtmak ve koruma profilleri geliştirmek için bir veri koruyucu tanımlayın. 
2. **YAPMAK**. Veri sınıflandırma ilkeleri varılan sonra program dağıtın ve zorlama teknolojileri için gizli verileri gerektiği gibi uygulayın.  
3. **DENETLEME**. Denetleyin ve kullanılan yöntemleri ve araçları sınıflandırma ilkeleri etkili bir şekilde ele alır emin olmak için raporlar doğrulayın. 
4. **ACT**. Veri erişimi ve gözden geçirme dosyaları ve değişiklikleri benimsemek için yeniden sınıflandırma ve düzeltme bir yöntemi kullanarak gözden geçirme gerektiren veri ve adres yeni riskler durumunu gözden geçirin.  

![Planlama, denetleme hareket,](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Gereksinimlerinize adresleri terminolojisi modelini seçin
El ile işlemleri, bir kullanıcının veya sistemin konumu, uygulama tabanlı işlemler veritabanına özel sınıflandırma gibi temel alır ve otomatik verileri sınıflandırmak konum temelli işlemleri dahil verileri sınıflandırmak için çeşitli işlemler var bazıları bu makalenin sonraki bölümlerinde "gizli verileri korumak" bölümünde açıklanan çeşitli teknolojiler tarafından kullanılan işlemleri.  

Bu makale iyi kullanılan ve endüstri dikkate modellerinde tabanlı iki genelleştirilmiş terminolojisi modeli sunar. Her ikisi de, üç düzeyde sınıflandırma duyarlılık sağlamak, bu terimleri modeller aşağıdaki tabloda gösterilmektedir.  

> [!NOTE]
> bir dosya veya genellikle farklı düzeylerde sınıflandırılmış verileri birleştirir kaynağa Sınıflandırma, sınıflandırma mevcut en yüksek düzeyde genel sınıflandırma oluşturmanız gerekir. Örneğin, hassas ve kısıtlı verileri içeren bir dosyayı sınıflandırılmalıdır olarak kısıtlı.  
> 
> 

| **Duyarlılık** | **1 terminolojisi modeli** | **Terminolojisi modeli 2** |
| --- | --- | --- |
| Yüksek |Gizli |Sınırlı |
| Orta |Yalnızca dahili kullanım |Hassas |
| Düşük |Genel |Sınırsız |

#### <a name="confidential-restricted"></a>Gizli (sınırlı)
Gizli veya kısıtlı olarak sınıflandırılan bilgi gizliliği ihlal edilmiş veya kayıp, bir veya daha fazla kişiler ve/veya kuruluşlar için geri dönülemez olabilir verileri içerir. Bu tür bilgiler sık "bilmeniz gereken" bir temelde sağlanır ve şunlar olabilir: 

* Sosyal Güvenlik veya Ulusal Kimlik numaraları, passport numaraları, kredi kartı numaraları, sürücünün lisans sayıları, tıbbi kaydeder ve sağlık sigortası ilkesi kimlik numaraları gibi kişisel bilgiler dahil olmak üzere kişisel veriler.  
* Denetimi gibi finansal hesap numarası veya yatırım hesap numaraları gibi finansal kaydeder. 
* Belgeler veya benzersiz veya belirli fikri mülkiyet veriler gibi iş malzemeler.  
* Olası avukata ayrıcalıklı malzeme gibi yasal veriler. 
* Özel şifreleme anahtarları, kullanıcı adı parola çiftleri veya biyometrik özel anahtar dosyaları gibi diğer kimlik sıraları dahil olmak üzere, kimlik doğrulama verileri. 

Gizli olarak sık sınıflandırılır verileri içeren yasal ve veri işleme için uyumluluk gereksinimleri. 

#### <a name="for-internal-use-only-sensitive"></a>Dahili kullanım yalnızca (hassas)
Orta duyarlılığını olacak şekilde sınıflandırılır bilgi dosyaları ve bir kişi ve/veya kuruluş üzerinde ciddi bir etkisi kaybolur veya yok olması gereken olmayan verileri içerir. Gibi bilgileri içerebilir: 

* E-posta, çoğunu silinmiş ya da (gizli sınıflandırmasında tanımlanan kişilerin posta kutuları veya e-posta hariç) kriz neden olmadan dağıtılmış.  
* Belgeler ve gizli verileri içermez dosyaları.

Genellikle, bu sınıflandırma, gizli olmayan bir şey içerir. Bu Sınıflandırma, yönetilen veya günlük kullanılan çoğu dosyaları gizli olarak sınıflandırılmış çünkü çoğu işletme verilerini dahil edebilirsiniz. Genel kullanıma açılmadan veya gizli verileri dışında bir iş kuruluş içindeki tüm veriler hassas olarak varsayılan olarak sınıflandırılabilir. 

#### <a name="public-unrestricted"></a>Public (sınırsız)
Genel olarak sınıflandırılır bilgi verileri ve iş gereksinimlerini veya işlemleri için kritik olmayan dosyaları içerir. Bu sınıflandırma da kasıtlı olarak genel pazarlama malzemeleri gibi bunların kullanılması için yayımlanan verileri dahil etmek veya Duyurular tuşuna basın. Ayrıca, bu sınıflandırma, bir e-posta hizmeti tarafından depolanan istenmeyen e-posta iletileri gibi verileri içerebilir. 

### <a name="define-data-ownership"></a>Veri sahipliği tanımlayın
Tüm veri varlıklarının sahipliğini temizleyin custodial zinciri oluşturmak önemlidir. Aşağıdaki tabloda, farklı veri sahipliği veri sınıflandırma çaba rollerinde ve ilgili haklarını tanımlar.  

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

**Veri varlık sahibi** temsilci sahipliği ve bir koruyucu atamak verilerin, özgün Oluşturucu. Bir dosya oluşturulduğunda, sahibi ne gizli olarak sınıflandırılmış gerekiyor, kuruluşun ilkelerine bağlı olarak anlamak için sorumluluk sahip oldukları anlamına gelir bir sınıflandırma atayabilirsiniz olmalıdır. Sahip veya gizli (sınırlı) veri türleri oluşturma sorumlu edilmedikleri sürece tüm veri varlık sahibinin verileri dahili kullanım yalnızca (duyarlı olduğu gibi) otomatik olarak sınıflandırılan olabilir. Genellikle, veri sınıflandırması sonra sahibin rol değiştirilir. Örneğin, sahibi bir sınıflandırılmış bilgileri bir veritabanı oluşturun ve veri koruyucu haklarını teknisyene.  

> [!NOTE]
> Veri varlık sahipleri genellikle Hizmetleri, aygıtları ve bazıları da kişisel ve bazıları da kuruluşa ait medya karışımını kullanın. Clear kuruluş ilkesi, dizüstü bilgisayarlar gibi ve akıllı aygıtlar kullanımını veri sınıflandırma yönergelerine uygun olduğundan emin olun yardımcı olabilir.  
> 
> 

**Veri varlık koruyucu** sözleşmeleri uygulanabilir ilke gereksinimlere uygun veya varlık sahibi ile göre varlık yönetmek için varlık sahibinin (veya kendi temsilci) atanır. İdeal olarak, otomatik bir sistemde koruyucu rol uygulanabilir. Bir varlık koruyucusu gerekli erişim denetimleri sağlanır ve yönetme ve bunların bakımı için temsilci varlıkların korunması sorumlu sağlar. Varlık koruyucu sorumluluklarını dahil olabilir:  

* Varlık sahibinin yönü uygun olarak ya da varlık sahibinin belirlendiği varlık koruma 
* Sınıflandırma ilkeleri ile uyum emin olma 
* Bildiren varlık sahipleri anlaşılan denetimleri ve/veya koruma yordamları etkisi alarak bu değişiklikleri önce herhangi bir değişiklik 
* Varlık sahibi değişiklikler veya varlık koruyucu'nın sorumlulukları kaldırılması hakkında raporlama 
* Bir **yönetici** bütünlüğü saklanır, ancak veri varlık sahibi, koruyucu veya kullanıcı olmadıkları sağlamak için sorumlu kullanıcıyı temsil eder. Aslında, çok sayıda yönetici rolleri, verilere erişimi gerek kalmadan veri kapsayıcısı Yönetim Hizmetleri sağlar. Yönetici rolü yedekleme ve geri yükleme varlıklar kayıtlarının bakımı ve seçme, alınırken ve depolama alanını ve cihazları bu ev işletim veri varlıkları içerir. 
* Varlık kullanıcı verileri veya bir dosyaya erişim izni olan herkes içerir. Erişim atama varlık koruyucu sahibi tarafından çoğunlukla temsilci.  

### <a name="implementation"></a>Uygulama
Yönetim değerlendirmeleri tüm sınıflandırma yöntemleri için geçerlidir. Bu noktalar kim ayrıntılarını eklemeniz ne, nerede, ne zaman ve neden bir veri varlığına kullanılan, erişilen, değiştirilen veya silinen. Tüm varlık yönetimi nasıl bir kuruluş kendi riskleri görünümleri ile ilgili bir anlama yapılması gerekir, ancak basit bir yöntemi veri sınıflandırması işleminde tanımlanan uygulanabilir. Veri sınıflandırması için ek hususlar yeni uygulamaları ve araçları ve sınıflandırma yöntemi uygulandıktan sonra değişikliği yönetme giriş içerir.  

### <a name="reclassification"></a>Sınıflama
Yeniden sınıflama veya bir veri varlığına sınıflandırma durumunu değiştirme bir kullanıcı veya sistem veri varlığın önem veya riski profili değişti belirlediğinde yapılmalıdır. Bu çalışmaların sınıflandırma durumu ve geçerli olmaya devam sağlamak için önemlidir. El ile sınıflandırılmaz çoğu içerik otomatik olarak sınıflandırılmış veya bir veri koruyucu veya veri sahibi tarafından kullanıma dayalı. 

### <a name="manual-data-reclassification"></a>El ile veri Sınıflama
İdeal olarak, bu çalışmaların bir değişiklik ayrıntılarını yakalanan ve denetlenen olduğundan emin olun. El ile yeniden sınıflandırma en olası nedeni duyarlılık nedenlerinden ya da kağıt biçimi veya başlangıçta bildireceğinizi verileri gözden geçirmek için bir gereksinim tutulan kayıtlar için olacaktır. Bu raporda veri sınıflandırması ve bulut için veri taşımayı algıladığından, el ile yeniden sınıflandırma çaba olay temelinde dikkat gerektiren ve risk yönetimi İnceleme adresi sınıflandırma gereksinimlerine en uygun olacaktır. Genellikle, bu tür bir çaba olması gerekenler hakkında kuruluşun ilkesine göz önünde bulundurun sınıflandırılmış, varsayılan sınıflandırma durumu (tüm verileri ve hassas ancak gizli olan dosyaları) ve yüksek riskli veri özel durumlarını uygulayın. 

### <a name="automatic-data-reclassification"></a>Otomatik veri Sınıflama
Otomatik veri Sınıflama aynı genel kural elle sınıflandırma kullanır. Otomatik çözümleri kurallarını izleyen ve gerektiğinde uygulanan sağlayabilirsiniz istisnadır. Veri sınıflandırması, verilerin Kullanımdaki ve yetkilendirme teknolojisini kullanarak Aktarımdaki depolandığında zorunlu tutulabilir olan bir veri Sınıflandırma zorlama İlkesi, bir parçası olarak yapılabilir.

* Uygulama tabanlı. Bazı uygulamalar varsayılan olarak kullanarak bir sınıflandırma düzeyini ayarlar. Örneğin, müşteri ilişkileri yönetimi (CRM) yazılımı, İK ve sistem durumu kayıt yönetimi araçları verilerini varsayılan olarak gizlidir. 
* Konum temelli. Veri konumu, veri duyarlılık tanımlamaya yardımcı olabilir. Örneğin, bir HR veya Finans departmanı tarafından depolanan verileri doğası gereği gizli olması olasılığı daha yüksektir.  

### <a name="data-retention-recovery-and-disposal"></a>Veri bekletme, kurtarma ve çıkarma
Veri kurtarma ve veri Sınıflama gibi elden veri varlıklarını yönetme önemli bir durum değil. Veri kurtarma ve elden ilkeleri veri bekletme ilkesi tarafından tanımlanan ve verileri yeniden sınıflandırma aynı şekilde zorlanan; Böyle bir çaba işbirliğine dayalı bir görev olarak koruyucusu ve yönetici rolleri tarafından gerçekleştirilmesi.  

Veri bekletme ilkesine sahip olması için hata, veri kaybı veya kurallar ve yasal bulma gereksinimlerine uymak için hata anlamına gelebilir. Açıkça tanımlanmış veri bekletme ilkesine sahip olmayan çoğu kuruluş, varsayılan "her şeyi tut" bir bekletme ilkesi kullanır eğilimindedir. Ancak, bu tür bir bekletme ilkesi bulut Hizmetleri senaryolarda ek risk vardır. 

Örneğin, (veriler korunur için hizmet ödenen sürece) bulut hizmeti sağlayıcıları için bir veri Bekletme İlkesi "süresi boyunca abonelik için olduğu gibi" düşünülebilir. Bu tür bir bekletme için ödeme sözleşmesi Kurumsal veya yasal bekletme ilkeleri adresi değil. Gizli veriler için bir ilke tanımlama veriler depolanır ve en iyi uygulamalar hakkında temel kaldırılan emin olabilirsiniz. Ayrıca, arşivleme İlkesi, hangi verilerin atıldı hakkında anlayarak resmileştirin için oluşturulabilir ve ne zaman. 

Veri bekletme ilkesi gerekli adres yasal düzenleme ve uyumluluk gereksinimleri, hem de şirket yasal tutma gereksinimleri. Sınıflandırılmış veri tutma süresi ve özel durumları zamandır depolanmış veriler için bir sağlayıcı ile ilgili sorular yol açabilirsiniz; Bu tür sorular için doğru bir şekilde Sınıflandırılmamış verileri daha yüksektir. 

> [!TIP]
> Azure veri bekletme ilkeleri vb. okuyarak hakkında daha fazla bilgi [Microsoft çevrimiçi Abonelik Sözleşmesi](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Gizli verileri koruma
Veri sınıflandırması sonra bulma ve gizli verileri koruma yolları uygulama hiçbir veri koruma dağıtım stratejisini ayrılmaz bir parçası olur. Gizli verileri korumak veriler nasıl depolanır ve bulut olduğu gibi da geleneksel mimarilerindeki aktarılan için ek ilgilenilmesi gerekiyor. 

Bu bölümde, gizli olarak sınıflandırılmış verilerin korunmasına yardımcı olmak üzere zorlama çabalarına otomatikleştirebilirsiniz bazı teknolojiler hakkında temel bilgiler sağlar. 

Aşağıdaki şekilde gösterildiği gibi bu teknolojiler şirket içi veya bulut tabanlı çözümlerle dağıtılabilir — veya onlara dağıtılan şirket içi bazıları ve bazı bulutta bir karma şekilde. (Şifreleme ve hak yönetimi gibi bazı teknolojiler de kullanıcı aygıtları için genişletir.)  

![Teknolojileri](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Hak Yönetimi yazılımı
Veri kaybını engellemek için bir hak yönetimi yazılımı çözümüdür. Bir kuruluştaki çıkış noktalarda bilgi akışını kesintiye girişimi yaklaşımlardan farklı olarak, hak yönetimi yazılımı veri depolama teknolojileri içindeki derin düzeylerde çalışır. Belgeler şifrelenir ve kimin bunların şifrelerini çözmek üzerinde denetim bir dizin hizmeti gibi bir kimlik doğrulama denetimi çözümde tanımlanan erişim denetimlerini kullanır.  

> [!TIP]
> farklı senaryolar verileri korumak için bilgi koruma çözümü Azure Rights Management (Azure RMS) kullanabilirsiniz. Okuma [Azure Rights Management nedir?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) Azure Bu çözüm hakkında daha fazla bilgi için.
> 
> 

Rights management yazılım avantajlarından bazıları şunlardır: 

* Hassas bilgileri korunması. Kullanıcıların rights management özellikli uygulamalar kullanarak doğrudan verilerini koruyabilir. Başka adım gerekli değildir — belgeleri yazma, e-posta göndermek ve veri yayımlama tutarlı veri koruma deneyimi sunar. 
* Koruma verilerle dolaşır. Müşteriler kimin verilerini, bulutta olup olmadığını, var olan BT altyapısı veya kullanıcının masaüstü erişimi denetim kalır. Kuruluşlar, verileri şifrelemek ve iş gereksinimlerine göre erişimi kısıtlamak seçebilirsiniz. 
* Varsayılan bilgi koruma ilkeleri. Yöneticiler ve kullanıcılar "Şirket Gizli – Read Only" ve "İletmeyin." gibi çok sayıda yaygın iş senaryolar için standart ilkelerini kullanabilirsiniz Kullanım hakları gibi okuma, desteklenen kopyalama, yazdırma, kaydetme, düzenleme ve iletme özel kullanım hakları tanımlama esneklik izin vermek için zengin bir dizi. 

> [!TIP]
> Azure depolama biriminde bulunan verilere kullanarak koruyabilirsiniz [Azure depolama hizmeti şifrelemesi](../storage/storage-service-encryption.md) bekleyen veri için. Aynı zamanda [Azure Disk şifrelemesi](azure-security-disk-encryption.md) Azure sanal makineler için kullanılan sanal diskler üzerinde yer alan verileri koruyabilirsiniz.
> 
> 

### <a name="encryption-gateways"></a>Şifreleme ağ geçitleri
Tüm bulut tabanlı veri erişimi yeniden yönlendirilmesine şifreleme hizmetleri sağlamak için kendi katmanlarında şifreleme ağ geçitleri çalışır. Bu yaklaşım, sanal özel ağ (VPN) ile karıştırılmamalıdır. Şifreleme ağ geçitleri, bulut tabanlı çözümlerle saydam bir katmana sağlamak üzere tasarlanmıştır.   

Şifreleme ağ geçitleri yönetmek için anlamına gelir ve gizli olarak Aktarımdaki verileri ve aynı zamanda kalan verileri şifreleyerek sınıflandırılmış güvenli veri sağlar.  

Şifreleme ağ geçitleri, şifreleme/şifre çözme hizmetleri sağlamak üzere merkezi kullanıcı aygıtları ve uygulama verilerini arasındaki veri akışını içine yerleştirilir. Bu çözümler, VPN gibi daha şirket içi çözümdür. Bir üçüncü taraf şifreleme anahtarları, yardımcı olan bir sağlayıcı ile hem veri hem de anahtar yönetimi yerleştirme riskini azaltmak üzerinde denetim sağlamak için tasarlanmıştır. Bu tür çözümler, sorunsuz bir şekilde çalışması için çok şifreleme gibi ve kullanıcılar ve hizmet arasındaki saydam olarak tasarlanmıştır. 

> [!TIP]
> Şirket içi ağlarınızı Microsoft bulutuna adanmış özel bağlantı genişletmek için Azure ExpressRoute kullanabilirsiniz. Okuma [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md) bu özelliği hakkında daha fazla bilgi için. Başka seçenekler için şirket içi ağınız arasında bağlantı arası ve [Azure olan bir siteden siteye VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Veri kaybını önleme
Veri kaybı (bazen veri sızıntısını adlandırılır) önemli bir konudur ve kötü amaçlı ve yanlışlıkla Insider aracılığıyla dış veri kaybı önleme çoğu kuruluş için en önemli.  

Veri kaybı önleme (DLP) teknolojilerini çözümleri e-posta hizmetleri gibi gizli olarak sınıflandırılmış veri iletme sağlanmasına yardımcı olur. Kuruluşlar DLP özelliklerin veri kaybını önlemeye yardımcı olmak için mevcut ürünlerinde yararlanabilir. Bu özellikler baştan ya da yazılım sağlayıcısı tarafından sağlanan bir şablon kullanarak kolayca oluşturulabilir ilkelerini kullanın.  

DLP teknolojileri anahtar sözcük eşleştirmeleri, sözlük eşleştirmeleri, normal ifade hesaplaması ve diğer içerik incelemelerini kullanarak kuruluş DLP ilkeleri ihlal içerik algılamak için derin içerik çözümlemesi gerçekleştirebilirsiniz. Örneğin, DLP aşağıdaki veri türlerini kaybını önlemeye yardımcı olabilir: 

* Sosyal Güvenlik ve Ulusal Kimlik numaraları 
* Bankacılık bilgilerini 
* Kredi kartı numaraları  
* IP adresleri 

Bazı DLP teknolojileri de (örneğin, bir kuruluşun bir bordro işlemciye sosyal güvenlik numarası bilgi iletimi gerekiyorsa) DLP yapılandırmasını geçersiz kılma olanağı sağlar. Ayrıca, böylece bunlar bile değil iletilmesi hassas bilgiler göndermeyi denemeden önce kullanıcılara bildirim gönderilip DLP yapılandırmak mümkündür. 

> [!TIP]
> Belgelerinizi korumak için Office 365 DLP özelliklerini kullanabilirsiniz. Okuma [Office 365 uyumluluk denetimleri: veri kaybını önleme](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) daha fazla bilgi için.
> 
> 

## <a name="see-also"></a>Ayrıca bkz.
* [Azure veri şifreleme en iyi uygulamalar](azure-security-data-encryption-best-practices.md)
* [En iyi güvenlik uygulamaları Azure kimlik yönetimi ve erişim denetimi](azure-security-identity-management-best-practices.md)
* [Azure Güvenlik Ekibi Blogu](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft Güvenlik Yanıt Merkezi](https://technet.microsoft.com/library/dn440717.aspx)

