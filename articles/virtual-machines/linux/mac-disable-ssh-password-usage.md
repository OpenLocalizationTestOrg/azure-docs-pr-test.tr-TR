---
title: "aaaDisable SSH parolaları SSHD yapılandırarak, Linux VM'de | Microsoft Docs"
description: "Azure üzerinde Linux VM için SSH parolalı oturum açma devre dışı bırakarak güvenli hale getirin."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Linux VM SSH parolalarını SSHD yapılandırarak devre dışı bırak
Bu makalede odaklanılmaktadır toolock hello oturum açma güvenlik Linux VM kapalı.  SSH bağlantı noktası 22'Hello açıldığında hemen toohello world aracılarını parolalarını tahmin toologin çalışırken başlatın.  Biz bu makalede ne yapacağını parola kullanarak oturum açamayan SSH üzerinden devre dışı değil.  Merhaba özelliği tamamen kaldırarak saldırı Biz bu kaba türünden hello Linux VM koruma toouse parolaları zorlar.  Merhaba eklenir ödül biz Linux tooonly izin SSHD yapılandıracağınız SSH ortak ve özel anahtarlar aracılığıyla oturumları kullanarak en güvenli yolu toologin tooLinux hello.  Merhaba olası birleşimlerini onu tooguess hello özel anahtarı büyük ve bu nedenle bile tootry toobrute zorla SSH anahtarları rahatsız etme gelen aracılarını zorlaştırır gerektirir.

## <a name="goals"></a>Hedefleri
* SSHD toodisallow yapılandırın:
  * Parola oturum açmalar
  * Kök kullanıcı oturum açma
  * Sınama yanıtı kimlik doğrulaması
* SSHD tooallow yapılandırın:
  * yalnızca SSH anahtar oturumları
* Hala oturum açmış durumdayken SSHD yeniden başlatın
* Test hello yeni SSHD yapılandırma

## <a name="introduction"></a>Giriş
[Tanımlanan SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD hello SSH hello Linux VM üzerinde çalışan sunucu ' dir.  SSH Kabuğu'ndan MacBook ya da Linux iş istasyonunuza çalıştıran bir istemci olur.  SSH de hello Protokolü toosecure kullanılan ve iş istasyonu ve hello Linux VM arasındaki hello iletişimi şifrelemek olur.

Bu makale için bu Linux VM hello tüm açık size yol çok önemli tookeep bir oturum açma tooyour olur.  Bu nedenle şu iki Terminal ve SSH toohello Linux VM hem de bunların açılır.  Biz hello ilk terminal toomake hello değişiklikleri tooSSHDs yapılandırma dosyası kullanın ve hello SSHD hizmetini yeniden başlatın.  Merhaba ikinci terminal tootest hello hizmet yeniden başlatıldıktan sonra bu değişiklikleri kullanacağız.  Biz SSH parolaları devre dışı ve kesinlikle SSH anahtarları üzerinde SSH anahtarlarınız doğru değildir ve hello bağlantı toohello VM kapatırsanız bağlı olan hello VM kalıcı olarak kilitli ve hiç kimse silinir ve yeniden toobe gerektiren mümkün toologin tooit olacaktır.

## <a name="prerequisites"></a>Ön koşullar
* [Azure Linux VM'ler için Linux ve Mac'de SSH anahtarları oluşturma](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure hesabı
  * [ücretsiz deneme kaydolma](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure portal](http://portal.azure.com)
* Linux azure üzerinde çalışan VM
* SSH ortak ve özel anahtar çiftini`~/.ssh/`
* SSH ortak anahtarını `~/.ssh/authorized_keys` hello Linux VM üzerinde
* Merhaba VM Sudo hakları
* Bağlantı noktası 22 Aç

## <a name="quick-commands"></a>Hızlı Komutlar
*Merhaba TLDR sürümü yalnızca isteyen dönemlik Linux Admins buradan başlayın.  Bu bölümde ayrıntılı bir açıklama ve ilerleme herkes için başka hello istediği atlayın.*

```bash
sudo vim /etc/ssh/sshd_config
```

Merhaba yapılandırma dosyası şu şekilde düzenleyin:

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Merhaba SSHD hizmetini yeniden başlatın. Debian tabanlı distro'lar üzerinde:

```bash
sudo service ssh restart
```

Red Hat tabanlı distro'lar üzerinde:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Aracılığıyla ayrıntılı ilerlemesi
Oturum açma toohello Linux VM terminal 1 (T1).  Oturum açma toohello Linux VM terminal 2 (T2).

Üzerinde T2 biz tooedit hello SSHD yapılandırma dosyası adımıdır.  

```bash
sudo vim /etc/ssh/sshd_config
```

Buradan biz yalnızca hello ayarları toodisable parolaları düzenleyin ve SSH anahtar oturum açmayı etkinleştirebilir.  Araştırma ve gerekir toomake Linux & SSH gerektiği kadar güvenli değiştirmek, bu dosyada birçok ayarları vardır.

#### <a name="disable-password-logins"></a>Parola oturum açmalar devre dışı bırak

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Ortak anahtar kimlik doğrulamasını etkinleştir

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Kök oturum açma devre dışı bırak

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Sınama yanıtı kimlik doğrulamasını devre dışı
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>SSHD yeniden başlatın
Merhaba T1 Kabuğu'ndan, hala oturum açtığınızdan emin olun.  Bu, SSH anahtarlarınız doğru değilse parolaları şimdi devre dışı olduğundan, VM dışında kilitlenmesine değil için önemlidir.  Herhangi bir ayar, hala kaydedilir ve SSH hello bağlantı Canlı SSHD hizmet hello sırasında tutar T1 toofix sshd_config kullanabilirsiniz, Linux VM'de hatalıysa yeniden başlatın.

T2 çalıştırın:

##### <a name="on-hello-debian-family"></a>Debian ailesi Hello üzerinde
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>RedHat ailesi Hello üzerinde
```bash
sudo service sshd restart
```

Parolalar şimdi yanılma parola oturum açma saldırılara karşı korumaya, VM devre dışı bırakılır.  Yalnızca SSH izin anahtarlarla mümkün toologin daha hızlı ve daha güvenli olacaktır.

