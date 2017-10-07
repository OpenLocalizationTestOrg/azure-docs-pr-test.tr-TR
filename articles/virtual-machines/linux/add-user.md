---
title: "aaaAdd kullanıcı tooa Azure Linux VM'de | Microsoft Docs"
description: "Bir kullanıcı tooa Linux VM Azure üzerinde ekleyin."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Bir kullanıcı tooan Azure VM ekleme
Yeni bir Linux VM ilk görevlerde hello toocreate yeni bir kullanıcı biridir.  Bu makalede, biz oluşturmada size sudo kullanıcı hesabı, hello parola ayarlama, SSH ortak anahtarları ekleme yol ve son olarak `visudo` tooallow sudo parolasız.

Önkoşullar şunlardır: [bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/), [SSH ortak ve özel anahtarları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), bir Azure kaynak grubu ve hello Azure CLI yüklenmiş ve tooAzure Resource Manager modunu kullanarak geçiş `azure config mode arm`.

## <a name="quick-commands"></a>Hızlı Komutlar
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Ayrıntılı Kılavuz
### <a name="introduction"></a>Giriş
Yeni bir sunucu ile Merhaba ilk ve en yaygın görevi tooadd bir kullanıcı hesabı biridir.  Kök oturum açmalar devre dışı bırakılmalıdır ve hello kök hesabının kendisi Linux sunucunuzla, yalnızca sudo kullanılmamalıdır.  Bir kullanıcı kök yükseltme uygun şekilde tooadminister hello ve Linux kullanmak sudo kullanılarak ayrıcalıkları vermek.

Merhaba komutunu kullanarak `useradd` kullanıcı hesapları toohello Linux VM ekliyoruz.  Çalışan `useradd` değiştirir `/etc/passwd`, `/etc/shadow`, `/etc/group`, ve `/etc/gshadow`.  Bir komut satırı bayrağı toohello ekliyoruz `useradd` komutu tooalso Linux'ta hello yeni kullanıcı toohello uygun sudo gruba ekleyin.  Hatta sen `useradd` içine bir giriş oluşturur `/etc/passwd` hello yeni kullanıcı hesabı parola sağlamaz.  Merhaba basit kullanarak hello yeni kullanıcı için bir başlangıç parolası oluşturuyoruz `passwd` komutu.  Merhaba son toomodify hello sudo tooallow tooenter her komut için bir parola gerek kalmadan bu kullanıcı tooexecute komutları sudo ayrıcalıklarıyla kuralları adımdır.  Bu kullanıcı hesabı varsayıyoruz hello özel anahtarı kullanarak oturum kötü aktörlerden güvendedir ve bir parola olmadan tooallow sudo erişim geçiyor.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Bir tek sudo kullanıcı tooan Azure VM ekleme
İçinde toohello Azure VM SSH anahtarları kullanarak oturum açın.  Kurulum SSH ortak anahtar erişimi varsa, bu makalenin ilk tamamlamak [kullanan ortak anahtar kimlik doğrulaması ile Azure](http://link.to/article).  

Merhaba `useradd` komutu hello aşağıdaki görevleri tamamlar:

* Yeni bir kullanıcı hesabı oluşturma
* Merhaba ile yeni bir kullanıcı grubu oluşturma aynı adı
* boş bir girdiyi çok ekleme`/etc/passwd`
* boş bir girdiyi çok ekleme`/etc/gpasswd`

Merhaba `-G` komut satırı bayrağı hello yeni kullanıcı hesabı kök yükseltme ayrıcalıkları vermek hello yeni kullanıcı hesabı toohello uygun Linux grubu ekler.

#### <a name="add-hello-user"></a>Merhaba kullanıcı ekleme
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Bir parola ayarlama
Merhaba `useradd` komut hello kullanıcı oluşturur ve bir giriş tooboth ekler `/etc/passwd` ve `/etc/gpasswd` gerçekten hello parola ayarlı değil ancak.  Merhaba parola hello kullanarak toohello girişini eklenir `passwd` komutu.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Şimdi sudo ayrıcalıklarına sahip bir kullanıcı hello sunucuda sahibiz.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>SSH ortak anahtarı toohello yeni kullanıcı hesabınızı ekleme
Merhaba, makinenizden kullanmak `ssh-copy-id` hello yeni parolayla komutu.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Visudo tooallow sudo kullanımı bir parola olmadan kullanma
Kullanarak `visudo` tooedit hello `/etc/sudoers` dosya yanlış bu önemli dosyasını değiştirerek karşı koruma birkaç katmanları ekler.  Yürütme sırasında `visudo`, hello `/etc/sudoers` dosyasıdır kilitli tooensure etkin olarak düzenlenmekte olan sırada başka bir kullanıcı değişiklik yapabilirsiniz.  Merhaba `/etc/sudoers` dosya da denetlenir hatalardan kaynaklanan `visudo` ne zaman toosave denemek veya çıkış bozuk sudoers dosyası kaydedilemiyor.

Biz zaten sudo erişim hello doğru varsayılan grubundaki kullanıcılar.  Şimdi Biz bu grupları toouse sudo parolasız tooenable çağıracaksınız.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Merhaba kullanıcı ssh anahtarları ve sudo doğrulayın
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
