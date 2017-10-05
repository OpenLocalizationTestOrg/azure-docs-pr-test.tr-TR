---
title: "Azure anahtar kasası Geliştirici Kılavuzu"
description: "Geliştiriciler, Azure anahtar kasası, Microsoft Azure ortamı içindeki şifreleme anahtarlarını yönetmek için kullanabilirsiniz."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: fec4769c0bd571edea84dd2f766bb907d8819be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-developers-guide"></a>Azure anahtar kasası Geliştirici Kılavuzu

Anahtar kasası uygulamalarınızı hassas bilgileri güvenli bir şekilde erişmenize olanak tanır:

- Kodu kendiniz yazmak zorunda kalmadan anahtarları ve gizli anahtarları korunur ve bunları uygulamalarınızdan kolayca kullanabilirsiniz.
- Müşterilerinizin kendi ve çekirdek yazılım özelliklerini sağlamaya yoğunlaşabilirsiniz şekilde kendi anahtarlarını yönetmek kullanabilirsiniz. Bu şekilde, uygulamalarınızı sorumluluk veya olası yükümlülük müşterilerinizin Kiracı anahtarları ve gizli anahtarları sahip olacağını değil.
- Uygulamanızı imzalamak için tuşlarını kullanabilirsiniz ve anahtar yönetimi şifreleme henüz coğrafi olarak dağıtılmış bir uygulama olarak uygun olması, çözümünüzün izin vererek uygulamanızdan dış tutar.
- Anahtar kasası Eylül 2016 güncelleştirmesinden itibaren uygulamalarınızı artık anahtar kasası kullanabilir [Sertifikalar](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Daha fazla bilgi için bkz: [anahtarları, gizli ve sertifikaları hakkında](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Azure anahtar kasası hakkında daha fazla genel bilgi için bkz: [anahtar kasası nedir](key-vault-whatis.md).

## <a name="public-previews"></a>Genel Önizleme

Düzenli olarak yeni bir anahtar kasası özelliği genel önizlemesini bırakın. Lütfen bu deneyin ve aracılığıyla düşüncelerinizi bize bildirin azurekeyvault@microsoft.com, bizim geri bildirim e-posta adresi.

### <a name="storage-account-keys---july-10-2017"></a>Depolama hesabı anahtarları - 10 Temmuz 2017

>[!NOTE]
>Azure anahtar kasası bu güncelleştirmeleri yalnızca **depolama hesabı anahtarlarını** Önizleme'de bir özelliktir.

Bu önizleme yeni depolama hesabı anahtarlarını özelliğimizi, bu arabirimleri aracılığıyla kullanılabilir içerir; [.NET / C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) ve [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Yeni depolama hesabı anahtarlarını özelliği hakkında daha fazla bilgi için bkz: [Azure anahtar kasası depolama hesabı anahtarları genel bakış](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Videolar

Bu videoda, anahtar kasanızı oluşturmak nasıl ve 'Hello anahtar Kasası' örnek uygulamadan kullanma gösterir.

- [Anahtar kasası Geliştirici - Hızlı Başlangıç Kılavuzu](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Video belirtilen kaynaklar:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Azure anahtar kasası örnek kod](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Oluşturma ve anahtar kasalarını yönetme

Kodunuzu Azure anahtar kasası ile çalışmaya başlamadan önce oluşturabilir ve aşağıdaki makalelerde açıklanan kasalarını REST, Resource Manager şablonları, PowerShell veya CLI, aracılığıyla yönetebilirsiniz:

- [Oluşturma ve REST ile anahtar kasalarını yönetme](https://docs.microsoft.com/rest/api/keyvault/)
- [Oluşturma ve anahtar kasalarını PowerShell ile yönetme](key-vault-get-started.md)
- [Oluşturma ve anahtar kasalarını CLI ile yönetme](key-vault-manage-with-cli2.md)
- [Bir anahtar kasası oluşturun ve Azure Resource Manager şablonu aracılığıyla bir gizlilik ekleyin](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Anahtar kasalarını karşı işlemleri AAD ile kimlik doğrulaması ve kasa tanımlı anahtar Kasası'nın kendi erişim ilkesiyle yetkili.

## <a name="coding-with-key-vault"></a>Anahtar kasası ile kodlama

Anahtar kasası yönetim sistemi programcıları için temel olarak REST ile çeşitli arabirimler oluşur. REST arabirimi aracılığıyla tüm anahtar kasalarını kaynaklarınız erişilebilir; anahtarları, gizli ve sertifikalar. [Anahtar kasası REST API Başvurusu](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Desteklenen programlama dilleri

#### <a name="net"></a>.NET

- [.NET API refence anahtar kasası için](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

.NET SDK'sı 2.x sürümü hakkında daha fazla bilgi için bkz: [sürüm notları](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java anahtar kasası için SDK'sı](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

Node.js içinde kasa yönetim API'si ve kasa nesne API ayrıdır. Anahtar kasası yönetim oluşturma ve anahtar kasanızı güncelleştirme sağlar. Anahtar kasası işlemleri gibi kasası nesnelerle çalışmak için API'dir; anahtarları, gizli ve sertifikalar. 

- [Anahtar kasası yönetimi için node.js API Başvurusu](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Anahtar kasası işlemleri için node.js API Başvurusu](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Hızlı başlangıç

- [Anahtar kasası oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Node.js içinde anahtar kasası ile çalışmaya başlama](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Kod örnekleri

Anahtar kasası uygulamalarınızla kullanarak tüm örnekler için bkz:

- [Azure anahtar kasası kod örnekleri](http://www.microsoft.com/download/details.aspx?id=45343) -.NET örnek uygulaması *HelloKeyVault* ve bir Azure web hizmeti örneği. 
- [Azure anahtar kasası bir Web uygulamasından kullanma](key-vault-use-from-web-application.md) -öğretici bir Azure web uygulamasından Azure anahtar kasası kullanmayı öğrenmenize yardımcı olacak. 

## <a name="how-tos"></a>Nasıl yapılır makaleleri

Aşağıdaki makaleler ve senaryoları Azure anahtar kasası ile çalışmaya yönelik görev özgü yönergeler sağlar:

- [Değişiklik anahtar kasası Kiracı kimliği abonelik sonra taşıma](key-vault-subscription-move-fix.md) - Kiracı B, A kiracıdan, Azure aboneliğinizin taşıdığınızda varolan anahtar kasalarınıza kiracısında B. Bu kılavuzu kullanarak bu düzeltme ilkelerini (kullanıcılar ve uygulamalar) tarafından erişilemez.
- [Anahtar kasası güvenlik duvarının arkasında erişme](key-vault-access-behind-firewall.md) - anahtar kasasını istemci uygulamanız gereken çeşitli işlevler için birden çok uç noktalarının erişebilmeleri için bir anahtar kasası erişmek için.
- [Oluşturma ve Transfer HSM-Protected anahtarları Azure anahtar kasası için nasıl](key-vault-hsm-protected-keys.md) -Bu, planlama, oluşturma ve ardından Azure anahtar kasası ile kullanmak üzere kendi HSM korumalı anahtarları aktarma yardımcı olur.
- [Dağıtım sırasında (parolalar gibi) güvenli değerleri geçirmek nasıl](../azure-resource-manager/resource-manager-keyvault-parameter.md) - güvenli bir değerle (örneğin, parola), dağıtım sırasında bir parametre olarak geçirmek gerektiğinde bu değeri bir Azure anahtar Kasası'nda bir gizli olarak depolamak ve diğer kaynak değerinde başvuru Manager şablonları.
- [SQL Server ile Genişletilebilir anahtar yönetimi için anahtar kasası kullanmayı](https://msdn.microsoft.com/library/dn198405.aspx) -SQL Server ve VM, SQL Azure anahtar kasası hizmetindeki korumak için bir Genişletilebilir anahtar yönetimi (EKM) sağlayıcısı olarak yararlanmak Azure anahtar kasası için SQL Server Bağlayıcısı sağlar, uygulamaları bağlantı için şifreleme anahtarları; Saydam veri şifreleme, yedek şifreleme ve sütun düzeyinde şifreleme.
- [Anahtar Kasası'nı VM'ler için sertifikaları dağıtma konusunda](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - Azure gereksinimlerine göre bir sertifika bir VM'de çalıştıran bir bulut uygulaması. Bu sertifika bu VM'de oturum bugün nereden?
- [Anahtar kasası uçtan uca anahtar döndürme ve Denetim ile nasıl ayarlanacağını](key-vault-key-rotation-log-monitoring.md) - bu anahtar döndürme ayarlama anlatılmaktadır ve Azure anahtar kasası ile denetleme.
- [Anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) parçası olarak anahtar kasasında depolanan sertifikaları dağıtmak için adım adım yönergeler sağlar [uygulama hizmet sertifikası](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) sunar.
- [Bir anahtar kasası erişmek için birçok uygulamalara iznini](key-vault-group-permissions-for-apps.md) anahtar kasası erişim denetimi ilkesini yalnızca 16 girişleri destekler. Ancak, bir Azure Active Directory güvenlik grubu oluşturabilirsiniz. Tüm ilişkili hizmet asıl adı bu güvenlik grubuna ekleyin ve bu anahtar kasası güvenlik grubuna erişim hakkı.
- Tümleştirme ve anahtar kasalarını Azure ile kullanma hakkında daha fazla görev özgü yönergeler için bkz: [Ryan CAN Azure Resource Manager şablonu örnekleri anahtar kasası için](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Anahtar kasası soft-delete CLI ile kullanmak nasıl](key-vault-soft-delete-cli.md) soft-etkin delete ile kullanın ve bir anahtar kasası ve çeşitli anahtar kasası nesnelerin ömrü aracılığıyla kılavuzluk eder.
- [Anahtar kasası soft-delete PowerShell ile kullanmak nasıl](key-vault-soft-delete-powershell.md) soft-etkin delete ile kullanın ve bir anahtar kasası ve çeşitli anahtar kasası nesnelerin ömrü aracılığıyla kılavuzluk eder.

## <a name="integrated-with-key-vault"></a>Anahtar kasası ile tümleşik

Bu makaleler, diğer senaryolar ve kullanın veya anahtar kasası ile tümleştirme hizmetleri hakkında ilgilidir.

- [Azure Disk şifrelemesi](../security/azure-security-disk-encryption.md) endüstri standardı yararlanır [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) Windows özelliğidir ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux işletim sistemi ve veri diskleri için birim şifrelemesi sağlamak için özelliğidir. Çözüm denetlemek ve disk şifreleme anahtarları ve gizli anahtarları Azure depolama alanınızı bekleyen sanal makine disklerdeki tüm veriler şifrelenir sağlarken anahtar kasası aboneliğinizde yönetmenize yardımcı olmak için Azure anahtar kasası ile tümleşiktir.
- [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) hesapta depolanan verilerin şifrelenmesi için seçeneği sağlar. Anahtar Yönetimi için Data Lake Store'da depolanan verilerin şifresini çözmek için gerekli olan ana şifreleme anahtarlarınızı (MEKs) yönetmek için Data Lake Store iki mod sağlar. Data Lake Store MEKs yönettiğiniz ya da Azure anahtar kasası hesabınızı kullanarak MEKs sahipliğini tutmayı seçin ya da izin verebilirsiniz. Bir Data Lake Store hesabı oluşturulurken anahtar yönetimi modunu belirtin. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) kendi Kiracı anahtarınızı yöneticisine sağlar. Örneğin, Kiracı anahtarınızı (varsayılan) yönetme Microsoft yerine, kuruluşunuz için geçerli olan belirli düzenlemelere uymak üzere kendi Kiracı anahtarınızı yönetebilirsiniz. Kendi Kiracı anahtarınızı yönetme olarak kendi anahtarını Getir veya BYOK için de denir.

## <a name="key-vault-overviews-and-concepts"></a>Anahtar kasası genel bakışlar ve kavramları

- [Anahtar kasası soft-silme davranışı](key-vault-ovw-soft-delete.md) silinen nesnelerin kurtarma sağlayan bir özelliği yanlışlıkla veya kasıtlı silme olup olmadığını açıklar.
- [Anahtar kasası istemci azaltma](key-vault-ovw-throttling.md) hızlandırma temel kavramları yönlendirir ve uygulamanız için bir yaklaşım sunmaktadır.
- [Anahtar kasası depolama hesabı anahtarları genel bakış](key-vault-ovw-storage-keys.md) anahtar kasası tümleştirme Azure depolama hesapları anahtarları açıklar.
- [Anahtar kasası güvenlik dünyaları](key-vault-ovw-security-worlds.md) bölgeler ve güvenlik alanları arasındaki ilişkileri açıklar.

## <a name="social"></a>Sosyal

- [Anahtar kasası blogu](http://aka.ms/kvblog)
- [Anahtar kasası Forumu](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Kitaplıkları destekleme

- [Microsoft Azure anahtar kasası çekirdek Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) sağlar **IKey** ve **IKeyResolver** tanımlayıcıları anahtarları bulma ve anahtarlarla işlemleri gerçekleştirmek için arabirim.
- [Microsoft Azure anahtar kasası uzantıları](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) Azure anahtar kasası için genişletilmiş yetenekleri sağlar.


