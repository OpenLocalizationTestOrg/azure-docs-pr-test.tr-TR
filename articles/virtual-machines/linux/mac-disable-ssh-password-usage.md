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
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="cc274-103">Linux VM SSH parolalarını SSHD yapılandırarak devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cc274-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="cc274-104">Bu makalede odaklanılmaktadır toolock hello oturum açma güvenlik Linux VM kapalı.</span><span class="sxs-lookup"><span data-stu-id="cc274-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="cc274-105">SSH bağlantı noktası 22'Hello açıldığında hemen toohello world aracılarını parolalarını tahmin toologin çalışırken başlatın.</span><span class="sxs-lookup"><span data-stu-id="cc274-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="cc274-106">Biz bu makalede ne yapacağını parola kullanarak oturum açamayan SSH üzerinden devre dışı değil.</span><span class="sxs-lookup"><span data-stu-id="cc274-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="cc274-107">Merhaba özelliği tamamen kaldırarak saldırı Biz bu kaba türünden hello Linux VM koruma toouse parolaları zorlar.</span><span class="sxs-lookup"><span data-stu-id="cc274-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="cc274-108">Merhaba eklenir ödül biz Linux tooonly izin SSHD yapılandıracağınız SSH ortak ve özel anahtarlar aracılığıyla oturumları kullanarak en güvenli yolu toologin tooLinux hello.</span><span class="sxs-lookup"><span data-stu-id="cc274-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="cc274-109">Merhaba olası birleşimlerini onu tooguess hello özel anahtarı büyük ve bu nedenle bile tootry toobrute zorla SSH anahtarları rahatsız etme gelen aracılarını zorlaştırır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cc274-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="cc274-110">Hedefleri</span><span class="sxs-lookup"><span data-stu-id="cc274-110">Goals</span></span>
* <span data-ttu-id="cc274-111">SSHD toodisallow yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cc274-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="cc274-112">Parola oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="cc274-112">Password logins</span></span>
  * <span data-ttu-id="cc274-113">Kök kullanıcı oturum açma</span><span class="sxs-lookup"><span data-stu-id="cc274-113">Root user login</span></span>
  * <span data-ttu-id="cc274-114">Sınama yanıtı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cc274-114">Challenge-response authentication</span></span>
* <span data-ttu-id="cc274-115">SSHD tooallow yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cc274-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="cc274-116">yalnızca SSH anahtar oturumları</span><span class="sxs-lookup"><span data-stu-id="cc274-116">only SSH key logins</span></span>
* <span data-ttu-id="cc274-117">Hala oturum açmış durumdayken SSHD yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cc274-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="cc274-118">Test hello yeni SSHD yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc274-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="cc274-119">Giriş</span><span class="sxs-lookup"><span data-stu-id="cc274-119">Introduction</span></span>
[<span data-ttu-id="cc274-120">Tanımlanan SSH</span><span class="sxs-lookup"><span data-stu-id="cc274-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="cc274-121">SSHD hello SSH hello Linux VM üzerinde çalışan sunucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="cc274-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="cc274-122">SSH Kabuğu'ndan MacBook ya da Linux iş istasyonunuza çalıştıran bir istemci olur.</span><span class="sxs-lookup"><span data-stu-id="cc274-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="cc274-123">SSH de hello Protokolü toosecure kullanılan ve iş istasyonu ve hello Linux VM arasındaki hello iletişimi şifrelemek olur.</span><span class="sxs-lookup"><span data-stu-id="cc274-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="cc274-124">Bu makale için bu Linux VM hello tüm açık size yol çok önemli tookeep bir oturum açma tooyour olur.</span><span class="sxs-lookup"><span data-stu-id="cc274-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="cc274-125">Bu nedenle şu iki Terminal ve SSH toohello Linux VM hem de bunların açılır.</span><span class="sxs-lookup"><span data-stu-id="cc274-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="cc274-126">Biz hello ilk terminal toomake hello değişiklikleri tooSSHDs yapılandırma dosyası kullanın ve hello SSHD hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cc274-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="cc274-127">Merhaba ikinci terminal tootest hello hizmet yeniden başlatıldıktan sonra bu değişiklikleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="cc274-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="cc274-128">Biz SSH parolaları devre dışı ve kesinlikle SSH anahtarları üzerinde SSH anahtarlarınız doğru değildir ve hello bağlantı toohello VM kapatırsanız bağlı olan hello VM kalıcı olarak kilitli ve hiç kimse silinir ve yeniden toobe gerektiren mümkün toologin tooit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc274-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc274-129">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc274-129">Prerequisites</span></span>
* [<span data-ttu-id="cc274-130">Azure Linux VM'ler için Linux ve Mac'de SSH anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc274-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="cc274-131">Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="cc274-131">Azure account</span></span>
  * [<span data-ttu-id="cc274-132">ücretsiz deneme kaydolma</span><span class="sxs-lookup"><span data-stu-id="cc274-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="cc274-133">Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc274-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="cc274-134">Linux azure üzerinde çalışan VM</span><span class="sxs-lookup"><span data-stu-id="cc274-134">Linux VM running on azure</span></span>
* <span data-ttu-id="cc274-135">SSH ortak ve özel anahtar çiftini`~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="cc274-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="cc274-136">SSH ortak anahtarını `~/.ssh/authorized_keys` hello Linux VM üzerinde</span><span class="sxs-lookup"><span data-stu-id="cc274-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="cc274-137">Merhaba VM Sudo hakları</span><span class="sxs-lookup"><span data-stu-id="cc274-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="cc274-138">Bağlantı noktası 22 Aç</span><span class="sxs-lookup"><span data-stu-id="cc274-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="cc274-139">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="cc274-139">Quick Commands</span></span>
<span data-ttu-id="cc274-140">*Merhaba TLDR sürümü yalnızca isteyen dönemlik Linux Admins buradan başlayın.  Bu bölümde ayrıntılı bir açıklama ve ilerleme herkes için başka hello istediği atlayın.*</span><span class="sxs-lookup"><span data-stu-id="cc274-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="cc274-141">Merhaba yapılandırma dosyası şu şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="cc274-141">Edit hello config file as follows:</span></span>

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

<span data-ttu-id="cc274-142">Merhaba SSHD hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cc274-142">Restart hello SSHD service.</span></span> <span data-ttu-id="cc274-143">Debian tabanlı distro'lar üzerinde:</span><span class="sxs-lookup"><span data-stu-id="cc274-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="cc274-144">Red Hat tabanlı distro'lar üzerinde:</span><span class="sxs-lookup"><span data-stu-id="cc274-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="cc274-145">Aracılığıyla ayrıntılı ilerlemesi</span><span class="sxs-lookup"><span data-stu-id="cc274-145">Detailed Walk Through</span></span>
<span data-ttu-id="cc274-146">Oturum açma toohello Linux VM terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="cc274-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="cc274-147">Oturum açma toohello Linux VM terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="cc274-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="cc274-148">Üzerinde T2 biz tooedit hello SSHD yapılandırma dosyası adımıdır.</span><span class="sxs-lookup"><span data-stu-id="cc274-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="cc274-149">Buradan biz yalnızca hello ayarları toodisable parolaları düzenleyin ve SSH anahtar oturum açmayı etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="cc274-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="cc274-150">Araştırma ve gerekir toomake Linux & SSH gerektiği kadar güvenli değiştirmek, bu dosyada birçok ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="cc274-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="cc274-151">Parola oturum açmalar devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cc274-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="cc274-152">Ortak anahtar kimlik doğrulamasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cc274-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="cc274-153">Kök oturum açma devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="cc274-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="cc274-154">Sınama yanıtı kimlik doğrulamasını devre dışı</span><span class="sxs-lookup"><span data-stu-id="cc274-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="cc274-155">SSHD yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cc274-155">Restart SSHD</span></span>
<span data-ttu-id="cc274-156">Merhaba T1 Kabuğu'ndan, hala oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cc274-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="cc274-157">Bu, SSH anahtarlarınız doğru değilse parolaları şimdi devre dışı olduğundan, VM dışında kilitlenmesine değil için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="cc274-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="cc274-158">Herhangi bir ayar, hala kaydedilir ve SSH hello bağlantı Canlı SSHD hizmet hello sırasında tutar T1 toofix sshd_config kullanabilirsiniz, Linux VM'de hatalıysa yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="cc274-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="cc274-159">T2 çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cc274-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="cc274-160">Debian ailesi Hello üzerinde</span><span class="sxs-lookup"><span data-stu-id="cc274-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="cc274-161">RedHat ailesi Hello üzerinde</span><span class="sxs-lookup"><span data-stu-id="cc274-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="cc274-162">Parolalar şimdi yanılma parola oturum açma saldırılara karşı korumaya, VM devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="cc274-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="cc274-163">Yalnızca SSH izin anahtarlarla mümkün toologin daha hızlı ve daha güvenli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc274-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

