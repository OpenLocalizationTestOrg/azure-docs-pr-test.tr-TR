---
title: aaaJoin RedHat Linux VM tooan Azure Active Directory DS | Microsoft Docs
description: "Nasıl toojoin var olan bir RedHat Enterprise Linux 7 VM tooan Azure Active Directory etki alanı hizmeti."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>RedHat Linux VM tooan Azure Active Directory etki alanı Hizmeti'ne katılın

Bu makalede, etki alanı toojoin Red Hat Enterprise Linux (RHEL) 7 sanal makine tooan Azure Active Directory etki alanı Hizmetleri (AADDS) nasıl yönetileceğini gösterir.  Hello gereksinimleri şunlardır:

- [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)

- [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)

- [DC bir Azure Active Directory etki alanı Hizmetleri](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Hızlı Komutlar

_Tüm örnekleri kendi ayarlarınızla değiştirin._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Hello azure CLI tooclassic dağıtım moda geç

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>RHEL sürüm ve görüntü arayın

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Redhat Linux VM oluşturma

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Güncelleştirme YUM paketleri

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Gerekli paketleri yüklemek

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Merhaba Linux sanal makinede yüklü gerekli hello paketlerini, hello sonraki görev toojoin hello sanal makine toohello yönetilen etki alanıdır.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Merhaba AAD etki alanı Hizmetleri yönetilen etki Bul

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Kerberos başlatma

Toohello 'AAD DC Yöneticiler' grubuna üye olduğu bir kullanıcı belirttiğinizden emin olun. Yalnızca bu kullanıcılar, bilgisayarlar toohello yönetilen etki alanına eklenebilir.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Merhaba makine toohello etki alanına katılma

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Merhaba makine birleştirilmiş toohello etki alanı olduğunu doğrulayın

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Sonraki Adımlar

* [Red Hat güncelleştirme altyapısı (RHUI) isteğe bağlı Red Hat Enterprise Linux VM'ler için Azure'da için](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Dağıtma ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
