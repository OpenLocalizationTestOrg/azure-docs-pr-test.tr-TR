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
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="e7228-103">Azure Linux VM'ler üzerinde SSHD yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e7228-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="e7228-104">Bu makalede nasıl toolockdown hello SSH sunucuda Linux, tooprovide en iyi yöntemler güvenlik ve ayrıca toospeed hello SSH oturum açma işlemini yerine parolaları SSH anahtarları kullanılarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e7228-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="e7228-105">toofurther kilitleme mümkün toologin olmaktan biz toodisable hello kök kullanıcının kalacaklarını SSHD SSH Protokolü sürüm 1 devre dışı bırakma toologin bir onaylanmış Grup listesi aracılığıyla izin verilen hello kullanıcıları sınırlamak, en az bir anahtar bit ayarlamak ve otomatik oturum kapatma boşta kullanıcıların yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7228-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="e7228-106">Bu makale için Hello gereksinimleri şunlardır: bir Azure hesabı ([ücretsiz bir deneme sürümünü edinin](https://azure.microsoft.com/pricing/free-trial/)) ve [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7228-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e7228-107">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="e7228-107">Quick Commands</span></span>

<span data-ttu-id="e7228-108">Yapılandırma `/etc/ssh/sshd_config` ayarları aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="e7228-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="e7228-109">Parola oturum açmalar devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="e7228-110">Oturum açma hello kök kullanıcı tarafından devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="e7228-111">İzin verilen grupların listesini</span><span class="sxs-lookup"><span data-stu-id="e7228-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="e7228-112">İzin verilen kullanıcılar listesi</span><span class="sxs-lookup"><span data-stu-id="e7228-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="e7228-113">SSH Protokolü sürüm 1 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="e7228-114">En az anahtar bitleri</span><span class="sxs-lookup"><span data-stu-id="e7228-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="e7228-115">Boşta kullanıcıların bağlantısını kesin</span><span class="sxs-lookup"><span data-stu-id="e7228-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e7228-116">Ayrıntılı Kılavuz</span><span class="sxs-lookup"><span data-stu-id="e7228-116">Detailed Walkthrough</span></span>

<span data-ttu-id="e7228-117">SSHD hello SSH hello Linux VM üzerinde çalışan sunucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="e7228-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="e7228-118">SSH, MacBook Linux iş istasyonunda, üzerinde bir kabuk ya da bir Bash Windows çalıştıran bir istemci olur.</span><span class="sxs-lookup"><span data-stu-id="e7228-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="e7228-119">SSH de hello Protokolü toosecure kullanılan ve iş istasyonu ve hello Linux SSH ayrıca VPN (sanal özel ağ) oluşturma VM arasındaki hello iletişimi şifrelemek olur.</span><span class="sxs-lookup"><span data-stu-id="e7228-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="e7228-120">Bu makalede, bu Linux VM açmak hello tüm gözden geçirme için çok önemli tookeep bir oturum açma tooyour olur.</span><span class="sxs-lookup"><span data-stu-id="e7228-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="e7228-121">Bir SSH bağlantısı kurulduktan sonra hello penceresi kapalı olduğu sürece, açık bir oturum olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="e7228-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="e7228-122">' De, oturum açmış bir terminal sağlar değişiklikleri yapılan toobe toohello için SSHD hizmeti önemli bir değişiklik yaptıysanız, kilitlenmelerini olmadan.</span><span class="sxs-lookup"><span data-stu-id="e7228-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="e7228-123">Linux VM'NİZDE bozuk SSHD yapılandırmasıyla dışında kilitlenmesine, Azure hello özelliği tooreset hello bozuk SSHD yapılandırmayla sunar. [Azure VM erişim uzantısı](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7228-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e7228-124">Bu nedenle şu iki Terminal ve SSH toohello Linux VM hem de bunların açın.</span><span class="sxs-lookup"><span data-stu-id="e7228-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="e7228-125">Biz hello ilk terminal toomake hello değişiklikleri tooSSHDs yapılandırma dosyası kullanın ve hello SSHD hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e7228-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="e7228-126">Merhaba ikinci terminal tootest hello hizmet yeniden başlatıldıktan sonra bu değişiklikleri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="e7228-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="e7228-127">Biz SSH parolaları devre dışı ve kesinlikle SSH anahtarları üzerinde SSH anahtarlarınız doğru değildir ve hello bağlantı toohello VM kapatırsanız bağlı olan hello VM kalıcı olarak kilitli ve hiç kimse silinir ve yeniden toobe gerektiren mümkün toologin tooit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e7228-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="e7228-128">Parola oturum açmalar devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-128">Disable password logins</span></span>

<span data-ttu-id="e7228-129">hızlı şekilde toosecure hello Linux VM olduğunu toodisable parola oturum açma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e7228-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="e7228-130">Parola kullanarak oturum açamayan etkinleştirildiğinde, gezinme hello web toobrute çalışırken başlayacaktır aracılarını tahmin hello parola SSH kullanarak, Linux VM için zorlar.</span><span class="sxs-lookup"><span data-stu-id="e7228-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="e7228-131">Parola kullanarak oturum açamayan tamamen devre dışı bırakma, tüm parola oturum açma denemesi hello SSH sunucu tooignore sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7228-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="e7228-132">Oturum açma hello kök kullanıcı tarafından devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-132">Disable login by hello root user</span></span>

<span data-ttu-id="e7228-133">Aşağıdaki Linux en iyi yöntemler, hello `root` kullanıcı hiçbir zaman oturum açmış olmanız halinde SSH veya kullanarak üzerinden `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="e7228-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="e7228-134">Kök düzeyinde izinler gerektiren tüm komutları hello her zaman çalışması gerektiğini `sudo` gelecekteki denetlemek için tüm eylemleri kaydeder komutu.</span><span class="sxs-lookup"><span data-stu-id="e7228-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="e7228-135">Devre dışı bırakma hello `root` SSH yoluyla açmasını kullanıcıdır tooSSH yalnızca yetkili kullanıcılar izin verilen sağlayan bir güvenlik en iyi yöntemler adımı.</span><span class="sxs-lookup"><span data-stu-id="e7228-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="e7228-136">İzin verilen grupların listesini</span><span class="sxs-lookup"><span data-stu-id="e7228-136">Allowed groups list</span></span>

<span data-ttu-id="e7228-137">SSH SSH üzerinden oturum açmayı gelen kullanıcılar ve izin verilen veya izin verilmeyen Grup kısıtlama bir yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="e7228-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="e7228-138">Bu özellik belirli kullanıcılar ve gruplar açmasını Engelle veya listeleri tooapprove kullanır.</span><span class="sxs-lookup"><span data-stu-id="e7228-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="e7228-139">Merhaba tekerleği Grup toohello ayarı `AllowGroups` listesi hello tekerleği grubunda yer alan SSH toojust kullanıcı hesapları üzerinden onaylanan oturumları kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="e7228-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="e7228-140">İzin verilen kullanıcılar listesi</span><span class="sxs-lookup"><span data-stu-id="e7228-140">Allowed users list</span></span>

<span data-ttu-id="e7228-141">SSH oturumu açma toojust kullanıcılar sınırlandırma olduğu tooaccomplish aynı hello daha belirli bir şekilde görev `AllowGroups` değil.</span><span class="sxs-lookup"><span data-stu-id="e7228-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="e7228-142">SSH Protokolü sürüm 1 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e7228-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="e7228-143">SSH Protokolü sürüm 1 güvenli değil ve devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7228-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="e7228-144">SSH Protokolü sürüm 2 güvenli şekilde tooSSH tooyour sunucusu sunar hello geçerli sürümdür.</span><span class="sxs-lookup"><span data-stu-id="e7228-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="e7228-145">SSH sürüm 1 devre dışı bırakma tooestablish çalıştığınız SSH istemcilere SSH sürüm 1 kullanılarak hello SSH sunucusuyla bir bağlantı reddeder.</span><span class="sxs-lookup"><span data-stu-id="e7228-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="e7228-146">SSH sürüm 2 bağlantıları toonegotiate izin yalnızca hello SSH sunucusuyla bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e7228-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="e7228-147">En az anahtar bitleri</span><span class="sxs-lookup"><span data-stu-id="e7228-147">Minimum key bits</span></span>

<span data-ttu-id="e7228-148">Aşağıdaki en iyi güvenlik uygulamaları, parola SSH oturumu açma devre dışı bırakılır ve yalnızca SSH anahtarları toobe tooauthenticate hello SSH sunucusuyla kullanılan izin verilir.</span><span class="sxs-lookup"><span data-stu-id="e7228-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="e7228-149">Bu SSH anahtarları bit cinsinden ölçülen farklı uzunlukta anahtarlar kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e7228-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="e7228-150">En iyi anahtarlarının uzunluğu 2048 bit hello minimum kabul edilebilir anahtarı kuvvetini olduğunu durumları yöntemler.</span><span class="sxs-lookup"><span data-stu-id="e7228-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="e7228-151">Teorik olarak az 2048 bit anahtarları bozuk olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7228-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="e7228-152">Ayar hello `ServerKeyBits` çok`2048` 2048 bit veya daha büyük tuşlarıyla bağlantılarına izin veren ve az 2048 bit bağlantı reddedilecek.</span><span class="sxs-lookup"><span data-stu-id="e7228-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="e7228-153">Boşta kullanıcıların bağlantısını kesin</span><span class="sxs-lookup"><span data-stu-id="e7228-153">Disconnect idle users</span></span>

<span data-ttu-id="e7228-154">SSH birden çok belirlenen süre saniye boyunca boşta kaldığı açık bağlantıları olan hello özelliği toodisconnect kullanıcılar sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e7228-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="e7228-155">Açık oturumu tooonly etkin sınırları hello hello Linux VM riskini bu kullanıcılar kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7228-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="e7228-156">SSHD yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="e7228-156">Restart SSHD</span></span>

<span data-ttu-id="e7228-157">tooenable hello ayarlarında `/etc/ssh/sshd_config` hello SSH sunucu yeniden başlatıldıktan hello SSHD işlemini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e7228-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="e7228-158">toorestart hello SSH sunucusu kullandığınız hello terminal penceresi açık kaldığını hello açık SSH oturumu kaybetmeden.</span><span class="sxs-lookup"><span data-stu-id="e7228-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="e7228-159">İkinci bir terminal penceresi veya sekmesinde tootest hello yeni SSH server ayarlarını kullanın.  Ayrı terminal tootest hello SSH bağlantısını kullanarak verir geri toogo ve yapma ek değişiklikler toohello `/etc/ssh/sshd_config` göre önemli bir SSHD değişiklik kilitlenmelerini olmadan ilk Terminal Merhaba,.</span><span class="sxs-lookup"><span data-stu-id="e7228-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="e7228-160">RedHat, Centos ve Fedora</span><span class="sxs-lookup"><span data-stu-id="e7228-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="e7228-161">Debian ve Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e7228-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="e7228-162">Azure sıfırlama erişimi kullanarak SSHD Sıfırla</span><span class="sxs-lookup"><span data-stu-id="e7228-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="e7228-163">Son değişiklik toohello SSHD yapılandırma kilitli olmadığını hello Azure VM erişim-uzantısı tooreset hello SSHD yapılandırma geri toohello özgün yapılandırmayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7228-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="e7228-164">Tüm örnek adları kendi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7228-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="e7228-165">Fail2ban yükleyin</span><span class="sxs-lookup"><span data-stu-id="e7228-165">Install Fail2ban</span></span>

<span data-ttu-id="e7228-166">Hangi blokları denemeleri toologin tooyour Linux VM yanılma kullanarak SSH üzerinde yinelenen tooinstall ve Kurulum hello açık kaynak uygulama Fail2ban, kesinlikle önerilir.</span><span class="sxs-lookup"><span data-stu-id="e7228-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="e7228-167">Yinelenen Fail2ban günlükleri denemeleri toologin SSH üzerinde başarısız oldu ve ardından güvenlik duvarı kuralları hello denemeleri kaynaklanan tooblock başlangıç IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e7228-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="e7228-168">Fail2ban giriş sayfası</span><span class="sxs-lookup"><span data-stu-id="e7228-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="e7228-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e7228-169">Next Steps</span></span>

<span data-ttu-id="e7228-170">Artık, yapılandırılmış ve Linux VM üzerinde hello SSH sunucuyu kilitli izleyebilirsiniz ek güvenlik en iyi yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="e7228-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="e7228-171">Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello</span><span class="sxs-lookup"><span data-stu-id="e7228-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="e7228-172">Hello Azure CLI kullanarak bir Linux VM disklerde şifrele</span><span class="sxs-lookup"><span data-stu-id="e7228-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="e7228-173">Azure Resource Manager şablonları güvenlik ve erişim</span><span class="sxs-lookup"><span data-stu-id="e7228-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
