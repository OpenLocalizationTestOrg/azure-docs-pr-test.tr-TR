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
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="2a11a-103">Windows Azure üzerinde ile nasıl tooUse SSH anahtarları</span><span class="sxs-lookup"><span data-stu-id="2a11a-103">How tooUse SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a11a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2a11a-104">Windows</span></span>](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [<span data-ttu-id="2a11a-105">Linux/Mac</span><span class="sxs-lookup"><span data-stu-id="2a11a-105">Linux/Mac</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="2a11a-106">Azure'da tooLinux sanal makineler (VM'ler) bağlandığınızda, kullanması gereken [ortak anahtar şifrelemesini](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide tooyour Linux VM içinde daha güvenli bir şekilde toolog.</span><span class="sxs-lookup"><span data-stu-id="2a11a-106">When you connect tooLinux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide a more secure way toolog in tooyour Linux VM.</span></span> <span data-ttu-id="2a11a-107">Bu işlem, bir kullanıcı adı ve parola yerine hello güvenli Kabuk (SSH) komutu tooauthenticate kendiniz kullanarak ortak ve özel bir anahtar değişimi içerir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-107">This process involves a public and private key exchange using hello secure shell (SSH) command tooauthenticate yourself rather than a username and password.</span></span> <span data-ttu-id="2a11a-108">Parolalar web sunucuları gibi İnternete vm'lerinde özellikle savunmasız toobrute kuvvet saldırıları ' dir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-108">Passwords are vulnerable toobrute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="2a11a-109">Bu makalede SSH anahtarları ve nasıl toogenerate hello bir Windows bilgisayarda uygun anahtarlara genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a11a-109">This article provides an overview of SSH keys and how toogenerate hello appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="2a11a-110">SSH ve anahtarları genel bakış</span><span class="sxs-lookup"><span data-stu-id="2a11a-110">Overview of SSH and keys</span></span>
<span data-ttu-id="2a11a-111">Tooyour Linux VM ortak ve özel anahtarları kullanarak güvenli bir şekilde kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a11a-111">You can securely log in tooyour Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="2a11a-112">Merhaba **ortak anahtar** Linux VM veya ortak anahtar şifrelemesinde toouse istediğiniz başka bir hizmet yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-112">hello **public key** is placed on your Linux VM, or any other service that you wish toouse with public-key cryptography.</span></span>
* <span data-ttu-id="2a11a-113">Merhaba **özel anahtarı** tooverify, oturum açtığınızda ne mevcut tooyour Linux VM olduğu kimliğinizi.</span><span class="sxs-lookup"><span data-stu-id="2a11a-113">hello **private key** is what you present tooyour Linux VM when you log in, tooverify your identity.</span></span> <span data-ttu-id="2a11a-114">Bu özel anahtarı koruyun.</span><span class="sxs-lookup"><span data-stu-id="2a11a-114">Protect this private key.</span></span> <span data-ttu-id="2a11a-115">Özel anahtarı paylaşmayın.</span><span class="sxs-lookup"><span data-stu-id="2a11a-115">Do not share it.</span></span>

<span data-ttu-id="2a11a-116">Bu ortak ve özel anahtarlar, birden çok sanal makineleri ve hizmetleri üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="2a11a-117">Her VM veya tooaccess istediğiniz hizmet için bir çift anahtar gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a11a-117">You do not need a pair of keys for each VM or service you wish tooaccess.</span></span> <span data-ttu-id="2a11a-118">Daha ayrıntılı bir bakış için bkz: [ortak anahtar şifrelemesini](https://wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="2a11a-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="2a11a-119">SSH güvenli olmayan bağlantıları üzerinden güvenli oturum açma bilgileri veren bir şifreli bir bağlantı protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="2a11a-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="2a11a-120">Bunu hello varsayılan bağlantı Azure'da barındırılan Linux VM'ler için protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="2a11a-120">It is hello default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="2a11a-121">SSH kendisini şifreli bir bağlantı sağlasa da, SSH bağlantılarla parolalarla hala hello VM savunmasız toobrute kuvvet saldırıları veya parolalarını tahmin bırakır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves hello VM vulnerable toobrute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="2a11a-122">Bir daha güvenli ve tercih edilen bağlantı tooa SSH kullanarak VM bu ortak ve özel anahtarları olarak da bilinen SSH anahtarları kullanılarak yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-122">A more secure and preferred method of connecting tooa VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="2a11a-123">Toouse SSH anahtarları istemiyorsanız hala tooyour Linux VM'ler bir parola kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-123">If you do not wish toouse SSH keys, you can still log in tooyour Linux VMs using a password.</span></span> <span data-ttu-id="2a11a-124">VM gösterilen toohello Internet değilse, parolaları kullanarak yeterli olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-124">If your VM is not exposed toohello Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="2a11a-125">Ancak, yine toomanage parolalarınızı için her bir Linux VM ve gerekir sağlıklı parola ilkeleri ve minimum parola uzunluğu ve bunları düzenli olarak güncelleştirilmesi gibi uygulamalarını korumak.</span><span class="sxs-lookup"><span data-stu-id="2a11a-125">However, you still need toomanage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="2a11a-126">SSH anahtarları Hello kullanımını arasında birden çok sanal makineleri tek tek kimlik bilgilerini yönetme hello karmaşıklığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-126">hello use of SSH keys reduces hello complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="2a11a-127">Windows paketleri ve SSH istemcileri</span><span class="sxs-lookup"><span data-stu-id="2a11a-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="2a11a-128">Tooand bağlanmak Azure kullanarak Linux sanal makineleri yönetme bir **SSH istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="2a11a-128">You connect tooand manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="2a11a-129">Windows bilgisayarlarda yüklü olan bir SSH istemcisi genellikle yok.</span><span class="sxs-lookup"><span data-stu-id="2a11a-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="2a11a-130">Bash için Windows Hello Windows 10 Anniversary güncelleştirme eklenir ve hello en son Windows 10 oluşturucuları güncelleştirmesi ek güncelleştirmeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a11a-130">hello Windows 10 Anniversary Update added Bash for Windows, and hello latest Windows 10 Creators Update provides additional updates.</span></span> <span data-ttu-id="2a11a-131">Bu Windows alt sistemi Linux için yerel bir Bash kabuğunda içinde bir SSH istemcisi gibi toorun ve erişim yardımcı programlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a11a-131">This Windows Subsystem for Linux allows you toorun and access utilities such as an SSH client natively within a Bash shell.</span></span> <span data-ttu-id="2a11a-132">Ardından herhangi bir hello Linux belgeleri gibi izleyebilirsiniz [nasıl toogenerate SSH anahtarı için Linux çiftleri](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="2a11a-132">You can then follow any of hello Linux docs, such as [How toogenerate SSH key pairs for Linux](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="2a11a-133">Bash Windows halen geliştirilme aşamasındadır ve beta sürümü olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-133">Bash for Windows is still under development, and is considered a beta release.</span></span> <span data-ttu-id="2a11a-134">Windows için Bash hakkında daha fazla bilgi için bkz: [Bash Ubuntu Windows üzerinde](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="2a11a-134">For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="2a11a-135">Toouse bir şey Windows dışındaki Bash isterseniz, yükleyebilmek için ortak Windows SSH istemcilerini paketleri aşağıdaki hello bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2a11a-135">If you wish toouse something other than Bash for Windows, common Windows SSH clients you can install are included in hello following packages:</span></span>

* [<span data-ttu-id="2a11a-136">Windows için Git</span><span class="sxs-lookup"><span data-stu-id="2a11a-136">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="2a11a-137">puTTY</span><span class="sxs-lookup"><span data-stu-id="2a11a-137">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="2a11a-138">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="2a11a-138">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="2a11a-139">Cygwin</span><span class="sxs-lookup"><span data-stu-id="2a11a-139">Cygwin</span></span>](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a><span data-ttu-id="2a11a-140">Dosyaları anahtar toocreate gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="2a11a-140">Which key files do you need toocreate?</span></span>
<span data-ttu-id="2a11a-141">Azure en az 2048 bit gerektirir **ssh-rsa** ortak ve özel anahtarlar biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="2a11a-141">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="2a11a-142">Merhaba Klasik dağıtım modeli kullanarak Azure kaynaklarına yönetiyorsanız, toogenerate bir PEM da gerekir (`.pem` dosyası).</span><span class="sxs-lookup"><span data-stu-id="2a11a-142">If you are managing Azure resources using hello Classic deployment model, you also need toogenerate a PEM (`.pem` file).</span></span>

<span data-ttu-id="2a11a-143">Merhaba dağıtım senaryoları ve her kullanan dosyaları hello türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2a11a-143">Here are hello deployment scenarios, and hello types of files you use in each:</span></span>

1. <span data-ttu-id="2a11a-144">**SSH-rsa** anahtarları hello kullanarak herhangi bir dağıtım için gerekli [Azure portal](https://portal.azure.com)ve Resource Manager dağıtımları hello kullanarak [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2a11a-144">**ssh-rsa** keys are required for any deployment using hello [Azure portal](https://portal.azure.com), and Resource Manager deployments using hello [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="2a11a-145">Bu anahtarları, genellikle tüm çoğu kişi ihtiyacınız olan.</span><span class="sxs-lookup"><span data-stu-id="2a11a-145">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="2a11a-146">A `.pem` hello Klasik dağıtım kullanarak gerekli toocreate VM'ler bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-146">A `.pem` file is required toocreate VMs using hello Classic deployment.</span></span> <span data-ttu-id="2a11a-147">Bu anahtarları Klasik dağıtımlarda hello kullanılırken desteklenen [Azure portal](https://portal.azure.com) veya [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2a11a-147">These keys are supported in Classic deployments when using hello [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="2a11a-148">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan kaynakları yönetiyorsanız, yalnızca toocreate bu ek anahtar ve sertifikalar gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-148">You only need toocreate these additional keys and certificates if you are managing resources created using hello Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="2a11a-149">Windows için Git yükleme</span><span class="sxs-lookup"><span data-stu-id="2a11a-149">Install Git for Windows</span></span>
<span data-ttu-id="2a11a-150">Merhaba önceki bölümde listelenen hello dahil çeşitli paketler `openssl` Windows için aracı.</span><span class="sxs-lookup"><span data-stu-id="2a11a-150">hello preceding section listed several packages that include hello `openssl` tool for Windows.</span></span> <span data-ttu-id="2a11a-151">Gerekli toocreate ortak ve özel anahtarlar aracıdır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-151">This tool is needed toocreate public and private keys.</span></span> <span data-ttu-id="2a11a-152">örnekler ayrıntı nasıl aşağıdaki hello tooinstall ve **Windows için Git**tercih ettiğiniz hangi paket seçebilirsiniz ancak.</span><span class="sxs-lookup"><span data-stu-id="2a11a-152">hello following examples detail how tooinstall and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="2a11a-153">**Windows için Git** toosome ek açık kaynaklı yazılım erişim verir ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) araçları ve yardımcı programları Linux VM'ler ile çalışırken, yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-153">**Git for Windows** gives you access toosome additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="2a11a-154">İndirme ve yükleme **Windows için Git** konumu aşağıdaki hello gelen: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span><span class="sxs-lookup"><span data-stu-id="2a11a-154">Download and install **Git for Windows** from hello following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="2a11a-155">Merhaba varsayılan seçenekleri hello sırasında yükleme işlemi toochange özellikle gerekmedikçe kabul bunları.</span><span class="sxs-lookup"><span data-stu-id="2a11a-155">Accept hello default options during hello install process unless you specifically need toochange them.</span></span>
3. <span data-ttu-id="2a11a-156">Çalıştırma **Git Bash** hello gelen **Başlat menüsü** > **Git** > **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="2a11a-156">Run **Git Bash** from hello **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="2a11a-157">Hello konsol benzer toohello örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2a11a-157">hello console looks similar toohello following example:</span></span>

    ![Windows için Git Bash Kabuk](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="2a11a-159">Özel bir anahtar oluşturun</span><span class="sxs-lookup"><span data-stu-id="2a11a-159">Create a private key</span></span>
1. <span data-ttu-id="2a11a-160">İçinde **Git Bash** penceresi, kullanım `openssl.exe` toocreate bir özel anahtar.</span><span class="sxs-lookup"><span data-stu-id="2a11a-160">In your **Git Bash** window, use `openssl.exe` toocreate a private key.</span></span> <span data-ttu-id="2a11a-161">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myPrivateKey` ve adlı sertifika `myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="2a11a-161">hello following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="2a11a-162">Hello çıkış benzer toohello örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2a11a-162">hello output looks similar toohello following example:</span></span>

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

   <span data-ttu-id="2a11a-163">Bash hata bildirirse, yeni bir açmayı deneyin **Git Bash** yükseltilmiş ayrıcalıklarla penceresi.</span><span class="sxs-lookup"><span data-stu-id="2a11a-163">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="2a11a-164">Merhaba daha sonra yeniden `openssl` komutu.</span><span class="sxs-lookup"><span data-stu-id="2a11a-164">Then, rerun hello `openssl` command.</span></span>

2. <span data-ttu-id="2a11a-165">Yanıt hello ülke adı, konumu, kuruluşunuzun adı, vb. için ister.</span><span class="sxs-lookup"><span data-stu-id="2a11a-165">Answer hello prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="2a11a-166">Yeni özel anahtar ve sertifika, geçerli çalışma dizini içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a11a-166">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="2a11a-167">Bir güvenlik önlemi olarak, böylece yalnızca erişebilir özel anahtarınızı hello izinleri ayarlamalısınız:</span><span class="sxs-lookup"><span data-stu-id="2a11a-167">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="2a11a-168">Merhaba [sonraki bölümde](#create-a-private-key-for-putty) PuTTYgen tooboth kullanarak ayrıntılarını görüntülemek ve hello ortak anahtarı kullanır ve bir özel anahtar PuTTY tooSSH tooLinux VM'ler kullanmak için belirli oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a11a-168">hello [next section](#create-a-private-key-for-putty) details using PuTTYgen tooboth view and use hello public key, and create a private key specific for using PuTTY tooSSH tooLinux VMs.</span></span> <span data-ttu-id="2a11a-169">Merhaba aşağıdaki komutu adlı bir ortak anahtar dosyası oluşturur `myPublicKey.key` hemen kullanabileceğiniz:</span><span class="sxs-lookup"><span data-stu-id="2a11a-169">hello following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="2a11a-170">Ayrıca toomanage Klasik kaynakları gerekiyorsa, hello Dönüştür `myCert.pem` çok`myCert.cer` (DER ile kodlanmış X509 sertifika).</span><span class="sxs-lookup"><span data-stu-id="2a11a-170">If you also need toomanage Classic resources, convert hello `myCert.pem` too`myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="2a11a-171">Yalnızca toospecifically gerekiyorsa bu isteğe bağlı bir adım gerçekleştirmeniz eski Classic kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="2a11a-171">Perform this optional step only if you need toospecifically manage older Classic resources.</span></span>

    <span data-ttu-id="2a11a-172">Komutu aşağıdaki hello kullanarak hello sertifika Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="2a11a-172">Convert hello certificate using hello following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="2a11a-173">PuTTY için özel bir anahtar oluşturun</span><span class="sxs-lookup"><span data-stu-id="2a11a-173">Create a private key for PuTTY</span></span>
<span data-ttu-id="2a11a-174">Putty'yi Windows için ortak bir SSH İstemcisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-174">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="2a11a-175">İstediğiniz herhangi bir SSH istemcisi ücretsiz toouse şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-175">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="2a11a-176">PuTTY toouse toocreate key - PuTTY özel anahtar (PPK) ek bir türde gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-176">toouse PuTTY, you need toocreate an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="2a11a-177">Toouse PuTTY istemiyorsanız bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a11a-177">If you do not wish toouse PuTTY, skip this section.</span></span>

<span data-ttu-id="2a11a-178">Merhaba aşağıdaki örnek PuTTY toouse için özel olarak bu ek özel anahtarı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2a11a-178">hello following example creates this additional private key specifically for PuTTY toouse:</span></span>

1. <span data-ttu-id="2a11a-179">Kullanım **Git Bash** tooconvert, özel anahtar bir RSA özel anahtarı PuTTYgen anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a11a-179">Use **Git Bash** tooconvert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="2a11a-180">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myPrivateKey_rsa` adlı hello var olan anahtardan `myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="2a11a-180">hello following example creates a key named `myPrivateKey_rsa` from hello existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="2a11a-181">Bir güvenlik önlemi olarak, böylece yalnızca erişebilir özel anahtarınızı hello izinleri ayarlamalısınız:</span><span class="sxs-lookup"><span data-stu-id="2a11a-181">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="2a11a-182">Karşıdan yükleme ve konumu aşağıdaki hello PuTTYgen çalıştırma: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="2a11a-182">Download and run PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="2a11a-183">Merhaba menüsünü tıklatın: **dosya** > **yük özel anahtar**</span><span class="sxs-lookup"><span data-stu-id="2a11a-183">Click hello menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="2a11a-184">Özel anahtarınızı bulun (`myPrivateKey_rsa` hello önceki örnekte).</span><span class="sxs-lookup"><span data-stu-id="2a11a-184">Locate your private key (`myPrivateKey_rsa` in hello previous example).</span></span> <span data-ttu-id="2a11a-185">başlattığınızda hello varsayılan dizin **Git Bash** olan `C:\Users\%username%`.</span><span class="sxs-lookup"><span data-stu-id="2a11a-185">hello default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="2a11a-186">Değiştirme hello dosya filtresi tooshow **tüm dosyalar (\*.\*)** :</span><span class="sxs-lookup"><span data-stu-id="2a11a-186">Change hello file filter tooshow **All Files (\*.\*)**:</span></span>

    ![PuTTYgen Hello var olan özel anahtarı yükleme](./media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="2a11a-188">Tıklatın **açık**.</span><span class="sxs-lookup"><span data-stu-id="2a11a-188">Click **Open**.</span></span> <span data-ttu-id="2a11a-189">Bir istem hello anahtara başarıyla içe aktarıldığından gösterir:</span><span class="sxs-lookup"><span data-stu-id="2a11a-189">A prompt indicates that hello key has been successfully imported:</span></span>

    ![Anahtar tooPuTTYgen başarıyla alındı](./media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="2a11a-191">Tıklatın **Tamam** tooclose hello istemi.</span><span class="sxs-lookup"><span data-stu-id="2a11a-191">Click **OK** tooclose hello prompt.</span></span>
7. <span data-ttu-id="2a11a-192">Merhaba ortak anahtar hello hello üstünde görüntülenen **PuTTYgen** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2a11a-192">hello public key is displayed at hello top of hello **PuTTYgen** window.</span></span> <span data-ttu-id="2a11a-193">Kopyalayın ve bir Linux VM oluşturduğunuzda, bu ortak anahtar hello Azure portalında veya Azure Resource Manager şablonu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a11a-193">You copy and paste this public key into hello Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="2a11a-194">Tıklatarak **ortak anahtarı Kaydet** toosave bir kopya tooyour bilgisayar:</span><span class="sxs-lookup"><span data-stu-id="2a11a-194">You can also click **Save public key** toosave a copy tooyour computer:</span></span>

    ![PuTTY ortak anahtar dosyasını kaydedin](./media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="2a11a-196">Merhaba aşağıdaki örnekte nasıl kopyalayıp bir Linux VM oluşturduğunuzda, bu ortak anahtar Azure portal hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-196">hello following example shows how you would copy and paste this public key into hello Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="2a11a-197">Merhaba ortak anahtarı genellikle sonra depolanır `~/.ssh/authorized_keys` , yeni bir VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2a11a-197">hello public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Hello Azure portalında bir VM oluşturduğunuzda ortak anahtarı kullan](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="2a11a-199">Geri **PuTTYgen**, tıklatın **özel anahtarı Kaydet**:</span><span class="sxs-lookup"><span data-stu-id="2a11a-199">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![PuTTY özel anahtar dosyasını kaydedin](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > <span data-ttu-id="2a11a-201">Bir istem, toocontinue anahtarınız için bir parola girmeden isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="2a11a-201">A prompt asks if you wish toocontinue without entering a passphrase for your key.</span></span> <span data-ttu-id="2a11a-202">Bir parola parola ekli tooyour özel gibi anahtardır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-202">A passphrase is like a password attached tooyour private key.</span></span> <span data-ttu-id="2a11a-203">Birisi olsa bile tooobtain özel anahtarınızı bunlar hala yalnızca hello anahtarını kullanarak yapabilir tooauthenticate olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-203">Even if someone were tooobtain your private key, they still would not be able tooauthenticate using just hello key.</span></span> <span data-ttu-id="2a11a-204">Bunlar ayrıca hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-204">They would also need hello passphrase.</span></span> <span data-ttu-id="2a11a-205">Bir parola birinin özel anahtarınızı elde ederse tooany VM oturum açabilecekleri, anahtar kullanan hizmet.</span><span class="sxs-lookup"><span data-stu-id="2a11a-205">Without a passphrase, if someone obtains your private key, they can log in tooany VM or service that uses that key.</span></span> <span data-ttu-id="2a11a-206">Bir parola oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-206">We recommend you create a passphrase.</span></span> <span data-ttu-id="2a11a-207">Ancak, hello parolayı unutursanız, yoktur hiçbir şekilde toorecover.</span><span class="sxs-lookup"><span data-stu-id="2a11a-207">However, if you forget hello passphrase, there is no way toorecover it.</span></span>
   >
   >

    <span data-ttu-id="2a11a-208">Bir parola tooenter isterseniz tıklayın **Hayır**hello ana PuTTYgen penceresinde bir parola girin ve ardından **özel anahtarı Kaydet** yeniden.</span><span class="sxs-lookup"><span data-stu-id="2a11a-208">If you wish tooenter a passphrase, click **No**, enter a passphrase in hello main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="2a11a-209">Aksi takdirde tıklatın **Evet** hello isteğe bağlı bir parola sağlamadan toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2a11a-209">Otherwise, click **Yes** toocontinue without providing hello optional passphrase.</span></span>
9. <span data-ttu-id="2a11a-210">Bir ad ve konum toosave PPK dosyanızı girin.</span><span class="sxs-lookup"><span data-stu-id="2a11a-210">Enter a name and location toosave your PPK file.</span></span>

## <a name="use-putty-toossh-tooa-linux-machine"></a><span data-ttu-id="2a11a-211">Putty tooSSH tooa Linux makine kullanın</span><span class="sxs-lookup"><span data-stu-id="2a11a-211">Use Putty tooSSH tooa Linux Machine</span></span>
<span data-ttu-id="2a11a-212">Yeniden PuTTY Windows için ortak bir SSH İstemcisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-212">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="2a11a-213">İstediğiniz herhangi bir SSH istemcisi ücretsiz toouse şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2a11a-213">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="2a11a-214">adımları ayrıntı nasıl aşağıdaki hello toouse, özel anahtar tooauthenticate SSH kullanarak, Azure VM ile.</span><span class="sxs-lookup"><span data-stu-id="2a11a-214">hello following steps detail how toouse your private key tooauthenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="2a11a-215">tooload, özel anahtar tooauthenticate hello SSH bağlantısı gerektiren bakımından diğer SSH anahtar istemcileri başlangıç adımları benzerdir.</span><span class="sxs-lookup"><span data-stu-id="2a11a-215">hello steps are similar in other SSH key clients in terms of needing tooload your private key tooauthenticate hello SSH connection.</span></span>

1. <span data-ttu-id="2a11a-216">İndirme ve çalıştırma putty gelen hello konumu: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="2a11a-216">Download and run putty from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="2a11a-217">Merhaba ana bilgisayar adı veya IP adresini hello Azure portal, VM'den doldurun:</span><span class="sxs-lookup"><span data-stu-id="2a11a-217">Fill in hello host name or IP address of your VM from hello Azure portal:</span></span>

    ![PuTTY yeni bağlantı Aç](./media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="2a11a-219">Seçmeden önce **açık**, tıklatın **bağlantı** > **SSH** > **Auth** sekmesi. Gözat tooand özel anahtarınızı seçin:</span><span class="sxs-lookup"><span data-stu-id="2a11a-219">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse tooand select your private key:</span></span>

    ![Kimlik doğrulaması için PuTTY özel anahtarınızı seçin](./media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="2a11a-221">Tıklatın **açık** tooconnect tooyour sanal makine</span><span class="sxs-lookup"><span data-stu-id="2a11a-221">Click **Open** tooconnect tooyour virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a11a-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a11a-222">Next steps</span></span>
<span data-ttu-id="2a11a-223">Merhaba ortak ve özel anahtarlar da oluşturabileceğiniz [OS X ile Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a11a-223">You can also generate hello public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2a11a-224">Windows için Bash ve Windows bilgisayarınızda OSS araçları kullanıma hazır olan bir hello yararları hakkında daha fazla bilgi için bkz: [Bash Ubuntu Windows üzerinde](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="2a11a-224">For more information about Bash for Windows and hello benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="2a11a-225">SSH tooconnect tooyour Linux VM'ler kullanma konusunda sorun yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure Linux VM'de](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a11a-225">If you have trouble using SSH tooconnect tooyour Linux VMs, see [Troubleshoot SSH connections tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
