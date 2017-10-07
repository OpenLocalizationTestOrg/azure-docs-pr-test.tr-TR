---
title: azure'da bir Linux VM aaaEncrypt disklerde | Microsoft Docs
description: "Nasıl tooencrypt sanal diskler için Artırılmış güvenliği kullanarak bir Linux VM üzerinde Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Nasıl bir Linux VM üzerindeki tooencrypt sanal diskler
Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri şifrelenebilir. Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir. Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz. Bu makalede nasıl tooencrypt sanal diskler kullanarak bir Linux VM üzerinde Azure CLI 2.0 hello ayrıntıları verilmektedir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, VM'yi sanal disklerde tooencrypt hello bölüm ayrıntıları hello temel aşağıdaki komutları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).

Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login). Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.

İlk olarak, Azure aboneliğinizle içinde hello Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin. İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create). Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac). kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi Hello hizmet asıl tanıtıcıları hello. sonraki komutlarını kullanmak için kimliğini ve parolayı hello hizmet sorumlusu için hello değerler aşağıdaki örneğine hello okur:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Hizmet sorumlusu hello oluşturduğunuzda hello parola yalnızca çıktı. İsterseniz, Görünüm ve kayıt parolanızı hello (`echo $sp_password`). Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).

Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy). Aşağıdaki örneğine hello hello hizmet asıl kimliği komutu önceki hello sağlanır:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Bir VM ile oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin. Disk şifrelemesi yalnızca belirli Market görüntülerini destekler. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` kullanarak bir **CentOS 7.2n** görüntü:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH VM tooyour kullanarak hello `publicIpAddress` komutu önceki hello hello çıktıda gösterilen. Bir bölüm ve dosya sistemi oluşturun, sonra hello veri diski bağlayabilir. Daha fazla bilgi için bkz: [tooa Linux VM toomount hello yeni disk bağlanmak](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). SSH oturumunuzu kapatın.

VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable). Merhaba aşağıdaki örnek kullanır hello `$sp_id` ve `$sp_password` hello önceki değişkenlerinden `ad sp create-for-rbac` komutu:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Merhaba disk şifreleme işlemi toocomplete için biraz zaman alabilir. Merhaba işlemine hello durumunu izlemek [az vm şifreleme Göster](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Merhaba durumu **EncryptionInProgress**. Merhaba durum beklemeniz hello işletim sistemi disk raporlar için **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Merhaba disk şifreleme işlemi hello önyükleme işlemi sırasında sonlandırılır, böylece şifrelemeyle yeniden hello durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Merhaba durum şimdi raporu hello işletim sistemi diski ve veri diski olarak **şifreli**.

## <a name="overview-of-disk-encryption"></a>Disk şifrelemesi'ne genel bakış
Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Azure sanal diskleri şifreleme ücretsizdir. Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur. Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz. Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini. Bir Azure Active Directory Hizmet sorumlusu VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.

bir VM şifrelemek için hello işlem aşağıdaki gibidir:

1. Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.
2. Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.
3. tooread hello şifreleme anahtarını hello Azure anahtar kasası oluşturma bir Azure Active Directory hizmet asıl hello uygun izinlere sahip.
4. Merhaba komutu tooencrypt hello Azure Active Directory hizmet asıl ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.
5. Hello Azure Active Directory hizmet asıl istekleri Azure anahtar kasası gerekli şifreleme anahtarından hello.
6. Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.

## <a name="encryption-process"></a>Şifreleme işlemi
Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:

* **Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır.
  * Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz. Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.
  * tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.
* **Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler.
  * Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.
  * Merhaba hizmet sorumlusu hello uygun şifreleme anahtarları verilmesi ve güvenli mekanizması toorequest sağlar. Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.

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

## <a name="create-azure-key-vault-and-keys"></a>Azure anahtar kasası ve anahtarları oluşturma
Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login). Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.

Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil. Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan. Sanal disk şifrelemesi için anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı kullanın veya sanal diskleri şifresini.

Azure aboneliğinizle içinde Hello Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde `eastus` konumu:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello. Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin. İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz. HSM kullanmanın premium anahtar kasası gerektirir. Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur. bir ' % s'premium anahtar kasası, adım önceki hello içinde eklemek toocreate `--sku Premium` toohello komutu. Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır.

Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir. Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create). Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Azure Active Directory hizmet asıl Hello oluşturma
Sanal diskler şifrelenmiş veya şifresi olduğunda bir hesabı toohandle hello kimlik doğrulaması ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi belirtin. Bu hesabı, bir Azure Active Directory hizmet asıl hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir. Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.

Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac). sonraki komutlarını kullanmak için kimliğini ve parolayı hello hizmet sorumlusu için hello değerler aşağıdaki örneğine hello okur:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Merhaba parola yalnızca hello hizmet sorumlusu oluşturma görüntülenir. İsterseniz, Görünüm ve kayıt parolanızı hello (`echo $sp_password`). Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).

toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory hizmet asıl tooread hello anahtarları olmalıdır. Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy). Aşağıdaki örneğine hello hello hizmet asıl kimliği komutu önceki hello sağlanır:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Sanal makine oluşturma
tooactually bazı sanal diskler şifrelerseniz, bir VM oluşturun ve bir veri diski Ekle olanak tanır. VM tooencrypt ile oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin. Disk şifrelemesi yalnızca belirli Market görüntülerini destekler. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* kullanarak bir **CentOS 7.2n** görüntü:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH VM tooyour kullanarak hello `publicIpAddress` komutu önceki hello hello çıktıda gösterilen. Bir bölüm ve dosya sistemi oluşturun, sonra hello veri diski bağlayabilir. Daha fazla bilgi için bkz: [tooa Linux VM toomount hello yeni disk bağlanmak](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). SSH oturumunuzu kapatın.


## <a name="encrypt-virtual-machine"></a>Sanal makine şifrele
tooencrypt hello sanal diskler, tüm hello önceki bileşenleri birlikte getirin:

1. Hello Azure Active Directory hizmet asıl ve parola belirtin.
2. Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.
3. Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.
4. Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.

VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable). Merhaba aşağıdaki örnek kullanır hello `$sp_id` ve `$sp_password` hello önceki değişkenlerinden `ad sp create-for-rbac` komutu:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Merhaba disk şifreleme işlemi toocomplete için biraz zaman alabilir. Merhaba işlemine hello durumunu izlemek [az vm şifreleme Göster](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Merhaba, benzer toohello aşağıdaki kesilmiş örneğine çıktı:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Merhaba durum beklemeniz hello işletim sistemi disk raporlar için **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Merhaba disk şifreleme işlemi hello önyükleme işlemi sırasında sonlandırılır, böylece şifrelemeyle yeniden hello durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Merhaba durum şimdi raporu hello işletim sistemi diski ve veri diski olarak **şifreli**.


## <a name="add-additional-data-disks"></a>Ek veri disklerinin ekleme
Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskler tooyour VM eklemek ve de şifreleme. Örneğin, ikinci bir sanal disk tooyour VM aşağıdaki şekilde ekleyin olanak sağlar:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Merhaba komutu tooencrypt hello sanal diskler gibi yeniden çalıştırın:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Sonraki adımlar
* Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).
* Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).
