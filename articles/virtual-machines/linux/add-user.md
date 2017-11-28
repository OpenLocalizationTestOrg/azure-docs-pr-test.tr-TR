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
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="558f8-103">Bir kullanıcı tooan Azure VM ekleme</span><span class="sxs-lookup"><span data-stu-id="558f8-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="558f8-104">Yeni bir Linux VM ilk görevlerde hello toocreate yeni bir kullanıcı biridir.</span><span class="sxs-lookup"><span data-stu-id="558f8-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="558f8-105">Bu makalede, biz oluşturmada size sudo kullanıcı hesabı, hello parola ayarlama, SSH ortak anahtarları ekleme yol ve son olarak `visudo` tooallow sudo parolasız.</span><span class="sxs-lookup"><span data-stu-id="558f8-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="558f8-106">Önkoşullar şunlardır: [bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/), [SSH ortak ve özel anahtarları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), bir Azure kaynak grubu ve hello Azure CLI yüklenmiş ve tooAzure Resource Manager modunu kullanarak geçiş `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="558f8-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="558f8-107">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="558f8-107">Quick Commands</span></span>
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

## <a name="detailed-walkthrough"></a><span data-ttu-id="558f8-108">Ayrıntılı Kılavuz</span><span class="sxs-lookup"><span data-stu-id="558f8-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="558f8-109">Giriş</span><span class="sxs-lookup"><span data-stu-id="558f8-109">Introduction</span></span>
<span data-ttu-id="558f8-110">Yeni bir sunucu ile Merhaba ilk ve en yaygın görevi tooadd bir kullanıcı hesabı biridir.</span><span class="sxs-lookup"><span data-stu-id="558f8-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="558f8-111">Kök oturum açmalar devre dışı bırakılmalıdır ve hello kök hesabının kendisi Linux sunucunuzla, yalnızca sudo kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="558f8-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="558f8-112">Bir kullanıcı kök yükseltme uygun şekilde tooadminister hello ve Linux kullanmak sudo kullanılarak ayrıcalıkları vermek.</span><span class="sxs-lookup"><span data-stu-id="558f8-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="558f8-113">Merhaba komutunu kullanarak `useradd` kullanıcı hesapları toohello Linux VM ekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="558f8-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="558f8-114">Çalışan `useradd` değiştirir `/etc/passwd`, `/etc/shadow`, `/etc/group`, ve `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="558f8-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="558f8-115">Bir komut satırı bayrağı toohello ekliyoruz `useradd` komutu tooalso Linux'ta hello yeni kullanıcı toohello uygun sudo gruba ekleyin.</span><span class="sxs-lookup"><span data-stu-id="558f8-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="558f8-116">Hatta sen `useradd` içine bir giriş oluşturur `/etc/passwd` hello yeni kullanıcı hesabı parola sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="558f8-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="558f8-117">Merhaba basit kullanarak hello yeni kullanıcı için bir başlangıç parolası oluşturuyoruz `passwd` komutu.</span><span class="sxs-lookup"><span data-stu-id="558f8-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="558f8-118">Merhaba son toomodify hello sudo tooallow tooenter her komut için bir parola gerek kalmadan bu kullanıcı tooexecute komutları sudo ayrıcalıklarıyla kuralları adımdır.</span><span class="sxs-lookup"><span data-stu-id="558f8-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="558f8-119">Bu kullanıcı hesabı varsayıyoruz hello özel anahtarı kullanarak oturum kötü aktörlerden güvendedir ve bir parola olmadan tooallow sudo erişim geçiyor.</span><span class="sxs-lookup"><span data-stu-id="558f8-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="558f8-120">Bir tek sudo kullanıcı tooan Azure VM ekleme</span><span class="sxs-lookup"><span data-stu-id="558f8-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="558f8-121">İçinde toohello Azure VM SSH anahtarları kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="558f8-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="558f8-122">Kurulum SSH ortak anahtar erişimi varsa, bu makalenin ilk tamamlamak [kullanan ortak anahtar kimlik doğrulaması ile Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="558f8-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="558f8-123">Merhaba `useradd` komutu hello aşağıdaki görevleri tamamlar:</span><span class="sxs-lookup"><span data-stu-id="558f8-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="558f8-124">Yeni bir kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="558f8-124">create a new user account</span></span>
* <span data-ttu-id="558f8-125">Merhaba ile yeni bir kullanıcı grubu oluşturma aynı adı</span><span class="sxs-lookup"><span data-stu-id="558f8-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="558f8-126">boş bir girdiyi çok ekleme`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="558f8-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="558f8-127">boş bir girdiyi çok ekleme`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="558f8-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="558f8-128">Merhaba `-G` komut satırı bayrağı hello yeni kullanıcı hesabı kök yükseltme ayrıcalıkları vermek hello yeni kullanıcı hesabı toohello uygun Linux grubu ekler.</span><span class="sxs-lookup"><span data-stu-id="558f8-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="558f8-129">Merhaba kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="558f8-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="558f8-130">Bir parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="558f8-130">Set a password</span></span>
<span data-ttu-id="558f8-131">Merhaba `useradd` komut hello kullanıcı oluşturur ve bir giriş tooboth ekler `/etc/passwd` ve `/etc/gpasswd` gerçekten hello parola ayarlı değil ancak.</span><span class="sxs-lookup"><span data-stu-id="558f8-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="558f8-132">Merhaba parola hello kullanarak toohello girişini eklenir `passwd` komutu.</span><span class="sxs-lookup"><span data-stu-id="558f8-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="558f8-133">Şimdi sudo ayrıcalıklarına sahip bir kullanıcı hello sunucuda sahibiz.</span><span class="sxs-lookup"><span data-stu-id="558f8-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="558f8-134">SSH ortak anahtarı toohello yeni kullanıcı hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="558f8-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="558f8-135">Merhaba, makinenizden kullanmak `ssh-copy-id` hello yeni parolayla komutu.</span><span class="sxs-lookup"><span data-stu-id="558f8-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="558f8-136">Visudo tooallow sudo kullanımı bir parola olmadan kullanma</span><span class="sxs-lookup"><span data-stu-id="558f8-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="558f8-137">Kullanarak `visudo` tooedit hello `/etc/sudoers` dosya yanlış bu önemli dosyasını değiştirerek karşı koruma birkaç katmanları ekler.</span><span class="sxs-lookup"><span data-stu-id="558f8-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="558f8-138">Yürütme sırasında `visudo`, hello `/etc/sudoers` dosyasıdır kilitli tooensure etkin olarak düzenlenmekte olan sırada başka bir kullanıcı değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="558f8-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="558f8-139">Merhaba `/etc/sudoers` dosya da denetlenir hatalardan kaynaklanan `visudo` ne zaman toosave denemek veya çıkış bozuk sudoers dosyası kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="558f8-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="558f8-140">Biz zaten sudo erişim hello doğru varsayılan grubundaki kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="558f8-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="558f8-141">Şimdi Biz bu grupları toouse sudo parolasız tooenable çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="558f8-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

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

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="558f8-142">Merhaba kullanıcı ssh anahtarları ve sudo doğrulayın</span><span class="sxs-lookup"><span data-stu-id="558f8-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
