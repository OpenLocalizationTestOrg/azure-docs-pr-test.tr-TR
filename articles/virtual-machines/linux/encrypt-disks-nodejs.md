---
title: bir Linux VM hello Azure CLI 1.0 ile aaaEncrypt disklerde | Microsoft Docs
description: "Azure CLI 1.0 ve hello Resource Manager dağıtım modeli kullanarak bir Linux VM tooencrypt disklerde nasıl hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanarak bir Linux VM disklerde şifrele
Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri bekleyen şifrelenebilir. Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir. Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz. Bu makalede, Azure CLI 1.0 ve hello Resource Manager dağıtım modeli kullanarak bir Linux VM sanal disklerde tooencrypt nasıl hello ayrıntıları.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, VM'yi sanal disklerde tooencrypt hello bölüm ayrıntıları hello temel aşağıdaki komutları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).

Merhaba gereksinim [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `myKeyVault`, ve `myVM`.

İlk olarak, Azure aboneliğinizde içinde hello Azure anahtar kasası sağlayıcısı etkinleştirin ve bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı `myResourceGroup` hello içinde `WestUS` konumu:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Azure anahtar kasası oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar kasası `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Bir şifreleme anahtarı anahtar kasanızı oluşturmak ve disk şifrelemesi için etkinleştirin. Merhaba aşağıdaki örnek adlı bir anahtar oluşturur `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

İşleme hello kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi için Azure Active Directory'yi kullanarak bir uç nokta oluşturun. Merhaba `--home-page` ve `--identifier-uris` gerek kalmaz toobe gerçek yönlendirilebilir adres. Merhaba yüksek düzeyde güvenlik için istemci gizli yerine parolalar kullanılmalıdır. Hello Azure CLI istemci gizli şu anda oluşturulamıyor. İstemci gizli yalnızca hello Azure portal oluşturulabilir. Merhaba aşağıdaki örnek adlı bir Azure Active Directory uç nokta oluşturuyor `myAADApp` ve bir parola kullanıyorsa `myPassword`. Kendi parolanızı aşağıdaki gibi belirtin:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Not hello `applicationId` komutu önceki hello hello çıktısını gösterilen. Bu uygulama kimliği, aşağıdaki adımları hello kullanılır:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

VM varolan bir veri diski tooan ekleyin. Merhaba aşağıdaki örnek, bir veri diski tooa adlı VM `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Oluşturduğunuz anahtar kasası ve hello anahtarınızı Hello ayrıntılarını gözden geçirin. Anahtar kasası kimliği, URI ve anahtar hello hello son adımda URL. Merhaba aşağıdaki örnek hello ayrıntılarını adlı bir anahtar kasası için gözden geçiriyor `myKeyVault` ve adlı anahtar `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Disklerinizi gibi kendi parametre adları boyunca girme şifrelemek:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello Azure CLI ayrıntılı hataları hello şifreleme işlemi sırasında sağlamaz. Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Hello komut önceki birçok değişkeni yok ve kadar göstergesi toowhy hello işlemi başarısız olarak alamayabilirsiniz, tam komut örneği aşağıdaki gibi olur:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Son olarak, gözden geçirme hello şifreleme durumu yeniden sanal diskler şimdi şifrelendikten tooconfirm. Merhaba aşağıdaki örnek hello durumunu adlı bir VM denetler `myVM` hello içinde `myResourceGroup` kaynak grubu:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Disk şifrelemesi'ne genel bakış
Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Azure sanal diskleri şifreleme ücretsizdir. Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur. Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz. Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini. Bir Azure Active Directory uç nokta VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.

bir VM şifrelemek için hello işlem aşağıdaki gibidir:

1. Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.
2. Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.
3. tooread hello şifreleme anahtarını hello Azure anahtar kasası, Azure Active Directory'yi kullanarak hello uygun izinlere sahip bir uç nokta oluşturun.
4. Merhaba komutu tooencrypt hello Azure Active Directory uç noktası ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.
5. Hello Azure Active Directory uç nokta Azure anahtar Kasası'hello gereken şifreleme anahtarını ister.
6. Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.

## <a name="supporting-services-and-encryption-process"></a>Destek Hizmetleri ve şifreleme işlemi
Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:

* **Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır.
  * Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz. Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.
  * tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.
* **Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler.
  * Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.
  * Merhaba uygulama uç noktası hello anahtar kasası için ve sanal makine Hizmetleri toorequest daha fazla bilgi ve hello uygun şifreleme anahtarları verilen. Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.

## <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar
Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:

* Linux sunucusu SKU'ları - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) ve Red Hat Enterprise Linux aşağıdaki hello.
* Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) hello olmalıdır aynı Azure bölgesinde ve abonelik.
* Standart bir, D, DS, G ve GS serisi VM'ler.

Disk şifrelemesi senaryoları aşağıdaki hello şu anda desteklenmiyor:

* Temel katman VM'ler.
* Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.
* İşletim sistemi disk şifrelemesi Linux sanal makineleri üzerinde devre dışı bırakılıyor.
* Şifreleme anahtarlarının zaten şifrelenmiş bir Linux VM Hello güncelleştiriliyor.

## <a name="create-hello-azure-key-vault-and-keys"></a>Oluşturma Azure anahtar kasası ve anahtarları hello
toocomplete hello geri kalanında bu kılavuz, gereksinim duyduğunuz hello [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:

```azurecli
azure config mode arm
```

Merhaba komut örnekleri tüm örnek parametreleri kendi adları, konum ve anahtar değerlerini değiştirin. Merhaba aşağıdaki örnekleri kullanmak, bir kural `myResourceGroup`, `myKeyVault`, `myAADApp`vb..

Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil. Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan. Sanal disk şifrelemesi için anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı kullanın veya sanal diskleri şifresini.

Azure aboneliğinizde Hello Azure anahtar kasası sağlayıcısını etkinleştirin, ardından bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUS` konumu:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello. Merhaba aşağıdaki örnekte oluşturur adlı bir Azure anahtar kasası `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz. HSM kullanmanın premium anahtar kasası gerektirir. Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur. bir ' % s'premium anahtar kasası, adım önceki hello içinde eklemek toocreate `--sku Premium` toohello komutu. Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır.

Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir. Bir şifreleme anahtarı, anahtar kasası içinde oluşturun, sonra sanal disk şifrelemesi ile kullanmak için etkinleştirin. Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myKey` ve disk şifrelemesi için sağlar:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Merhaba Azure Active Directory uygulaması oluşturma
Sanal diskler şifrelenmiş veya şifresi, bir uç nokta toohandle hello kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi kullanın. Bu uç noktası, bir Azure Active Directory uygulaması hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir. Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.

Tam bir Azure Active Directory Uygulama oluşturmadığınızı gibi hello `--home-page` ve `--identifier-uris` aşağıdaki örneğine hello parametrelerinde toobe gerçek yönlendirilebilir adres gerek yoktur. Merhaba aşağıdaki örnek, ayrıca hello Azure portal oluşturma anahtarları yerine bir parola tabanlı gizlilik belirtir. Bu sürede anahtarlar oluşturma hello Azure CLI ' yapılamaz.

Azure Active Directory uygulamanızı oluşturun. Merhaba aşağıdaki örnek adlı bir uygulama oluşturur `myAADApp` ve bir parola kullanıyorsa `myPassword`. Kendi parolanızı aşağıdaki gibi belirtin:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Merhaba Not `applicationId` döndürülen hello çıktısında komutu önceki hello. Bu uygulama kimliği bazı adımları kalan hello kullanılır. Merhaba uygulaması ortamınızda erişilebilir olmasını sağlayın, ardından, bir hizmet asıl adı (SPN) oluşturun. toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory Uygulama tooread hello anahtarları olmalıdır.

Merhaba SPN oluşturmak ve hello uygun izinleri aşağıdaki gibi ayarlayın:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Sanal bir disk ekleyin ve şifreleme durumunu gözden geçirin
tooactually bazı sanal diskler şifrelerseniz, VM var olan bir disk tooan eklemek olanak sağlar. VM gibi varolan bir 5 Gb veri diski tooan ekleyin:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Merhaba sanal diskleri şu anda şifrelenmez. Merhaba, VM geçerli şifreleme durumu aşağıdaki gibi gözden geçirin:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Sanal diskler şifrele
toonow şifrelemek hello sanal diskler, tüm hello önceki bileşenleri araya getirin:

1. Merhaba Azure Active Directory uygulaması ve parola belirtin.
2. Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.
3. Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.
4. Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.

Anahtar kasası kimliği URI hello ve ardından URL hello son adımda anahtar, oluşturulan Azure anahtar kasası ve hello anahtarınızı Hello ayrıntılarını gözden olanak sağlar:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Merhaba Hello çıktısını kullanarak, sanal disklere şifrelemek `azure keyvault show` ve `azure keyvault key show` gibi komutlar:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello yukarıdaki komut sahip birçok değişkenleri olarak hello aşağıdaki hello tam komut başvurusu için bir örnektir:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello Azure CLI ayrıntılı hataları hello şifreleme işlemi sırasında sağlamaz. Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` hello şifreleme VM üzerinde.

Son olarak, hello şifreleme durumunu gözden geçirmek sağlar yeniden sanal diskler şimdi şifrelendikten tooconfirm:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Ek veri disklerinin ekleme
Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskler tooyour VM eklemek ve de şifreleme. Merhaba çalıştırdığınızda `azure vm enable-disk-encryption` komutu, hello kullanarak artışı hello dizisi sürümü `--sequence-version` parametresi. Bu sıra sürüm parametresi tooperform verir üzerinde yinelenen işlemler hello aynı VM.

Örneğin, ikinci bir sanal disk tooyour VM aşağıdaki şekilde ekleyin olanak sağlar:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Merhaba ekleyerek bu kez Hello komutu tooencrypt hello sanal diskler, yeniden `--sequence-version` parametre ve artan hello değerini bizim ilk aşağıdaki gibi çalıştırın:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Sonraki adımlar
* Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).
* Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).
