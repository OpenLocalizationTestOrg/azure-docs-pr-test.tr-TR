---
title: "aaaCreate kullanımı bir SSH anahtar ve çifti Azure Linux VM'ler için | Microsoft Docs"
description: "Nasıl toocreate ve kullanımda bir SSH ortak ve özel anahtar çifti Linux VM'ler için Azure tooimprove hello kimlik doğrulama işlemi güvenliğini hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Azure Linux VM'ler için toocreate ve kullanım bir SSH ortak ve özel anahtarı nasıl eşleştirin
Güvenli Kabuk (SSH) anahtar çifti ile azure'da hello parolaları toolog gereksinimini kimlik doğrulaması için SSH anahtarları kullanan sanal makineleri (VM'ler) oluşturabilirsiniz. Bu makalede nasıl tooquickly oluşturmak ve bir SSH Protokolü sürüm 2 RSA ortak ve özel anahtar dosyası çifti Linux VM'ler için kullanma gösterilmektedir. Daha ayrıntılı adımları ve ek örnekler için bkz: [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>SSH anahtar çifti oluşturma
Kullanım hello `ssh-keygen` komutu hello oluşturulan varsayılan toocreate SSH ortak ve özel anahtar dosyaları `~/.ssh` dizin, ancak farklı bir konum ve ek parolayı (bir parola tooaccess hello özel anahtar dosyası) belirtebilirsiniz olduğunda istenir. Merhaba yanıtlama Bash Kabuk komut aşağıdaki hello çalıştırmak, kendi bilgilerle ister.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Merhaba SSH anahtar çiftini kullanın
azure'da, Linux VM Yerleştir hello ortak anahtarı olan depolanan varsayılan `~/.ssh/id_rsa.pub`, bunları oluşturduğunuzda hello konumu değiştirmediyse. Merhaba kullanırsanız [Azure CLI 2.0](/cli/azure) toocreate, VM hello kullandığınızda bu ortak anahtar hello konumunu belirtin [az vm oluşturma](/cli/azure/vm#create) hello ile `--ssh-key-path` seçeneği. Hello Azure portal veya Resource Manager şablonunda hello ortak anahtar dosyası toouse hello içeriğini kopyalayıp, tüm ek boşluk kopyalama emin olun. Örneğin, OS X kullanıyorsanız hello ortak anahtar dosyası iletebildiğiniz (varsayılan olarak, **~/.ssh/id_rsa.pub**) çok**pbcopy** toocopy hello içeriği (vardır gibiaynışeyihellodiğerLinuxprogramları`xclip`).

SSH ortak anahtarları hakkında bilgi sahibi değilseniz, aşağıdaki gibi `~/.ssh/id_rsa.pub` öğesini kendi ortak anahtar dosyası konumunuz ile değiştirip `cat` çalıştırarak ortak anahtarınızı görebilirsiniz:

```bash
cat ~/.ssh/id_rsa.pub
```

Merhaba ortak anahtarı ile Azure VM'de VM tooyour SSH kullanarak hello IP adresi veya VM DNS adını (tooreplace unutmayın `azureuser` ve `myvm.westus.cloudapp.azure.com` aşağıda hello yönetici kullanıcı adı ve hello tam etki alanı adı--veya IP adresi):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Anahtar çifti oluştururken bir parola sağladıysanız hello oturum açma işlemi sırasında istendiğinde hello parola girin. (Merhaba sunucu tooyour eklenen `~/.ssh/known_hosts` klasörü ve olmaz sorulan tooconnect yeniden hello ortak anahtar kadar Azure VM değişikliklerinizi veya hello sunucu adı kaldırılır `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Sonraki adımlar

SSH anahtarları kullanılarak oluşturulan sanal makineleri devre dışı parolaları ile yapılandırılmış varsayılan olarak, böylelikle daha pahalı olması ve bu nedenle zor deneme yanılma yoluyla yapılan zorla toomake tahmin çalışır. Bu konu başlığında, hızlı kullanım için basit bir SSH anahtar çifti oluşturma açıklanmaktadır. SSH anahtar çifti oluşturma daha fazla yardıma gereksinim veya ek sertifika gerektiren bakın [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).

Hello Azure portal, CLI ve şablonlar kullanarak, SSH anahtar çifti kullanan sanal makineleri oluşturabilirsiniz:

* [Hello Azure portal kullanarak güvenli bir Linux VM oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure CLI 2.0 kullanarak güvenli bir Linux VM oluşturma)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure şablonu kullanarak güvenli bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
