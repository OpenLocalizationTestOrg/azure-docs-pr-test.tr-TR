---
title: "aaaGet Azure anahtar kasası ile çalışmaya | Microsoft Docs"
description: "Size Bu öğretici toohelp kullanmak ile Azure anahtar kasası toocreate toostore Azure'da sağlamlaştırılmış bir kapsayıcı başlatıldı ve şifreleme anahtarları ve gizli anahtarları azure'da yönetin."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Azure Anahtar Kasası kullanmaya başlama 
Azure Anahtar Kasası çoğu bölgede kullanılabilir. Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Giriş
Size Bu öğretici toohelp kullanmak ile Azure anahtar kasası toocreate toostore Azure'da sağlamlaştırılmış bir kapsayıcı (bir kasa) başlatıldı ve şifreleme anahtarları ve gizli anahtarları azure'da yönetin. Bu, Azure PowerShell toocreate kullanarak hello sürecinde bir anahtar ya da sonra bir Azure uygulamasıyla kullanabileceğiniz parola içeren bir kasa yardımcı olur. Ardından, bu anahtarı veya parolayı bir uygulamanın nasıl kullanacağını gösterir.

**Zaman toocomplete tahmini:** 20 dakika

> [!NOTE]
> Bu öğretici nasıl toowrite hello hello adımlardan birini içeren Azure uygulaması, yani nasıl tooauthorize uygulama toouse bir anahtar veya gizli hello anahtarında kasa için yönergeler içermez.
>
> Bu öğretici Azure PowerShell kullanır. Platformlar Arası Komut Satırı Arabirimi yönergeleri için [bu eşdeğer öğreticiye](key-vault-manage-with-cli2.md) bakın.
>
>

Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello olması gerekir:

* Abonelik tooMicrosoft Azure. Bir aboneliğiniz yoksa [ücretsiz hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Azure PowerShell'in, **en az 1.1.0 sürümü**. tooinstall Azure PowerShell ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Azure PowerShell'i zaten yüklediyseniz ve hello sürüm hello Azure PowerShell konsolundan bilmiyorsanız, çalışamazsa `(Get-Module azure -ListAvailable).Version`. Azure PowerShell'in 0.9.8 - 0.9.1 sürümleri arasında bir sürümü yüklüyse bazı küçük değişikliklerle bu öğreticiyi kullanmaya devam edebilirsiniz. Örneğin, hello kullanmalısınız `Switch-AzureMode AzureResourceManager` komutu ve bazı hello Azure anahtar kasası komutları değişmiştir. Merhaba 0.9.1-0.9.8 arasındaki sürümlere yönelik anahtar kasası cmdlet listesi için bkz: [Azure anahtar kasası cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault).
* Yapılandırılmış toouse hello anahtar ya da Bu öğreticide oluşturduğunuz parola olacak bir uygulama. Bir örnek uygulama hello kullanılabilir [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Yönergeler için Benioku dosyası ile birlikte gelen hello bakın.

Bu öğretici Azure PowerShell'e yeni başlayanlar için tasarlanmıştır ancak modüller, cmdlet'ler ve oturumlar gibi hello temel kavramları anladığınız varsayılır. Daha fazla bilgi için bkz. [Windows Power Shell ile Çalışmaya Başlama](https://technet.microsoft.com/library/hh857337.aspx)

tooget ayrıntılı kullanım hello Bu öğreticide gördüğünüz herhangi bir cmdlet için Yardım **Get-Help** cmdlet'i.

    Get-Help <cmdlet-name> -Detailed

Örneğin, tooget yardımını hello **Login-AzureRmAccount** cmdlet, türü:

    Get-Help Login-AzureRmAccount -Detailed

Ayrıca, Azure PowerShell'de Azure Resource Manager ile tanıdık öğreticileri tooget aşağıdaki hello okuyabilirsiniz:

* [Nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)
* [Azure PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Tooyour abonelikleri Bağlan
Bir Azure PowerShell oturumu Başlat ve tooyour Azure hesabı komutu aşağıdaki hello ile oturum açın:  

    Login-AzureRmAccount

Azure, Azure kamu gibi belirli bir örneği kullanıyorsanız Not hello - Environment parametresini bu komutla. Örneğin, `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin. Varsayılan olarak bu hesap ile ilişkilendirilmiş tüm hello abonelikleri Azure PowerShell alır, birinci kullanır hello.

Birden çok aboneliğiniz varsa ve Azure anahtar kasası için toospecify belirli bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:

    Get-AzureRmSubscription

Ardından, toospecify hello abonelik toouse, türü:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Azure PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a id="resource"></a>Yeni bir kaynak grubu oluşturma
Azure Resource Manager'ı kullandığınızda, tüm ilgili kaynaklar bir kaynak grubu içinde oluşturulur. Bu öğretici için **ContosoResourceGroup** adlı yeni bir kaynak grubu oluşturacağız:

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Anahtar kasası oluşturma
Kullanım hello [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate bir anahtar kasası. Bu cmdlet, üç zorunlu parametreye sahiptir: bir **kaynak grubu adı**, **anahtar kasası adı**ve hello **coğrafi konum**.

Merhaba kasa adını kullanırsanız, örneğin, **ContosoKeyVault**, hello kaynak grubu adını **ContosoResourceGroup**ve hello konumunu **Doğu Asya**, türü:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

Merhaba bu cmdlet'in çıktısı, yeni oluşturduğunuz hello anahtar kasasının özelliklerini gösterir. Merhaba iki en önemli özellikleri şunlardır:

* **Kasa adı**: hello örnekte budur **ContosoKeyVault**. Bu adı diğer Anahtar Kasası cmdlet'leri için kullanacaksınız.
* **Kasa URI'si**: hello örnekte https://contosokeyvault.vault.azure.net/ şeklindedir. REST API'si aracılığıyla kasanızı kullanan uygulamaların bu URI'yi kullanması gerekir.

Bu anahtarı üzerindeki herhangi bir işlem yetkili tooperform kasa artık Azure hesabınız bulunuyor. Henüz başka kimse yetkilendirilmedi.

> [!NOTE]
> Merhaba hata görürseniz **hello abonelik 'Microsoft.KeyVault' kayıtlı toouse ad alanını değil** toocreate çalıştırmak, yeni bir anahtar kasanızı çalıştığınızda `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` ve New-AzureRmKeyVault komutunuzu yeniden çalıştırın. Daha fazla bilgi için bkz. [AzureRmResourceProvider'ı kaydetme](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Bir anahtar veya gizli toohello anahtar kasası ekleme
Sizin için Azure anahtar kasası toocreate yazılımla korunan anahtardan istiyorsanız, hello kullanın [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet'ini ve hello aşağıdakileri yazın:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Ancak, varolan bir yazılım korumalı anahtar varsa bir. PFX dosyası kaydedilmiş tooyour C:\ sürücüsü tooupload tooAzure anahtar kasası, tooset hello değişkeni aşağıdaki türü hello istediğiniz softkey.pfx adlı bir dosyada **securepfxpwd** parolası için **123** hello için. PFX dosyası:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Ardından hello tooimport hello anahtar aşağıdaki hello yazın. Yazılım hello anahtar kasası hizmeti ile Merhaba anahtarı korur PFX dosyası:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Artık oluşturduğunuz veya tooAzure anahtar kasası URI'sini kullanarak karşıya bu anahtarı başvurabilirsiniz. Kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget bu belirli sürümü.  

Bu anahtar türü için toodisplay hello URI:

    $Key.key.kid

tooadd SQLPassword adlı bir parola ve Pa$ $w0rd tooAzure anahtar kasası hello değerine sahip, gizli toohello kasası dönüştürmeniz hello Pa$ $w0rd tooa güvenli dize değerini hello aşağıdakileri yazarak:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Merhaba aşağıdakileri yazın:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Artık bu parolayı URI'sini kullanarak tooAzure anahtar kasası, eklenen başvurabilirsiniz. Kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget bu belirli sürümü.

Bu parola türü için toodisplay hello URI:

    $secret.Id

Şimdi hello anahtar veya yeni oluşturduğunuz gizli görüntüleyin:

* tooview anahtar, türünüz:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview, gizli, türü:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Artık, anahtar kasası ve anahtar veya gizli uygulamalar toouse için hazırdır. Uygulamaları toouse yetkilendirmeniz gerekir bunları.  

## <a id="register"></a>Bir uygulamayı Azure Active Directory’ye kaydetme
Bu adım genellikle ayrı bir bilgisayarda bir geliştirici tarafından yapılır. Belirli tooAzure anahtar kasası değildir ancak bütünlük açısından buraya dahil edilir.

> [!IMPORTANT]
> toocomplete hello Öğreticisi, hesap, hello kasası ve bu adımda kaydedeceğiniz Merhaba uygulaması tüm olmalıdır hello aynı Azure dizini.
>
>

Bir anahtar kasası kullanan uygulamaların, Azure Active Directory'den bir belirteç kullanarak kimlik doğrulama yapması gerekir. toodo Bu, hello hello uygulama sahibi ilk kaydetmeniz gerekir hello uygulama Azure Active Directory'de. Kayıt Hello sonunda, hello uygulama sahibi aşağıdaki değerleri hello alır:

* Bir **uygulama kimliği** (istemci kimliği olarak da bilinir) ve **kimlik doğrulama anahtarı** (olarak da bilinen hello paylaşılan gizlilik). Merhaba uygulaması hem de bu değerleri tooAzure Active Directory tooget bir belirteç sunması gerekir. Nasıl Merhaba uygulaması, bu hello uygulamaya bağlıdır toodo yapılandırılır. Merhaba anahtar kasası örnek uygulaması hello uygulama sahibi bu değerleri hello app.config dosyasında ayarlar.

Azure Active Directory'de tooregister hello uygulama:

1. İçinde toohello Klasik Azure portalında oturum açın.
2. Hello solda tıklatın **Active Directory**ve ardından içinde kaydettiğiniz uygulamanızı hello dizini seçin. <br> <br> **Not:** hello seçmelisiniz hello ile anahtar kasanızı oluşturduğunuz Azure aboneliğini içeren aynı dizini. Hangi dizine bu bilmiyorsanız, tıklatın olduğu **ayarları**ile anahtar kasanızı oluşturduğunuz hello aboneliği tanımlayın ve hello dizinin adını not hello hello son sütununda görüntülenir.
3. **UYGULAMALAR**'a tıklayın. Tooyour dizin hiçbir uygulama eklenmemişse bu sayfa yalnızca hello gösterir **bir uygulama ekleyin** bağlantı. Merhaba bağlantısına tıklayın veya alternatif olarak, tıklatabilirsiniz **ekleme** hello komut çubuğunda.
4. Merhaba, **uygulama Ekle** sihirbazında, hello **neler toodo istediğiniz?** sayfasında, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
5. Merhaba üzerinde **bize uygulamanızı anlatın** sayfasında, uygulamanız için bir ad belirtin ve ardından **WEB uygulaması ve/veya WEB API** (Merhaba varsayılan). Merhaba tıklatın **sonraki** simgesi.
6. Merhaba üzerinde **uygulama özellikleri** sayfasında, hello belirtin **oturum açma URL** ve **uygulama kimliği URI'si** web uygulamanız için. Uygulamanız bu değerlere sahip değilse değerleri bu adım için kendiniz belirleyebilirsiniz. (örneğin, her iki kutu için http://test1.contoso.com belirtebilirsiniz). Bu sitelerin mevcut olup olmaması önemli değildir. Önemli olan her uygulama için bu hello uygulama kimliği URI'SİNİN dizininizdeki her uygulama için farklı olmasıdır. Merhaba directory Bu dize tooidentify uygulamanızı kullanır.
7. Merhaba tıklatın **tam** simgesi toosave değişikliklerinizi hello Sihirbazı'nda.
8. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **yapılandırma**.
9. Toohello kaydırma **anahtarları** bölümünde, hello süre seçin ve ardından **KAYDETMEK**. Merhaba sayfa yenilenir ve artık bir anahtar değeri gösterir. Bu anahtar değeri ve hello ile uygulamanızı yapılandırmanız gerekir **istemci kimliği** değeri. (Bu yapılandırma için yönergeler uygulamaya özgü olur.)
10. Bu sayfadan, sonraki adım tooset izinleri hello kasanızda kullanacağınız Hello istemci kimliği değerini kopyalayın.

## <a id="authorize"></a>Merhaba uygulama toouse hello anahtar veya gizli yetkilendirmek
tooauthorize hello uygulama tooaccess hello anahtar veya gizli hello kasadaki kullanım [kümesi AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet'i.

Örneğin, kasa adınız ise **ContosoKeyVault** ve tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed istemci Kimliğine sahip ve anahtarlara sahip tooauthorize hello uygulama toodecrypt ve oturum istediğiniz istediğiniz hello uygulama Merhaba aşağıdaki komutu çalıştırın, Kasası:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Kasa adınız, aynı uygulama tooread gizli tooauthorize istiyorsanız, hello aşağıdaki komutu çalıştırın:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Bir donanım güvenlik modülü (HSM) toouse istiyorsanız
Ek güvence için alma veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur. Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır. Bu gereksinim tooyou geçerli değilse bu bölümü atlayın ve çok gidin[hello anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme](#delete).

toocreate bu HSM korumalı anahtarları hello kullanmalısınız [Azure anahtar kasası Premium Hizmet katmanını toosupport HSM korumalı anahtarlar](https://azure.microsoft.com/pricing/free-trial/). Ek olarak, bu işlevin Azure Çin'de kullanılamadığını unutmayın.

Merhaba anahtar kasası oluşturduğunuzda, hello eklemek **- SKU** parametre:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Yazılım korumalı anahtarlar (daha önce gösterildiği gibi) ve HSM korumalı anahtarlar toothis anahtar kasası ekleyebilirsiniz. toocreate HSM korumalı bir anahtar kümesi hello **-hedef** parametresi too'HSM':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Bir anahtarından komutu tooimport aşağıdaki hello kullanabileceğiniz bir. PFX dosyası, bilgisayarınızdaki. Bu komut hello anahtar hello anahtar kasası hizmetindeki Hsm'lere aktarır:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


Merhaba sonraki komutu içe aktaran bir "kendi anahtarını getir" (BYOK) paketini. Bu senaryo, yerel HSM'NİZDE anahtarınızı oluşturmak hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarmanızı sağlar:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Daha ayrıntılı hakkında yönergeler için toogenerate bu BYOK paketini bkz [nasıl toogenerate ve aktarım HSM korumalı anahtarları Azure anahtar kasası için](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Merhaba anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme
Merhaba anahtar kasası ve başlangıç anahtarı veya içerdiği gizli artık ihtiyacınız varsa, hello kullanarak hello anahtar kasası silebilirsiniz [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Ya da hello anahtar kasasını ve bu gruba dahil diğer kaynakları içeren bir tüm Azure kaynak grubu silebilirsiniz:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Diğer Azure PowerShell Cmdlet’leri
Azure Anahtar Kasası'nı yönetmede kullanışlı bulabileceğiniz diğer komutlar:

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: Bu komut, tüm anahtarların ve seçilen özelliklerin tablosal bir görüntüsünü alır.
* `$Keys[0]`: Bu komut hello belirtilen anahtar için özelliklerin tam listesini görüntüler
* `Get-AzureKeyVaultSecret`: Bu komut, tüm gizli adların ve seçilen özelliklerin tablosal bir görüntüsünü listeler.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Örnek nasıl tooremove belirli bir anahtarı.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Örnek nasıl tooremove belirli bir gizli anahtar.

## <a id="next"></a>Sonraki adımlar
Azure Anahtar Kasası'nı bir web uygulamasında kullanan bir izleme öğreticisi için bkz. [Azure Anahtar Kasası'nı bir Web Uygulamasından Kullanma](key-vault-use-from-web-application.md).

anahtar kasanızı kullanılan toosee bkz [Azure anahtar kasası günlüğü](key-vault-logging.md).

Azure anahtar kasası için hello en son Azure PowerShell cmdlet'leri listesi için bkz: [Azure anahtar kasası cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault).

Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).
