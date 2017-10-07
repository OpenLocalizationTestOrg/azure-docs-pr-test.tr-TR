---
title: "aaaUse SSH anahtarları Windows'da Linux VM'ler için | Microsoft Docs"
description: "Toogenerate ve kullanım SSH anahtarları nasıl bir Windows bilgisayar tooconnect tooa Linux sanal makinede Azure ile ilgili bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Windows Azure üzerinde ile nasıl tooUse SSH anahtarları
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Azure'da tooLinux sanal makineler (VM'ler) bağlandığınızda, kullanması gereken [ortak anahtar şifrelemesini](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide tooyour Linux VM içinde daha güvenli bir şekilde toolog. Bu işlem, bir kullanıcı adı ve parola yerine hello güvenli Kabuk (SSH) komutu tooauthenticate kendiniz kullanarak ortak ve özel bir anahtar değişimi içerir. Parolalar web sunucuları gibi İnternete vm'lerinde özellikle savunmasız toobrute kuvvet saldırıları ' dir. Bu makalede SSH anahtarları ve nasıl toogenerate hello bir Windows bilgisayarda uygun anahtarlara genel bakış sağlar.

## <a name="overview-of-ssh-and-keys"></a>SSH ve anahtarları genel bakış
Tooyour Linux VM ortak ve özel anahtarları kullanarak güvenli bir şekilde kaydedebilirsiniz:

* Merhaba **ortak anahtar** Linux VM veya ortak anahtar şifrelemesinde toouse istediğiniz başka bir hizmet yerleştirilir.
* Merhaba **özel anahtarı** tooverify, oturum açtığınızda ne mevcut tooyour Linux VM olduğu kimliğinizi. Bu özel anahtarı koruyun. Özel anahtarı paylaşmayın.

Bu ortak ve özel anahtarlar, birden çok sanal makineleri ve hizmetleri üzerinde kullanılabilir. Her VM veya tooaccess istediğiniz hizmet için bir çift anahtar gerekmez. Daha ayrıntılı bir bakış için bkz: [ortak anahtar şifrelemesini](https://wikipedia.org/wiki/Public-key_cryptography).

SSH güvenli olmayan bağlantıları üzerinden güvenli oturum açma bilgileri veren bir şifreli bir bağlantı protokolüdür. Bunu hello varsayılan bağlantı Azure'da barındırılan Linux VM'ler için protokolüdür. SSH kendisini şifreli bir bağlantı sağlasa da, SSH bağlantılarla parolalarla hala hello VM savunmasız toobrute kuvvet saldırıları veya parolalarını tahmin bırakır. Bir daha güvenli ve tercih edilen bağlantı tooa SSH kullanarak VM bu ortak ve özel anahtarları olarak da bilinen SSH anahtarları kullanılarak yöntemidir.

Toouse SSH anahtarları istemiyorsanız hala tooyour Linux VM'ler bir parola kullanarak oturum açabilir. VM gösterilen toohello Internet değilse, parolaları kullanarak yeterli olabilir. Ancak, yine toomanage parolalarınızı için her bir Linux VM ve gerekir sağlıklı parola ilkeleri ve minimum parola uzunluğu ve bunları düzenli olarak güncelleştirilmesi gibi uygulamalarını korumak. SSH anahtarları Hello kullanımını arasında birden çok sanal makineleri tek tek kimlik bilgilerini yönetme hello karmaşıklığını azaltır.

## <a name="windows-packages-and-ssh-clients"></a>Windows paketleri ve SSH istemcileri
Tooand bağlanmak Azure kullanarak Linux sanal makineleri yönetme bir **SSH istemcisi**. Windows bilgisayarlarda yüklü olan bir SSH istemcisi genellikle yok. Bash için Windows Hello Windows 10 Anniversary güncelleştirme eklenir ve hello en son Windows 10 oluşturucuları güncelleştirmesi ek güncelleştirmeler sağlar. Bu Windows alt sistemi Linux için yerel bir Bash kabuğunda içinde bir SSH istemcisi gibi toorun ve erişim yardımcı programlarını sağlar. Ardından herhangi bir hello Linux belgeleri gibi izleyebilirsiniz [nasıl toogenerate SSH anahtarı için Linux çiftleri](mac-create-ssh-keys.md). Bash Windows halen geliştirilme aşamasındadır ve beta sürümü olarak kabul edilir. Windows için Bash hakkında daha fazla bilgi için bkz: [Bash Ubuntu Windows üzerinde](https://msdn.microsoft.com/commandline/wsl/about).

Toouse bir şey Windows dışındaki Bash isterseniz, yükleyebilmek için ortak Windows SSH istemcilerini paketleri aşağıdaki hello bulunmaktadır:

* [Windows için Git](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Dosyaları anahtar toocreate gerekiyor mu?
Azure en az 2048 bit gerektirir **ssh-rsa** ortak ve özel anahtarlar biçimlendirilmiş. Merhaba Klasik dağıtım modeli kullanarak Azure kaynaklarına yönetiyorsanız, toogenerate bir PEM da gerekir (`.pem` dosyası).

Merhaba dağıtım senaryoları ve her kullanan dosyaları hello türleri şunlardır:

1. **SSH-rsa** anahtarları hello kullanarak herhangi bir dağıtım için gerekli [Azure portal](https://portal.azure.com)ve Resource Manager dağıtımları hello kullanarak [Azure CLI](../../cli-install-nodejs.md).
   * Bu anahtarları, genellikle tüm çoğu kişi ihtiyacınız olan.
2. A `.pem` hello Klasik dağıtım kullanarak gerekli toocreate VM'ler bir dosyadır. Bu anahtarları Klasik dağıtımlarda hello kullanılırken desteklenen [Azure portal](https://portal.azure.com) veya [Azure CLI](../../cli-install-nodejs.md).
   * Merhaba Klasik dağıtım modeli kullanılarak oluşturulan kaynakları yönetiyorsanız, yalnızca toocreate bu ek anahtar ve sertifikalar gerekir.

## <a name="install-git-for-windows"></a>Windows için Git yükleme
Merhaba önceki bölümde listelenen hello dahil çeşitli paketler `openssl` Windows için aracı. Gerekli toocreate ortak ve özel anahtarlar aracıdır. örnekler ayrıntı nasıl aşağıdaki hello tooinstall ve **Windows için Git**tercih ettiğiniz hangi paket seçebilirsiniz ancak. **Windows için Git** toosome ek açık kaynaklı yazılım erişim verir ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) araçları ve yardımcı programları Linux VM'ler ile çalışırken, yararlı olabilir.

1. İndirme ve yükleme **Windows için Git** konumu aşağıdaki hello gelen: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Merhaba varsayılan seçenekleri hello sırasında yükleme işlemi toochange özellikle gerekmedikçe kabul bunları.
3. Çalıştırma **Git Bash** hello gelen **Başlat menüsü** > **Git** > **Git Bash**. Hello konsol benzer toohello örnek aşağıdaki gibidir:

    ![Windows için Git Bash Kabuk](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Özel bir anahtar oluşturun
1. İçinde **Git Bash** penceresi, kullanım `openssl.exe` toocreate bir özel anahtar. Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myPrivateKey` ve adlı sertifika `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    Hello çıkış benzer toohello örnek aşağıdaki gibidir:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Bash hata bildirirse, yeni bir açmayı deneyin **Git Bash** yükseltilmiş ayrıcalıklarla penceresi. Merhaba daha sonra yeniden `openssl` komutu.

2. Yanıt hello ülke adı, konumu, kuruluşunuzun adı, vb. için ister.
3. Yeni özel anahtar ve sertifika, geçerli çalışma dizini içinde oluşturulur. Bir güvenlik önlemi olarak, böylece yalnızca erişebilir özel anahtarınızı hello izinleri ayarlamalısınız:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Merhaba [sonraki bölümde](#create-a-private-key-for-putty) PuTTYgen tooboth kullanarak ayrıntılarını görüntülemek ve hello ortak anahtarı kullanır ve bir özel anahtar PuTTY tooSSH tooLinux VM'ler kullanmak için belirli oluşturun. Merhaba aşağıdaki komutu adlı bir ortak anahtar dosyası oluşturur `myPublicKey.key` hemen kullanabileceğiniz:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Ayrıca toomanage Klasik kaynakları gerekiyorsa, hello Dönüştür `myCert.pem` çok`myCert.cer` (DER ile kodlanmış X509 sertifika). Yalnızca toospecifically gerekiyorsa bu isteğe bağlı bir adım gerçekleştirmeniz eski Classic kaynaklarını yönetme.

    Komutu aşağıdaki hello kullanarak hello sertifika Dönüştür:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>PuTTY için özel bir anahtar oluşturun
Putty'yi Windows için ortak bir SSH İstemcisi ' dir. İstediğiniz herhangi bir SSH istemcisi ücretsiz toouse şunlardır. PuTTY toouse toocreate key - PuTTY özel anahtar (PPK) ek bir türde gerekir. Toouse PuTTY istemiyorsanız bu bölümü atlayabilirsiniz.

Merhaba aşağıdaki örnek PuTTY toouse için özel olarak bu ek özel anahtarı oluşturur:

1. Kullanım **Git Bash** tooconvert, özel anahtar bir RSA özel anahtarı PuTTYgen anlayabilirsiniz. Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myPrivateKey_rsa` adlı hello var olan anahtardan `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Bir güvenlik önlemi olarak, böylece yalnızca erişebilir özel anahtarınızı hello izinleri ayarlamalısınız:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Karşıdan yükleme ve konumu aşağıdaki hello PuTTYgen çalıştırma: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Merhaba menüsünü tıklatın: **dosya** > **yük özel anahtar**
4. Özel anahtarınızı bulun (`myPrivateKey_rsa` hello önceki örnekte). başlattığınızda hello varsayılan dizin **Git Bash** olan `C:\Users\%username%`. Değiştirme hello dosya filtresi tooshow **tüm dosyalar (\*.\*)** :

    ![PuTTYgen Hello var olan özel anahtarı yükleme](./media/ssh-from-windows/load-private-key.png)
5. Tıklatın **açık**. Bir istem hello anahtara başarıyla içe aktarıldığından gösterir:

    ![Anahtar tooPuTTYgen başarıyla alındı](./media/ssh-from-windows/successfully-imported-key.png)
6. Tıklatın **Tamam** tooclose hello istemi.
7. Merhaba ortak anahtar hello hello üstünde görüntülenen **PuTTYgen** penceresi. Kopyalayın ve bir Linux VM oluşturduğunuzda, bu ortak anahtar hello Azure portalında veya Azure Resource Manager şablonu yapıştırın. Tıklatarak **ortak anahtarı Kaydet** toosave bir kopya tooyour bilgisayar:

    ![PuTTY ortak anahtar dosyasını kaydedin](./media/ssh-from-windows/save-public-key.png)

    Merhaba aşağıdaki örnekte nasıl kopyalayıp bir Linux VM oluşturduğunuzda, bu ortak anahtar Azure portal hello gösterilmektedir. Merhaba ortak anahtarı genellikle sonra depolanır `~/.ssh/authorized_keys` , yeni bir VM üzerinde.

    ![Hello Azure portalında bir VM oluşturduğunuzda ortak anahtarı kullan](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Geri **PuTTYgen**, tıklatın **özel anahtarı Kaydet**:

    ![PuTTY özel anahtar dosyasını kaydedin](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Bir istem, toocontinue anahtarınız için bir parola girmeden isteyip istemediğinizi sorar. Bir parola parola ekli tooyour özel gibi anahtardır. Birisi olsa bile tooobtain özel anahtarınızı bunlar hala yalnızca hello anahtarını kullanarak yapabilir tooauthenticate olmayacaktır. Bunlar ayrıca hello parola gerekir. Bir parola birinin özel anahtarınızı elde ederse tooany VM oturum açabilecekleri, anahtar kullanan hizmet. Bir parola oluşturmanız önerilir. Ancak, hello parolayı unutursanız, yoktur hiçbir şekilde toorecover.
   >
   >

    Bir parola tooenter isterseniz tıklayın **Hayır**hello ana PuTTYgen penceresinde bir parola girin ve ardından **özel anahtarı Kaydet** yeniden. Aksi takdirde tıklatın **Evet** hello isteğe bağlı bir parola sağlamadan toocontinue.
9. Bir ad ve konum toosave PPK dosyanızı girin.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Putty tooSSH tooa Linux makine kullanın
Yeniden PuTTY Windows için ortak bir SSH İstemcisi ' dir. İstediğiniz herhangi bir SSH istemcisi ücretsiz toouse şunlardır. adımları ayrıntı nasıl aşağıdaki hello toouse, özel anahtar tooauthenticate SSH kullanarak, Azure VM ile. tooload, özel anahtar tooauthenticate hello SSH bağlantısı gerektiren bakımından diğer SSH anahtar istemcileri başlangıç adımları benzerdir.

1. İndirme ve çalıştırma putty gelen hello konumu: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Merhaba ana bilgisayar adı veya IP adresini hello Azure portal, VM'den doldurun:

    ![PuTTY yeni bağlantı Aç](./media/ssh-from-windows/putty-new-connection.png)
3. Seçmeden önce **açık**, tıklatın **bağlantı** > **SSH** > **Auth** sekmesi. Gözat tooand özel anahtarınızı seçin:

    ![Kimlik doğrulaması için PuTTY özel anahtarınızı seçin](./media/ssh-from-windows/putty-auth-dialog.png)
4. Tıklatın **açık** tooconnect tooyour sanal makine

## <a name="next-steps"></a>Sonraki adımlar
Merhaba ortak ve özel anahtarlar da oluşturabileceğiniz [OS X ile Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Windows için Bash ve Windows bilgisayarınızda OSS araçları kullanıma hazır olan bir hello yararları hakkında daha fazla bilgi için bkz: [Bash Ubuntu Windows üzerinde](https://msdn.microsoft.com/commandline/wsl/about).

SSH tooconnect tooyour Linux VM'ler kullanma konusunda sorun yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure Linux VM'de](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
