---
title: "aaaDetailed adımları toocreate bir SSH anahtar çifti Azure Linux VM'ler için | Microsoft Docs"
description: "Farklı kullanım örnekleri için belirli sertifikalar yanı sıra, azure'daki Linux VM'ler için ek adımlar toocreate bir SSH ortak ve özel anahtar çifti öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Toocreate SSH anahtar çiftiniz ve azure'da bir Linux VM için ek sertifika aracılığıyla ayrıntılı ilerlemesi
SSH anahtar çifti ile Parolaları toolog hello gereksinimini toousing SSH anahtarları kimlik doğrulama için varsayılan Azure üzerinde sanal makineleri oluşturabilirsiniz. Parolalar, tahmin edilebilir ve parolanızı toorelentless yanılma denemeleri tooguess, Vm'leri açın. Hello Azure CLI ya da Resource Manager şablonları ile oluşturulan VM'ler SSH ortak anahtarınız için SSH parolalı oturum açma devre dışı bırakma post dağıtım yapılandırma adımı kaldırma hello dağıtımının bir parçası olarak dahil edebilirsiniz. Bu makalede ayrıntılı adımlar ve ek örnekler oluşturma sertifikaların gibi Linux sanal makineleri ile kullanılmak üzere sağlar. Tooquickly istiyorsanız oluşturmak ve SSH anahtar çiftini kullanın, bkz: [nasıl toocreate bir SSH ortak ve özel anahtarı eşleştirin Azure Linux VM'ler için](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>SSH anahtarlarını anlama

SSH ortak ve özel anahtarları hello en kolay yolu toolog tooyour Linux sunucularda kullanmaktır. [Ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) kolayca deneme yanılmayla parolalara göre çok daha güvenli bir şekilde toolog tooyour Linux içinde veya Azure BSD VM'de sağlar.

Ortak anahtarınız herkesle paylaşılabilir; ancak, özel anahtarınıza yalnızca siz (veya yerel güvenlik altyapınız) sahip olursunuz.  Hello SSH özel anahtara sahip bir [çok güvenli parola](https://www.xkcd.com/936/) (kaynak:[xkcd.com](https://xkcd.com)) toosafeguard onu.  Bu parolayı yalnızca tooaccess hello özel SSH anahtar dosyası olduğunu ve **değil** hello kullanıcı hesabı parolası.  Bir parola tooyour SSH anahtarı eklediğinizde, böylece hello özel anahtar hello parola toodecrypt gereksizdir, 128 bit AES kullanarak hello özel anahtarı şifreler.  Bir saldırgan özel anahtarınızı çalıntı varsa ve anahtarı bir parola sahip değilse, bu özel mümkün toouse olacaktır hello karşılık gelen ortak anahtara sahip bir tooany sunucuya toolog anahtarı.  Özel anahtar parola korumalı ise, Azure’daki altyapınız için ek bir güvenlik katmanı sağlayarak, bu saldırgan tarafından kullanılamaz.

Bu makalede, Azure Resource Manager ile dağıtımlar için önerilen 2 RSA ortak ve özel anahtar dosyası çifti (Ayrıca başvurulan tooas "ssh-rsa" anahtarlar), bir SSH Protokolü sürüm oluşturur. *SSH-rsa* anahtarları hello üzerinde gerekli [portal](https://portal.azure.com) Klasik ve Resource Manager dağıtımları için.

## <a name="ssh-keys-use-and-benefits"></a>SSH anahtarlarının kullanımı ve avantajları

En az 2048 bit, Azure gerektirir SSH Protokolü sürüm 2, RSA biçimi ortak ve özel anahtarları; Merhaba ortak anahtar dosyası sahip hello `.pub` kapsayıcı biçimi. toocreate hello anahtarları kullanmak `ssh-keygen`, bir seri soru soran ve özel anahtar ve eşleşen ortak anahtarı yazar. Bir Azure VM oluşturulduğunda, ortak anahtar toohello Azure kopyaları hello `~/.ssh/authorized_keys` hello VM klasörü. SSH anahtarları `~/.ssh/authorized_keys` kullanılan toochallenge hello istemci toomatch hello karşılık gelen özel anahtar bir SSH oturum açma bağlantısı.  Kimlik doğrulaması için SSH anahtarları kullanarak bir Azure Linux VM oluşturulduğunda, Azure hello SSHD yapılandırır sunucu toonot izin parola oturum açmalar, yalnızca SSH anahtarları.  Bu nedenle, SSH anahtarları ile Azure Linux VM'ler oluşturarak, kendiniz hello parolalarda devre dışı bırakma hello tipik dağıtım sonrası yapılandırma adımı kaydedin ve güvenli hello VM dağıtımı yardımcı olabilir **sshd_config** dosya.

## <a name="using-ssh-keygen"></a>SSH-keygen’i kullanma

Bu komut, 2048 bit RSA kullanarak (şifrelenmiş) SSH anahtar çifti güvenli bir parola oluşturur ve onu geçersiz kılınan tooeasily tanımlayın.  

SSH anahtarları hello tutulan varsayılan olan `~/.ssh` dizini.  Yoksa bir `~/.ssh` dizin, hello `ssh-keygen` komut oluşturur, sizin için hello ile doğru izinleri.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Komut açıklaması*

`ssh-keygen`Merhaba kullanılan program toocreate hello anahtarları =

`-t rsa`Merhaba RSA biçimi [wikipedia] olan anahtar toocreate türü =[sonunda parens](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` hello anahtar bitleri =

`-C "azureuser@myserver"`Merhaba ortak anahtar dosyası tooeasily eklenmiş toohello sonuna tanımlamak açıklama =.  Normalde hello açıklama olarak bir e-posta kullanılır ancak iyi ne olursa olsun, altyapınız için kullanabilirsiniz.

## <a name="classic-deploy-using-asm"></a>`asm` kullanarak klasik dağıtım

Merhaba Klasik dağıtım modeli kullanılıyorsa (`asm` hello CLI moduna), bir SSH-RSA ortak anahtar kullanabilir veya bir RFC4716 biçimlendirilmiş pem kapsayıcısında anahtar.  Merhaba SSH-RSA ortak anahtardır daha önce bu makalede kullanarak oluşturulan öğeleri `ssh-keygen`.

Mevcut bir SSH ortak anahtarı anahtarından toocreate bir RFC4716 biçimlendirilmiş:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen örneği

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
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

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

Bu makalede Hello anahtar çifti adı.  Adlı bir anahtar çiftine **id_rsa** hello varsayılandır ve bazı araçlar hello bekleyebilirsiniz **id_rsa** tane olması iyi bir fikirdir böylece özel anahtar dosya adı. Merhaba dizin `~/.ssh/` SSH anahtar çiftleriniz ve hello SSH yapılandırma dosyası için hello varsayılan konumdur.  Bir tam yol belirtilmezse `ssh-keygen` hello anahtarları hello geçerli çalışma dizini içinde hello varsayılan oluşturur `~/.ssh`.

Merhaba listesini `~/.ssh` dizin.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Anahtar Parolası:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`tooa parola hello özel anahtar dosyası için "parola." anlamına gelir.  Bu *kesinlikle* parola tooyour özel anahtar tooadd önerilir. Bir parola koruma hello anahtar dosyası, hello dosya kimseyle bunu hello karşılık gelen ortak anahtarı var. tooany Server'daki toolog kullanabilirsiniz. Bir parola (parola) katıştırılabilecek daha fazla koruma birisi mümkün toogain erişim tooyour özel anahtar dosyası olması durumunda, size verilen zaman toochange hello anahtarları tooauthenticate kullanılan.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>SSH aracı toostore özel anahtar parolanızı kullanma

Her SSH oturumu açışınızda özel anahtar dosya parolanızı yazmaya tooavoid kullanabileceğiniz `ssh-agent` toocache özel anahtar dosya parolanızı. Mac kullanıyorsanız, çağırdığınızda hello OSX Anahtarlığa güvenli bir şekilde hello özel anahtar parolaları depolar `ssh-agent`.

Doğrulayın ve ssh aracı ve ssh-tooinform hello SSH sistemi hello anahtar dosyaları hakkında hello parola etkileşimli olarak kullanılan toobe ihtiyacınız olmadığından böylece ekleyin.

```bash
eval "$(ssh-agent -s)"
```

Şimdi hello özel anahtarı çok ekleyin`ssh-agent` hello komutunu kullanarak `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Merhaba özel anahtar parolası şimdi depolanır `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>Kullanarak `ssh-copy-id` toocopy hello anahtar tooan VM var
Bir VM zaten oluşturduysanız hello yeni SSH ortak anahtarı tooyour Linux VM yükleyebilirsiniz ile:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>SSH yapılandırma dosyası oluşturma ve yapılandırma

Önerilen bir en iyi yöntem toocreate olduğundan ve yapılandırma bir `~/.ssh/config` dosya toospeed yukarı oturum açmalar ve SSH istemci davranışını en iyi duruma getirme için.

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

Sonraki yukarı toocreate Azure Linux VM'ler hello yeni SSH ortak anahtarını kullanıyor.  Hello oturum açma olarak bir SSH ortak anahtarıyla oluşturulan azure VM'ler, daha iyi parolalar hello varsayılan oturum açma yöntemi ile oluşturulan VM'ler daha güvenli.  SSH anahtarları kullanılarak oluşturulan Azure VM'ler, varsayılan olarak parola kullanımı devre dışı bırakılmış şekilde yapılandırılır; böylece parola tahminiyle gerçekleştirilen saldırı girişimleri önlenir.

* [Azure şablonu kullanarak güvenli bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure portal kullanarak güvenli bir Linux VM oluşturma](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello Azure CLI kullanarak güvenli bir Linux VM oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
