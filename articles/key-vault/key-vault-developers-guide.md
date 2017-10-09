---
title: "aaaAzure anahtar kasası Geliştirici Kılavuzu"
description: "Geliştiriciler hello Microsoft Azure ortamında toomanage şifreleme anahtarları Azure anahtar kasası kullanabilir."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Azure anahtar kasası Geliştirici Kılavuzu

Anahtar kasası toosecurely erişim hassas bilgileri uygulamalarınızdaki sağlar:

- Anahtarları ve gizli anahtarları korunmasını toowrite hello kodu kendiniz gerek kalmadan ve kolayca mümkün toouse olduğunuz atamalarını uygulamalarınızı kaldırın.
- Müşterileriniz kendi mümkün toohave olacaktır ve hello çekirdek yazılım özelliklerini sağlamaya yoğunlaşabilirsiniz şekilde kendi anahtarları Yönet. Bu şekilde, uygulamalarınızı hello sorumluluk veya olası yükümlülük müşterilerinizin Kiracı anahtarları ve gizli anahtarları sahip olacağını değil.
- Uygulamanızı imzalamak için tuşlarını kullanabilirsiniz ve şifreleme henüz hello anahtar yönetimi çözümü toobe coğrafi olarak dağıtılmış bir uygulama olarak uygun izin vererek uygulamanızdan dış tutar.
- İtibariyle Hello Eylül 2016 sürümü anahtar kasası, uygulamalarınızı artık anahtar kasası kullanabilir [Sertifikalar](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Daha fazla bilgi için bkz: [anahtarları, gizli ve sertifikaları hakkında](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Azure anahtar kasası hakkında daha fazla genel bilgi için bkz: [anahtar kasası nedir](key-vault-whatis.md).

## <a name="public-previews"></a>Genel Önizleme

Düzenli olarak yeni bir anahtar kasası özelliği genel önizlemesini bırakın. Lütfen bu deneyin ve aracılığıyla düşüncelerinizi bize bildirin azurekeyvault@microsoft.com, bizim geri bildirim e-posta adresi.

### <a name="storage-account-keys---july-10-2017"></a>Depolama hesabı anahtarları - 10 Temmuz 2017

>[!NOTE]
>Azure anahtar kasası yalnızca Merhaba, bu güncelleştirme için **depolama hesabı anahtarlarını** Önizleme'de bir özelliktir.

Bu önizleme yeni depolama hesabı anahtarlarını özelliğimizi, bu arabirimleri aracılığıyla kullanılabilir içerir; [.NET / C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) ve [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Merhaba yeni depolama hesabı anahtarlarını özelliği hakkında daha fazla bilgi için bkz: [Azure anahtar kasası depolama hesabı anahtarları genel bakış](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Videolar

Bu video toocreate kendi anahtarınızı kasa nasıl ve ne gösterir toouse hello 'Hello anahtar Kasası' örnek uygulaması ondan.

- [Anahtar kasası Geliştirici - Hızlı Başlangıç Kılavuzu](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Video belirtilen kaynaklar:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Azure anahtar kasası örnek kod](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Oluşturma ve anahtar kasalarını yönetme

Kodunuzda Azure anahtar kasası ile çalışmaya başlamadan önce oluşturabilir ve makaleler hello açıklandığı gibi REST, Resource Manager şablonları, PowerShell veya CLI, aracılığıyla kasalarını yönetebilirsiniz:

- [Oluşturma ve REST ile anahtar kasalarını yönetme](https://docs.microsoft.com/rest/api/keyvault/)
- [Oluşturma ve anahtar kasalarını PowerShell ile yönetme](key-vault-get-started.md)
- [Oluşturma ve anahtar kasalarını CLI ile yönetme](key-vault-manage-with-cli2.md)
- [Bir anahtar kasası oluşturun ve Azure Resource Manager şablonu aracılığıyla bir gizlilik ekleyin](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Anahtar kasalarını karşı işlemleri AAD ile kimlik doğrulaması ve kasa tanımlı anahtar Kasası'nın kendi erişim ilkesiyle yetkili.

## <a name="coding-with-key-vault"></a>Anahtar kasası ile kodlama

Merhaba anahtar kasası yönetim sistemi programcıları için REST hello foundation olarak olan birkaç arabirimler oluşur. Merhaba REST arabirimi aracılığıyla tüm anahtar kasalarını kaynaklarınız erişilebilir; anahtarları, gizli ve sertifikalar. [Anahtar kasası REST API Başvurusu](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Desteklenen programlama dilleri

#### <a name="net"></a>.NET

- [.NET API refence anahtar kasası için](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Merhaba hello 2.x hello .NET SDK sürümü hakkında daha fazla bilgi için bkz: [sürüm notları](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java anahtar kasası için SDK'sı](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

Node.js içinde hello kasa yönetim API'si ve hello kasası nesne API ayrıdır. Anahtar kasası yönetim oluşturma ve anahtar kasanızı güncelleştirme sağlar. Anahtar kasası işlemleri gibi kasası nesnelerle çalışmak için API'dir; anahtarları, gizli ve sertifikalar. 

- [Anahtar kasası yönetimi için node.js API Başvurusu](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Anahtar kasası işlemleri için node.js API Başvurusu](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Hızlı başlangıç

- [Anahtar kasası oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Node.js içinde anahtar kasası ile çalışmaya başlama](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Kod örnekleri

Anahtar kasası uygulamalarınızla kullanarak tüm örnekler için bkz:

- [Azure anahtar kasası kod örnekleri](http://www.microsoft.com/download/details.aspx?id=45343) -.NET örnek uygulaması *HelloKeyVault* ve bir Azure web hizmeti örneği. 
- [Azure anahtar kasası bir Web uygulamasından kullanma](key-vault-use-from-web-application.md) -öğrenin toouse Azure anahtar kasası nasıl Azure web uygulamasından Öğreticisi toohelp. 

## <a name="how-tos"></a>Nasıl yapılır makaleleri

Merhaba Aşağıdaki makaleler ve senaryoları Azure anahtar kasası ile çalışmaya yönelik görev özgü rehberlik sağlar:

- [Değişiklik anahtar kasası Kiracı kimliği abonelik sonra taşıma](key-vault-subscription-move-fix.md) - ne zaman, Azure aboneliğinizin Kiracı tootenant B ' taşıdığınızda, varolan anahtar kasalarınıza kiracısında B. Bu kılavuzu kullanarak bu düzeltme hello ilkelerini (kullanıcılar ve uygulamalar) tarafından erişilemez.
- [Anahtar kasası güvenlik duvarının arkasında erişme](key-vault-access-behind-firewall.md) -tooaccess bir anahtar kasası, anahtar kasası istemci uygulama gereksinimlerini toobe mümkün tooaccess çeşitli işlevler için birden çok uç nokta sabittir.
- [Nasıl tooGenerate ve Transfer HSM-Protected anahtarları Azure anahtar kasası için](key-vault-hsm-protected-keys.md) -Bu, planlama, oluşturma ve ardından Azure anahtar kasası ile kendi HSM korumalı anahtarlar toouse aktarma yardımcı olur.
- [Toopass dağıtım sırasında değerleri (parolalar gibi) güvenliğini nasıl](../azure-resource-manager/resource-manager-keyvault-parameter.md) - dağıtım sırasında bir parametre olarak toopass (örneğin, parola) güvenli bir değerle gerektiğinde bir Azure anahtar kasası ve başvuru hello değerindeki diğer gizli olarak değeri depola Resource Manager şablonları.
- [Nasıl SQL Server ile Genişletilebilir anahtar yönetimi için anahtar kasası toouse](https://msdn.microsoft.com/library/dn198405.aspx) -SQL Server ve VM içinde SQL tooleverage hello Azure anahtar kasası hizmetine bir Genişletilebilir anahtar yönetimi (EKM) sağlayıcısı olarak Azure anahtar kasası sağlar, SQL Server Connector hello tooprotect uygulamaları bağlantı için şifreleme anahtarları; Saydam veri şifreleme, yedek şifreleme ve sütun düzeyinde şifreleme.
- [Nasıl toodeploy sertifikaları tooVMs anahtar Kasası'ndan](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - Azure gereksinimlerine göre bir sertifika bir VM'de çalıştıran bir bulut uygulaması. Bu sertifika bu VM'de oturum bugün nereden?
- [Anahtar kasası yukarı tooset son tooend ile nasıl anahtar döndürme ve Denetim](key-vault-key-rotation-log-monitoring.md) -bu nasıl anlatılmaktadır tooset anahtar döndürme ve Azure anahtar kasası ile denetleme.
- [Anahtar kasası aracılığıyla Azure Web uygulaması sertifikası dağıtma]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) parçası olarak anahtar kasasında depolanan sertifikaları dağıtmak için adım adım yönergeler sağlar [uygulama hizmet sertifikası](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) sunar.
- [Bir anahtar kasası izni toomany uygulamaları tooaccess vermek](key-vault-group-permissions-for-apps.md) anahtar kasası erişim denetimi ilkesini yalnızca 16 girişleri destekler. Ancak, bir Azure Active Directory güvenlik grubu oluşturabilirsiniz. Tüm hello ilişkilendirilmiş hizmet sorumluları toothis güvenlik grubu ve ardından erişim toothis güvenlik grubu tooKey kasası verin ekleyin.
- Tümleştirme ve anahtar kasalarını Azure ile kullanma hakkında daha fazla görev özgü yönergeler için bkz: [Ryan CAN Azure Resource Manager şablonu örnekleri anahtar kasası için](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Nasıl toouse anahtar kasası soft-delete CLI ile](key-vault-soft-delete-cli.md) soft-etkin delete ile Merhaba kullanın ve bir anahtar kasası ve çeşitli anahtar kasası nesnelerin ömrü aracılığıyla kılavuzluk eder.
- [Nasıl toouse anahtar kasası soft-delete PowerShell ile](key-vault-soft-delete-powershell.md) soft-etkin delete ile Merhaba kullanın ve bir anahtar kasası ve çeşitli anahtar kasası nesnelerin ömrü aracılığıyla kılavuzluk eder.

## <a name="integrated-with-key-vault"></a>Anahtar kasası ile tümleşik

Bu makaleler, diğer senaryolar ve kullanın veya anahtar kasası ile tümleştirme hizmetleri hakkında ilgilidir.

- [Azure Disk şifrelemesi](../security/azure-security-disk-encryption.md) yararlanır hello endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) özelliği Windows hello ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooprovide birim şifrelemesi hello işletim sistemi ve hello veri özelliği diskler. Merhaba çözüm denetlemek ve hello disk şifreleme anahtarları ve gizli anahtarları Azure depolama alanınızı bekleyen hello sanal makine disklerdeki tüm veriler şifrelenir sağlarken anahtar kasası aboneliğinizi yönetmek Azure anahtar kasası toohelp tümleşiktir.
- [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) hello hesapta depolanan verilerin şifrelenmesi için seçeneği sağlar. Anahtar Yönetimi için Data Lake Store hello Data Lake Store depolanan verilerin şifresini çözmek için gerekli olan ana şifreleme anahtarlarınızı (MEKs) yönetmek için iki mod sağlar. Data Lake Store hello MEKs yönettiğiniz veya Azure anahtar kasası hesabınızı kullanarak hello MEKs tooretain sahipliğini seçin ya da izin verebilirsiniz. Bir Data Lake Store hesabı oluşturulurken anahtar yönetimi hello modunu belirtin. 
- [Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) toomanager sağlar, kendi Kiracı anahtarınızı. Örneğin, Kiracı anahtarınızı (Merhaba varsayılan) yönetme Microsoft yerine, kendi Kiracı anahtar toocomply tooyour kuruluş geçerli olan belirli düzenlemelere yönetebilirsiniz. Kendi Kiracı anahtarınızı yönetme de başvurulan tooas Getir kendi anahtar veya BYOK olur.

## <a name="key-vault-overviews-and-concepts"></a>Anahtar kasası genel bakışlar ve kavramları

- [Anahtar kasası soft-silme davranışı](key-vault-ovw-soft-delete.md) silinen nesnelerin kurtarma sağlayan bir özelliği yanlışlıkla veya kasıtlı hello silme işlemi olup olmadığını açıklar.
- [Anahtar kasası istemci azaltma](key-vault-ovw-throttling.md) azaltma toohello temel kavramları yönlendirir ve uygulamanız için bir yaklaşım sunmaktadır.
- [Anahtar kasası depolama hesabı anahtarları genel bakış](key-vault-ovw-storage-keys.md) hello anahtar kasası tümleştirme Azure depolama hesapları anahtarları açıklar.
- [Anahtar kasası güvenlik dünyaları](key-vault-ovw-security-worlds.md) hello bölgeler ve güvenlik alanları arasındaki ilişkileri açıklar.

## <a name="social"></a>Sosyal

- [Anahtar kasası blogu](http://aka.ms/kvblog)
- [Anahtar kasası Forumu](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Kitaplıkları destekleme

- [Microsoft Azure anahtar kasası çekirdek Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) sağlar **IKey** ve **IKeyResolver** tanımlayıcıları anahtarları bulma ve anahtarlarla işlemleri gerçekleştirmek için arabirim.
- [Microsoft Azure anahtar kasası uzantıları](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) Azure anahtar kasası için genişletilmiş yetenekleri sağlar.


