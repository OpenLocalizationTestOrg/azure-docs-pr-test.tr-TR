---
title: "Azure veri şifreleme çalışmıyorken-aaaMicrosoft | Microsoft Docs"
description: "Bu makalede Microsoft Azure veri şifrelemesi genel bir bakış sağlar çalışmıyorken, genel özellikleri ve genel konular hello."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Azure veri şifreleme çalışmıyorken-
Microsoft Azure toosafeguard veri tooyour şirketin güvenlik ve uyumluluk gereksinimlerine göre içinde birden çok araç vardır. Bu yazı nasıl veri bekleyen Microsoft Azure arasında korumalı, hello hello veri koruma uygulama bölümü alma çeşitli bileşenler açıklar ve Artıları ve eksileri hello farklı anahtar yönetimi koruma yaklaşımlardan incelemeleri odaklanır. 

Bekleyen şifreleme ortak güvenlik gerekli değildir. Microsoft Azure avantajı, uygulama hello maliyetini ve bir özel anahtar yönetimi çözümü yönetimi ve hello riskini gerek kalmadan kuruluşların bekleyen şifreleme gerçekleştirebilirsiniz ' dir. Kuruluşlar tamamen bekleyen şifreleme yönetmek Azure izin vererek hello seçeneğiniz vardır. Ayrıca, kuruluş, şifreleme veya şifreleme anahtarlarını yönetmek çeşitli seçenekler tooclosely sahiptir.

## <a name="what-is-encryption-at-rest"></a>Bekleyen Şifreleme nedir?
Bekleyen şifreleme kalıcı olduğunda toohello şifreleme (şifreleme) kodlama verileri ifade eder. Hello Azure Rest tasarımları şifreleme simetrik şifreleme tooencrypt kullanın ve büyük miktarlarda verinin hızla tooa basit kavramsal model göre şifresini:

- Simetrik şifreleme anahtarını kalıcı hale getirilir kullanılan tooencrypt veri aynıdır 
- Merhaba aynı şifreleme anahtarını kullanılan toodecrypt bellek kullanmak için readied verileri aynıdır
- Veri bölümlendirilebilir ve farklı anahtarlar her bölüm için kullanılabilir
- Anahtarları erişim toocertain kimlikleri ve günlüğe kaydetme anahtar kullanımını sınırlama erişim denetimi ilkeleri ile güvenli bir konumda depolanması gerekir. Veri şifreleme anahtarları genellikle asimetrik şifreleme toofurther sınırı erişimle şifrelenmiş (hello ele alınan *anahtar hiyerarşi*, bu makalenin ilerisinde yer)

Yukarıdaki Hello ortak üst düzey öğeleri bekleyen şifreleme hello açıklar. Uygulamada, ölçek ve kullanılabilirlik çıkışların yanı sıra, yönetim ve denetimi senaryoları ek yapılarını gerektirir. Microsoft Azure şifreleme Rest kavramları ve bileşenleri aşağıda açıklanmıştır.

## <a name="hello-purpose-of-encryption-at-rest"></a>Bekleyen şifreleme Hello amacı
Bekleyen şifreleme (yukarıda açıklandığı gibi.) hedeflenen tooprovide veri koruma çalışmıyorken verileri için olan Veri güvenliğinin aşılmasına hello yer alan ve çalışmıyorken veri saldırıları denemeleri tooobtain fiziksel erişim toohello donanım üzerinde hangi hello veriler içerir. Bu tür bir saldırısında, bir sunucunun sabit disk bir saldırganın tooremove hello sabit sürücü izin vererek bakım sırasında mishandled. Sonraki hello saldırganın bir bilgisayarda, Denetim tooattempt tooaccess hello verilerini altında hello sabit sürücü koyabilirsiniz. 

Bekleyen şifreleme zaman diskteki veri şifrelenir hello sağlayarak şifrelenmemiş hello veri erişimini tasarlanmış tooprevent hello saldırgan ' dir. Bir saldırgan tooobtain olsaydı bir sabit sürücü gibi ile şifrelenmiş veri ve hiçbir erişim toohello şifreleme anahtarları, hello saldırgan, harika zorlanmadan hello veri tehlikeye değil. Böyle bir senaryoda, bir saldırganın tooattempt saldırılarına karşı daha karmaşık olan şifrelenmiş veri yoktur ve erişme fazla kaynak tüketen verileri bir sabit sürücüde şifresiz. Bu nedenle, bekleyen şifreleme önerilir ve çoğu kuruluş için yüksek öncelikli gereksinimdir. 

Bazı durumlarda, bir kuruluşun gerektiğinden veri denetim ve uyumu çalışmaları için bekleyen şifreleme gereklidir. Endüstri ve devlet düzenlemeleri HIPAA, PCI ve FedRAMP ve uluslararası Mevzuat gereklilikleri gibi işlemleri ve veri koruma ve şifreleme gereksinimleri ile ilgili ilkeler aracılığıyla belirli korumaları yerleştirme. Çoğu bu düzenlemeler için bekleyen şifreleme uyumlu veri yönetimi ve koruması için gerekli bir zorunlu ölçüsüdür. 

Ayrıca toocompliance ve Mevzuat gereklilikleri, bekleyen şifreleme savunma platformu özelliği algılanan. Microsoft Hizmetleri, uygulamaları, uyumlu bir platform sağlar ve verileri, kapsamlı tesis ve fiziksel güvenliği, veri erişim denetimi ve denetim olsa da, önemli tooprovide ek "çakışan" güvenlik önlemleri hello birini durumda olduğu diğer güvenlik başarısız ölçer. Bekleyen şifreleme bir böyle bir ek koruma mekanizması sağlar.

Microsoft bulut Hizmetleri ve şifreleme anahtarlarını ve şifreleme anahtarları kullanıldığında gösteren erişim toologs tooprovide müşterilerin uygun yönetilebilirlik arasında kalan seçenekler taahhüt tooproviding şifreleme eder. Ayrıca, Microsoft, varsayılan olarak şifrelenen tüm müşteri verilerine yapmadan hello amacı doğrultusunda çalışmaktadır.

## <a name="azure-encryption-at-rest-components"></a>Rest bileşenleri Azure şifreleme

Daha önce açıklandığı gibi hello bekleyen şifreleme diskte kalıcı veri gizli şifreleme anahtarıyla şifrelenir hedefidir. Bu hedefe tooachieve anahtar oluşturma, depolama, erişim denetimi ve yönetim hello şifreleme anahtarları sağlanmalıdır güvenli hale getirin. Ayrıntılar değişebilir ancak geri kalan uygulamaları adresinde Azure Hizmetleri şifreleme hello diyagramı aşağıdaki hello sonra gösterilen kavramları aşağıda bakımından açıklanabilir.

![Bileşenler](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Azure Key Vault

Merhaba depolama hello şifreleme anahtarları ve erişim denetimi toothose anahtarları rest modeli merkezi tooan şifreleme konumudur. Merhaba anahtarları yüksek oranda yönetilebilir belirtilen kullanıcılar ve kullanılabilir toospecific hizmetler tarafından güvenli hale toobe gerekir. Azure Hizmetleri için Azure anahtar kasası olduğu hello anahtar depolama alanı çözümü önerilir ve hizmetleri arasında ortak bir yönetim deneyimi sağlar. Anahtarları saklanır ve anahtar kasalarını içinde yönetilir ve erişim tooa anahtar kasası toousers veya hizmetleri verilebilir. Azure anahtar kasası, müşteri tarafından yönetilen bir şifreleme anahtarı senaryolarda kullanım için anahtarların müşteri oluşturma veya içeri aktarma müşteri anahtarların destekler.

### <a name="azure-active-directory"></a>Azure Active Directory

İzinleri toouse hello anahtarları Azure anahtar kasası, toomanage veya tooaccess bunları şifreleme için bekleyen şifreleme ve şifre çözme sırasında depolanan, tooAzure Active Directory hesapları verilebilir. 

### <a name="key-hierarchy"></a>Anahtar hiyerarşisi

Genellikle birden fazla şifreleme anahtarı rest uygulaması bir şifreleme kullanılır. Asimetrik şifreleme hello güven ve anahtar erişimi ve yönetimi için gereken kimlik doğrulama oluşturmak için kullanışlıdır. Simetrik şifreleme toplu şifreleme ve şifre çözme, daha güçlü şifreleme ve daha iyi performans için izin vermek için daha verimli olur. Ayrıca, anahtar hello hello risk tehlikeye ve bir anahtar değiştirilmelidir olduğunda yeniden şifreleme maliyeti hello bir tek şifreleme anahtar düşüşleri hello kullanımını sınırlama. Asimetrik ve simetrik şifreleme ve sınırı hello kullan tooleverage hello avantajları ve tek bir anahtar riskini, rest modelleri Azure şifreleme anahtarları türleri aşağıdaki Merhaba oluşan bir anahtar hiyerarşi kullanın:

- **Veri şifreleme anahtarı (DEK)** – bir bölüm veya veri bloğu tooencrypt simetrik AES256 anahtar kullanılır.  Tek bir kaynak birçok bölüm ve çok sayıda veri şifreleme anahtarları olabilir. Her veri bloğu farklı bir anahtarla şifreleme şifre analiz saldırıları daha zor hale getirir. Erişim tooDEKs şifreleme ve belirli bir blok çözme hello kaynak sağlayıcısı veya uygulama örneği tarafından gereklidir. Yeni bir anahtarla bir DEK değiştirildiğinde yalnızca hello verilerin ilişkili bloğundaki yeniden hello yeni anahtarla şifrelenmiş olması gerekir.
- **Anahtar şifreleme anahtarı (KEK)** – bir asimetrik şifreleme anahtarı tooencrypt hello veri şifreleme anahtarları kullanılır. Anahtar şifreleme anahtarı hello veri şifreleme anahtarları kendilerini toobe şifrelenir ve denetlenen izin verir. erişim toohello sahip hello varlık KEK hello DEK gerektiren hello varlık farklı olabilir. Bu, her DEK toospecific bölümünün sınırlı erişim sağlamaya hello amacı bir varlık toobroker erişim toohello DEK sağlar. Merhaba KEK gerekli toodecrypt hello DEKs olduğundan hello KEK etkin olarak DEKs etkili bir şekilde hello KEK silinmesini tarafından silinebilir bir tek noktasıdır.

Anahtar şifreleme anahtarları hello ile şifrelenmiş Hello veri şifreleme anahtarları ayrı olarak depolanır ve yalnızca anahtar şifreleme anahtarı herhangi veri şifreleme anahtarları alabilirsiniz erişim toohello sahip bir varlık bu anahtarla şifrelenir. Anahtar depolama başka modellerinin desteklenir. Her model daha ayrıntılı hello sonraki bölümde aşağıdakiler ele alınacaktır.

## <a name="data-encryption-models"></a>Veri şifreleme modelleri

Anlama hello çeşitli şifreleme modelleri ve bunların Artıları ve eksileri önemlidir anlama nasıl hello için bekleyen Azure uygulama şifreleme çeşitli kaynak sağlayıcıları. Bu tanımları, Azure tooensure ortak dil ve sınıflandırma tüm kaynak sağlayıcıları arasında paylaşılır. 

Sunucu tarafı şifrelemesi için üç senaryo vardır:

- Sunucu tarafı şifreleme hizmeti yönetilen tuşlarını kullanma
    - Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemleri
    - Microsoft hello anahtarları yönetir
    - Tam bulut işlevi

- Müşteri tarafından yönetilen anahtarları Azure anahtar kasası kullanarak sunucu tarafı şifreleme
    - Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemleri
    - Azure anahtar kasası anahtarlarında müşteri denetler
    - Tam bulut işlevi

- Denetlenen müşteri donanımında müşteri tarafından yönetilen tuşlarını kullanarak sunucu tarafı şifreleme
    - Azure kaynak sağlayıcıları hello şifreleme ve şifre çözme işlemleri
    - Müşteri denetimleri anahtarları müşteri donanım denetlenen
    - Tam bulut işlevi

İstemci tarafı şifreleme için hello aşağıdakileri göz önünde bulundurun:

- Azure Hizmetleri şifresi çözülmüş veriler göremiyorum
- Müşteriler yönetin ve anahtarları şirket içi depolama (veya diğer depoları güvenli). Anahtarları kullanılabilir tooAzure Hizmetleri olup olmadığı
- Azaltılmış bulut işlevi

desteklenen hello şifreleme modeller iki ana gruplara ayırın azure'da: "İstemci şifrelemesi" ve "daha önce bahsedilen sunucu tarafı şifreleme" olarak. Rest modeli hello şifreleme bağımsız kullanılan, Azure Hizmetleri zaman TLS ya da HTTPS gibi güvenli bir taşıma hello kullanımını, unutmayın. Bu nedenle, aktarım şifreleme hello Aktarım Protokolü tarafından ele alınması gereken ve rest modeli toouse hangi şifreleme belirlemede önemli bir etken olmamalıdır.

### <a name="client-encryption-model"></a>İstemci şifreleme modeli

İstemci şifreleme modeli kaynak sağlayıcısı veya Azure hello dışında hello hizmet ya da çağıran uygulama tarafından gerçekleştirilen tooencryption başvuruyor. Merhaba şifreleme azure'da hello hizmet uygulaması tarafından ya da hello müşteri veri merkezinde çalışan bir uygulama tarafından gerçekleştirilebilir. Bu şifreleme modeli yararlanırken her iki durumda da, hello Azure kaynak sağlayıcısı herhangi bir şekilde hello özelliği toodecrypt hello verileri olmayan verilerin şifrelenmiş bir blobu alır veya erişim toohello şifreleme anahtarları sahip. Bu modelde hello anahtar yönetimi hizmeti/uygulama çağırma hello tarafından yapılır ve tamamen opak toohello Azure hizmeti.

![İstemci](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Sunucu tarafı şifreleme modeli

Sunucu tarafı şifreleme modelleri hello Azure hizmeti tarafından gerçekleştirilen tooencryption bakın. Bu modelde hello kaynak sağlayıcısı hello gerçekleştirir şifrelemek ve şifresini çözmek işlemleri. Örneğin, Azure Storage veri düz metin işlemlerinde alabilirsiniz ve hello şifreleme ve şifre çözme dahili olarak gerçekleştirir. Merhaba kaynak sağlayıcısı yapılandırmasını sağlanan hello bağlı olarak hello müşteri veya Microsoft tarafından yönetilen şifreleme anahtarlarını kullanabilir. 

![Sunucu](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Sunucu tarafı şifreleme anahtar yönetimi modelleri

Her rest modelleri hello sunucu tarafı şifreleme anahtar yönetimi ayırıcı özelliklerini anlamına gelir. Bu where içerir ve şifreleme anahtarlarını oluşturulan depolanan ve nasıl gibi hello erişim modelleri olarak yanı sıra ve anahtar döndürme yordamları hello. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Yönetilen hizmet anahtarları kullanarak sunucu tarafı şifreleme

Birçok müşteri için bekleyen olduğunda veri hello tooensure şifrelenir hello temel gerekli değildir. Sunucu tarafı şifreleme hizmeti yönetilen anahtarları kullanarak, müşterilerin toomark hello belirli bir kaynak (depolama hesabı, SQL DB, vb.) için şifreleme tanır ve anahtar verme, döndürme ve yedekleme gibi tüm anahtar yönetimi özelliklerini bırakarak bu modeli sağlar. tooMicrosoft. Bekleyen şifreleme desteği genellikle çoğu Azure Hizmetleri hello şifreleme anahtarları tooAzure hello yönetimini boşaltma bu modelini destekler. Hello Azure kaynak sağlayıcısı hello anahtarları oluşturur, bunları güvenli depolama yerleştirir ve bunları gerektiğinde alır. Bunun anlamı hello hizmeti tam erişim toohello anahtarlara sahip ve hello hizmeti hello kimlik bilgisi yaşam döngüsü yönetimi üzerinde tam denetime sahiptir.

![Yönetilen](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Yönetilen hizmet anahtarları bu nedenle hızlı bir şekilde kullanarak sunucu tarafı şifreleme Itanium tabanlı sistemler için hello gerek toohave şifreleme REST düşük genel gider toohello müşteri ile giderir. Kullanılabilir olduğunda bir müşteri genellikle hello hello hedef abonelik ve kaynak sağlayıcısı için Azure portalı açar ve şifrelenmiş hello veri toobe istediğiniz belirten bir kutusunu denetler. Bazı kaynak yöneticileri sunucu tarafı şifreleme hizmeti ile yönetilen anahtarlar varsayılan olarak açıktır. 

Sunucu tarafı şifreleme Microsoft tarafından yönetilen anahtarlarla hello hizmeti tam erişim toostore sahiptir ve hello anahtarları yönetir anlamına gelmez. Daha fazla güvenlik sağlayabilirsiniz eşitleyerek çünkü bazı müşteriler toomanage hello anahtarlarını isteyebilirsiniz, ancak hello maliyet ve bir özel anahtar depolama çözümü ile ilişkili risk bu modeli değerlendirirken dikkate alınmalıdır. Çoğu durumda, bir kuruluşun kaynak kısıtlamaları veya bir şirket içi çözüm risklerini rest anahtarları hello şifrelemeyi bulut yönetimini hello riskini büyük olabilir belirleyebilir.  Ancak, bu model gereksinimleri toocontrol hello oluşturma olan kuruluşlar için yeterli olmayabilir veya yaşam döngüsü boyunca hello şifreleme anahtarları veya toohave farklı personel hello hizmetini (yani, yönetme olandan bir hizmetin şifreleme anahtarları Yönet Anahtar Yönetimi'nden hello ayrımı hello hizmeti için genel yönetim modeli).

##### <a name="key-access"></a>Anahtar erişimi

Sunucu tarafı şifreleme hizmeti yönetilen anahtarlarla kullanıldığında, anahtar oluşturmayı hello depolama ve hizmet erişimi tüm yönetilen hello hizmeti tarafından. Genellikle, hello temel Azure kaynak sağlayıcıları hello veri şifreleme anahtarları toohello veri kapatın ve hızlı bir şekilde kullanılabilir ve erişilebilir hello anahtar şifreleme anahtarları sırasında güvenli bir iç deposunda saklanır bir deposu depolar.

**Avantajları**

- Basit Kurulumu
- Microsoft anahtar döndürme, yedekleme ve artıklık yönetir
- Müşteri yok hello bir özel anahtar yönetimi düzeni uygulama veya hello riskini ile ilişkili maliyeti.

**Olumsuz yönleri**

- Merhaba şifreleme anahtarları (anahtar belirtimi, yaşam döngüsü, iptal, vb.) üzerinde hiçbir müşteri denetimi
- Hiçbir özelliği toosegregate Anahtar Yönetimi'nden hello hizmeti için genel yönetim modeli

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Müşteri kullanarak sunucu tarafı şifreleme anahtarları Azure anahtar Kasası'yönetilen 

Burada hello gereksinim tooencrypt hello veri şifrelenir ve denetim hello şifreleme anahtarları müşterileri sunucu tarafı şifreleme kullanabilir senaryoları için anahtar kasasına müşteri yönetilen anahtarları kullanma. Bazı hizmetler yalnızca hello kök anahtar şifreleme anahtarı Azure anahtar kasası depolayabilir ve deposu hello veri şifreleme anahtarı bir iç konumu daha yakından toohello verileri şifrelenir. Buna senaryo müşteriler kendi getirebileceğinizden emin tooKey kasası (BYOK – kendi anahtarını Getir), anahtarlar veya yenilerini oluşturun ve tooencrypt istenen hello kaynakları kullanın. Merhaba kaynak sağlayıcısı hello şifreleme ve şifre çözme işlemleri gerçekleştirirken tüm şifreleme işlemleri için hello kök anahtarı olarak yapılandırılmış hello anahtarı kullanır. 

##### <a name="key-access"></a>Anahtar erişimi

Hello sunucu tarafı şifreleme modeli ile yönetilen müşteri anahtarları Azure anahtar Kasası'hello hizmet erişilirken hello anahtarları tooencrypt ve şifresini çözme gerektikçe içerir. Rest anahtarları şifreleme erişilebilir tooa hizmeti, hizmet kimliği erişim tooreceive hello anahtarı verme bir erişim denetimi İlkesi aracılığıyla yapılır. Bu abonelik içindeki bu hizmet için bir kimlik ile ilişkili bir abonelik adına çalıştıran bir Azure hizmeti yapılandırılabilir. Merhaba hizmeti, Azure Active Directory kimlik doğrulaması yapmak ve kendisini hello abonelik adına hareket hizmet olarak tanımlayan bir kimlik doğrulama belirtecini alma. Sunulan tooKey kasa tooobtain bir anahtarı olması, erişimi verilip verilmediğini bundan sonra bu belirteci kullanabilirsiniz.

Şifreleme anahtarları kullanılarak işlemleri için erişim tooany işlemleri aşağıdaki Merhaba, bir hizmet kimliği verilebilir: şifre çözme, wrapKey unwrapKey, şifreleme, doğrulayın, oturum, almak, listesinde, güncelleştirme, oluşturma, alma, silme, yedekleme ve geri.

tooobtain kullanımda şifrelemek veya bu hello UnwrapKey (tooget hello anahtar şifre çözme için) ve WrapKey (tooinsert bir anahtar olarak yeni bir anahtar oluşturulurken anahtar kasası) olarak hizmet örneği çalışacak Resource Manager rest hello hizmet kimliği, verilerin şifresini çözmek için bir anahtar.


>[!NOTE] 
>Anahtar kasası hakkında daha fazla ayrıntı için bkz anahtar kasası sayfanızda hello güvenli hello [Azure anahtar kasası belgelerine](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Avantajları**

- Merhaba anahtarları üzerinde tam denetim kullanılan – şifreleme anahtarları hello Müşteri'nin anahtar kasası hello Müşteri'nin denetimindeki yönetilir.
- Özelliği tooencrypt birden çok Hizmetleri tooone ana
- Anahtar Yönetimi hello hizmeti için genel yönetim modelden ayırabilirsiniz
- Hizmet ve anahtar konumu bölgeler arasında tanımlayabilir

**Olumsuz yönleri**

- Müşteri, anahtarı erişim yönetimi için tam sorumluluk sahiptir.
- Müşteri, anahtar yaşam döngüsü yönetimi için tam sorumluluk sahiptir.
- Ek kurulum ve yapılandırma yükü

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Hizmetini kullanarak sunucu tarafı şifreleme anahtarları denetlenen müşteri donanımında yönetilen

Burada hello gereksinimleri tooencrypt hello veri şifrelenir ve Microsoft'un denetimi dışında özel bir havuzda hello anahtarları Yönet senaryoları için bazı Azure Hizmetleri hello ana bilgisayarınızı kendi anahtarını Taşı (HYOK) anahtar yönetim modeli etkinleştirin. Bu model, hello hizmet başlangıç anahtarı bir dış sitesinden almanız gerekir ve bu nedenle performansı ve kullanılabilirliği garanti etkilenen yapılandırma daha karmaşıktır. Ayrıca, hello hizmeti erişim toohello DEK sırasında hello şifreleme ve şifre çözme işlemleri Bu modelin genel güvenlik garantileri hello beri benzer toowhen hello anahtarları Azure anahtar kasası müşteri yönetilen olan kullanılabilir.  Sonuç olarak, belirli anahtar yönetimi gereksinimleri, araya sahip oldukları sürece bu modeli çoğu kuruluş için uygun değil. Toothese sınırlamaları, çoğu Azure Hizmetleri denetlenen müşteri donanımında sunucusu yönetilen tuşlarını kullanarak sunucu tarafı şifrelemeyi desteklemez.

##### <a name="key-access"></a>Anahtar erişimi

Yönetilen hizmet anahtarları denetlenen müşteri donanımında kullanarak sunucu tarafı şifreleme kullanıldığında hello anahtarları hello müşteri tarafından yapılandırılan bir sistemde saklanır. Güvenli bağlantı tooa müşteri oluşturma yolu anahtar deposunda sağlanan bu modelini destekleyen azure hizmetleri sağlar.

**Avantajları**

- Merhaba kök anahtarı üzerinde tam denetim kullanılan – şifreleme anahtarları sağlanan müşteri mağaza tarafından yönetilir
- Özelliği tooencrypt birden çok Hizmetleri tooone ana
- Anahtar Yönetimi hello hizmeti için genel yönetim modelden ayırabilirsiniz
- Hizmet ve anahtar konumu bölgeler arasında tanımlayabilir

**Olumsuz yönleri**

- Anahtar depolama, güvenlik, performans ve kullanılabilirlik tam sorumluluk
- Tam sorumluluk anahtar erişim yönetimi
- Tam sorumluluk anahtar yaşam döngüsü yönetimi
- Önemli Kurulum, yapılandırma ve devam eden bakım maliyeti
- Ağ kullanılabilirliğini hello müşteri veri merkezi ve Azure veri merkezleri arasında artan bağımlılığı.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Microsoft bulut hizmetlerinde bekleyen şifreleme

Microsoft Cloud services, tüm üç bulut modellerinde kullanılır: Iaas, PaaS, SaaS. Aşağıda, bunların her model üzerinde nasıl uyduğunu örnekler vardır:

- Yazılım Hizmetleri, başvurulan tooas bir sunucu veya Office 365 gibi hello bulut tarafından sağlanan uygulamaya sahip SaaS olarak yazılım.
- Platform Hizmetleri kullanılarak hello bulut işlemler için hangi müşterilerin kendi uygulamalarında hello bulut yararlanan depolama, analiz ve hizmet veri yolu işlevselliğini ister.
- Altyapı hizmetleri veya hangi müşteri hizmet (Iaas) olarak işletim sistemlerini ve hello barındırılan uygulamalara dağıtmak altyapı Bulut ve büyük olasılıkla diğer yararlanarak bulut hizmetlerini.

### <a name="encryption-at-rest-for-saas-customers"></a>SaaS müşteriler için bekleyen şifreleme

Bir hizmet (SaaS) müşteri olarak genellikle yazılımınız şifreleme REST etkin ya da her hizmetindeki kullanılabilir. Office 365 Hizmetleri bekleyen müşteriler tooverify veya etkinleştir şifreleme için birkaç seçenek vardır. Office 365 hizmetleri hakkında bilgi için Office 365 için veri şifreleme teknolojileri bakın.

### <a name="encryption-at-rest-for-paas-customers"></a>PaaS müşteriler için bekleyen şifreleme

Hizmet (PaaS) Müşteri'nin veri olarak Platform genellikle uygulama yürütme ortamında bulunan ve hiçbir Azure kaynak sağlayıcısı toostore müşteri verileri kullanılır. rest seçenekleri kullanılabilir tooyou toosee hello şifreleme hello kullandığınız hello depolama ve uygulama platformlar için aşağıdaki tabloyu inceleyin. Desteklenen durumlarda bekleyen şifreleme etkinleştirme bağlantılar tooinstructions her kaynak sağlayıcısı için sağlanır. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Iaas müşteriler için bekleyen şifreleme

Altyapı (Iaas) müşteri olarak hizmetler ve uygulamalar, çeşitli kullanımda olabilir. Iaas Hizmetleri etkinleştirebilir kendi Azure bekleyen şifreleme barındırılan sanal makineleri ve VHD Azure Disk Şifrelemesi'ni kullanarak. 

#### <a name="encrypted-storage"></a>Şifrelenmiş depolama

PaaS gibi Iaas çözümleri şifrelenen verileri depolamak diğer Azure hizmetleriyle yararlanabilirsiniz. Bu durumlarda, her tüketilen Azure hizmeti tarafından sağlanan gibi hello şifreleme Rest destek adresindeki etkinleştirebilirsiniz. Merhaba tablonun altındaki hello ana depolama, hizmetleri ve uygulama platformları ve desteklenen bekleyen şifreleme hello modelinin numaralandırır. Desteklenen durumlarda bağlantılar bekleyen şifreleme etkinleştirme hakkında tooinstructions sağlanır. 

#### <a name="encrypted-compute"></a>Şifrelenmiş işlem

Rest çözüm tam bir şifreleme veri hiçbir zaman şifresiz biçimde kalıcı bu hello gerektirir. Kullanımdayken, bellek, veri verileri yerel olarak hello Windows disk belleği dosyası, bir kilitlenme dökümü ve hiçbir günlüğü hello dahil olmak üzere çeşitli yollarla kalıcı bir sunucu yükleme hello üzerinde uygulama gerçekleştirebilir. Bu veri şifrelenir tooensure bekleyen Iaas uygulamaları Azure Disk şifrelemesi bir Azure Iaas sanal makine (Windows veya Linux) ve sanal disk kullanabilirsiniz. 

#### <a name="custom-encryption-at-rest"></a>Bekleyen özel şifreleme

Mümkün olduğunda, Iaas uygulamaları Azure Disk şifrelemesi ve şifreleme tüketilen Azure Hizmetleri tarafından sağlanan Rest seçeneklerini adresindeki yararlanan olduğunu önerilir. Düzensiz şifreleme gereksinimleri veya Azure dışı tabanlı depolama, bir Iaas uygulama geliştiricisi tooimplement şifreleme gerekebilir gibi bazı durumlarda, kendilerini bekletin. Iaas çözümleri daha iyi geliştiriciler, Azure belirli bileşenlerini yararlanarak Azure yönetimi ve müşteri beklentilerini ile tümleştirin. Özellikle, geliştiricilerin hello hizmet tooprovide anahtar depolama güvenli yanı sıra, çoğu Azure platform hizmetlerini ile tutarlı anahtar yönetim seçeneklerini müşterilerine sağlamak Azure anahtar kasası kullanmanız gerekir. Ayrıca, özel çözümler Azure yönetilen hizmet kimliği tooenable hizmet hesapları tooaccess şifreleme anahtarlarını kullanmanız gerekir. Azure anahtar kasası ve yönetilen hizmet kimlikleri hakkında bilgi için geliştirici kendi ilgili SDK'ları bakın.

## <a name="azure-resource-providers-encryption-model-support"></a>Azure kaynak sağlayıcıları şifreleme modeli desteği

Microsoft Azure hizmetleri her bir veya daha fazla rest modelleri hello şifrelemeyi destekler. Bazı hizmetler için ancak, bir veya daha fazla hello şifreleme modelleri geçerli olmayabilir. Ayrıca, değişik zamanlamalar, bu senaryolar için Destek Hizmetleri yayımlayabilir. Bu bölümde rest destek hello büyük Azure veri depolama hizmetlerinin her biri için bu yazma hello zamanında hello şifreleme açıklanmaktadır.

### <a name="azure-disk-encryption"></a>Azure disk şifrelemesi

Bir hizmet (Iaas) olarak Azure altyapısı kullanarak müşteri özellikleri Iaas Vm'leri ve Azure Disk şifrelemesi ile diskleri bekleyen şifreleme elde edebilirsiniz. Azure diski hakkında daha fazla bilgi için bkz: şifreleme hello [Azure Disk şifrelemesi belgelerine](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Azure Storage

Azure Blob ve dosya şifreli müşteri verilerini (istemci tarafı şifreleme) yanı sıra sunucu tarafı şifrelenmiş senaryoları için bekleyen Şifreleme destekler.

- Sunucu tarafı: Azure blob depolama kullanan müşteriler REST her Azure depolama kaynak hesabı üzerinde şifrelemeyi etkinleştirebilirsiniz. Etkinleştirildikten sonra sunucu tarafı şifreleme toohello uygulama şeffaf bir şekilde gerçekleştirilir. Bkz: [bekleyen veri için Azure depolama hizmeti şifrelemesi](https://docs.microsoft.com/azure/storage/storage-service-encryption) daha fazla bilgi için.
- İstemci-tarafı: Azure BLOB istemci tarafı şifreleme desteklenir. Ne zaman istemci tarafı şifreleme müşteriler kullanarak hello verileri şifrelemek ve hello verileri şifrelenmiş bir blobu olarak yükleyin. Anahtar Yönetimi hello müşteri tarafından gerçekleştirilir. Bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) daha fazla bilgi için.


#### <a name="sql-azure"></a>SQL Azure

SQL Azure şu anda Microsoft tarafından yönetilen hizmet tarafı ve istemci tarafı şifreleme senaryoları için bekleyen şifreleme desteklemektedir.

Desteği sever şifreleme şu anda saydam veri şifreleme adlı hello SQL özelliği sağlanır. Bir SQL Azure müşterisi etkinleştirir sonra TDE anahtarı otomatik olarak oluşturulur ve bunlar için yönetilir. Bekleyen şifreleme hello veritabanı ve sunucu düzeylerinde etkinleştirilebilir. Haziran 2017'dan sonra [saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/bb934049.aspx) yeni oluşturulan veritabanı üzerinde varsayılan olarak etkinleştirilir.

İstemci tarafı şifreleme SQL Azure veri hello desteklenen [her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx) özelliği. Her zaman şifreli oluşturulan ve saklanan bir anahtar hello istemci tarafından kullanır. Müşteriler, Windows sertifika deposu, Azure anahtar kasası veya yerel bir donanım güvenlik modülü hello ana anahtar depolayabilirsiniz. SQL Server Management Studio'yu kullanarak SQL kullanıcıların ne seçim anahtar toouse tooencrypt istedikleri hangi sütun.

|                                  |                |                     | **Şifreleme modeli**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **İstemci** |
|                                  | **Anahtar Yönetimi** | **Hizmet anahtarı yönetilen** | **Anahtar kasasına yönetilen müşteri** | **Yönetilen müşterinin şirket içi** |        |
| **Depolama ve veritabanları**            |                |                     |                              |                              |        |
| Disk (Iaas)                      |                | -                   | Evet                          | Evet*                         | -      |
| SQL Server (Iaas)                |                | Evet                 | Evet                          | Evet                          | Evet    |
| SQL Azure (PaaS)                 |                | Evet                 | Önizleme                      | -                            | Evet    |
| Azure depolama (blok/sayfa Bloblarını) |                | Evet                 | Önizleme                      | -                            | Evet    |
| Azure depolama (dosyaları)            |                | Evet                 | -                            | -                            | -      |
| Azure depolama (tablolar, kuyruklar)   |                | -                   | -                            | -                            | Evet    |
| Cosmos DB (belge DB)          |                | Evet                 | -                            | -                            | -      |
| StorSimple                       |                | Evet                 | -                            | -                            | Evet    |
| Backup                           |                | -                   | -                            | -                            | Evet    |
| **Intelligence ve analizi**       |                |                     |                              |                              |        |
| Azure Data Factory               |                | Evet                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Önizleme                      | -                            | -      |
| Azure Stream Analytics           |                | Evet                 | -                            | -                            | -      |
| Hdınsights (Azure Blob Depolama)  |                | Evet                 | -                            | -                            | -      |
| Hdınsights (Data Lake Store)   |                | Evet                 | -                            | -                            | -      |
| Azure Data Lake Store            |                | Evet                 | Evet                          | -                            | -      |
| Azure Veri Kataloğu               |                | Evet                 | -                            | -                            | -      |
| Power BI                         |                | Evet                 | -                            | -                            | -      |
| **IOT Hizmetleri**                     |                |                     |                              |                              |        |
| IoT Hub’ı                          |                | -                   | -                            | -                            | Evet    |
| Service Bus                      |                | -              | -                            | -                            | Evet    |
| Event Hubs                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Sonuç

Azure Services içinde depolanan müşteri verileri koruma en önemli önem tooMicrosoft ' dir. Barındırılan tüm Azure hizmetlerdir Rest seçenekleri adresindeki taahhüt tooproviding şifreleme. Zaten Azure Storage, SQL Azure ve anahtar analizi gibi temel Hizmetleri ve Destek Hizmetleri şifreleme Rest seçenekleri sağlar. Bu hizmetlerden bazılarını denetlenen müşteri anahtarları ve istemci tarafı şifreleme desteği olarak yönetilen anahtarlar ve şifreleme hizmeti. Microsoft Azure Hizmetleri Rest kullanılabilirliğine şifreleme geliştirme geniş ve hello gelecek aylarda Önizleme ve genel kullanılabilirlik için yeni seçenekler aşağıda verilmiştir.

