---
title: "aaaConfigure SSHD Azure Linux sanal makineler üzerinde | Microsoft Docs"
description: "SSHD en iyi güvenlik uygulamaları ve toolockdown SSH tooAzure Linux sanal makineleri için yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Azure Linux VM'ler üzerinde SSHD yapılandırın

Bu makalede nasıl toolockdown hello SSH sunucuda Linux, tooprovide en iyi yöntemler güvenlik ve ayrıca toospeed hello SSH oturum açma işlemini yerine parolaları SSH anahtarları kullanılarak gösterilmektedir.  toofurther kilitleme mümkün toologin olmaktan biz toodisable hello kök kullanıcının kalacaklarını SSHD SSH Protokolü sürüm 1 devre dışı bırakma toologin bir onaylanmış Grup listesi aracılığıyla izin verilen hello kullanıcıları sınırlamak, en az bir anahtar bit ayarlamak ve otomatik oturum kapatma boşta kullanıcıların yapılandırın.  Bu makale için Hello gereksinimleri şunlardır: bir Azure hesabı ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Hızlı Komutlar

Yapılandırma `/etc/ssh/sshd_config` ayarları aşağıdaki hello ile:

### <a name="disable-password-logins"></a>Parola oturum açmalar devre dışı bırak

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Oturum açma hello kök kullanıcı tarafından devre dışı bırak

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>İzin verilen grupların listesini

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>İzin verilen kullanıcılar listesi

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>SSH Protokolü sürüm 1 devre dışı bırak

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>En az anahtar bitleri

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Boşta kullanıcıların bağlantısını kesin

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Ayrıntılı Kılavuz

SSHD hello SSH hello Linux VM üzerinde çalışan sunucu ' dir.  SSH, MacBook Linux iş istasyonunda, üzerinde bir kabuk ya da bir Bash Windows çalıştıran bir istemci olur.  SSH de hello Protokolü toosecure kullanılan ve iş istasyonu ve hello Linux SSH ayrıca VPN (sanal özel ağ) oluşturma VM arasındaki hello iletişimi şifrelemek olur.

Bu makalede, bu Linux VM açmak hello tüm gözden geçirme için çok önemli tookeep bir oturum açma tooyour olur.  Bir SSH bağlantısı kurulduktan sonra hello penceresi kapalı olduğu sürece, açık bir oturum olarak kalır.  ' De, oturum açmış bir terminal sağlar değişiklikleri yapılan toobe toohello için SSHD hizmeti önemli bir değişiklik yaptıysanız, kilitlenmelerini olmadan.  Linux VM'NİZDE bozuk SSHD yapılandırmasıyla dışında kilitlenmesine, Azure hello özelliği tooreset hello bozuk SSHD yapılandırmayla sunar. [Azure VM erişim uzantısı](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu nedenle şu iki Terminal ve SSH toohello Linux VM hem de bunların açın.  Biz hello ilk terminal toomake hello değişiklikleri tooSSHDs yapılandırma dosyası kullanın ve hello SSHD hizmetini yeniden başlatın.  Merhaba ikinci terminal tootest hello hizmet yeniden başlatıldıktan sonra bu değişiklikleri kullanırız.  Biz SSH parolaları devre dışı ve kesinlikle SSH anahtarları üzerinde SSH anahtarlarınız doğru değildir ve hello bağlantı toohello VM kapatırsanız bağlı olan hello VM kalıcı olarak kilitli ve hiç kimse silinir ve yeniden toobe gerektiren mümkün toologin tooit olacaktır.

## <a name="disable-password-logins"></a>Parola oturum açmalar devre dışı bırak

hızlı şekilde toosecure hello Linux VM olduğunu toodisable parola oturum açma bilgileri.  Parola kullanarak oturum açamayan etkinleştirildiğinde, gezinme hello web toobrute çalışırken başlayacaktır aracılarını tahmin hello parola SSH kullanarak, Linux VM için zorlar.  Parola kullanarak oturum açamayan tamamen devre dışı bırakma, tüm parola oturum açma denemesi hello SSH sunucu tooignore sağlar.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Oturum açma hello kök kullanıcı tarafından devre dışı bırak

Aşağıdaki Linux en iyi yöntemler, hello `root` kullanıcı hiçbir zaman oturum açmış olmanız halinde SSH veya kullanarak üzerinden `sudo su`.  Kök düzeyinde izinler gerektiren tüm komutları hello her zaman çalışması gerektiğini `sudo` gelecekteki denetlemek için tüm eylemleri kaydeder komutu.  Devre dışı bırakma hello `root` SSH yoluyla açmasını kullanıcıdır tooSSH yalnızca yetkili kullanıcılar izin verilen sağlayan bir güvenlik en iyi yöntemler adımı.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>İzin verilen grupların listesini

SSH SSH üzerinden oturum açmayı gelen kullanıcılar ve izin verilen veya izin verilmeyen Grup kısıtlama bir yöntem sunar.  Bu özellik belirli kullanıcılar ve gruplar açmasını Engelle veya listeleri tooapprove kullanır.  Merhaba tekerleği Grup toohello ayarı `AllowGroups` listesi hello tekerleği grubunda yer alan SSH toojust kullanıcı hesapları üzerinden onaylanan oturumları kısıtlar.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>İzin verilen kullanıcılar listesi

SSH oturumu açma toojust kullanıcılar sınırlandırma olduğu tooaccomplish aynı hello daha belirli bir şekilde görev `AllowGroups` değil.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>SSH Protokolü sürüm 1 devre dışı bırak

SSH Protokolü sürüm 1 güvenli değil ve devre dışı bırakılması gerekir.  SSH Protokolü sürüm 2 güvenli şekilde tooSSH tooyour sunucusu sunar hello geçerli sürümdür.  SSH sürüm 1 devre dışı bırakma tooestablish çalıştığınız SSH istemcilere SSH sürüm 1 kullanılarak hello SSH sunucusuyla bir bağlantı reddeder.  SSH sürüm 2 bağlantıları toonegotiate izin yalnızca hello SSH sunucusuyla bir bağlantı.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>En az anahtar bitleri

Aşağıdaki en iyi güvenlik uygulamaları, parola SSH oturumu açma devre dışı bırakılır ve yalnızca SSH anahtarları toobe tooauthenticate hello SSH sunucusuyla kullanılan izin verilir.  Bu SSH anahtarları bit cinsinden ölçülen farklı uzunlukta anahtarlar kullanılarak oluşturulabilir.  En iyi anahtarlarının uzunluğu 2048 bit hello minimum kabul edilebilir anahtarı kuvvetini olduğunu durumları yöntemler.  Teorik olarak az 2048 bit anahtarları bozuk olabilir.  Ayar hello `ServerKeyBits` çok`2048` 2048 bit veya daha büyük tuşlarıyla bağlantılarına izin veren ve az 2048 bit bağlantı reddedilecek.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Boşta kullanıcıların bağlantısını kesin

SSH birden çok belirlenen süre saniye boyunca boşta kaldığı açık bağlantıları olan hello özelliği toodisconnect kullanıcılar sahiptir.  Açık oturumu tooonly etkin sınırları hello hello Linux VM riskini bu kullanıcılar kalmasını sağlar.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>SSHD yeniden başlatın

tooenable hello ayarlarında `/etc/ssh/sshd_config` hello SSH sunucu yeniden başlatıldıktan hello SSHD işlemini yeniden başlatın.  toorestart hello SSH sunucusu kullandığınız hello terminal penceresi açık kaldığını hello açık SSH oturumu kaybetmeden.  İkinci bir terminal penceresi veya sekmesinde tootest hello yeni SSH server ayarlarını kullanın.  Ayrı terminal tootest hello SSH bağlantısını kullanarak verir geri toogo ve yapma ek değişiklikler toohello `/etc/ssh/sshd_config` göre önemli bir SSHD değişiklik kilitlenmelerini olmadan ilk Terminal Merhaba,.  

### <a name="on-redhat-centos-and-fedora"></a>RedHat, Centos ve Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Debian ve Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Azure sıfırlama erişimi kullanarak SSHD Sıfırla

Son değişiklik toohello SSHD yapılandırma kilitli olmadığını hello Azure VM erişim-uzantısı tooreset hello SSHD yapılandırma geri toohello özgün yapılandırmayı kullanabilirsiniz.

Tüm örnek adları kendi ile değiştirin.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Fail2ban yükleyin

Hangi blokları denemeleri toologin tooyour Linux VM yanılma kullanarak SSH üzerinde yinelenen tooinstall ve Kurulum hello açık kaynak uygulama Fail2ban, kesinlikle önerilir.  Yinelenen Fail2ban günlükleri denemeleri toologin SSH üzerinde başarısız oldu ve ardından güvenlik duvarı kuralları hello denemeleri kaynaklanan tooblock başlangıç IP adresi oluşturur.

* [Fail2ban giriş sayfası](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Sonraki Adımlar

Artık, yapılandırılmış ve Linux VM üzerinde hello SSH sunucuyu kilitli izleyebilirsiniz ek güvenlik en iyi yöntemler vardır.  

* [Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Hello Azure CLI kullanarak bir Linux VM disklerde şifrele](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Azure Resource Manager şablonları güvenlik ve erişim](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
