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
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="dd4de-103">Linux VM'ler için SSH ortak ve özel anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4de-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="dd4de-104">Bu makalede nasıl toogenerate bir SSH Protokolü sürüm 2 RSA ortak ve özel anahtar çifti toouse Linux VM'ler ile dosya gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="dd4de-105">SSH anahtar çifti ile Parolaları toolog hello gereksinimini toousing SSH anahtarları kimlik doğrulama için varsayılan Azure üzerinde sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd4de-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="dd4de-106">Parolalar, tahmin edilebilir ve parolanızı toorelentless yanılma denemeleri tooguess, Vm'leri açın.</span><span class="sxs-lookup"><span data-stu-id="dd4de-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="dd4de-107">Azure şablonları veya hello ile oluşturulan VM'ler `azure-cli` SSH ortak anahtarınız için SSH parolalı oturum açma devre dışı bırakma post dağıtım yapılandırma adımı kaldırma hello dağıtımının bir parçası olarak dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd4de-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="dd4de-108">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="dd4de-108">Quick Commands</span></span>

<span data-ttu-id="dd4de-109">Bash Kabuk komutları izleyerek, hello örnekleri kendi seçenekleri değiştirme hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd4de-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="dd4de-110">SSH ortak anahtar dosyanız varsayılan olarak `~/.ssh/id_rsa.pub` konumunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dd4de-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="dd4de-111">Komutu aşağıdaki hello kullanarak istendiğinde, "parola" toosecure özel anahtarınızı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="dd4de-112">(Merhaba parola parola tooencrypt özel anahtarınızı kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="dd4de-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="dd4de-113">Yeni oluşturulan hello anahtar çok eklemek`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="dd4de-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="dd4de-114">komutları iş neredeyse tüm dağıtımlar, Linux işletim sistemlerinde yukarıda hello ancak hello ortamı tüketicisinin kısıtlanabilir gibi kapsayıcılara mutlaka çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="dd4de-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="dd4de-115">Ayrıntılı Kılavuz</span><span class="sxs-lookup"><span data-stu-id="dd4de-115">Detailed Walkthrough</span></span>

<span data-ttu-id="dd4de-116">SSH ortak ve özel anahtarları hello en kolay yolu toolog tooyour Linux sunucularda kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="dd4de-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="dd4de-117">[Ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) kolayca deneme yanılmayla parolalara göre çok daha güvenli bir şekilde toolog tooyour Linux içinde veya Azure BSD VM'de sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd4de-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd4de-118">Ortak anahtarınız herkesle paylaşılabilir; ancak, özel anahtarınıza yalnızca siz (veya yerel güvenlik altyapınız) sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="dd4de-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="dd4de-119">Hello SSH özel anahtara sahip bir [çok güvenli parola](https://www.xkcd.com/936/) (kaynak:[xkcd.com](https://xkcd.com)) toosafeguard onu.</span><span class="sxs-lookup"><span data-stu-id="dd4de-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="dd4de-120">Bu parolayı yalnızca tooaccess hello özel SSH anahtarı olan ve **değil** hello kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="dd4de-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="dd4de-121">Bir parola tooyour SSH anahtarı eklediğinizde, böylece hello özel anahtar hello parola toodecrypt gereksizdir, 128 bit AES kullanarak hello özel anahtarı şifreler.</span><span class="sxs-lookup"><span data-stu-id="dd4de-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="dd4de-122">Bir saldırgan özel anahtarınızı çalıntı varsa ve anahtarı bir parola sahip değilse, bu özel mümkün toouse olacaktır hello karşılık gelen ortak anahtara sahip bir tooany sunucuya toolog anahtarı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="dd4de-123">Özel anahtar parola korumalı ise, Azure’daki altyapınız için ek bir güvenlik katmanı sağlayarak, bu saldırgan tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="dd4de-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="dd4de-124">Bu makalede, Resource Manager hello üzerinde dağıtımlar için önerilen 2 RSA ortak ve özel anahtar dosyaları, SSH Protokolü sürüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dd4de-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="dd4de-125">*SSH-rsa* anahtarları hello üzerinde gerekli [portal](https://portal.azure.com) Klasik ve Resource Manager dağıtımları için.</span><span class="sxs-lookup"><span data-stu-id="dd4de-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="dd4de-126">SSH anahtarlarını kullanarak SSH parolalarını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="dd4de-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="dd4de-127">Azure en az 2048 bit, ssh-rsa biçimli ortak ve özel anahtarlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="dd4de-128">toocreate hello anahtarları kullanmak `ssh-keygen`, bir seri soru soran ve özel anahtar ve eşleşen ortak anahtarı yazar.</span><span class="sxs-lookup"><span data-stu-id="dd4de-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="dd4de-129">Bir Azure VM oluşturulduğunda, hello ortak anahtar çok kopyalanır`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="dd4de-130">SSH anahtarları `~/.ssh/authorized_keys` kullanılan toochallenge hello istemci toomatch hello karşılık gelen özel anahtar bir SSH oturum açma bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="dd4de-131">Kimlik doğrulaması için SSH anahtarları kullanarak bir Azure Linux VM oluşturulduğunda, Azure hello SSHD yapılandırır sunucu toonot izin parola oturum açmalar, yalnızca SSH anahtarları.</span><span class="sxs-lookup"><span data-stu-id="dd4de-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="dd4de-132">Bu nedenle, SSH anahtarları ile Azure Linux VM'ler oluşturarak, güvenli hello VM dağıtımı yardımcı olmak ve kendiniz hello sshd_config yapılandırma dosyası parolalar devre dışı bırakma hello tipik dağıtım sonrası yapılandırma adımı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dd4de-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="dd4de-133">SSH-keygen’i kullanma</span><span class="sxs-lookup"><span data-stu-id="dd4de-133">Using ssh-keygen</span></span>

<span data-ttu-id="dd4de-134">Bu komut, 2048 bit RSA kullanarak (şifrelenmiş) SSH anahtar çifti güvenli bir parola oluşturur ve onu geçersiz kılınan tooeasily tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="dd4de-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="dd4de-135">SSH anahtarları hello tutulan varsayılan olan `~/.ssh` dizini.</span><span class="sxs-lookup"><span data-stu-id="dd4de-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="dd4de-136">Yoksa bir `~/.ssh` dizin, hello `ssh-keygen` komut oluşturur, sizin için hello ile doğru izinleri.</span><span class="sxs-lookup"><span data-stu-id="dd4de-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="dd4de-137">*Komut açıklaması*</span><span class="sxs-lookup"><span data-stu-id="dd4de-137">*Command explained*</span></span>

<span data-ttu-id="dd4de-138">`ssh-keygen`Merhaba kullanılan program toocreate hello anahtarları =</span><span class="sxs-lookup"><span data-stu-id="dd4de-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="dd4de-139">`-t rsa`Merhaba RSA biçimi olan anahtar toocreate türü = [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="dd4de-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="dd4de-140">`-b 2048`BITS başlangıç anahtarı =</span><span class="sxs-lookup"><span data-stu-id="dd4de-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="dd4de-141">Klasik portal ve X.509 sertifikaları</span><span class="sxs-lookup"><span data-stu-id="dd4de-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="dd4de-142">Azure kullanıyorsanız hello [Klasik portal](https://manage.windowsazure.com/), hello SSH anahtarları için X.509 sertifikaları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="dd4de-143">Diğer SSH ortak anahtar türlerine izin verilmez, tümünün X.509 sertifikası *olması gerekir*.</span><span class="sxs-lookup"><span data-stu-id="dd4de-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="dd4de-144">toocreate varolan SSH-RSA özel anahtarınızı gelen bir X.509 sertifikası:</span><span class="sxs-lookup"><span data-stu-id="dd4de-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="dd4de-145">`asm` kullanarak klasik dağıtım</span><span class="sxs-lookup"><span data-stu-id="dd4de-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="dd4de-146">Merhaba Klasik kullanıyorsanız, model dağıtma (CLI Azure Hizmet Yönetimi `asm`), bir SSH-RSA ortak anahtar kullanabilir veya bir RFC4716 biçimlendirilmiş anahtarını bir **.pem** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="dd4de-147">Merhaba SSH-RSA ortak anahtardır daha önce bu makalede kullanarak oluşturulan öğeleri `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="dd4de-148">Mevcut bir SSH ortak anahtarı anahtarından toocreate bir RFC4716 biçimlendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="dd4de-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="dd4de-149">ssh-keygen örneği</span><span class="sxs-lookup"><span data-stu-id="dd4de-149">Example of ssh-keygen</span></span>

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

<span data-ttu-id="dd4de-150">Kaydedilen anahtar dosyaları:</span><span class="sxs-lookup"><span data-stu-id="dd4de-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="dd4de-151">Bu makalede Hello anahtar çifti adı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-151">hello key pair name for this article.</span></span>  <span data-ttu-id="dd4de-152">Adlı bir anahtar çiftine **id_rsa** hello varsayılandır ve bazı araçlar hello bekleyebilirsiniz **id_rsa** tane olması iyi bir fikirdir böylece özel anahtar dosya adı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="dd4de-153">Merhaba dizin `~/.ssh/` SSH anahtar çiftleriniz ve hello SSH yapılandırma dosyası için hello varsayılan konumdur.</span><span class="sxs-lookup"><span data-stu-id="dd4de-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="dd4de-154">Bir tam yol belirtilmezse `ssh-keygen` hello geçerli çalışma dizininde hello anahtarları oluşturma, varsayılan hello değil `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="dd4de-155">Merhaba listesini `~/.ssh` dizin.</span><span class="sxs-lookup"><span data-stu-id="dd4de-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="dd4de-156">Anahtar Parolası:</span><span class="sxs-lookup"><span data-stu-id="dd4de-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="dd4de-157">`ssh-keygen`"bir parola." tooa kullanılan parola tooencrypt hello özel anahtarı başvurur</span><span class="sxs-lookup"><span data-stu-id="dd4de-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="dd4de-158">Bu *kesinlikle* parola tooyour anahtar çiftleri tooadd önerilir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="dd4de-159">Bir parola koruma hello özel anahtar olmadan, hello anahtar dosyası olan herkes bu toolog hello karşılık gelen ortak anahtarı var. tooany Server'da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd4de-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="dd4de-160">Bir parola katıştırılabilecek daha fazla koruma birisi mümkün toogain erişim tooyour özel anahtar dosyası olması durumunda, size zaman toochange hello anahtarları tooauthenticate kullanılan.</span><span class="sxs-lookup"><span data-stu-id="dd4de-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="dd4de-161">SSH aracı toostore özel anahtar parolanızı kullanma</span><span class="sxs-lookup"><span data-stu-id="dd4de-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="dd4de-162">özel anahtarınızı yazarak tooavoid dosya parola her SSH oturum açma ile kullandığınız `ssh-agent` toocache özel anahtar dosya parolanızı.</span><span class="sxs-lookup"><span data-stu-id="dd4de-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="dd4de-163">Mac kullanıyorsanız, çağırdığınızda hello OSX Anahtarlığa güvenli bir şekilde hello özel anahtar parolaları depolar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="dd4de-164">Doğrulayın ve kullanmak `ssh-agent` ve `ssh-add` tooinform hello SSH sistemi hello anahtar dosyaları hakkında böylece hello parola etkileşimli olarak kullanılan toobe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="dd4de-165">Şimdi hello özel anahtarı çok ekleyin`ssh-agent` hello komutunu kullanarak `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="dd4de-166">Merhaba özel anahtar parolası şimdi depolanır `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="dd4de-167">Kullanarak `ssh-copy-id` tooinstall hello yeni anahtarı</span><span class="sxs-lookup"><span data-stu-id="dd4de-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="dd4de-168">Bir VM zaten oluşturduysanız aşağıdaki komut, hello VM kullanıcı adı ve hello sunucu adresi kendi değerlerinizle değiştirerek hello ile Merhaba yeni SSH ortak anahtarı tooyour Linux VM yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd4de-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="dd4de-169">SSH yapılandırma dosyası oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd4de-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="dd4de-170">En iyi yöntem toocreate olduğundan ve yapılandırma bir `~/.ssh/config` dosya toospeed yukarı oturum açmalar ve SSH istemci davranışını en iyi duruma getirme için.</span><span class="sxs-lookup"><span data-stu-id="dd4de-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="dd4de-171">Aşağıdaki örnek hello standart bir yapılandırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="dd4de-172">Merhaba dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4de-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="dd4de-173">Merhaba dosya tooadd hello yeni SSH yapılandırması düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="dd4de-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="dd4de-174">Örnek `~/.ssh/config` dosyası:</span><span class="sxs-lookup"><span data-stu-id="dd4de-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="dd4de-175">Her sunucu tooenable için kendi özel anahtar çiftini her toohave bölümler bu SSH yapılandırma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd4de-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="dd4de-176">Merhaba varsayılan ayarları (`Host *`) olan hello belirli ana bilgisayarlar yukarıya hello config dosyasına eşleşmeyen herhangi bir ana bilgisayar için.</span><span class="sxs-lookup"><span data-stu-id="dd4de-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="dd4de-177">Yapılandırma dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="dd4de-177">Config file explained</span></span>

<span data-ttu-id="dd4de-178">`Host`Merhaba ana bilgisayar üzerinde hello terminal çağrılan Hello adı =.</span><span class="sxs-lookup"><span data-stu-id="dd4de-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="dd4de-179">`ssh fedora22`söyler `SSH` toouse hello hello ayarları blok etiketli değerlerde `Host fedora22` Not: ana bilgisayar kullanımınız için mantıklı olan ve hello gerçek ana bilgisayar herhangi bir sunucu adını temsil etmeyen her etiket olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="dd4de-180">`Hostname 102.160.203.241`Başlangıç IP adresi veya erişilen hello sunucusu için DNS adı =.</span><span class="sxs-lookup"><span data-stu-id="dd4de-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="dd4de-181">`User ahmet`Merhaba uzak kullanıcı hesabı toouse toohello Server'da oturum açarken =.</span><span class="sxs-lookup"><span data-stu-id="dd4de-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="dd4de-182">`PubKeyAuthentication yes`= istediğiniz toouse bir SSH anahtarı toolog SSH söyler.</span><span class="sxs-lookup"><span data-stu-id="dd4de-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="dd4de-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`Merhaba SSH özel anahtar ve kimlik doğrulaması için karşılık gelen ortak anahtar toouse =.</span><span class="sxs-lookup"><span data-stu-id="dd4de-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="dd4de-184">Parolasız Linux içine SSH</span><span class="sxs-lookup"><span data-stu-id="dd4de-184">SSH into Linux without a password</span></span>

<span data-ttu-id="dd4de-185">SSH anahtar çiftiniz ve yapılandırılmış bir yapılandırma dosyasına sahip olduğunuza göre hızlı ve güvenli bir şekilde tooyour Linux VM içinde mümkün toolog şunlardır.</span><span class="sxs-lookup"><span data-stu-id="dd4de-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="dd4de-186">Merhaba, bir SSH anahtarı hello komut istemlerini kullanarak tooa Server'da hello parolası için bu anahtar dosyası için ilk oturum açışınızda.</span><span class="sxs-lookup"><span data-stu-id="dd4de-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="dd4de-187">Komut açıklaması</span><span class="sxs-lookup"><span data-stu-id="dd4de-187">Command explained</span></span>

<span data-ttu-id="dd4de-188">Zaman `ssh fedora22` yürütülür SSH ilk bulur ve hello tüm ayarları yükler `Host fedora22` blok yükler ve sonra tüm hello hello son blok ayarlarından kalan `Host *`.</span><span class="sxs-lookup"><span data-stu-id="dd4de-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd4de-189">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="dd4de-189">Next Steps</span></span>

<span data-ttu-id="dd4de-190">Sonraki yukarı toocreate Azure Linux VM'ler hello yeni SSH ortak anahtarını kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="dd4de-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="dd4de-191">Hello oturum açma olarak bir SSH ortak anahtarıyla oluşturulan azure VM'ler, daha iyi parolalar hello varsayılan oturum açma yöntemi ile oluşturulan VM'ler daha güvenli.</span><span class="sxs-lookup"><span data-stu-id="dd4de-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="dd4de-192">SSH anahtarları kullanılarak oluşturulan Azure VM'ler, varsayılan olarak parola kullanımı devre dışı bırakılmış şekilde yapılandırılır; böylece parola tahminiyle gerçekleştirilen saldırı girişimleri önlenir.</span><span class="sxs-lookup"><span data-stu-id="dd4de-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="dd4de-193">SSH anahtar çifti oluşturma daha fazla yardıma gereksinim veya ek sertifika gerektiren gibi hello Klasik portal ile kullanmak için bkz: [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="dd4de-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="dd4de-194">Azure şablonu kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4de-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="dd4de-195">Hello Azure portal kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4de-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="dd4de-196">Hello Azure CLI kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd4de-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
