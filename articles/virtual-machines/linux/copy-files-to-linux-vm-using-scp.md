---
title: "aaaMove tooand SCP ile Azure Linux Vm'lerden gelen dosyaları | Microsoft Docs"
description: "Güvenli bir şekilde dosyaları tooand SCP ve SSH anahtar çifti kullanarak azure'da bir Linux VM taşıyın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>SCP'yi kullanarak bir Linux VM dosyaları tooand Taşı

Bu makalede nasıl toomove tooan Azure Linux VM'de istasyonunuzu veya bir Azure güvenli kopyalama (SCP) kullanarak Linux VM tooyour iş istasyonunda, aşağı dosyaları gösterilmektedir. Hızlı ve güvenli bir şekilde, dosyalar, iş istasyonu ve bir Linux VM arasında taşıma Azure altyapınıza yönetmek için kritik öneme sahiptir. 

Bu makalede, bir Linux VM Azure kullanılarak dağıtılan gereksinim [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ayrıca, yerel bilgisayarınızda bir SCP istemcisi gerekir. SSH üzerinde oluşturulmuş ve hello varsayılan Bash kabuğunda çoğu Linux ve Mac bilgisayarların ve bazı Windows Kabukları dahil.

## <a name="quick-commands"></a>Hızlı komutlar

Bir Linux VM toohello dosyasını kopyalayın

```bash
scp file azureuser@azurehost:directory/targetfile
```

Linux VM hello aşağı dosya kopyalama

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

Örnekler, biz Azure yapılandırma dosyası tooa Linux VM Yukarı Taşı ve bir günlük dosyası dizini, çekme her ikisi de SCP ve SSH anahtarları kullanma.   

## <a name="ssh-key-pair-authentication"></a>SSH anahtar çifti kimlik doğrulaması

SCP SSH hello Aktarım katmanı için kullanır. SSH tanıtıcıları hello hello hedef ana bilgisayarda kimlik doğrulaması ve varsayılan olarak SSH ile sağlanan şifrelenmiş tüneli hello dosyasında taşır. SSH kimlik doğrulaması için kullanıcı adları ve parolalar kullanılabilir. Ancak, SSH ortak ve özel anahtar kimlik doğrulaması güvenlik açısından en iyisi önerilir. SSH hello bağlantı doğrulaması sonra SCP hello dosya kopyalama sonra başlar. Düzgün şekilde yapılandırılmış kullanarak `~/.ssh/config` ve yalnızca bir sunucu adı (veya IP adresi) kullanarak SSH ortak ve özel anahtarlar, hello SCP bağlantı kurulabileceği. Yalnızca bir SSH anahtarı varsa, SCP için hello görünüyor `~/.ssh/` dizini ve varsayılan toolog toohello VM içinde tarafından kullanır.

Yapılandırma hakkında daha fazla bilgi için `~/.ssh/config` ve SSH ortak ve özel anahtarları bkz [oluşturma SSH anahtarları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP dosya tooa Linux VM

Merhaba ilk örnek için kullanılan toodeploy Otomasyon olan bir Linux VM tooa bir Azure yapılandırma dosyasını kopyalayın. Bu dosya gizli kod dizeleri içerir, Azure API kimlik bilgilerini içerdiğinden güvenlik önemlidir. SSH tarafından sağlanan hello şifrelenmiş tünel hello hello dosyasının içeriğini korur.

komut kopyaları hello yerel Hello *.azure/config* tooan Azure VM FQDN ile dosya *myserver.eastus.cloudapp.azure.com*. hello yönetici kullanıcı adı'hello Azure VM üzerinde *azureuser* . Merhaba hedeflenen toohello dosyasıdır */home/azureuser/* dizin. Bu komutta kendi değerlerinizi yerleştirin.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>SCP bir dizinden bir Linux VM

Bu örnekte, hello Linux VM tooyour iş istasyonu aşağı gelen bir dizin günlük dosyaları kopyalayın. Bir günlük dosyası olabilir veya hassas veya gizli verileri içerebilir. Ancak, SCP'yi kullanarak hello günlük dosyalarını Merhaba içeriğine şifrelenmiş sağlar. SCP tootransfer hello dosyaları kullanmaktır hello en kolay yolu tooget hello günlük dizini ve tooyour iş istasyonu aşağı dosyaları da güvenli devam ederken.

Merhaba aşağıdaki komut dosyaları hello kopyalar */home/azureuser/günlükleri/* hello Azure VM toohello yerel tmp dizininde dizininde:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Merhaba `-r` CLI bayrak SCP toorecursively kopyalama hello dosyaları ve dizinleri hello komutta listelenen hello dizininin hello noktasından söyler.  Ayrıca komut satırı sözdizimi hello bildiriminin benzer tooa geldiği `cp` kopyalama komutu.

## <a name="next-steps"></a>Sonraki adımlar

* [Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
