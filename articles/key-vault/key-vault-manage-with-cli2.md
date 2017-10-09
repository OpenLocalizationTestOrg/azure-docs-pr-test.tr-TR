---
title: "Azure anahtar kasası CLI kullanarak aaaManage | Microsoft Docs"
description: "Bu öğretici tooautomate ortak görevler anahtar kasasına hello CLI 2.0 kullanarak"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>Anahtar kasası CLI 2.0 kullanarak yönetme
Azure Anahtar Kasası çoğu bölgede kullanılabilir. Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Giriş
Size Bu öğretici toohelp kullanmak ile Azure anahtar kasası toocreate toostore Azure'da sağlamlaştırılmış bir kapsayıcı (bir kasa) başlatıldı ve şifreleme anahtarları ve gizli anahtarları azure'da yönetin. Bu, Azure platformlar arası komut satırı arabirimi toocreate kullanarak hello sürecinde bir anahtar ya da sonra bir Azure uygulamasıyla kullanabileceğiniz parola içeren bir kasa yardımcı olur. Bunu daha sonra nasıl bir uygulama daha sonra bu anahtarı veya parolayı kullanabilirsiniz gösterir.

**Zaman toocomplete tahmini:** 20 dakika

> [!NOTE]
> Bu öğretici nasıl toowrite hello nasıl tooauthorize uygulama toouse bir anahtar veya gizli hello anahtarında kasa gösteren hello adımları içeren Azure uygulamanızı yönergeleri içermez.
>
> Bu öğretici kullanır, en son Azure CLI 2.0 hello.
>
>

Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello olması gerekir:

* Abonelik tooMicrosoft Azure. Bir yoksa için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial).
* Komut satırı arabirimi sürüm 2.0 veya üstü. tooinstall hello en son sürümünü ve tooyour Azure aboneliğine bağlanma Bkz [hello Azure platformlar arası komut satırı arabirimi 2.0 yükleyip](/cli/azure/install-azure-cli).
* Yapılandırılmış toouse hello anahtar ya da Bu öğreticide oluşturduğunuz parola olacak bir uygulama. Bir örnek uygulama hello kullanılabilir [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Yönergeler için Benioku dosyası ile birlikte gelen hello bakın.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Azure platformlar arası komut satırı arabirimi ile ilgili Yardım alma
Bu öğretici, başlangıç komut satırı arabirimi (Bash, Terminal, komut istemi) bildiğinizi varsayar

Merhaba--Yardım veya -h parametresi olabilir tooview Yardım belirli komutları için kullanılır. Alternatif olarak, aynı bilgileri hello azure Yardım [komut biçimi de kullanılan tooreturn olabilir] [Seçenekler] hello. Örneğin, tüm dönüş hello aşağıdaki komutları hello aynı bilgileri:

```
az account set --help
az account set -h
```

Toohelp kullanarak--zaman şüpheli bir komut tarafından gerekli hello parametreleri hakkında başvuru Yardım, -h veya [komut] Yardım az.

Ayrıca, Azure Resource Manager Azure platformlar arası komut satırı arabirimi ile tanıdık öğreticileri tooget aşağıdaki hello okuyabilirsiniz:

* [Azure CLI'yı yükleme](/cli/azure/install-azure-cli)
* [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Tooyour abonelikleri Bağlan
bir kuruluş hesabı, komutu aşağıdaki kullanım hello kullanarak toolog:

```
az login -u username@domain.com -p password
```

veya, toolog etkileşimli olarak yazarak istiyorsanız

```
az login
```

Birden çok aboneliğiniz varsa ve Azure anahtar kasası için toospecify belirli bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:

```
az account list
```

Ardından, toospecify hello abonelik toouse, türü:

```
az account set --subscription <subscription name or ID>
```

Azure platformlar arası komut satırı arabirimi yapılandırma hakkında daha fazla bilgi için bkz: [Azure CLI yükleme](/cli/azure/install-azure-cli).

## <a name="create-a-new-resource-group"></a>Yeni bir kaynak grubu oluşturma
Azure Kaynak Yöneticisi'ni kullanırken, tüm ilgili kaynaklar bir kaynak grubu içinde oluşturulur. Bu öğretici için yeni bir kaynak grubu 'ContosoResourceGroup' oluşturacağız.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

Merhaba ilk parametre kaynak grubu adı ve hello ikinci parametre başlangıç konumu. Konum için hello komutunu `az account list-locations` tooidentify nasıl toospecify bir alternatif konum toohello biri bu örnekte. Daha fazla bilgiye ihtiyacınız varsa, yazın: `az account list-locations -h`.

## <a name="register-hello-key-vault-resource-provider"></a>Merhaba anahtar kasası kaynak sağlayıcısını Kaydet
Bu anahtar kasası kaynak sağlayıcısı aboneliğinizde kayıtlı olduğundan emin olun:

```
az provider register -n Microsoft.KeyVault
```

Bu, yalnızca abonelik başına bir kez yapılır toobe gerekir.

## <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma
Kullanım hello `az keyvault create` komutu toocreate bir anahtar kasası. Bu komut dosyasını üç zorunlu parametreye sahiptir: bir kaynak grubu adı, anahtar kasası adı ve hello coğrafi konum.

Örneğin, ContosoKeyVault, ContosoResourceGroup hello kaynak grubu adını ve Doğu Asya konumunu hello hello kasa adını kullanırsanız yazın:
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

Bu komutun çıktısı Hello hello yeni oluşturduğunuz anahtar kasasının özelliklerini gösterir. Merhaba iki en önemli özellikleri şunlardır:

* **ad**: hello örnekte ContosoKeyVault budur. Bu adı diğer anahtar kasası komutları için kullanır.
* **vaultUri**: hello örnekte https://contosokeyvault.vault.azure.net budur. REST API'si aracılığıyla kasanızı kullanan uygulamaların bu URI'yi kullanması gerekir.

Bu anahtarı üzerindeki herhangi bir işlem yetkili tooperform kasa artık Azure hesabınız bulunuyor. Henüz başka kimse yetkilendirilmedi.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Bir anahtar veya gizli toohello anahtar kasası ekleme
Sizin için Azure anahtar kasası toocreate yazılımla korunan anahtardan istiyorsanız, hello kullanın `az key create` komut ve hello aşağıdakileri yazın:
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
Ancak, yerel dosya tooupload tooAzure anahtar kasası istediğiniz softkey.pem adlı bir dosya olarak kaydedilmiş bir .pem dosyasını mevcut bir anahtarı varsa, hello tooimport hello anahtar aşağıdaki hello yazın. PEM dosyası yazılım hello anahtar kasası hizmeti ile Merhaba anahtarı korur:
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
Artık oluşturduğunuz veya tooAzure anahtar kasası URI'sini kullanarak karşıya hello anahtar başvurabilirsiniz. Kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget bu belirli sürümü.

tooadd SQLPassword adlı bir parola olduğu ve Pa$ $w0rd tooAzure anahtar kasası, aşağıdaki türü hello hello değerine sahip bir gizli toohello Kasası:
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
Artık bu parolayı URI'sini kullanarak tooAzure anahtar kasası, eklenen başvurabilirsiniz. Kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello geçerli sürümü almak ve kullanmak **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget bu belirli sürümü.

Şimdi hello anahtar veya yeni oluşturduğunuz gizli görüntüleyin:

* tooview anahtar, türünüz:`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview, gizli, türü:`az keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Bir uygulamayı Azure Active Directory'ye kaydetme
Bu adım genellikle ayrı bir bilgisayarda bir geliştirici tarafından yapılır. Belirli tooAzure anahtar kasası değildir ancak bütünlük açısından buraya eklenmiştir.

> [!IMPORTANT]
> toocomplete hello Öğreticisi, hesap, hello kasası ve bu adımda kaydedeceğiniz Merhaba uygulaması tüm olmalıdır hello aynı Azure dizini.
>
>

Bir anahtar kasası kullanan uygulamaların, Azure Active Directory'den bir belirteç kullanarak kimlik doğrulama yapması gerekir. toodo Bu, hello hello uygulama sahibi ilk kaydetmeniz gerekir hello uygulama Azure Active Directory'de. Kayıt Hello sonunda, hello uygulama sahibi aşağıdaki değerleri hello alır:

* Bir **uygulama kimliği** (istemci kimliği olarak da bilinir) ve **kimlik doğrulama anahtarı** (olarak da bilinen hello paylaşılan gizlilik). Merhaba uygulaması bu değerleri tooAzure Active Directory, tooget bir belirteç her ikisi de sunması gerekir. Nasıl Merhaba uygulaması, bu hello uygulamaya bağlıdır toodo yapılandırılır. Merhaba anahtar kasası örnek uygulaması hello uygulama sahibi bu değerleri hello app.config dosyasında ayarlar.

Azure Active Directory'de tooregister hello uygulama:

1. Toohello Azure portalında oturum açın.
2. Hello solda tıklatın **Azure Active Directory**ve ardından içinde kaydettiğiniz uygulamanızı hello dizini seçin. <br> <br> 

> [!Note] 
> Merhaba seçmelisiniz hello ile anahtar kasanızı oluşturduğunuz Azure aboneliğini içeren aynı dizini. Hangi dizine bu bilmiyorsanız, tıklatın olduğu **ayarları**ile anahtar kasanızı oluşturduğunuz hello aboneliği tanımlayın ve hello dizinin adını not hello hello son sütununda görüntülenir.

3. **UYGULAMALAR**'a tıklayın. Tooyour dizin hiçbir uygulama eklenmemişse bu sayfa yalnızca hello gösterecektir **bir uygulama ekleyin** bağlantı. Merhaba bağlantısına tıklayın veya alternatif olarak, hello tıklatabilirsiniz **ekleme** hello komut çubuğunda.
4. Merhaba, **uygulama Ekle** sihirbazında, hello **neler toodo istediğiniz?** sayfasında, **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
5. Merhaba üzerinde **bize uygulamanızı anlatın** sayfasında uygulamanız için bir ad belirtin ve seçin **WEB uygulaması ve/veya WEB API** (Merhaba varsayılan). Merhaba sonraki simgeyi tıklatın.
6. Merhaba üzerinde **uygulama özellikleri** sayfasında, hello belirtin **oturum açma URL** ve **uygulama kimliği URI'si** web uygulamanız için. Uygulamanız bu değerlere sahip değilse değerleri bu adım için kendiniz belirleyebilirsiniz. (örneğin, her iki kutu için http://test1.contoso.com belirtebilirsiniz). Bu sitelerin var olup olmaması önemli değildir; önemli olan her uygulama için bu hello uygulama kimliği URI'SİNİN dizininizdeki her uygulama için farklı olmasıdır. Merhaba directory Bu dize tooidentify uygulamanızı kullanır.
7. Merhaba tam simgesi toosave değişikliklerinizi hello Sihirbazı'nı tıklatın.
8. Merhaba hızlı başlangıç sayfasında, tıklatın **yapılandırma**.
9. Toohello kaydırma **anahtarları** bölümünde, hello süre seçin ve ardından **KAYDETMEK**. Merhaba sayfa yenilenir ve artık bir anahtar değeri gösterir. Bu anahtar değeri ve hello ile uygulamanızı yapılandırmanız gerekir **istemci kimliği** değeri. (Bu yapılandırma için yönergeler uygulamaya özgü olur.)
10. Bu sayfadan, sonraki adım tooset izinleri hello kasanızda kullanacağınız Hello istemci kimliği değerini kopyalayın.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Merhaba uygulama toouse hello anahtar veya gizli yetkilendirmek
tooauthorize hello uygulama tooaccess hello anahtar veya gizli hello kasadaki kullanım hello `az keyvault set-policy` komutu.

Örneğin, kasa adınız tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed istemci Kimliğine sahip ve tooauthorize hello uygulama toodecrypt ve oturum anahtarları, kasaya istediğiniz istediğiniz ContosoKeyVault ve hello uygulama ise, ardından hello çalıştırın Aşağıdaki:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

Kasa adınız, aynı uygulama tooread gizli tooauthorize istiyorsanız, hello aşağıdaki komutu çalıştırın:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Bir donanım güvenlik modülü (HSM) toouse istiyorsanız
Ek güvence için alma veya donanım güvenlik modülleri (HSM'ler)'hello HSM sınırını asla bırakın anahtarları oluştur. Merhaba HSM'ler, FIPS 140-2 Düzey 2 doğrulanmasına şunlardır. Bu gereksinim tooyou geçerli değilse bu bölümü atlayın ve çok gidin[hello anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate bu HSM korumalı anahtarları HSM korumalı anahtarları destekleyen bir kasa aboneliğine sahip olmalıdır.

Merhaba keyvault oluşturduğunuzda, hello 'sku' parametresini ekleyin:

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
HSM korumalı anahtarlar toothis kasa ve yazılım korumalı anahtarlar (daha önce gösterildiği gibi) ekleyebilirsiniz. toocreate HSM korumalı bir anahtar kümesi hello hedef parametre too'HSM':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

.Pem dosyasını bilgisayarınızdaki komutu tooimport bir anahtar yükseltmesinin hello kullanabilirsiniz. Bu komut hello anahtar hello anahtar kasası hizmetindeki Hsm'lere aktarır:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
Merhaba sonraki komutu içe aktaran bir "kendi anahtarını getir" (BYOK) paketini. Bu, yerel HSM'NİZDE anahtarınızı oluşturur ve hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarım sağlar:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
Daha ayrıntılı hakkında yönergeler için toogenerate bu BYOK paketini bkz [nasıl toouse HSM-Protected anahtarları Azure anahtar kasası ile](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Merhaba anahtar kasasını ve ilişkili anahtarları ve gizli anahtarları silme
Merhaba anahtar kasası ve başlangıç anahtarı veya içerdiği gizli artık ihtiyacınız varsa, hello kullanarak hello anahtar kasası silebilirsiniz `az keyvault delete` komutu:

```
az keyvault delete --name 'ContosoKeyVault'
```

Ya da hello anahtar kasasını ve bu gruba dahil diğer kaynakları içeren bir tüm Azure kaynak grubu silebilirsiniz:

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Diğer Azure platformlar arası komut satırı arabirimi komutları
Diğer komutlar Azure anahtar kasası yönetmek için kullanışlı olabilir.

Bu komut tüm anahtarların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:

az keyvault anahtar listesi--kasa adı 'ContosoKeyVault'

Bu komut hello belirtilen anahtar için özelliklerin tam bir liste görüntüler:

az keyvault anahtar Göster--kasa adı 'ContosoKeyVault'--ad 'ContosoFirstKey'

Bu komut tüm gizli adların ve seçilen özelliklerin tablolu bir görüntüsünü listeler:

az keyvault gizli listesi--kasa adı 'ContosoKeyVault'

Örneği nasıl tooremove belirli bir anahtarı:

az keyvault anahtarını silmek--kasa adı 'ContosoKeyVault'--ad 'ContosoFirstKey'

Örneği nasıl tooremove belirli bir gizli anahtarın:

az keyvault gizli anahtarı silme--kasa adı 'ContosoKeyVault'--ad 'SQLPassword'


## <a name="next-steps"></a>Sonraki adımlar
Anahtar kasası komutları için tam Azure CLI başvuru için bkz: [anahtar kasası CLI başvurusu](/cli/azure/keyvault)

Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).
