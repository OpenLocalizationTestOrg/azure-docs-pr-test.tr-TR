---
title: azure'da aaaGovernance | Microsoft Docs
description: "Geniş işlem örnekleri dahil bulut tabanlı bilgi işlem Hizmetleri & otomatik olarak toomeet hello ihtiyaçlarını uygulamanızı veya Kurumsal yukarı ve aşağı ölçeklenebilen hizmetleri hakkında bilgi edinin."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Azure Yönetimi

Güvenlik hello bulutta iş ve nasıl önemli Azure güvenliği hakkında doğru ve güncel bilgi bulma olduğunu olduğunu biliyoruz. Merhaba en iyi uygulamalar ve hizmetler için nedenleri toouse Azure, çeşitli güvenlik araçları ve yetenekleri tootake avantajlarından biri. Bu araçları ve yetenekleri, olası toocreate güvenli çözümleri hello güvenli Azure platformu yardımcı olur.

Merhaba dizi idare denetimlerin Microsoft Azure içinde her iki hello müşterinin uygulanan ve "İdare içinde Azure", bu makalede, Microsoft operations perspektiflerin yazılmış hello kapsamlı bir bakış sağlayan daha iyi anlamak toohelp İdare özellikleri Microsoft Azure ile kullanılabilir.

## <a name="azure-platform"></a>Azure platformu

Azure işletim sistemleri, programlama dilleri, çerçeveleri, Araçlar, veritabanları ve aygıtları geniş çapta destekleyen bir genel bulut hizmeti platformudur. Linux kapsayıcıları Dockers tümleşme çalıştırabilirsiniz; JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma; Yapı geri-iOS, Android ve Windows cihazları sona erer. Azure genel bulut Hizmetleri, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Derleme ya da BT varlıklarına geçirmek hello Hizmetleri ve hello denetimleri ile veri ve uygulamaları, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı bir genel bulut hizmeti sağlayıcısı, bulut tabanlı toomanage hello güvenliğini sağlarlar varlıklar.

Azure'un altyapısından aynı anda milyonlarca müşteri barındırmak için hello tesis tooapplications gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, birçok güvenlik seçenekleri ve hello özelliği toocontrol sağlayan bunları böylece güvenlik toomeet hello benzersiz gereksinimleri, kuruluşunuzun dağıtımlarının özelleştirebilirsiniz.

Bu belge, Azure idare özellikleri bu gereksinimleri karşılamak nasıl yardımcı olabileceğini anlamanıza yardımcı olur.

## <a name="abstract"></a>Özet

Microsoft Azure bulut idare bir tümleşik denetim ve gözden geçirmek ve hello Azure platformu kullanıcıların kullanımına kuruluşlar bildiren için danışmanlık yaklaşımı sağlar. Microsoft Azure bulut idare, toohello işlerinizdeki karar verme işlemlerini, ölçüt ve ilkeleri söz konusu hello planlama, mimarisi, edinme, dağıtım, işlem ve bir bulutun yönetim başvuruyor bilgi işlem.

sonra BT tooconsistently kolaylaştırır yapı çerçeveleri son sağlarken iş gereksinimlerini desteklemek ve Microsoft Azure bulut idare planlama toocreate, tootake hello kişiler, işlemleri ve şu anda yerinde teknolojileri ilişkin ayrıntılı bir bakış gerekir Kullanıcılar hello esneklik toouse hello güçlü özellikler ile Microsoft Azure.

Bu yazı, BT kaynaklarınız Microsoft Azure İdaresi yükseltilmiş bir düzeyde nasıl elde edebilirsiniz açıklar. Bu yazı tooMicrosoft Azure yerleşik hello güvenlik ve idare özelliklerini anlamanıza yardımcı olabilir.

Merhaba, bu makalede ele alınan ana hello idare sorunlar şunlardır:

- Uygulama ilkeleri, işlemler ve yordamlar kuruluş hedefleri göredir.

- Güvenlik ve kuruluş standartlarıyla sürekli uyumluluk

- Uyarı verme ve izleme

## <a name="implementation-of-policies-processes-and-procedures"></a>Uygulama ilkeleri, işlemler ve yordamlar 

Yönetim rolleri ve sorumlulukları toooversee uygulaması hello bilgi güvenlik ilkesi ve işletimsel sürekliliği Azure oluşturmuştur. Microsoft Azure yönetim, güvenlik ve ilgili takımlar (üçüncü tarafların dahil olmak üzere) ve güvenlik ilkeleri, işlemleri ve standartları ile gönderilmesini kolaylaştıran Uyumluluk dahilinde sürekliliği yöntemler gözlemledikten sorumludur.

Gelişen hello faktörleri şunlardır:

- Hesap Sağlama

- Abonelik denetimleri

- Rol tabanlı erişim denetimleri

- Kaynak Yönetimi

- Kaynak İzleme

- Kritik kaynak denetimi

- API erişimini tooBilling bilgileri

- Ağ denetimleri

## <a name="account-provisioning"></a>Hesap sağlama

Hiyerarşi önemli adım toouse ve yapısı bir şirket içinde Azure Hizmetleri ve hello çekirdek yönetim yapısı hesabı tanımlama. Merhaba Kurumsal anlaşma ile müşteriler durumunda, müşterilerin daha fazla hello ortamına Departmanlar, hesapları ve son olarak, abonelikleri ayırabilir.

![Hesap Sağlama](./media/governance-in-azure/security-governance-in-azure-fig1.png)

Bir Kurumsal Anlaşma yoksa kullanmayı [Azure etiketleri](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) abonelik düzeyi toodefine hiyerarşi adresindeki. Bir Azure aboneliği, tüm kaynakların bulunduğu hello temel birimidir. Ayrıca, Azure, çekirdek, kaynaklar, vb. sayısı gibi birkaç sınırlarda tanımlar. Abonelikleri içerebilir [kaynak grupları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), kaynakları içerebilir. [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) ilkeler bu üç düzeyde uygulanır.

Her Kuruluş farklıdır ve hello hiyerarşi Kurumsal olmayan müşteriler durumunda Azure etiketleri kullanarak Azure hello şirket içinde nasıl düzenlendiğini önemli esneklik sağlar. Microsoft Azure kaynaklarında dağıtmadan önce hiyerarşi model ve faturalama, kaynak erişimi ve karmaşıklık hello etkisini anlamak gerekir.

## <a name="subscription-controls"></a>Abonelik denetimleri

Abonelik, kaynak kullanımı nasıl bildirilen ve fatura denetler. Abonelikleri Kurulum ayrı faturalandırma ve ödeme için olabilir. Belirtilen önceki altında bir Azure hesabı olarak biz birden fazla abonelik olabilir. Abonelikler, bir şirkette birden çok bölümlerin kullanılan toodetermine hello Azure kaynak kullanımı olabilir.

Örneğin, bir şirket varsa BT, İK ve pazarlama departmanları ve bu Departmanlar çalıştıran farklı projelere sahip. Sanal makineler gibi Azure kaynaklarını hello kullanımını her departmana göre bağlı olarak, bunlar uygun şekilde fatura. Bu her bölümünün hello Finans denetleyebilirsiniz.

Azure abonelikleri üç parametre kurar:

- benzersiz abone kimliği

- Fatura konumu

- Kullanılabilir kaynak kümesi

Tüketim sınırları, hello abonelik türüne bağlı olarak Microsoft zorlar rağmen bireyin her zaman bir Microsoft hesabı kimliği içerir, kredi kartı numarası ve hello tam dizisi Azure--Hizmetleri.

Azure kayıt hiyerarşileri, hizmetleri bir Kurumsal Anlaşma içinde nasıl yapılandırıldığı tanımlayın. Merhaba Enterprise Portal müşterilerin benzersiz esnek hiyerarşileri özelleştirilebilir tooan kuruluşunuzun ihtiyaçlarına göre bir kurumsal anlaşma ile ilişkili toodivide tooAzure erişimine olanak tanır. Hello hiyerarşi düzeni, kuruluşun yönetim ve coğrafi yapısı hello faturalama ilişkili ve kaynak erişimini doğru şekilde olunması eşleşmelidir.

işlev, iş birimi Hello üç üst düzey desenleri alır ve coğrafi, kullanarak Departmanlar için yönetimsel bir yapı olarak gruplandırmaları hesap. Her bölüm içinde hesapları siloları fatura ve birkaç anahtar sınırları için (örneğin, sayısı VM'ler, depolama hesapları, vb.) oluşturma abonelikleri atanabilir.

![Abonelik denetimleri](./media/governance-in-azure/security-governance-in-azure-fig2.png)


Bir Kurumsal Anlaşma olan kuruluşlar için Azure abonelikleri dört düzeyli bir hiyerarşiye izleyin:

- Kuruluş kayıt Yöneticisi

- Bölüm Yöneticisi

- hesap sahibi

- Hizmet Yöneticisi

Bu hiyerarşi hello aşağıdaki yönetir:

- Faturalama ilişkisi

- Hesap Yönetimi

- Rol tabanlı erişim denetimi (RBAC) tooartifacts

- Sınırları/sınırları

- Sınırları

  - Kullanım ve fatura (teklif sayılara göre oranı kartı)

  - Sınırlar

  - Sanal Ağ

- Too1 AAD bağlı (1 AAD birçok aboneliği ile ilişkili)

- İlişkili tooan Kurumsal kayıt hesabı

## <a name="role-based-access-controls"></a>Rol tabanlı erişim denetimleri

Azure başlangıçta yayımlandığında, erişim denetimleri tooa abonelik temel: Yöneticisi veya ortak Yöneticisi. Merhaba Klasik modeli kapsanan erişim tooall hello kaynakları hello portalında tooa abonelikte erişin. Bu ayrıntılı denetim eksikliği abonelikleri tooprovide makul erişim denetimi düzeyine toohello artışı Azure kayıt için gerektiriyordu.

![Rol tabanlı erişim denetimleri](./media/governance-in-azure/security-governance-in-azure-fig3.png)

Bu abonelikleri çoğalmasıdır artık gerekli değildir. Rol tabanlı erişim denetimi ile toostandard rolleri (örneğin, ortak "okuyucu" ve "yazan" türleri rollerinin) kullanıcıları atayabilirsiniz. Özel roller tanımlayabilir.

[Azure rol tabanlı erişim denetimi (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) Azure için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, kullanıcıların işlerini tooperform gerektiğini yalnızca hello erişim miktarını verebilirsiniz. Güvenlik odaklı şirketler çalışanlar gereksinim duydukları hello tam izinleri vermiş odaklanmanız gerekir. Çok fazla izinleri bir hesap tooattackers kullanıma sunar. Çok az izinleri çalışanlar verimli bir şekilde işlerini alınamıyor anlamına gelir. Azure rol tabanlı erişim denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sunarak bu sorunu gidermeye yardımcı olur. RBAC toosegregate görevlerini, ekip ve grant yalnızca hello süre içinde tooperform işlerini gereken erişim toousers yardımcı olur. Kısıtlanmamış izinlerini herkes vermek yerine, Azure aboneliği veya kaynakları yalnızca belirli eylemleri izin verebilirsiniz.

Örneğin, kullanım RBAC toolet bir çalışan bir Abonelikteki sanal makineleri yönetmek için başka yönetebilirsiniz sırada SQL hello içinde aynı veritabanları abonelik.

Azure RBAC tooall kaynak türleri geçerli üç temel rol vardır:

- **Sahibi** hello sağ toodelegate erişim tooothers dahil olmak üzere tam erişim tooall kaynaklara sahip.

- **Katkıda bulunan** olabilir oluşturun ve tüm türlerini Azure kaynaklarını yönetmek ancak erişim tooothers veremezsiniz.

- **Okuyucu** mevcut Azure kaynaklarını görüntüleyebilirsiniz.

azure'da hello RBAC rollerin Hello rest belirli Azure kaynaklarının yönetimini sağlar. Örneğin, hello sanal makine katkıda bulunan rolü hello kullanıcı toocreate verir ve sanal makineleri yönetme. Bunları erişim toohello sanal ağ vermez veya sanal makine hello hello alt ağa bağlanır.

[RBAC yerleşik rolleri](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listeleri hello rolleri Azure üzerinde kullanılabilir. Merhaba işlemler ve her yerleşik rol toousers verir kapsam belirtir.

Merhaba uygun RBAC rolü toousers, gruplar ve uygulamalar belirli bir kapsamda atayarak erişim sağla. bir rol ataması Hello kapsamını bir abonelik, bir kaynak grubu veya tek bir kaynak olabilir. Bir üst kapsamda atanan bir rol, ayrıca içerdiği toohello alt erişim verir.

Örneğin, erişim tooa kaynak grubuna sahip bir kullanıcı, Web siteleri, sanal makineler ve alt ağlar gibi içerdiği tüm hello kaynakları yönetebilir.

Azure RBAC destekleyen yönetim işlemlerini Azure kaynaklarında hello yalnızca Azure portalı ve Azure Resource Manager API'leri hello. Azure kaynakları için tüm veri düzeyi işlemleri yetkilendirilemiyor. Örneğin, birisi toomanage depolama hesapları, ancak değil toohello BLOB veya bir depolama hesabı içindeki tabloları olamaz yetki verebilir. Benzer şekilde, bir SQL veritabanı yönetilebilir, ancak içindeki tabloları hello değil.

RBAC'nin erişimi yönetmenize nasıl yardımcı olduğu konusunda daha fazla bilgi isterseniz bkz. [Rol Tabanlı Erişim Denetimi Nedir?](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).

Ayrıca [özel bir rol oluşturmak](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) hello yerleşik roller hiçbiri belirli erişiminizi karşılamıyorsa Azure rol tabanlı erişim denetimi (RBAC) gerekir. Özel roller kullanılarak oluşturulabilir [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure komut satırı arabirimi (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli)ve hello [REST API](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest). Yalnızca yerleşik roller gibi özel roller toousers, grupları ve uygulamaları abonelik, kaynak grubu ve kaynak kapsamları atanabilir.

Her abonelik içinde too2000 rol atamalarını verebilirsiniz.

## <a name="resource-management"></a>Kaynak Yönetimi

Azure başlangıçta yalnızca hello Klasik dağıtım modeli sağlanan. Bu modelde, bağımsız olarak her bir kaynağın var; hiçbir yolu yoktu toogroup ilgili kaynakları birlikte. Bunun yerine, çözüm ya da uygulama yapılan hangi kaynaklara izlemek ve toomanage unutmayın toomanually vardı koordineli bir yaklaşım bunları.

toodeploy bir çözüm, hello Klasik portal üzerinden ayrı ayrı her bir kaynağın veya tüm hello kaynakları hello doğru sırayla dağıtılan bir komut dosyası oluşturmak tooeither vardı. toodelete bir çözüm, sizin toodelete her bir kaynağın ayrı ayrı vardı. Kolayca uygulanır ve ilgili kaynaklar için erişim denetimi ilkeleri güncelleştirin. Son olarak, bunları yardımcı koşullarla kaynaklarınızı izlemek ve faturalama yönetmek etiketleri tooresources toolabel uygulanamadı.

2014'te Azure Kaynak Yöneticisi, bir kaynak grubu hello kavramı eklenen kullanıma sunuldu. Bir kaynak grubu, ortak bir yaşam döngüsü paylaşmak kaynaklar için bir kapsayıcıdır. Merhaba Resource Manager dağıtım modeli çeşitli avantajlar sunar:

- Dağıtmak, yönetmek ve bir Grup yerine bu hizmetleri ayrı ayrı ele çözümünüz için tüm hello hizmetlerini izleyin.

- Art arda çözümünüzü yaşam döngüsü dağıtmak ve kaynaklarınızın tutarlı bir durumda dağıtılması da size güven verir.

- Erişim denetimi tooall kaynakları kaynak grubunuzdaki uygulayabilirsiniz ve yeni kaynaklar toohello kaynak grubuna eklendiğinde bu ilkeleri otomatik olarak uygulanır.

- Etiketleri uygulayabilirsiniz tooresources toologically aboneliğinizdeki tüm hello kaynakları düzenleyin.

- JavaScript nesne gösterimi (JSON) toodefine hello altyapısı çözümünüz için kullanabilirsiniz. Merhaba JSON dosyası Resource Manager şablonu olarak bilinir.

- Merhaba doğru sırayla dağıtılmalarını sağlamak için kaynaklarınız arasındaki hello bağımlılıkları tanımlayabilirsiniz.

![Kaynak Yönetimi](./media/governance-in-azure/security-governance-in-azure-fig4.png)

Resource Manager yönetim, faturalama veya doğal benzeşimi anlamlı gruplar halinde tooput kaynaklar sağlar. Daha önce belirtildiği gibi Azure iki dağıtım modeline sahiptir. Daha önce hello içinde [Klasik modeli](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), hello temel yönetim birimidir hello abonelik oluştu. Abonelikleri çok sayıda toohello oluşturulmasına neden bir abonelik içindeki kaynaklara aşağı zor toobreak oluştu. Merhaba Resource Manager modeli ile kaynak gruplarının hello giriş gördük.

Bir kaynak grubu Azure çözümünü ilgili kaynaklara tutan bir kapsayıcıdır. [Merhaba kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) hello çözüm için tüm hello kaynakları veya yalnızca bir grup olarak toomanage istediğiniz kaynakları içerebilir. Tooallocate kaynakları istediğiniz karar tooresource gruplara göre ne hello en kuruluşunuz için anlamlı üzerinde.

Şablonlar hakkında öneriler için bkz. [Azure Resource Manager şablonları oluşturmaya yönelik en iyi uygulamalar](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

Azure Resource Manager tooensure kaynakları hello doğru sırada oluşturulmasını bağımlılıkları analiz eder. Bir kaynak başka bir kaynaktaki değere bağımlıysa (diskler için depolama hesabına ihtiyaç duyan bir sanal makine gibi) bir bağımlılık ayarlayın.

>[!Note]
>Daha fazla bilgi için bkz. [Azure Resource Manager’da bağımlılıkları tanımlama](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies).

Merhaba şablon güncelleştirmeleri toohello altyapısı için de kullanabilirsiniz. Örneğin, bir kaynak tooyour çözümü ekleyin ve önceden dağıtılan hello kaynaklar için yapılandırma kuralları ekleyin. Merhaba şablonu kaynak zaten olan bir kaynak oluşturulmasını belirtiyorsa, Azure Resource Manager yeni bir varlık oluşturmak yerine bir güncelleştirme gerçekleştirir. Aynı olarak durum azure Resource Manager güncelleştirmelerini hello varolan varlık toohello olarak yeni olacaktır.

Merhaba kurulumunda bulunmayan yazılım yükleme gibi ek işlemlere ihtiyaç resource Manager senaryoları için uzantılar sağlar.

## <a name="resource-tracking"></a>Kaynak İzleme

Kuruluşunuzdaki kullanıcılar kaynakları toohello abonelik ekledikçe giderek önemli tooassociate kaynaklarla hello uygun departmanı, müşteri ve ortam haline gelir. Meta veri tooresources etiketleri aracılığıyla ekleyebilirsiniz. Kullandığınız [etiketleri](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) tooprovide bilgilerini hello kaynak veya hello sahibi. Etiketleri toonot yalnızca toplama ve Grup kaynaklarının çeşitli şekillerde etkinleştirmek, ancak geri ödeme hello amaçları doğrultusunda bu verileri kullanın.

Kaynak grubu ve kaynak karmaşık koleksiyonu vardır ve bu varlıkları hello çoğu algılama tooyou hello şekilde toovisualize gerekir etiketleri kullanın. Örneğin, kuruluşunuzda benzer bir rolü hizmet veya toohello ait olan kaynakları etiketleyebilirsiniz aynı bölüm.

Etiketler, kuruluşunuzdaki kullanıcılar oluşturabilirsiniz olmadan zor toolater olabilir birden çok kaynakları tanımlamak ve yönetmek. Örneğin, bir proje için tüm hello kaynakları toodelete isteyebilir. Bu kaynakları hello projesi için etiketlenir değil, bunları el ile bulmalıdır. Etiketleme, aboneliğinizde tooreduce gereksiz maliyetleri için önemli bir yolu olabilir.

Kaynakları hello tooreside gerek yoktur aynı kaynak grubu tooshare bir etiket. Kuruluşunuzdaki tüm kullanıcıların yanlışlıkla birbirinden kısmen farklı etiketler (örneğin "departman" yerine"") uygulama kullanıcılar yerine genel etiketler kullanmasını kendi etiket sınıflandırma tooensure oluşturabilirsiniz.

Kaynak ilkeleri toocreate standart kurallar, kuruluşunuz için etkinleştirin. Kaynakları hello uygun değerlerle etiketlenir olun ilkeleri oluşturabilirsiniz.

> [!Note]
> Daha fazla bilgi için bkz: [etiketleri için kaynak ilkelerini uygulamak](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags).

Etiketli kaynaklara hello Azure portal aracılığıyla da görüntüleyebilirsiniz.

Merhaba [kullanım raporu](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) aboneliğinizi etiket adları ve değerleri, etiketlere göre toobreak maliyetleri çıkışı sağlayan içerir.

> [!Note]
> Etiketler hakkında daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

aşağıdaki sınırlamalar hello tootags Uygula:

- Her kaynak veya kaynak grubu en fazla 15 etiketi anahtar/değer çifti olabilir. Bu sınırlama yalnızca doğrudan uygulanan tootags toohello kaynak grubu veya kaynak için geçerlidir. Bir kaynak grubu, her 15 etiketi anahtar/değer çiftleri sahip birçok kaynakları içerebilir.

- Merhaba etiket adı sınırlı too512 karakterdir.

- Merhaba etiket değeri sınırlı too256 karakterdir.

- Uygulanan etiketleri toohello kaynak grubu, kaynak grubunda hello kaynaklar tarafından devralınmaz.

15'ten fazla değerleri bir kaynakla tooassociate ihtiyacınız varsa, bir JSON dizesinde hello etiket değeri için kullanın. Merhaba JSON dizesi uygulanan tooa tek etiket anahtarı çok değerler içerebilir.

### <a name="tags-and-billing"></a>Etiketleri ve faturalama

Etiketler, toogroup faturalama verileriniz etkinleştirin. Örneğin, birden çok VM farklı kuruluşlarda çalıştırıyorsanız, hello etiketleri toogroup kullanımını maliyet merkezi tarafından kullanın. Çalışma zamanı ortamı tarafından etiketleri toocategorize maliyetleri de kullanabilirsiniz; gibi üretim ortamında çalışan sanal makineler için fatura kullanım hello.

Merhaba aracılığıyla etiketleri hakkında bilgi alabilir [Azure kaynak kullanımı ve RateCard API'leri](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) veya hello kullanım virgülle ayrılmış değerler (CSV) dosyası. Hello hello kullanım dosyasını karşıdan [Azure hesap portalını](https://account.windowsazure.com/) veya [EA portal](https://ea.azure.com/).

>[!Note]
> Programlı erişim toobilling bilgileri hakkında daha fazla bilgi için bkz: [Microsoft Azure kaynak tüketimini Öngörüler elde](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview). REST API işlemleri için bkz: [Azure faturalama REST API Başvurusu](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).

Faturalama etiketleriyle destekleyen hizmetler için hello kullanım CSV yüklediğinizde hello etiketler hello etiketleri sütununda görünür.

## <a name="critical-resource-controls"></a>Kritik kaynak denetimleri

Kuruluşunuz Çekirdek Hizmetleri toohello abonelik ekler gibi bu hizmetlerin kullanılabilir tooavoid iş kesintisi olduğundan giderek önemli tooensure haline gelir. [Kaynak kilitleri](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) değiştirilmesini veya silinmesini sahip olduğu uygulamalar veya Bulut altyapısı üzerinde önemli bir etkisi yüksek değerli kaynaklar üzerinde toorestrict işlemlerine etkinleştirin. Kilitleri tooa abonelik, kaynak grubuna ya da kaynağa uygulayabilirsiniz. Genellikle, sanal ağlar, ağ geçitleri ve depolama hesapları gibi kilitleri toofoundational kaynaklarına uygulanır.

Kaynak kilitleri şu anda iki değer destekler: CanNotDelete ve salt okunur. Kullanıcılarla (Merhaba uygun hakları) hala CanNotDelete anlamına gelir okuma veya bir kaynak değiştirme ancak bunu silemezsiniz. Salt okunur, yetkili kullanıcıların silemez veya bir kaynak değiştirme olduğunu anlamına gelir.

Resource Manager kilitleri uygulamak çok gönderilen işlemden oluşur hello Yönetim düzeyi içinde gerçekleşen toooperations<https://management.azure.com>. hello kilitleri değil kısıtlamak nasıl kaynakları kendi işlevleri gerçekleştirebilirsiniz. Kaynak kısıtlı değişir, ancak kaynak işlemlerinin sınırlı değildir. Örneğin, bir SQL veritabanında salt okunur kilit silmesini engeller veya hello veritabanı, ancak değiştirme, oluşturma, güncelleştirme ya da hello veritabanındaki verileri silme engellemez.

Uygulama **ReadOnly** gibi görünen bazı işlemler gerektirir ek eylemleri okuma olduğundan toounexpected sonuçları yol açabilir. Örneğin, yerleştirme bir **ReadOnly** bir depolama hesabı üzerinde kilit hello anahtarları listeleme tüm kullanıcıları engeller. yazma işlemlerini hello listesi Hello anahtarların döndürdüğünden anahtarları işlemi bir POST isteği gerçekleştirilir.

![Kritik kaynak denetimleri](./media/governance-in-azure/security-governance-in-azure-fig5.png)

Başka bir örnek için bir uygulama hizmeti kaynakta bir salt okunur kilidi yerleştirme, Visual Studio Sunucu Gezgini'bu etkileşimi yazma erişimi gerektirdiğinden hello kaynak dosyaları görüntülenmesini engeller.

Rol tabanlı erişim denetimi farklı olarak, tüm kullanıcılar ve roller yönetim kilitleri tooapply bir kısıtlama kullanın. Kullanıcılar ve roller için izinleri ayarlama hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure).

Bir üst kapsamda kilit uyguladığınızda, kapsamı içindeki tüm kaynakların hello devral aynı kilitle. Hatta kaynak daha sonra Ekle hello kilit hello üst öğeden devralır. Merhaba en kısıtlayıcı kilit hello Devralmada önceliklidir.

Yönetim kilit toocreate ya da delete erişim tooMicrosoft.Authorization/ olmalıdır _veya Microsoft.Authorization/locks/_ eylemler. Merhaba yerleşik roller, yalnızca **sahibi** ve **kullanıcı erişimi Yöneticisi** bu eylemleri verilir.

## <a name="api-access-toobilling-information"></a>API toobilling bilgilerine erişme

Azure faturalama API'leri toopull kullanımı ve kaynak verileri, tercih edilen veri çözümleme araçları kullanın. Hello Azure kaynak kullanımı ve RateCard API'leri doğru şekilde tahmin etmek ve maliyetlerinizi yönetmenize yardımcı olabilir. Merhaba API'leri bir kaynak sağlayıcısı ve Azure Resource Manager hello tarafından kullanıma sunulan API hello ailesinin bir parçası olarak uygulanır.

### <a name="azure-resource-usage-api-preview"></a>Azure kaynak kullanım API'si (Önizleme)

Kullanım hello Azure [kaynak kullanım API'si](https://msdn.microsoft.com/library/azure/mt219003) tooget tahmini Azure tüketim verilerinizi. Merhaba API içerir:

- **Azure rol tabanlı erişim denetimi** -erişimi yapılandırma hello ilkeleri [Azure portal](https://portal.azure.com/) aracılığıyla veya [Azure PowerShell cmdlet'lerini](https://docs.microsoft.com/powershell/azure/overview) toospecify hangi kullanıcıların veya uygulamaların erişim alabilirsiniz toohello aboneliğin kullanım verileri. Arayanlar, kimlik doğrulaması için standart Azure Active Directory belirteçleri kullanmanız gerekir. Merhaba arayan tooeither hello faturalama Okuyucu, okuyucu, sahibi veya katkıda bulunan rolü tooget erişim toohello kullanım verilerini belirli bir Azure aboneliği için ekleyin.

- **Saatlik veya günlük toplamalar** - arayanlar olup Azure kullanım verilerini saatlik istedikleri aralıkları belirtebilirsiniz veya günlük aralıkları. Merhaba varsayılan günlük.

- **(Kaynak etiketleri içerir) örneği meta veri** – tam Kaynak URI hello gibi örnek düzeyinde ayrıntı almak (/subscriptions/ {subscrıptıon-ID} /..), kaynak grubu bilgileri ve kaynak etiketleri hello. Bu meta veriler belirleyici biçimde yardımcı olur ve program aracılığıyla çapraz ücretlendirme gibi kullanım örnekleri için hello etiketleriyle kullanım paylaştırabilirsiniz.

- **Kaynak meta verilerini** -kaynak ayrıntılarını hello ölçüm adı, ölçüm kategori, ölçüm alt kategorisi, birim ve bölge gibi daha iyi ne tüketilen anlamak hello çağıran verin. Ayrıca tooalign kaynak meta verileri terminolojisi hello Azure portal, Azure kullanım CSV, CSV, faturalama EA ve diğer genel kullanıma yönelik deneyimleri deneyimleri arasında verilerin bağıntısını toolet üzerinde çalışıyoruz.

- **Tüm kullanım teklif türleri** – kullanım verilerini, tüm Kullandıkça Öde, MSDN, parasal taahhüt, kredi ve EA gibi türlerinde sunmak için kullanılabilir.

**Azure kaynak RateCard API (Önizleme)**

Kullanım hello Azure kaynak RateCard API tooget kullanılabilir Azure kaynakları listesini hello ve fiyatlandırma bilgileri her tahmini. Merhaba API içerir:

- **Azure rol tabanlı erişim denetimi** - hello Azure portalı üzerinde erişim ilkelerinizi yapılandırmak veya hangi kullanıcıların veya uygulamaların edinebilirsiniz Azure PowerShell cmdlet'leri toospecify toohello RateCard veri erişim. Arayanlar, kimlik doğrulaması için standart Azure Active Directory belirteçleri kullanmanız gerekir. Merhaba arayan tooeither hello Okuyucu, sahibi veya katkıda bulunan rolü tooget erişim toohello kullanım verilerini belirli bir Azure aboneliği için ekleyin.

- **Kullandıkça Öde, MSDN, parasal taahhüt ve kredi desteği sunar (EA desteklenmiyor)** -bu API Azure teklifi düzeyi oranı bilgi sağlar. Bu API Hello çağıran hello teklif bilgileri tooget kaynak ayrıntıları ve ücretlerin geçmesi gerekir. EA teklifleri kayıt göre oranları özelleştirilmiş olduğundan şu anda işleyemiyor tooprovide EA oranları çalışıyoruz. Merhaba kullanım ve hello RateCard API'leri hello birlikte olası hale getirilen hello senaryolardan bazıları şunlardır:

- **Azure hello ay sırasında harcadığı** -kullanım hello hello kullanım ve RateCard API'leri tooget daha iyi fikir bulut birleşimi hello ay sırasında harcadığı. Hello saatlik çözümleyebilir ve kullanımı ve Ücret günlük demet tahmin eder.

- **Uyarıları ayarlamak** – hello kullanım kullanın ve hello RateCard API'leri tooget tahmini bulut kullanımı ve ücretleri ve kaynak veya parasal tabanlı uyarıları ayarlayın.

- **Fatura tahmin** – tahmini tüketim ve bulut harcamanız ve hangi hello fatura döngüsü faturalama hello hello sonunda olacaktır algoritmaları toopredict öğrenme makinesi geçerli alın.

- **Analiz maliyetiyle öncesi tüketim** – ne kadar faturanızı, beklenen kullanımınız için olacaktır, iş yüklerini tooAzure taşıdığınızda hello RateCard API toopredict kullanın. Var olan iş yükleri diğer Bulut veya özel bulutlara varsa, ayrıca Azure daha iyi bir tahmin harcamanız hello Azure oranları tooget ile kullanımınızı eşleyebilirsiniz. Teklif üzerinde özelliği toopivot hello ve Kullandıkça Öde, ötesinde hello farklı teklif türleri arasında karşılaştırma tahmin kazandırır parasal taahhüt ve kredi gibi. Merhaba API de size hello özelliği toosee maliyet farkları bölgeye göre ve toodo dağıtım kararları yaptığınız benzetim maliyet analiz toohelp sağlar.

- **Çözümlemeleri** -daha fazla uygun maliyetli toorun iş yükünü başka bir bölgede ya da başka bir yapılandırması hello Azure kaynak olup olmadığını belirleyebilirsiniz. Azure kaynak maliyetleri değişebilir kullanmakta olduğunuz Azure bölgesi hello üzerinde temel.

- Başka bir Azure Teklif türü bir Azure kaynağı üzerinde daha iyi oranı sağlar, ayrıca belirleyebilirsiniz.

## <a name="networking-controls"></a>Ağ denetimleri

Erişim tooresources (Merhaba corporation'ın ağından) iç veya dış olabilir (aracılığıyla Internet hello). Kuruluş tooinadvertently put kaynaklarınızı hello yanlış nokta kullanıcılar için kolaydır ve potansiyel olarak bunları toomalicious erişim açın. Olduğu gibi şirket içi / aygıtlar, kuruluşların Azure kullanıcılar hello doğru kararlar, uygun denetimleri tooensure eklemelisiniz.

![Ağ denetimleri](./media/governance-in-azure/security-governance-in-azure-fig6.png)

Abonelik Yönetimi için temel Denetim erişim sağlayan çekirdek kaynakları belirleyin. Merhaba çekirdek kaynakları oluşur:

### <a name="network-connectivity"></a>Ağ bağlantısı

[Sanal ağlar](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) alt ağlar için kapsayıcı nesnelerdir. Kesinlikle gerekli olsa, uygulamaları toointernal şirket kaynaklarına bağlanırken çoğunlukla kullanılır. Merhaba, toosecurely bağlanmak tooeach Azure kaynaklarını diğer sanal ağlar (Vnet'ler) ile Azure Virtual Network service etkinleştirir.

Bir VNet kendi ağ hello bulutta gösterimidir. Bir VNet hello ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının ' dir. Ayrıca, sanal ağlar tooyour şirket ağına bağlanabilir.

Azure sanal ağlar için özellikleri şunlardır:

- **Yalıtım**: sanal ağlar birbirinden yalıtılmış. Bu kullanım hello geliştirme, test ve üretim için ayrı sanal ağlar oluşturabilirsiniz aynı CIDR adres bloklarını. Buna karşılık, ağları birbirine bağlamak ve farklı CIDR adres bloklarını kullanan birden çok sanal ağlar oluşturabilirsiniz. Bir sanal ağ birden çok alt ağa bölebilirsiniz. Azure VM'ler için dahili ad çözümlemesi sağlar ve bulut Hizmetleri rol örnekleri tooa VNet bağlı. Bu gibi durumlarda, bir VNet toouse isteğe bağlı olarak Azure dahili ad çözümlemesi yerine kendi DNS sunucularınızı yapılandırabilirsiniz.

- **Internet bağlantısı**: bağlı tooa VNet sahip tüm Azure sanal makineler (VM) ve bulut Hizmetleri rol örnekleri varsayılan toohello Internet erişim. Gelen erişim toospecific kaynakları, gerektiğinde de etkinleştirebilirsiniz.

- **Azure kaynak bağlantısı**: Bulut Hizmetleri ve sanal makineleri gibi Azure kaynakları bağlı toohello olabilir aynı sanal ağı. Merhaba kaynakları tooeach diğer bağlanabilir özel IP adresleri, farklı alt ağlarda olsalar bile. Azure yoksa tooconfigure ve yollar yönetmek için varsayılan alt ağlar, sanal ağlar ve şirket içi ağlar arasında yönlendirme sağlar.

- **VNet bağlantısı**: sanal ağlar, diğer bağlı tooeach olabilir, kaynakları etkinleştirme bağlı tooany VNet toocommunicate başka bir VNet üzerinde herhangi bir kaynağa sahip.

- **Şirket içi bağlantı**: sanal ağlar hello Internet ağınız ve Azure arasında özel ağ bağlantıları üzerinden veya siteden siteye VPN bağlantısı üzerinden bağlı tooon içi ağlar olabilir.

- **Trafik filtreleme**: rol örneklerini ağ trafiğini VM ve bulut Hizmetleri filtre gelen ve giden kaynak IP adresi ve bağlantı noktası, hedef IP adresi ve bağlantı noktası ve protokolü tarafından.

- **Yönlendirme**: isteğe bağlı olarak, kendi yolları yapılandırmak veya bir ağ geçidi üzerinden BGP yollarını kullanarak yönlendirme Azure'un varsayılan ayarlarını geçersiz kılabilir.

## <a name="network-access-controls"></a>Ağ erişim denetimleri

[Ağ güvenlik grupları](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) gibi bir güvenlik duvarının ve nasıl kaynak "iletişim kurabilirsiniz için" Merhaba ağ üzerinden kurallar sağlar. Nasıl üzerinde ayrıntılı denetim sağlayan / alt ağ (veya sanal makine) toohello Internet veya diğer alt ağlara bağlanabiliyorsa aynı hello sanal ağ.

Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiği tooresources tooAzure sanal ağ (VNet) bağlı güvenlik kurallarının bir listesini içerir. Nsg'ler ilişkili toosubnets, tek tek sanal makineleri (Klasik) olabilir veya tek tek ağ arabirimleri (NIC) tooVMs (Resource Manager) bağlı.

Bir NSG'yi ilişkili tooa alt olduğunda hello kuralları tooall kaynaklara bağlı toohello alt uygulayın. Trafik daha da bir NSG tooa VM veya NIC ilişkilendirerek kısıtlanabilir

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>Güvenlik ve kuruluş standartlarıyla sürekli uyumluluk

Her iş farklı gereksinimleri vardır ve her iş bulut çözümleri den farklı avantajları yararlanmasını. Yine de, her tür müşterilerin hello sahip toohello bulut taşıma hakkında aynı temel sorunları. Tooretain denetim verilerini istedikleri ve tüm saydamlık ve uyumluluk korurken tutulan güvenli ve özel, bu veri toobe istiyor.

Müşterilere bulut sağlayıcılardan istediğinizi aşağıdaki gibidir:

- **Verilerimizi güvenli** artırılmış veri güvenliği ve yönetimsel denetim hello bulut sağlayabilir aktarımının olsa da, BT yöneticileri hala geçirme toohello bulut bunları kendi geçerli değerinden daha savunmasız toohackers bırakın duyarlıdır Şirket içi çözümler.

- **Verilerimizi korumak** özel bulut Hizmetleri işletmeler için benzersiz gizlilik zorlukları Yükselt. Şirketler altyapı maliyetlerini toohello bulut toosave arayın ve kendi esnekliğinde geliştirmek gibi bunlar Ayrıca, verilerini depolandıkları, kimin erişmekte olduğunu ve nasıl kullanıldıkları denetim kaybetme endişesi.

- **Bize denetime** bunlar hello bulut toodeploy daha fazla yenilikçi çözümleri yararlanmak gibi şirket verilerini denetimini kaybetmesini hakkında çok endişe. Son Merhaba açıklamalarına kamu kurumlarının hukuk ve çok yasal yollarla müşteri verilerine erişme bazı CIO verilerini hello buluta depolamaya çok dikkatli olun.

- **Saydamlık Yükselt** güvenlik, gizlilik ve denetim önemli toobusiness karar verenler olsa da, aynı zamanda hello özelliği istedikleri tooindependently doğrulayın nasıl verilerini, erişilen ve güvenli depolanıyor.

- **Uygunluğun sürdürülmesine** kullanımlarını bulut teknolojileri Şirketleri Genişlet gibi hello karmaşıklığı ve standartları ve düzenlemelere kapsamını tooevolve devam eder. Şirketler, kendi uyumluluk standartlarını karşılaması gereken ve o uyumluluk düzenlemeleri değişiklik zaman içinde değiştikçe tooknow gerekir.

## <a name="security-configuration-monitoring-and-alerting"></a>Güvenlik Yapılandırması, izleme ve uyarma

Azure aboneleri yönetim iş istasyonları, geliştirici PC’leri ve hatta göreve özel izinleri bulunan ayrıcalıklı son kullanıcı cihazları dahil birden fazla cihazda kendi bulut ortamlarını yönetebilir. Bazı durumlarda, yönetim işlevleri hello Azure portal gibi web tabanlı konsollar aracılığıyla gerçekleştirilir. Diğer durumlarda, olabilir doğrudan bağlantılar tooAzure şirket içi sistemlerden sanal özel ağlar (VPN), Terminal Hizmetleri, istemci uygulaması protokolleri veya hello Azure Hizmet Yönetimi API'si (SMAPI) (programlı olarak). Ayrıca, istemci uç noktaları ya da etki alanına katılmış veya yalıtılmış ve yönetilmeyen olabilir, tabletler veya akıllı telefonlar gibi.

Birden çok erişim ve yönetim özellikleri zengin bir seçenek kümesi sunmasına karşın, bu değişkenlik önemli riski tooa bulut dağıtımı ekleyebilirsiniz. Zor toomanage olabilir izleme ve denetim yönetim eylemlerini. Ayrıca bu değişkenlik bulut hizmetlerini yönetmek için kullanılan tooclient uç düzenlenmemiş erişim aracılığıyla güvenlik tehditlerine neden olabilir. Altyapı geliştirme ve yönetme amacıyla genel ya da kişisel iş istasyonlarını kullanmak, web’e gözatma (örneğin, su kaynağı saldırıları) ya da e-posta (örneğin, sosyal mühendislik ve kimlik avı) gibi öngörülemeyen tehdit vektörlerini açar.

İzleme, günlüğe kaydetme ve Denetim izleme ve yönetim etkinlikleri anlamak için bir temel sunar ancak ayrıntı toohello oluşturulan veri miktarı nedeniyle tüm eylemlerin tamamlamak uygun tooaudit her zaman olmayabilir. Merhaba hello yönetim ilkelerinin verimliliğini denetlemek en iyi, ancak uygulamadır.

AD DS GPO'ları toocontrol Azure güvenlikten idare tüm hello yöneticinin Windows, dosya paylaşımı gibi arabirimleri. Yönetim iş istasyonlarını denetim, izleme ve günlüğe kaydetme işlemlerine dahil edin. Tüm yönetici ve geliştirici erişimini ve kullanımını izleyin.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi

Merhaba [Azure Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-intro) hello güvenlik hello Aboneliklerde kaynakların durumunu merkezi bir görünümünü sağlar ve tehlike giren kaynaklarını önlemeye yardımcı öneriler sağlar. Daha ayrıntılı ilkelerini (bunlar adresleme kendi duruş toohello risk hello Kurumsal tootailor sağlayan Örneğin, uygulama ilkeleri toospecific kaynak grupları) etkinleştirebilirsiniz.

![Azure Güvenlik Merkezi](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Güvenlik Merkezi, Azure aboneliklerinize arasında tümleşik güvenlik izleme ve ilke yönetimi sağlar, kaçabilecek tehditleri ve güvenlik çözümlerinin geniş ekosistemiyle çalışır algılamaya yardımcı olur. Etkinleştirdikten sonra [güvenlik ilkeleri](https://docs.microsoft.com/azure/security-center/security-center-policies) bir aboneliğin kaynakları için Güvenlik Merkezi, kaynakları tooidentify olası güvenlik açıklarını hello güvenliğini analiz eder. Ağ yapılandırmanız ile ilgili bilgiler hemen kullanımınıza sunulur.

Azure Güvenlik Merkezi, en iyi yöntem analiz ve Güvenlik İlkesi Yönetimi için Azure aboneliği içindeki tüm kaynakların bileşimini temsil eder. Bu güçlü ve kolay toouse araç güvenlik ekiplerinden sağlar ve risk görevlileri tooprevent algılamak ve otomatik olarak toplar ve Azure kaynakları, hello ağ ve gibi iş ortağı çözümlerinden güvenlik verilerini analiz eder gibi toosecurity tehditlerine yanıt kötü amaçlı yazılım programları ve güvenlik duvarları.

Ayrıca, Azure Güvenlik Merkezi Microsoft ürünleri ve Hizmetleri, Microsoft dijital Suçlar birimi (DCU), hello hello Microsoft küresel tehdit bilgilerinden yararlanarak sırasında makine öğrenme ve davranış analizi dahil olmak üzere gelişmiş analizler uygular Güvenlik Yanıt Merkezi (MSRC) ve dış akışların. [Güvenlik idare](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) hello abonelik düzeyinde kapsamlı uygulanabilir veya ilke tanımı kaynaklarına uygulanan ayrıntılı gereksinimler tooindividual toospecific daraltıldığı.

Son olarak, Azure Güvenlik Merkezi bu ilkelerine bağlı olarak kaynak güvenlik durumu analiz eder ve bu tooprovide ayrıntılı panolar ve kötü amaçlı yazılım algılama veya kötü amaçlı bir IP bağlantısı gibi olaylar için deneme uyarı kullanır.

>[!Note]
> Hakkında daha fazla bilgi için okuma tooapply önerileri [Azure Güvenlik Merkezi'nde güvenlik önerilerini uygulama](https://docs.microsoft.com/azure/security-center/security-center-recommendations).

Güvenlik Merkezi, sanal makineleri tooassess güvenlik durumlarına toplar, güvenlik önerileri sağlamak ve toothreats sizi uyarır. Güvenlik Merkezi ilk eriştiğinizde, veri toplama, aboneliğinizin tüm sanal makinelerin etkinleştirilir. Veri toplama önerilir ancak, tarafından çevirin [veri toplamayı devre dışı bırakma](https://docs.microsoft.com/azure/security-center/security-center-faq) hello Güvenlik Merkezi ilke içinde.

Son olarak, Azure Güvenlik Merkezi, Microsoft iş ortakları ve Azure Güvenlik Merkezi tooenhance yeteneklerini takılan bağımsız yazılım satıcıları toocreate yazılım sağlayan bir açık platformudur.

Azure Güvenlik Merkezi, Azure kaynaklarını aşağıdaki hello izler:

- Sanal makineler (VM'ler) (bulut Hizmetleri dahil)

- Azure Sanal Ağları

- Azure SQL Hizmeti

- İş ortağı çözümleri gibi bir web uygulaması güvenlik duvarı sanal makineleri ve üzerinde Azure aboneliğinizle tümleşik [uygulama hizmeti ortamı](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme).

### <a name="operations-management-suite"></a>Operations Management Suite

Merhaba OMS yazılım geliştirme ve hizmeti ekibin bilgi güvenliği ve [idare program](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) toolaws ve düzenlemelere konusunda açıklandığı gibi aynılarını ve kendi iş gereksinimlerini destekleyen [Microsoft Azure Trust Center ](https://azure.microsoft.com/support/trust-center/) ve [Microsoft Güven Merkezi Uyumluluk](https://www.microsoft.com/TrustCenter/Compliance/default.aspx). Nasıl OMS güvenlik gereksinimlerini belirlemek, güvenlik denetimleri tanımlar, yönetir ve riskleri izleyen de açıklanmaktadır vardır. Yıllık, biz gözden geçirme ilkeler, standartlar, yordamlar ve yönergeleri.

Her OMS geliştirme ekibi üyesi resmi uygulama güvenlik eğitimi alır. Dahili olarak, sürüm denetimi sistemi yazılım geliştirme için kullanırız. Her yazılım projesi hello sürüm denetimi sistemi tarafından korunur.

Microsoft, denetlediği ve tüm Microsoft hizmetlerinde değerlendirir güvenlik ve uyumluluk bir ekip sahiptir. Bilgi güvenliği görevlileri hello takım yapmak ve bunlar OMS geliştirmek Departmanlar mühendislik hello ile ilişkili değil. Merhaba güvenlik görevlileri kendi yönetim zinciri sahip ve ürün ve Hizmetleri tooensure güvenlik ve uyumluluk bağımsız değerlendirmeleri yürütün.

Operations Management Suite (OMS olarak da bilinir) hello başından hello bulutta tasarlanmış Yönetim Hizmetleri koleksiyonudur. Dağıtma ve şirket içi kaynakları yönetmek yerine, OMS bileşenleri tamamen Azure'da barındırılır. Çok az yapılandırma gerektirir ve yalnızca birkaç dakikada kullanmaya başlayabilirsiniz.

![Operations Manager paketi](./media/governance-in-azure/security-governance-in-azure-fig8.png)

Yalnızca OMS hizmetlerini çalıştırmak için hello bulut bunlar etkili bir şekilde şirket içi ortamınız yönetemez anlamına gelmez.

Bir aracı üzerinde herhangi bir Windows put veya Linux bilgisayarı veri merkezinizi ve bunu diğer verilerle birlikte burada çözümlenebilir Analytics Bulut veya şirket içi Hizmetleri toplanan verileri tooLog gönderir. Şirket içi kaynaklar için yedekleme ve yüksek kullanılabilirlik için Azure Backup ve Azure Site Recovery tooleverage hello bulut kullanın.

Runbook'ları hello bulutta şirket içi kaynaklarınıza genellikle erişemiyor, ancak bir veya daha fazla bilgisayara bir aracı yükleyebilirsiniz çok barındıracak runbook'ları veri merkezinizdeki. Bir runbook'u başlattığınızda, yalnızca toorun hello bulutta veya yerel bir çalışan üzerinde istediğinizi belirtin.

OMS Hello çekirdek işlevselliğini Azure üzerinde çalışan hizmetleri kümesi tarafından sağlanır. Her hizmet belirli yönetim işlevi sağlar ve Hizmetleri tooachieve farklı yönetim senaryoları birleştirebilirsiniz.

![Operations Manager paketi](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure işlem yöneticisi, kendi işlevler yönetim çözümleri sağlayarak genişletir. [Yönetim çözümleri](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) bir veya daha fazla OMS Hizmetleri yararlanarak Yönetimi senaryosu uygulayan paketlenmiş mantığı kümeleridir.

![Azure işlemi yönetme](./media/governance-in-azure/security-governance-in-azure-fig10.png)

Farklı çözümler, Microsoft'un ve iş ortakları OMS tooyour Azure aboneliği tooincrease hello yatırımınızı değerini kolayca ekleyebilirsiniz kullanılabilir.

Bir iş ortağı, kendi çözümleri toosupport uygulamaları ve hizmetleri oluşturmak ve bunları hello Azure Marketi veya hızlı başlangıç şablonlarından aracılığıyla toousers sağlayın.

## <a name="performance-alerting-and-monitoring"></a>Performans uyarı verme ve izleme

### <a name="alerting"></a>Uyarı

Azure kaynak ölçümleri, olayları ve günlükleri izleme yöntemi uyarılar ve bir koşul belirttiğinizde bildirilmesini karşılanır.

**Farklı Azure Hizmetleri uyarıları**

Uyarılar dahil olmak üzere farklı Hizmetleri kullanılabilir:

- Application Insights: web testi ve ölçüm uyarılar sağlar.

>[!Note]
> Bkz: [Application Insights'ta uyarıları ayarlama](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) ve [izlemek kullanılabilirlik ve yanıt herhangi bir Web sitesinin](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability).

- Günlük analizi (Operations Management Suite): hello etkinliği ve tanılama günlüklerini tooLog Analytics yönlendirme sağlar. Operations Management Suite, ölçüm, günlük ve diğer uyarı türleri sağlar.

>[!Note]
> Daha fazla bilgi için bkz [günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts).

- Azure İzleyici: ölçüm değerleri ve etkinlik günlüğü olaylarını göre uyarıları sağlar. Merhaba kullanabilirsiniz [Azure İzleyici REST API](https://msdn.microsoft.com/library/dn931943.aspx) toomanage uyarıları.

>[!Note]
> Daha fazla bilgi için bkz: [hello Azure portal, PowerShell veya hello komut satırı arabirimi toocreate uyarıları kullanarak](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal).

### <a name="monitoring"></a>İzleme

Performans sorunlarını bulut uygulamanızda iş etkileyebilir. Birden çok birbirine bağlı bileşenleri ve sık sürümleri ile degradations herhangi bir zamanda oluşabilir. Ve kullanıcılarınızın bir uygulama geliştiriyorsanız, genellikle testinde bulamadı sorunları keşfedin. Bu hemen bilmeniz ve hello sorunlarını tanılamak ve araçları olması gerekir. Microsoft Azure Araçları bu sorunları tanımlamak için bir aralığı yok.

**Azure bulut uygulamalarım nasıl izlerim?**

Çeşitli araçlar Azure uygulamaları ve Hizmetleri izleme yoktur. Bazı özelliklerine çakışıyor. Geliştirme ve bir uygulamanın işlemi toohello Bulanıklaştırma son kısmen ve kısmen geçmiş nedenlerle budur.

Merhaba asıl araçlar şunlardır:

- **Azure İzleyici** Azure üzerinde çalışan hizmetleri izlemek için temel araçtır. Altyapı düzeyinde veri hizmeti ve ortam çevreleyen hello hello işleme hakkında sağlar. Uygulamalarınızda tüm Azure yönetiyorsanız, yukarı veya aşağı kaynakları tooscale, ardından Azure İzleyicisi, ne kullandığınız sunar olup olmadığını karar toostart.

- **Application Insights** geliştirme için ve bir üretim izleme çözümü olarak kullanılabilir. Uygulamanıza bir paketi yükleyerek çalışır ve bu nedenle neler olup bittiğini daha iç bir görünümünü sağlar. Verileri bağımlılıkları, özel durum izleme, anlık görüntüler, yürütme profilleri hata ayıklama yanıt sürelerini içerir. Güçlü akıllı araçlar bu telemetri çözümlemek için bir uygulama ve hangi kullanıcıların ile yaptıklarını anlamak toohelp hata ayıklama hem toohelp sağlar. Bir ani artış yanıt süreleri nedeniyle mi olduğunu anlayabilirsiniz toosomething bir uygulama ya da dış bazı resourcing sorun. Bunu düzeltmek için Visual Studio kullanıyorsanız ve hello uygulama hataya neden olduğunu, doğru toohello sorun satır kod alınabilir.

- **Günlük analizi** tootune performans ve planı bakım üretimde çalışan uygulamalara gereksinim duyan olanlar içindir. Azure'da temel alır. Toplar ve 10 too15 dakikalık bir gecikme olsa birçok kaynaktan verileri toplar. Azure için bir bütünsel BT yönetim çözümü sunar şirket içi ve üçüncü taraf bulut tabanlı altyapı (örneğin, Amazon Web Hizmetleri). Daha zengin araçları tooanalyze veri arasında daha fazla kaynaklarına sağlar, karmaşık sorgular tüm günlükleri sağlar ve belirtilen koşullara proaktif olarak uyarabilir. Özel verileri sorgulamak ve onu görselleştirmek için kendi merkezi depoya bile toplayabilirsiniz.

- **System Center Operations Manager (SCOM)** yönetme ve büyük bulut yüklemeleri izleme içindir. Zaten bir yönetim aracı için Windows Server ve Hyper-V tabanlı Bulutlar şirket içi ancak aynı zamanda tümleştirileceğini ve Azure uygulamalarını yönetme gibi ile bilgi sahibi olmanız. Bunun yanı sıra, Application Insights mevcut Canlı uygulamaları yükleyebilirsiniz. Bir uygulama kullanılamaz hale gelirse, saniye cinsinden belirtir.


## <a name="next-steps"></a>Sonraki adımlar

- [En iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices).

- [Azure aboneliği idare uygulamanın örnekleri](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples).

- [Microsoft Azure kamu](https://docs.microsoft.com/azure/azure-government/).
