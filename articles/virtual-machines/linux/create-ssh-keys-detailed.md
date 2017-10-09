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
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="0dcf8-103">Toocreate SSH anahtar çiftiniz ve azure'da bir Linux VM için ek sertifika aracılığıyla ayrıntılı ilerlemesi</span><span class="sxs-lookup"><span data-stu-id="0dcf8-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="0dcf8-104">SSH anahtar çifti ile Parolaları toolog hello gereksinimini toousing SSH anahtarları kimlik doğrulama için varsayılan Azure üzerinde sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="0dcf8-105">Parolalar, tahmin edilebilir ve parolanızı toorelentless yanılma denemeleri tooguess, Vm'leri açın.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="0dcf8-106">Hello Azure CLI ya da Resource Manager şablonları ile oluşturulan VM'ler SSH ortak anahtarınız için SSH parolalı oturum açma devre dışı bırakma post dağıtım yapılandırma adımı kaldırma hello dağıtımının bir parçası olarak dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="0dcf8-107">Bu makalede ayrıntılı adımlar ve ek örnekler oluşturma sertifikaların gibi Linux sanal makineleri ile kullanılmak üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="0dcf8-108">Tooquickly istiyorsanız oluşturmak ve SSH anahtar çiftini kullanın, bkz: [nasıl toocreate bir SSH ortak ve özel anahtarı eşleştirin Azure Linux VM'ler için](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0dcf8-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="0dcf8-109">SSH anahtarlarını anlama</span><span class="sxs-lookup"><span data-stu-id="0dcf8-109">Understanding SSH keys</span></span>

<span data-ttu-id="0dcf8-110">SSH ortak ve özel anahtarları hello en kolay yolu toolog tooyour Linux sunucularda kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="0dcf8-111">[Ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) kolayca deneme yanılmayla parolalara göre çok daha güvenli bir şekilde toolog tooyour Linux içinde veya Azure BSD VM'de sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="0dcf8-112">Ortak anahtarınız herkesle paylaşılabilir; ancak, özel anahtarınıza yalnızca siz (veya yerel güvenlik altyapınız) sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="0dcf8-113">Hello SSH özel anahtara sahip bir [çok güvenli parola](https://www.xkcd.com/936/) (kaynak:[xkcd.com](https://xkcd.com)) toosafeguard onu.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="0dcf8-114">Bu parolayı yalnızca tooaccess hello özel SSH anahtar dosyası olduğunu ve **değil** hello kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="0dcf8-115">Bir parola tooyour SSH anahtarı eklediğinizde, böylece hello özel anahtar hello parola toodecrypt gereksizdir, 128 bit AES kullanarak hello özel anahtarı şifreler.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="0dcf8-116">Bir saldırgan özel anahtarınızı çalıntı varsa ve anahtarı bir parola sahip değilse, bu özel mümkün toouse olacaktır hello karşılık gelen ortak anahtara sahip bir tooany sunucuya toolog anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="0dcf8-117">Özel anahtar parola korumalı ise, Azure’daki altyapınız için ek bir güvenlik katmanı sağlayarak, bu saldırgan tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="0dcf8-118">Bu makalede, Azure Resource Manager ile dağıtımlar için önerilen 2 RSA ortak ve özel anahtar dosyası çifti (Ayrıca başvurulan tooas "ssh-rsa" anahtarlar), bir SSH Protokolü sürüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="0dcf8-119">*SSH-rsa* anahtarları hello üzerinde gerekli [portal](https://portal.azure.com) Klasik ve Resource Manager dağıtımları için.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="0dcf8-120">SSH anahtarlarının kullanımı ve avantajları</span><span class="sxs-lookup"><span data-stu-id="0dcf8-120">SSH keys use and benefits</span></span>

<span data-ttu-id="0dcf8-121">En az 2048 bit, Azure gerektirir SSH Protokolü sürüm 2, RSA biçimi ortak ve özel anahtarları; Merhaba ortak anahtar dosyası sahip hello `.pub` kapsayıcı biçimi.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="0dcf8-122">toocreate hello anahtarları kullanmak `ssh-keygen`, bir seri soru soran ve özel anahtar ve eşleşen ortak anahtarı yazar.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="0dcf8-123">Bir Azure VM oluşturulduğunda, ortak anahtar toohello Azure kopyaları hello `~/.ssh/authorized_keys` hello VM klasörü.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="0dcf8-124">SSH anahtarları `~/.ssh/authorized_keys` kullanılan toochallenge hello istemci toomatch hello karşılık gelen özel anahtar bir SSH oturum açma bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="0dcf8-125">Kimlik doğrulaması için SSH anahtarları kullanarak bir Azure Linux VM oluşturulduğunda, Azure hello SSHD yapılandırır sunucu toonot izin parola oturum açmalar, yalnızca SSH anahtarları.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="0dcf8-126">Bu nedenle, SSH anahtarları ile Azure Linux VM'ler oluşturarak, kendiniz hello parolalarda devre dışı bırakma hello tipik dağıtım sonrası yapılandırma adımı kaydedin ve güvenli hello VM dağıtımı yardımcı olabilir **sshd_config** dosya.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="0dcf8-127">SSH-keygen’i kullanma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-127">Using ssh-keygen</span></span>

<span data-ttu-id="0dcf8-128">Bu komut, 2048 bit RSA kullanarak (şifrelenmiş) SSH anahtar çifti güvenli bir parola oluşturur ve onu geçersiz kılınan tooeasily tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="0dcf8-129">SSH anahtarları hello tutulan varsayılan olan `~/.ssh` dizini.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="0dcf8-130">Yoksa bir `~/.ssh` dizin, hello `ssh-keygen` komut oluşturur, sizin için hello ile doğru izinleri.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="0dcf8-131">*Komut açıklaması*</span><span class="sxs-lookup"><span data-stu-id="0dcf8-131">*Command explained*</span></span>

<span data-ttu-id="0dcf8-132">`ssh-keygen`Merhaba kullanılan program toocreate hello anahtarları =</span><span class="sxs-lookup"><span data-stu-id="0dcf8-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="0dcf8-133">`-t rsa`Merhaba RSA biçimi [wikipedia] olan anahtar toocreate türü =[sonunda parens](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` hello anahtar bitleri =</span><span class="sxs-lookup"><span data-stu-id="0dcf8-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="0dcf8-134">`-C "azureuser@myserver"`Merhaba ortak anahtar dosyası tooeasily eklenmiş toohello sonuna tanımlamak açıklama =.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="0dcf8-135">Normalde hello açıklama olarak bir e-posta kullanılır ancak iyi ne olursa olsun, altyapınız için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="0dcf8-136">`asm` kullanarak klasik dağıtım</span><span class="sxs-lookup"><span data-stu-id="0dcf8-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="0dcf8-137">Merhaba Klasik dağıtım modeli kullanılıyorsa (`asm` hello CLI moduna), bir SSH-RSA ortak anahtar kullanabilir veya bir RFC4716 biçimlendirilmiş pem kapsayıcısında anahtar.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="0dcf8-138">Merhaba SSH-RSA ortak anahtardır daha önce bu makalede kullanarak oluşturulan öğeleri `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="0dcf8-139">Mevcut bir SSH ortak anahtarı anahtarından toocreate bir RFC4716 biçimlendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="0dcf8-140">ssh-keygen örneği</span><span class="sxs-lookup"><span data-stu-id="0dcf8-140">Example of ssh-keygen</span></span>

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

<span data-ttu-id="0dcf8-141">Kaydedilen anahtar dosyaları:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="0dcf8-142">Bu makalede Hello anahtar çifti adı.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-142">hello key pair name for this article.</span></span>  <span data-ttu-id="0dcf8-143">Adlı bir anahtar çiftine **id_rsa** hello varsayılandır ve bazı araçlar hello bekleyebilirsiniz **id_rsa** tane olması iyi bir fikirdir böylece özel anahtar dosya adı.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="0dcf8-144">Merhaba dizin `~/.ssh/` SSH anahtar çiftleriniz ve hello SSH yapılandırma dosyası için hello varsayılan konumdur.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="0dcf8-145">Bir tam yol belirtilmezse `ssh-keygen` hello anahtarları hello geçerli çalışma dizini içinde hello varsayılan oluşturur `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="0dcf8-146">Merhaba listesini `~/.ssh` dizin.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="0dcf8-147">Anahtar Parolası:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="0dcf8-148">`ssh-keygen`tooa parola hello özel anahtar dosyası için "parola." anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="0dcf8-149">Bu *kesinlikle* parola tooyour özel anahtar tooadd önerilir.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="0dcf8-150">Bir parola koruma hello anahtar dosyası, hello dosya kimseyle bunu hello karşılık gelen ortak anahtarı var. tooany Server'daki toolog kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="0dcf8-151">Bir parola (parola) katıştırılabilecek daha fazla koruma birisi mümkün toogain erişim tooyour özel anahtar dosyası olması durumunda, size verilen zaman toochange hello anahtarları tooauthenticate kullanılan.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="0dcf8-152">SSH aracı toostore özel anahtar parolanızı kullanma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="0dcf8-153">Her SSH oturumu açışınızda özel anahtar dosya parolanızı yazmaya tooavoid kullanabileceğiniz `ssh-agent` toocache özel anahtar dosya parolanızı.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="0dcf8-154">Mac kullanıyorsanız, çağırdığınızda hello OSX Anahtarlığa güvenli bir şekilde hello özel anahtar parolaları depolar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="0dcf8-155">Doğrulayın ve ssh aracı ve ssh-tooinform hello SSH sistemi hello anahtar dosyaları hakkında hello parola etkileşimli olarak kullanılan toobe ihtiyacınız olmadığından böylece ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="0dcf8-156">Şimdi hello özel anahtarı çok ekleyin`ssh-agent` hello komutunu kullanarak `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="0dcf8-157">Merhaba özel anahtar parolası şimdi depolanır `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="0dcf8-158">Kullanarak `ssh-copy-id` toocopy hello anahtar tooan VM var</span><span class="sxs-lookup"><span data-stu-id="0dcf8-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="0dcf8-159">Bir VM zaten oluşturduysanız hello yeni SSH ortak anahtarı tooyour Linux VM yükleyebilirsiniz ile:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="0dcf8-160">SSH yapılandırma dosyası oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="0dcf8-161">Önerilen bir en iyi yöntem toocreate olduğundan ve yapılandırma bir `~/.ssh/config` dosya toospeed yukarı oturum açmalar ve SSH istemci davranışını en iyi duruma getirme için.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="0dcf8-162">Aşağıdaki örnek hello standart bir yapılandırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="0dcf8-163">Merhaba dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="0dcf8-164">Merhaba dosya tooadd hello yeni SSH yapılandırması düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="0dcf8-165">Örnek `~/.ssh/config` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0dcf8-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="0dcf8-166">Her sunucu tooenable için kendi özel anahtar çiftini her toohave bölümler bu SSH yapılandırma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="0dcf8-167">Merhaba varsayılan ayarları (`Host *`) olan hello belirli ana bilgisayarlar yukarıya hello config dosyasına eşleşmeyen herhangi bir ana bilgisayar için.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="0dcf8-168">Yapılandırma dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0dcf8-168">Config file explained</span></span>

<span data-ttu-id="0dcf8-169">`Host`Merhaba ana bilgisayar üzerinde hello terminal çağrılan Hello adı =.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="0dcf8-170">`ssh fedora22`söyler `SSH` toouse hello hello ayarları blok etiketli değerlerde `Host fedora22` Not: ana bilgisayar kullanımınız için mantıklı olan ve hello gerçek ana bilgisayar herhangi bir sunucu adını temsil etmeyen her etiket olabilir.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="0dcf8-171">`Hostname 102.160.203.241`Başlangıç IP adresi veya erişilen hello sunucusu için DNS adı =.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="0dcf8-172">`User ahmet`Merhaba uzak kullanıcı hesabı toouse toohello Server'da oturum açarken =.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="0dcf8-173">`PubKeyAuthentication yes`= istediğiniz toouse bir SSH anahtarı toolog SSH söyler.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="0dcf8-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`Merhaba SSH özel anahtar ve kimlik doğrulaması için karşılık gelen ortak anahtar toouse =.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="0dcf8-175">Parolasız Linux içine SSH</span><span class="sxs-lookup"><span data-stu-id="0dcf8-175">SSH into Linux without a password</span></span>

<span data-ttu-id="0dcf8-176">SSH anahtar çiftiniz ve yapılandırılmış bir yapılandırma dosyasına sahip olduğunuza göre hızlı ve güvenli bir şekilde tooyour Linux VM içinde mümkün toolog şunlardır.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="0dcf8-177">Merhaba, bir SSH anahtarı hello komut istemlerini kullanarak tooa Server'da hello parolası için bu anahtar dosyası için ilk oturum açışınızda.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="0dcf8-178">Komut açıklaması</span><span class="sxs-lookup"><span data-stu-id="0dcf8-178">Command explained</span></span>

<span data-ttu-id="0dcf8-179">Zaman `ssh fedora22` yürütülür SSH ilk bulur ve hello tüm ayarları yükler `Host fedora22` blok yükler ve sonra tüm hello hello son blok ayarlarından kalan `Host *`.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dcf8-180">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0dcf8-180">Next Steps</span></span>

<span data-ttu-id="0dcf8-181">Sonraki yukarı toocreate Azure Linux VM'ler hello yeni SSH ortak anahtarını kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="0dcf8-182">Hello oturum açma olarak bir SSH ortak anahtarıyla oluşturulan azure VM'ler, daha iyi parolalar hello varsayılan oturum açma yöntemi ile oluşturulan VM'ler daha güvenli.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="0dcf8-183">SSH anahtarları kullanılarak oluşturulan Azure VM'ler, varsayılan olarak parola kullanımı devre dışı bırakılmış şekilde yapılandırılır; böylece parola tahminiyle gerçekleştirilen saldırı girişimleri önlenir.</span><span class="sxs-lookup"><span data-stu-id="0dcf8-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="0dcf8-184">Azure şablonu kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0dcf8-185">Hello Azure portal kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0dcf8-186">Hello Azure CLI kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dcf8-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
