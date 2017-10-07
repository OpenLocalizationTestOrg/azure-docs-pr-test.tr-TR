---
title: "tooAzure taşıma kuruluşlar için aaaBest uygulamaları | Microsoft Docs"
description: "Kuruluşların tooensure güvenli ve yönetilebilir bir ortam kullanabilirsiniz iskele açıklar."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: 8692f37e-4d33-4100-b472-a8da37ce628f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: d1402cf21d0cf740e44c03fc345ecd39a6e1680c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-enterprise-scaffold---prescriptive-subscription-governance"></a>Azure enterprise iskele - Düzenleyici abonelik yönetimi
Kuruluşların giderek daha fazla esneklik ve Çeviklik için genel bulut hello geliştirilmektedir. Bunlar hello bulutun gücü toogenerate gelir kullanılarak veya kaynakları hello iş için en iyi duruma getirme. Microsoft Azure, işletmelerin çok çeşitli iş yükleri ve uygulamalar gibi yapı taşlarını tooaddress toplayabilir birçok sağlar. 

Ancak, toobegin genellikle zor olduğu bilerek. Toouse Azure karar verildikten sonra birkaç sorular yaygın olarak ortaya:

* "Nasıl ı bizim yasal veri egemenliği bazı ülkelerde gereksinimlerini?"
* "Nasıl ı birisi yanlışlıkla bir kritik sistem değiştirmemesini emin olursunuz?"
* "Nasıl ı hesap ve fatura geri doğru şekilde ne her kaynak destekliyor anlarım?"

hiçbir koruma rayları ile boş bir aboneliğin Hello aday zorlu olur. Bu boş alanı taşıma tooAzure engel olabilir.

Bu makalede, idare ve hello ile ihtiyaç Çeviklik için dengelemek için teknik uzmanları tooaddress hello gereksinimi için bir başlangıç noktası sağlar. Uygulama ve bunların Azure Aboneliklerini Yönetme kuruluşlar kılavuzları bir kurumsal iskele hello kavramını sunmaktadır. 

## <a name="need-for-governance"></a>İdare gereksinimini
TooAzure taşırken hello konu kullanımını idare erken tooensure hello başarılı hello bulut hello kuruluş içinde incelemeniz gerekir. Ne yazık ki, başlangıç saati ve kapsamlı idare sistem oluşturma geçmişi gelir doğrudan bazı iş grupları kurumsal BT karıştırılmaksızın toovendors gidin. Merhaba kaynakları düzgün yönetilmeyen varsa bu yaklaşımı hello Kurumsal açık toovulnerabilities bırakabilirsiniz. Merhaba genel bulut - çeviklik, esneklik ve tüketim tabanlı fiyatlandırma - Hello özelliklerini tooquickly gerek toobusiness grupları müşteriler (iç ve dış) hello isteklerini karşılamak önemlidir. Ancak, kurumsal BT veriler ve sistemlerle etkili bir şekilde korunmasını tooensure gerekiyor.

Gerçek Hayatta yapı iskelesi kullanılan toocreate hello hello yapısının temelini oluşturur. Merhaba iskele hello genel anahattı size rehberlik eder ve bağlantı noktaları için daha fazla kalıcı sistemleri toobe takılı sağlar. Bir kuruluş iskele aynı hello olduğu: esnek denetimler ve yapısı toohello ortamı ve bağlayıcılarını hello genel bulut üzerinde oluşturulmuş hizmetleri sağlamak Azure özellikleri kümesi. Merhaba oluşturucular sağlar (BT ve iş grupları) foundation toocreate ve yeni hizmetler ekleyebilirsiniz.

Merhaba iskele birçok katılımlar çeşitli boyutlarda istemcilerle toplanan olduğu yöntemler temel alır. Bu küçük kuruluşlar hello bulut tooFortune 500 kuruluşlar ve geçirme ve hello bulutta çözümleri geliştirme bağımsız yazılım satıcıları çözümleri geliştirme istemcileri arasındadır. Merhaba Kurumsal katman kalıbı iskeleti olup "amaca" toobe esnek toosupport geleneksel BT iş yüklerini ve Çevik iş yükleri; gibi geliştiricilerin yazılım olarak-hizmet (SaaS) uygulamaları oluşturma Azure yeteneklerini temel.

Merhaba Kurumsal iskele hedeflenen toobe hello Azure içinde her yeni abonelik temelini oluşturur. Yöneticiler tooensure iş yüklerini karşılayan hello minimum idare gereksinimleri, bir kuruluşun iş grupları ve geliştiricilerin kendi hedefleri hızlı bir şekilde toplantı önleme olmadan sağlar.

> [!IMPORTANT]
> İdare Azure önemli toohello başarılı olur. Bu makale hedefleri Kurumsal iskele teknik uyarlamasını hello ancak yalnızca hello daha geniş işlem ve hello bileşenleri arasındaki ilişkileri dokunur. İlke idare hello üstten aşağı akar ve hangi hello tarafından iş tooachieve istediği belirlenir. Doğal olarak, Azure için idare modelinin hello oluşturma temsilcileri içerir BT, ancak daha da önemlisi, iş grubu kılavuzları ve güvenliği ve risk yönetimi güçlü gösteriminden olması gerekir. Merhaba sonunda, bir kuruluş iskele iş risk toofacilitate kuruluşun görev ve hedeflerini azaltılmasıyla ilgilidir.
> 
> 

Görüntü aşağıdaki hello hello iskele hello bileşenlerini açıklar. Departmanlar, hesaplar ve abonelikler için sağlam bir planı Hello foundation kullanır. Merhaba ayaklar Resource Manager ilkeleri ve güçlü adlandırma standartları oluşur. Merhaba iskele Hello kalan çekirdek Azure özellikleri gelir ve bu etkinleştir güvenli ve yönetilebilir bir ortam özellikleri.

![iskele bileşenleri](./media/resource-manager-subscription-governance/components.png)

> [!NOTE]
> Azure hızlı bir şekilde kendi giriş 2008'de bu yana haline geldi. Bu büyüme, hizmetleri dağıtma ve yönetme için kendi yaklaşımı toorethink Microsoft mühendislik ekipleri gereklidir. Hello Azure Resource Manager modeli 2014'te kullanıma sunulmuştur ve hello Klasik dağıtım modeli değiştirir. Resource Manager toomore kolayca dağıtma, düzenleme ve Azure kaynaklarını denetleyen kuruluşlar sağlar. Kaynak Yöneticisi, karmaşık, birbirine çözümlerinin hızlı dağıtımı için kaynakları oluştururken paralelleştirme içerir. Ayrıntılı erişim denetimi ve hello özelliği tootag meta veri kaynaklarıyla de içerir. Microsoft, tüm kaynaklara hello Resource Manager modeli aracılığıyla oluşturduğunuz önerir. Merhaba Kurumsal iskele açıkça hello Resource Manager modeli için tasarlanmıştır.
> 
> 

## <a name="define-your-hierarchy"></a>Hiyerarşinizi tanımlayın
Merhaba hello iskele hello Azure işletme kaydı (ve hello Enterprise Portal) temelini oluşturur. Merhaba Kurumsal kayıt hello şekil tanımlar ve şirket içindeki Azure Hizmetleri kullanın ve hello çekirdek idare yapısıdır. Merhaba Kurumsal Anlaşma içinde müşteriler sorgulayabilmesi toofurther hello ortamına Departmanlar, hesapları ve son olarak, abonelikleri ayırabilir. Bir Azure aboneliği, tüm kaynakların bulunduğu hello temel birimidir. Ayrıca, Azure, çekirdek, kaynaklar, vb. sayısı gibi birkaç sınırlarda tanımlar.

![Hiyerarşisi](./media/resource-manager-subscription-governance/agreement.png)

Her Kuruluş farklıdır ve hello hiyerarşi hello önceki görüntüde Azure hello şirket içinde nasıl düzenlendiğini önemli esneklik sağlar. Bu belgede yer alan hello yönergeleri uygulamadan önce hiyerarşinizdeki model ve faturalama, kaynak erişimi ve karmaşıklık hello etkisini anlamak gerekir.

Azure kayıtları için üç ortak desenler Hello şunlardır:

* Merhaba **işlevsel** düzeni
  
    ![işlev](./media/resource-manager-subscription-governance/functional.png)
* Merhaba **departman** düzeni 
  
    ![başlar](./media/resource-manager-subscription-governance/business.png)
* Merhaba **coğrafi** düzeni
  
    ![coğrafi](./media/resource-manager-subscription-governance/geographic.png)

Merhaba iskele hello abonelik düzeyi tooextend hello idare gereksinimleri hello Enterprise hello aboneliğe sırasında uygulanır.

## <a name="naming-standards"></a>Adlandırma standartları
Merhaba iskele, ilk sütun Hello adlandırma standartlarının. İyi tasarlanmış adlandırma standartları hello portal, bir fatura ve komut dosyaları içinde tooidentify kaynaklarında etkinleştirin. Büyük olasılıkla, şirket içi altyapı için adlandırma standartlarının zaten vardır. Azure tooyour ortam eklerken, bu Azure kaynaklarını standartları tooyour adlandırma genişletmelidir. Adlandırma standardı, tüm düzeylerdeki hello ortamının daha verimli yönetimini kolaylaştırmak.

> [!TIP]
> Adlandırma kuralları için:
> * Gözden geçirin ve mümkün olduğunda benimsemeye hello [desenleri ve uygulamalar kılavuzunu](../guidance/guidance-naming-conventions.md). Bu kılavuz üzerinde anlamlı bir adlandırma standart bir karar vermenize yardımcı olur.
> * (Örneğin, contoso.com ve vnetNetworkName) kaynakların adları için camelCasing kullanın. Not: Vardır depolama hesapları gibi kaynaklara hello tek seçenek toouse küçük (ve diğer özel karakterler) olduğu.
> * Azure Resource Manager (Merhaba sonraki bölümde açıklanmıştır) İlkeleri tooenforce adlandırma standartlarının kullanmayı düşünün.
> 
> Merhaba önceki ipuçları tutarlı bir adlandırma kuralı uygulamanıza yardımcı olur.

## <a name="policies-and-auditing"></a>İlkeleri ve Denetim
Merhaba iskele, ikinci sütun Hello içerir oluşturma [Azure Resource Manager ilkeleri](resource-manager-policy.md) ve [hello etkinlik günlüğü denetleme](resource-group-audit.md). Kaynak Yöneticisi ilkeleri azure'da hello özelliği toomanage risk sağlar. Veri egemenliği kısıtlama zorlamayı veya belirli eylemleri denetim olun ilkeleri tanımlayabilirsiniz. 

* Varsayılan bir ilkedir **izin** sistem. Tanımlama ve reddetme veya Eylemler kaynaklar üzerinde denetim ilkeleri tooresources atayarak Eylemler denetler.
* İlke tanım dili (IF then koşulları) ilkesi tanımlarında tarafından ilkeleri açıklanmaktadır.
* Oluşturduğunuz JSON (Javascript nesne gösterimi) ile biçimlendirilmiş dosyalar ilkeleri. Bir ilke tanımladıktan sonra onu tooa belirli kapsamı atayın: Abonelik, kaynak grubu veya kaynak.

İlkeleri hassas bir yaklaşım tooyour senaryoları için birden çok eylem vardır. Merhaba eylemler şunlardır:

* **Reddetme**: blokları hello kaynak isteği
* **Denetim**: hello isteği ancak ekler (kullanılan tooprovide uyarıları veya olabilen tootrigger runbook'ları) satır toohello etkinlik günlüğü sağlar
* **Append**: ekler bilgi toohello kaynak belirtildi. Örneğin, bir kaynakta "CostCenter" etiketi değilse, varsayılan bir değerle bu etiketi ekleyin.

### <a name="common-uses-of-resource-manager-policies"></a>Resource Manager İlkeleri'nın yaygın kullanımları
Azure Resource Manager hello Azure Araç Seti güçlü bir araç ilkelerdir. Tooavoid etkinleştirmek beklenmeyen maliyetler, tooidentify bir maliyet merkezi etiketleme ve tooensure aracılığıyla kaynaklar için gereksinimleri karşılandıktan o uyumluluk. İlkeleri hello yerleşik denetim özellikleri ile birleştirildiğinde, karmaşık ve esnek çözümleri deneyerek. İlkeleri şirketler "Geleneksel BT" iş yükleri ve "Çevik" iş yükleri için tooprovide denetimleri sağlar; gibi müşteri uygulamaları geliştirme. Biz ilkeleri için bkz: hello en yaygın modeli şunlardır:

* **Coğrafi-uyumluluk/veri egemenliği** -Azure bölgeleri Merhaba dünya genelindeki sağlar. Kuruluşların (tooensure veri egemenliği veya yalnızca tooensure Kaynakları Kapat toohello son hello kaynakların tüketicileriyle oluşturulup oluşturulmayacağını) kaynakları oluşturulduğu toocontrol genellikle istiyor.
* **Yönetim maliyeti** -bir Azure aboneliği birçok türleri ve ölçek kaynakları içerebilir. Şirketler genellikle o standart tooensure istediğiniz abonelikleri kaçının dolar ayda bir veya daha fazla yüzlerce maliyet düşükse kaynakları kullanarak.
* **Varsayılan idare gerekli etiketleri aracılığıyla** -etiketleri gerektirmektir hello en yaygın ve yüksek oranda istenen özelliklerden biri. Azure Resource Manager ilkelerini kullanarak kuruluşların bir kaynağa uygun şekilde etiketli mümkün tooensure var. Merhaba en yaygın etiketleridir: departmanı, kaynak sahibi ve ortam türünü (örneğin - üretim, test, geliştirme)

**Örnekler**

"Geleneksel BT" abonelik satırı iş kolu uygulamaları için

* Departman zorlamak ve tüm kaynaklara sahip etiketleri
* Kaynak oluşturma toohello Kuzey Amerika bölge kısıtla
* Merhaba özelliği toocreate G-serisi VM'ler ve Hdınsight kümeleri kısıtlama

Bir iş biriminin bulut uygulamaları oluşturmak için "Çevik" ortamı

* toomeet veri egemenliği gereksinimleri, kaynakları hello oluşturulmasına izin yalnızca belirli bir bölgedeki.
* Ortam etiketi tüm kaynaklar hakkında zorlar. Bir etiketi olmayan bir kaynak oluşturduysanız, hello sona **ortam: Bilinmeyen** toohello kaynak etiketi.
* Denetim kaynakları Kuzey Amerika dışında oluşturulur ancak engel olmaz.
* Yüksek maliyetli kaynakları oluşturulduğunda denetim.

> [!TIP]
> Merhaba Resource Manager ilkeleri kuruluşlar arasında en yaygın kullanımı olan toocontrol *nerede* kaynakları oluşturulabilir ve *ne* kaynak türleri oluşturulabilir. Tooproviding ayrıca denetimlerini *nerede* ve *ne*, birçok kuruluşların kullanım ilkeleri tooensure kaynaklar hello uygun meta verileri toobill tüketimi için geri sahiptir. Merhaba abonelik düzeyinde ilkeleri uygulayarak öneririz:
> 
> * Coğrafi-uyumluluk/veri egemenliği
> * Maliyet yönetimi
> * Gerekli etiketleri (Determined BillTo, uygulama sahibi gibi iş gereksinimleri tarafından)
> 
> Kapsam daha düşük düzeylerdeki ek ilkeler uygulayabilirsiniz.
> 
> 

### <a name="audit---what-happened"></a>Denetim - ne oldu?
ortamınızı nasıl çalıştığını tooview tooaudit kullanıcı etkinliği gerekir. Çoğu kaynak türleri Azure içinde bir günlük araçla veya Azure Operations Management Suite çözümleyebilirsiniz tanılama günlüklerini oluşturun. Birden çok abonelik tooprovide bir departman genelinde etkinlik günlükleri veya Kurumsal görünümünde toplayabilirsiniz. Önemli bir tanılama aracı ve hello Azure ortamı önemli mekanizması tootrigger olaylarında denetim kayıtları için uygulanır.

Resource Manager dağıtımları etkinlik günlükleri toodetermine hello etkinleştirmek **operations** yerinde ve bunları gerçekleştiren sürdü. Etkinlik günlükleri toplanabilir ve günlük analizi gibi araçları kullanarak bir araya getirilir.

## <a name="resource-tags"></a>Kaynak etiketleri
Kuruluşunuzdaki kullanıcılar kaynakları toohello abonelik ekledikçe giderek önemli tooassociate kaynaklarla hello uygun departmanı, müşteri ve ortam haline gelir. Meta veri tooresources aracılığıyla iliştirebilirsiniz [etiketleri](resource-group-using-tags.md). Merhaba kaynak veya hello sahibi hakkında etiketleri tooprovide bilgileri kullanın. Etiketleri toonot yalnızca toplama ve Grup kaynaklarının çeşitli şekillerde etkinleştirmek, ancak geri ödeme hello amaçları doğrultusunda bu verileri kullanın. Too15 anahtar: değer çiftleri ile kaynakları etiketleyebilirsiniz. 

Kaynak etiketleri esnektir ve ekli toomost kaynakları olmalıdır. Ortak kaynak etiketleri örnekleri şunlardır:

* BillTo
* Departman (veya iş birimi)
* Ortam (üretim, aşama, geliştirme)
* Katman (Web katmanı, uygulama katmanı)
* Uygulama sahibi
* ProjectName

![etiketler](./media/resource-manager-subscription-governance/resource-group-tagging.png)

Daha fazla etiket örnekleri için bkz: [Azure kaynakları için adlandırma kurallarını önerilen](../guidance/guidance-naming-conventions.md).

> [!TIP]
> İçin etiketleme olması zorunlu tutulmuştur ilkesinde yapmadan göz önünde bulundurun:
> 
> * Kaynak grupları
> * Depolama
> * Virtual Machines
> * Uygulama hizmeti ortamları/web sunucuları
> 
> Bu etiketleme stratejisi, hangi meta veri hello iş, Finans, güvenlik, risk yönetimi ve hello ortamının genel yönetimini gereklidir aboneliklerinizi tanımlar. 

## <a name="resource-group"></a>Kaynak grubu
Resource Manager yönetim, faturalama veya doğal benzeşimi anlamlı gruplar halinde tooput kaynaklar sağlar. Daha önce belirtildiği gibi Azure iki dağıtım modeline sahiptir. Hello hello abonelik was önceki Klasik modeli, hello temel yönetim birimidir. Abonelikleri çok sayıda toohello oluşturulmasına neden bir abonelik içindeki kaynaklara aşağı zor toobreak oluştu. Merhaba Resource Manager modeli ile kaynak gruplarının hello giriş gördük. Kaynak grupları, ortak bir yaşam döngüsü veya "tüm SQL sunucuları" gibi bir özniteliği paylaşan kaynakları kapsayıcılar olan ya da "Uygulama A".

Kaynak grupları diğer içinde yer alamaz ve kaynakları yalnızca tooone kaynak grubuna ait olabilir. Bir kaynak grubundaki tüm kaynaklar üzerinde belirli eylemleri uygulayabilirsiniz. Örneğin, bir kaynak grubunu silme hello kaynak grubu içindeki tüm kaynakların kaldırır. Genellikle, tüm uygulama veya ilgili sistem hello yerleştirdiğiniz aynı kaynak grubu. Örneğin, Contoso Web uygulaması adlı üç katmanı uygulaması hello web sunucusu, uygulama sunucusu ve SQL Server'da hello içerecektir aynı kaynak grubu.

> [!TIP]
> Kaynak gruplarınızı düzenleme nasıl "Geleneksel BT" iş yüklerini çok değişebilir "Çevik BT" iş yükleri:
> 
> * "Geleneksel BT" iş yükleri en yaygın olarak hello içinde öğelerine göre gruplandırılır aynı yaşam döngüsü, bir uygulama gibi. Tek tek uygulama yönetimi için uygulama tarafından gruplandırma sağlar.
> * "Çevik BT" iş yüklerini eğilimindedir toofocus dış müşterilerle bulut uygulamaları. Merhaba kaynak grupları (örneğin, Web katmanı, uygulama katmanı) dağıtımının hello Katmanlar yansıtacak ve yönetimi.
> 
> İş yükünüzün anlama, bir kaynak grubu stratejisi geliştirme yardımcı olur.

## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi
Büyük olasılıkla kendiniz "kimlerin erişimi tooresources olmalı?" istiyoruz. ve "Bu erişimin nasıl denetlerim?" İzin verme veya erişim toohello Azure portal vermemek ve erişim tooresources hello portalında denetleme çok önemlidir. 

Azure başlangıçta yayımlandığında, erişim denetimleri tooa abonelik temel: Yöneticisi veya ortak Yöneticisi. Merhaba Klasik modeli kapsanan erişim tooall hello kaynakları hello portalında tooa abonelikte erişin. Bu ayrıntılı denetim eksikliği abonelikleri tooprovide makul erişim denetimi düzeyine toohello artışı Azure kayıt için gerektiriyordu.

Bu abonelikleri çoğalmasıdır artık gerekli değildir. Rol tabanlı erişim denetimi ile toostandard rolleri (örneğin, ortak "okuyucu" ve "yazan" türleri rollerinin) kullanıcıları atayabilirsiniz. Özel roller tanımlayabilir.

> [!TIP]
> tooimplement rol tabanlı erişim denetimi:
> * Merhaba AD Connect aracını, Kurumsal kimlik deposu (en yaygın olarak Active Directory) tooAzure Active Directory'yi kullanarak bağlayın.
> * Denetim hello yönetici/ortak yöneticisi olan bir yönetilen kimliğini kullanarak bir abonelik. **Verme** yönetici/ortak yönetici tooa yeni abonelik sahibi atayın. Bunun yerine, RBAC rolleri tooprovide kullanın **sahibi** hakları tooa grup veya kişi.
> * Azure users tooa grubunu (örneğin, uygulama X sahipleri) Active Directory'de ekleyin. Hello eşitlenen Grup tooprovide Grup üyeleri hello uygun hakları toomanage hello kaynak grubu Merhaba uygulaması içeren kullanın.
> * Merhaba verme hello İlkesi izleyin **en az ayrıcalık** gerekli toodo hello iş bekleniyordu. Örneğin:
>   * Dağıtım grubu: yalnızca mümkün toodeploy kaynak grubu.
>   * Sanal Makine Yönetimi: A grubudur mümkün toorestart VM'ler (için işlemler)
> 
> Bu ipuçları aboneliğinizi kullanıcı erişimi yönetmenize yardımcı olur.

## <a name="azure-resource-locks"></a>Azure kaynak kilitleri
Kuruluşunuz Çekirdek Hizmetleri toohello abonelik ekler gibi bu hizmetlerin kullanılabilir tooavoid iş kesintisi olduğundan giderek önemli tooensure haline gelir. [Kaynak kilitleri](resource-group-lock-resources.md) değiştirilmesini veya silinmesini sahip olduğu uygulamalar veya Bulut altyapısı üzerinde önemli bir etkisi yüksek değerli kaynaklar üzerinde toorestrict işlemlerine etkinleştirin. Kilitleri tooa abonelik, kaynak grubuna ya da kaynağa uygulayabilirsiniz. Genellikle, sanal ağlar, ağ geçitleri ve depolama hesapları gibi kilitleri toofoundational kaynaklarına uygulanır. 

Kaynak kilitleri şu anda iki değer destekler: CanNotDelete ve salt okunur. Kullanıcılarla (Merhaba uygun hakları) hala CanNotDelete anlamına gelir okuma veya bir kaynak değiştirme ancak bunu silemezsiniz. Salt okunur, yetkili kullanıcıların silemez veya bir kaynak değiştirme olduğunu anlamına gelir.

Yönetim kilit toocreate ya da delete gerekir erişiminiz çok`Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler.
Merhaba yerleşik rolleri, bu eylemleri yalnızca sahip ve kullanıcı erişimi Yöneticisi verilir.

> [!TIP]
> Çekirdek Ağ Seçenekleri Kilitleriyle korunmalıdır. Bir ağ geçidi, siteden siteye VPN yanlışlıkla silinmesini felaket niteliğinde tooan Azure aboneliği olacaktır. Azure toodelete kullanımda olan bir sanal ağ izin vermez, ancak daha fazla kısıtlamaları yararlı bir önlemidir. 
> 
> * Sanal ağ: CanNotDelete
> * Ağ güvenlik grubu: CanNotDelete
> * İlkeleri: CanNotDelete
> 
> Ayrıca uygun denetimlerin önemli toohello bakım ilkelerdir. Uyguladığınız öneririz bir **CanNotDelete** kilitlemek kullanımda olan toopolices.

## <a name="core-networking-resources"></a>Çekirdek Ağ kaynakları
Erişim tooresources (Merhaba corporation'ın ağından) iç veya dış olabilir (aracılığıyla Internet hello). Kuruluş tooinadvertently put kaynaklarınızı hello yanlış nokta kullanıcılar için kolaydır ve potansiyel olarak bunları toomalicious erişim açın. Şirket içi cihazları gibi kuruluşların Azure kullanıcılar hello doğru kararlar, uygun denetimleri tooensure eklemeniz gerekir. Abonelik Yönetimi için temel Denetim erişim sağlayan çekirdek kaynakları belirleyin. Merhaba çekirdek kaynakları oluşur:

* **Sanal ağlar** alt ağlar için kapsayıcı nesnelerdir. Kesinlikle gerekli olsa, uygulamaları toointernal şirket kaynaklarına bağlanırken çoğunlukla kullanılır.
* **Ağ güvenlik grupları** benzer tooa güvenlik duvarının ve nasıl kaynak "iletişim kurabilirsiniz için" Merhaba ağ üzerinden kurallar sağlar. Nasıl üzerinde ayrıntılı denetim sağlayan / alt ağ (veya sanal makine) toohello Internet veya diğer alt ağlara bağlanabiliyorsa aynı hello sanal ağ.

![Çekirdek Ağ](./media/resource-manager-subscription-governance/core-network.png)

> [!TIP]
> Ağ iletişimi için:
> * Sanal ağlar ayrılmış tooexternal dönük iş yükleri ve dahili kullanıma yönelik iş yükleri oluşturun. Bu yaklaşım, yanlışlıkla bir dış karşılıklı alanı iç iş yükleri için tasarlanmıştır sanal makineleri yerleştirme hello olasılığını azaltır.
> * Ağ güvenlik grupları toolimit erişimi yapılandırın. En azından erişim toohello engelleme iç sanal ağlar ve blok erişim toohello şirket ağından dış sanal ağlar Internet'ten.
> 
> Bu ipuçları güvenli ağ kaynaklarını uygulamanıza yardımcı olur.

### <a name="automation"></a>Otomasyon
Kaynaklarını ayrı ayrı yönetmek, olan her ikisini birden çok zaman alır ve büyük olasılıkla hataya belirli işlemler için. Azure, Azure Automation, Logic Apps ve Azure işlevleri dahil olmak üzere çeşitli Otomasyon özellikleri sağlar. [Azure Otomasyonu](../automation/automation-intro.md) Yöneticiler toocreate etkinleştirir ve kaynaklarını yönetme runbook'lar toohandle ortak görevleri tanımlayın. PowerShell Kod düzenleyicisinde veya bir grafik Düzenleyicisi kullanılarak runbook'lar oluşturun. Karmaşık çok aşamalı iş akışları oluşturabilir. Azure Otomasyonu kullanılmayan kaynakları kapatılıyor veya İnsan eli gerek kalmadan yanıt tooa belirli tetikleyici kaynakları oluşturma gibi genel görevleri kullanılan toohandle görülür.

> [!TIP]
> Otomasyon için:
> * Bir Azure Otomasyonu hesabı oluşturun ve hello kullanılabilir runbook'ları (grafik ve komut satırı) hello kullanılabilir gözden [Runbook Galerisi](../automation/automation-runbook-gallery.md).
> * İçeri aktarma ve anahtar runbook'ları, kendi kullanımınız için özelleştirebilirsiniz.
> 
> Yaygın bir senaryo hello özelliği tooStart/kapatma sanal makinelerin bir zamanlamaya göre şeklindedir. Bu senaryoyu ele hem nasıl öğretmek hello galeri kullanılabilen örnek runbook'lar vardır tooexpand onu.
> 
> 

## <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Belki de hello büyük blockers toocloud benimseme biri üzerinde güvenliği hello sorunları olmuştur. BT risk yöneticileri ve güvenlik Departmanlar Azure kaynaklarında güvenli tooensure gerekir. 

Merhaba [Azure Güvenlik Merkezi](../security-center/security-center-intro.md) hello güvenlik hello Aboneliklerde kaynakların durumunu merkezi bir görünümünü sağlar ve tehlike giren kaynaklarını önlemeye yardımcı öneriler sağlar. Daha ayrıntılı ilkelerini (bunlar adresleme kendi duruş toohello risk hello Kurumsal tootailor sağlayan Örneğin, uygulama ilkeleri toospecific kaynak grupları) etkinleştirebilirsiniz. Son olarak, Azure Güvenlik Merkezi, Microsoft iş ortakları ve Azure Güvenlik Merkezi tooenhance yeteneklerini takılan bağımsız yazılım satıcıları toocreate yazılım sağlayan bir açık platformudur. 

> [!TIP]
> Azure Güvenlik Merkezi, her Abonelikteki varsayılan olarak etkindir. Ancak, kendi Aracısı sanal makineleri tooallow Azure Güvenlik Merkezi tooinstall veri koleksiyonunu etkinleştirme ve veri toplamaya başlamak gerekir.
> 
> ![Veri toplama](./media/resource-manager-subscription-governance/data-collection.png)
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Abonelik idare hakkında öğrendiniz, zaman toosee olan uygulamada Bu öneriler. Bkz: [Azure aboneliği idare uygulamanın örnekleri](resource-manager-subscription-examples.md).

