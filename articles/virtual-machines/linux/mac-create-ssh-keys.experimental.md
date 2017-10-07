---
title: "Azure üzerinde Linux VM'ler için aaaCreate bir SSH anahtar çifti | Microsoft Docs"
description: "Azure Linux VM'leri için güvenli bir şekilde SSH ortak ve özel anahtar çifti oluşturun."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Linux VM'ler için SSH ortak ve özel anahtar çifti oluşturma

Bu makalede nasıl toogenerate bir SSH Protokolü sürüm 2 RSA ortak ve özel anahtar çifti toouse Linux VM'ler ile dosya gösterilmektedir.  SSH anahtar çifti ile Parolaları toolog hello gereksinimini toousing SSH anahtarları kimlik doğrulama için varsayılan Azure üzerinde sanal makineleri oluşturabilirsiniz.  Parolalar, tahmin edilebilir ve parolanızı toorelentless yanılma denemeleri tooguess, Vm'leri açın. Azure şablonları veya hello ile oluşturulan VM'ler `azure-cli` SSH ortak anahtarınız için SSH parolalı oturum açma devre dışı bırakma post dağıtım yapılandırma adımı kaldırma hello dağıtımının bir parçası olarak dahil edebilirsiniz.

## <a name="quick-commands"></a>Hızlı Komutlar

Bash Kabuk komutları izleyerek, hello örnekleri kendi seçenekleri değiştirme hello çalıştırın.

SSH ortak anahtar dosyanız varsayılan olarak `~/.ssh/id_rsa.pub` konumunda oluşturulur. Komutu aşağıdaki hello kullanarak istendiğinde, "parola" toosecure özel anahtarınızı oluşturmanız gerekir. (Merhaba parola parola tooencrypt özel anahtarınızı kullanılır.)

```bash
ssh-keygen -t rsa -b 2048 
```

Yeni oluşturulan hello anahtar çok eklemek`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> komutları iş neredeyse tüm dağıtımlar, Linux işletim sistemlerinde yukarıda hello ancak hello ortamı tüketicisinin kısıtlanabilir gibi kapsayıcılara mutlaka çalışmıyor. 

## <a name="detailed-walkthrough"></a>Ayrıntılı Kılavuz

SSH ortak ve özel anahtarları hello en kolay yolu toolog tooyour Linux sunucularda kullanmaktır. [Ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) kolayca deneme yanılmayla parolalara göre çok daha güvenli bir şekilde toolog tooyour Linux içinde veya Azure BSD VM'de sağlar.

> [!IMPORTANT]
> Ortak anahtarınız herkesle paylaşılabilir; ancak, özel anahtarınıza yalnızca siz (veya yerel güvenlik altyapınız) sahip olursunuz.  Hello SSH özel anahtara sahip bir [çok güvenli parola](https://www.xkcd.com/936/) (kaynak:[xkcd.com](https://xkcd.com)) toosafeguard onu.  Bu parolayı yalnızca tooaccess hello özel SSH anahtarı olan ve **değil** hello kullanıcı hesabı parolası.  Bir parola tooyour SSH anahtarı eklediğinizde, böylece hello özel anahtar hello parola toodecrypt gereksizdir, 128 bit AES kullanarak hello özel anahtarı şifreler.  Bir saldırgan özel anahtarınızı çalıntı varsa ve anahtarı bir parola sahip değilse, bu özel mümkün toouse olacaktır hello karşılık gelen ortak anahtara sahip bir tooany sunucuya toolog anahtarı.  Özel anahtar parola korumalı ise, Azure’daki altyapınız için ek bir güvenlik katmanı sağlayarak, bu saldırgan tarafından kullanılamaz.

Bu makalede, Resource Manager hello üzerinde dağıtımlar için önerilen 2 RSA ortak ve özel anahtar dosyaları, SSH Protokolü sürüm oluşturur.  *SSH-rsa* anahtarları hello üzerinde gerekli [portal](https://portal.azure.com) Klasik ve Resource Manager dağıtımları için.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>SSH anahtarlarını kullanarak SSH parolalarını devre dışı bırakma

Azure en az 2048 bit, ssh-rsa biçimli ortak ve özel anahtarlar gerektirir. toocreate hello anahtarları kullanmak `ssh-keygen`, bir seri soru soran ve özel anahtar ve eşleşen ortak anahtarı yazar. Bir Azure VM oluşturulduğunda, hello ortak anahtar çok kopyalanır`~/.ssh/authorized_keys`.  SSH anahtarları `~/.ssh/authorized_keys` kullanılan toochallenge hello istemci toomatch hello karşılık gelen özel anahtar bir SSH oturum açma bağlantısı.  Kimlik doğrulaması için SSH anahtarları kullanarak bir Azure Linux VM oluşturulduğunda, Azure hello SSHD yapılandırır sunucu toonot izin parola oturum açmalar, yalnızca SSH anahtarları.  Bu nedenle, SSH anahtarları ile Azure Linux VM'ler oluşturarak, güvenli hello VM dağıtımı yardımcı olmak ve kendiniz hello sshd_config yapılandırma dosyası parolalar devre dışı bırakma hello tipik dağıtım sonrası yapılandırma adımı kaydedin.

## <a name="using-ssh-keygen"></a>SSH-keygen’i kullanma

Bu komut, 2048 bit RSA kullanarak (şifrelenmiş) SSH anahtar çifti güvenli bir parola oluşturur ve onu geçersiz kılınan tooeasily tanımlayın.  

SSH anahtarları hello tutulan varsayılan olan `~/.ssh` dizini.  Yoksa bir `~/.ssh` dizin, hello `ssh-keygen` komut oluşturur, sizin için hello ile doğru izinleri.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Komut açıklaması*

`ssh-keygen`Merhaba kullanılan program toocreate hello anahtarları =

`-t rsa`Merhaba RSA biçimi olan anahtar toocreate türü = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`BITS başlangıç anahtarı =


## <a name="classic-portal-and-x509-certs"></a>Klasik portal ve X.509 sertifikaları

Azure kullanıyorsanız hello [Klasik portal](https://manage.windowsazure.com/), hello SSH anahtarları için X.509 sertifikaları gerektirir.  Diğer SSH ortak anahtar türlerine izin verilmez, tümünün X.509 sertifikası *olması gerekir*.

toocreate varolan SSH-RSA özel anahtarınızı gelen bir X.509 sertifikası:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>`asm` kullanarak klasik dağıtım

Merhaba Klasik kullanıyorsanız, model dağıtma (CLI Azure Hizmet Yönetimi `asm`), bir SSH-RSA ortak anahtar kullanabilir veya bir RFC4716 biçimlendirilmiş anahtarını bir **.pem** kapsayıcı.  Merhaba SSH-RSA ortak anahtardır daha önce bu makalede kullanarak oluşturulan öğeleri `ssh-keygen`.

Mevcut bir SSH ortak anahtarı anahtarından toocreate bir RFC4716 biçimlendirilmiş:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen örneği

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Kaydedilen anahtar dosyaları:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

Bu makalede Hello anahtar çifti adı.  Adlı bir anahtar çiftine **id_rsa** hello varsayılandır ve bazı araçlar hello bekleyebilirsiniz **id_rsa** tane olması iyi bir fikirdir böylece özel anahtar dosya adı. Merhaba dizin `~/.ssh/` SSH anahtar çiftleriniz ve hello SSH yapılandırma dosyası için hello varsayılan konumdur.  Bir tam yol belirtilmezse `ssh-keygen` hello geçerli çalışma dizininde hello anahtarları oluşturma, varsayılan hello değil `~/.ssh`.

Merhaba listesini `~/.ssh` dizin.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Anahtar Parolası:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`"bir parola." tooa kullanılan parola tooencrypt hello özel anahtarı başvurur  Bu *kesinlikle* parola tooyour anahtar çiftleri tooadd önerilir. Bir parola koruma hello özel anahtar olmadan, hello anahtar dosyası olan herkes bu toolog hello karşılık gelen ortak anahtarı var. tooany Server'da kullanabilirsiniz. Bir parola katıştırılabilecek daha fazla koruma birisi mümkün toogain erişim tooyour özel anahtar dosyası olması durumunda, size zaman toochange hello anahtarları tooauthenticate kullanılan.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>SSH aracı toostore özel anahtar parolanızı kullanma

özel anahtarınızı yazarak tooavoid dosya parola her SSH oturum açma ile kullandığınız `ssh-agent` toocache özel anahtar dosya parolanızı. Mac kullanıyorsanız, çağırdığınızda hello OSX Anahtarlığa güvenli bir şekilde hello özel anahtar parolaları depolar `ssh-agent`.

Doğrulayın ve kullanmak `ssh-agent` ve `ssh-add` tooinform hello SSH sistemi hello anahtar dosyaları hakkında böylece hello parola etkileşimli olarak kullanılan toobe gerekli değildir.

```bash
eval "$(ssh-agent -s)"
```

Şimdi hello özel anahtarı çok ekleyin`ssh-agent` hello komutunu kullanarak `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Merhaba özel anahtar parolası şimdi depolanır `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Kullanarak `ssh-copy-id` tooinstall hello yeni anahtarı
Bir VM zaten oluşturduysanız aşağıdaki komut, hello VM kullanıcı adı ve hello sunucu adresi kendi değerlerinizle değiştirerek hello ile Merhaba yeni SSH ortak anahtarı tooyour Linux VM yükleyebilirsiniz:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>SSH yapılandırma dosyası oluşturma ve yapılandırma

En iyi yöntem toocreate olduğundan ve yapılandırma bir `~/.ssh/config` dosya toospeed yukarı oturum açmalar ve SSH istemci davranışını en iyi duruma getirme için.

Aşağıdaki örnek hello standart bir yapılandırmayı gösterir.

### <a name="create-hello-file"></a>Merhaba dosyası oluşturma

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Merhaba dosya tooadd hello yeni SSH yapılandırması düzenleyin:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Örnek `~/.ssh/config` dosyası:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Her sunucu tooenable için kendi özel anahtar çiftini her toohave bölümler bu SSH yapılandırma olanağı sağlar. Merhaba varsayılan ayarları (`Host *`) olan hello belirli ana bilgisayarlar yukarıya hello config dosyasına eşleşmeyen herhangi bir ana bilgisayar için.

### <a name="config-file-explained"></a>Yapılandırma dosyası açıklaması

`Host`Merhaba ana bilgisayar üzerinde hello terminal çağrılan Hello adı =.  `ssh fedora22`söyler `SSH` toouse hello hello ayarları blok etiketli değerlerde `Host fedora22` Not: ana bilgisayar kullanımınız için mantıklı olan ve hello gerçek ana bilgisayar herhangi bir sunucu adını temsil etmeyen her etiket olabilir.

`Hostname 102.160.203.241`Başlangıç IP adresi veya erişilen hello sunucusu için DNS adı =.

`User ahmet`Merhaba uzak kullanıcı hesabı toouse toohello Server'da oturum açarken =.

`PubKeyAuthentication yes`= istediğiniz toouse bir SSH anahtarı toolog SSH söyler.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`Merhaba SSH özel anahtar ve kimlik doğrulaması için karşılık gelen ortak anahtar toouse =.

## <a name="ssh-into-linux-without-a-password"></a>Parolasız Linux içine SSH

SSH anahtar çiftiniz ve yapılandırılmış bir yapılandırma dosyasına sahip olduğunuza göre hızlı ve güvenli bir şekilde tooyour Linux VM içinde mümkün toolog şunlardır. Merhaba, bir SSH anahtarı hello komut istemlerini kullanarak tooa Server'da hello parolası için bu anahtar dosyası için ilk oturum açışınızda.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Komut açıklaması

Zaman `ssh fedora22` yürütülür SSH ilk bulur ve hello tüm ayarları yükler `Host fedora22` blok yükler ve sonra tüm hello hello son blok ayarlarından kalan `Host *`.

## <a name="next-steps"></a>Sonraki Adımlar

Sonraki yukarı toocreate Azure Linux VM'ler hello yeni SSH ortak anahtarını kullanıyor.  Hello oturum açma olarak bir SSH ortak anahtarıyla oluşturulan azure VM'ler, daha iyi parolalar hello varsayılan oturum açma yöntemi ile oluşturulan VM'ler daha güvenli.  SSH anahtarları kullanılarak oluşturulan Azure VM'ler, varsayılan olarak parola kullanımı devre dışı bırakılmış şekilde yapılandırılır; böylece parola tahminiyle gerçekleştirilen saldırı girişimleri önlenir. SSH anahtar çifti oluşturma daha fazla yardıma gereksinim veya ek sertifika gerektiren gibi hello Klasik portal ile kullanmak için bkz: [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).

* [Azure şablonu kullanarak güvenli bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure portal kullanarak güvenli bir Linux VM oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure CLI kullanarak güvenli bir Linux VM oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
