---
title: "Azure’da Linux VM’ler için SSH anahtar çifti oluşturmaya ilişkin ayrıntılı adımlar | Microsoft Belgeleri"
description: "Azure’da farklı kullanım örnekleri için belirli sertifikalarla birlikte Linux VM’ler için bir SSH ortak ve özel anahtar çifti oluşturmaya yönelik ek adımlar hakkında bilgi alın."
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="945cf-103">Azure’da Linux VM için SSH anahtar çifti ve ek sertifikalar oluşturmaya yönelik ayrıntılı izlenecek yol</span><span class="sxs-lookup"><span data-stu-id="945cf-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="945cf-104">SSH anahtar çiftiyle Azure'da Sanal Makineler oluşturabilirsiniz. Bu sayede kimlik doğrulaması için SSH anahtarlarının kullanımını varsayılan hale getirerek oturum açmak için parolalara duyulan gereksinimi ortadan kaldırırsınız.</span><span class="sxs-lookup"><span data-stu-id="945cf-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="945cf-105">Parolalar tahmin edilebilir ve sanal makinelerinizi, parolanızı tahmin etmeye yönelik sayısız girişime maruz bırakır.</span><span class="sxs-lookup"><span data-stu-id="945cf-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="945cf-106">Azure CLI veya Resource Manager şablonları ile oluşturulan sanal makineler, dağıtımın bir parçası olarak SSH ortak anahtarınızı içerebilir; böylece dağıtım sonrası SSH için parolayla girişleri devre dışı bırakma yapılandırma gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="945cf-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="945cf-107">Bu makalede ayrıntılı adımlar ve ek örnekler oluşturma sertifikaların gibi Linux sanal makineleri ile kullanılmak üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="945cf-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="945cf-108">Bir SSH anahtar çiftini hızlıca oluşturup kullanmak istiyorsanız bkz. [Azure’da Linux VM’ler için SSH ortak ve özel anahtar çifti oluşturma](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="945cf-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="945cf-109">SSH anahtarlarını anlama</span><span class="sxs-lookup"><span data-stu-id="945cf-109">Understanding SSH keys</span></span>

<span data-ttu-id="945cf-110">SSH ortak ve özel anahtarlarını kullanmak, Linux sunucularınızda oturum açmanın en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="945cf-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="945cf-111">[Ortak anahtar şifrelemesi](https://en.wikipedia.org/wiki/Public-key_cryptography), Azure'daki Linux veya BSD VM'nizde oturum açmak için parolalara kıyasla çok daha güvenli bir yol sunar. Parolalar, saldırılara çok daha kolay şekilde maruz kalır.</span><span class="sxs-lookup"><span data-stu-id="945cf-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="945cf-112">Ortak anahtarınız herkesle paylaşılabilir; ancak, özel anahtarınıza yalnızca siz (veya yerel güvenlik altyapınız) sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="945cf-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="945cf-113">SSH özel anahtarının korunması için [çok güvenli parola](https://www.xkcd.com/936/) (kaynak:[xkcd.com](https://xkcd.com)) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="945cf-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="945cf-114">Bu parola yalnızca özel SSH anahtar dosyasına erişim için kullanılır ve kullanıcı hesabı parolası **değildir**.</span><span class="sxs-lookup"><span data-stu-id="945cf-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="945cf-115">SSH anahtarınıza parola eklediğinizde bu parola özel anahtarı 128 bit AES kullanarak şifreler; böylece özel anahtar, şifresini çözen parola olmadan kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="945cf-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="945cf-116">Bir saldırganın özel anahtarınızı çalması ve bu anahtarın bir parolasının olmaması halinde saldırgan, bu özel anahtarı ilgili ortak anahtara sahip sunucularınızda oturum açmak için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="945cf-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="945cf-117">Özel anahtar parola korumalı ise, Azure’daki altyapınız için ek bir güvenlik katmanı sağlayarak, bu saldırgan tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="945cf-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="945cf-118">Bu makalede, Azure Resource Manager ile yapılan dağıtımlar için önerilen bir SSH protokolü sürüm 2 RSA ortak ve özel anahtar dosyası çifti (aynı zamanda "ssh-rsa" anahtarları olarak adlandırılır) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="945cf-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="945cf-119">Hem klasik hem de Resource Manager dağıtımları için [portalda](https://portal.azure.com) *ssh-rsa* anahtarları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="945cf-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="945cf-120">SSH anahtarlarının kullanımı ve avantajları</span><span class="sxs-lookup"><span data-stu-id="945cf-120">SSH keys use and benefits</span></span>

<span data-ttu-id="945cf-121">Azure en az 2048 bit, SSH protokolü sürüm 2 RSA biçiminde ortak ve özel anahtarlar gerektirir; ortak anahtar dosyası `.pub` kapsayıcısı biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="945cf-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="945cf-122">Anahtarları oluşturmak için `ssh-keygen` kullanın. Bu, bir dizi soru sorduktan sonra özel bir anahtar ve eşleşen bir ortak anahtar yazar.</span><span class="sxs-lookup"><span data-stu-id="945cf-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="945cf-123">Bir Azure VM oluşturulduğunda Azure, ortak anahtarı VM üzerindeki `~/.ssh/authorized_keys` klasörüne kopyalar.</span><span class="sxs-lookup"><span data-stu-id="945cf-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="945cf-124">`~/.ssh/authorized_keys` içindeki SSH anahtarları, bir istemcinin SSH oturum açma bağlantısındaki ilgili özel anahtarla eşleşip eşleşmediğini sınar.</span><span class="sxs-lookup"><span data-stu-id="945cf-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="945cf-125">Kimlik doğrulama için SSH anahtarları kullanılarak bir Azure Linux VM oluşturulduğunda Azure, SSHD sunucusunu parolayla girişleri devre dışı bırakarak yalnızca SSH anahtarlarına izin verecek şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="945cf-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="945cf-126">Dolayısıyla, SSH anahtarlarıyla Azure Linux VM'leri oluşturarak VM dağıtımının güvenliğini sağlamaya yardımcı olabilirsiniz ve dağıtım sonrasında **sshd_config** dosyasında parolaları devre dışı bırakma yapılandırma adımının uygulanmasına gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="945cf-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="945cf-127">SSH-keygen’i kullanma</span><span class="sxs-lookup"><span data-stu-id="945cf-127">Using ssh-keygen</span></span>

<span data-ttu-id="945cf-128">Bu komut, 2048 bit RSA kullanarak parola korumalı (şifrelenmiş) bir SSH anahtar çifti oluşturur; kolayca anlaşılabilmesi için komuta açıklama eklenir.</span><span class="sxs-lookup"><span data-stu-id="945cf-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="945cf-129">SSH anahtarları, varsayılan olarak `~/.ssh` dizininde tutulur.</span><span class="sxs-lookup"><span data-stu-id="945cf-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="945cf-130">`~/.ssh` dizininiz yoksa `ssh-keygen` komutu, doğru izinler ile sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="945cf-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="945cf-131">*Komut açıklaması*</span><span class="sxs-lookup"><span data-stu-id="945cf-131">*Command explained*</span></span>

<span data-ttu-id="945cf-132">`ssh-keygen` = anahtarları oluşturmak için kullanılan program</span><span class="sxs-lookup"><span data-stu-id="945cf-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="945cf-133">`-t rsa`RSA biçimi [wikipedia] oluşturulacak anahtar türü =[sonunda parens](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = anahtar bitleri</span><span class="sxs-lookup"><span data-stu-id="945cf-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="945cf-134">`-C "azureuser@myserver"` = kolayca tanımlamak için ortak anahtar dosyasının sonuna eklenen bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="945cf-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="945cf-135">Normalde açıklama olarak bir e-posta kullanılır ancak altyapınız için en uygun seçenek hangisiyse onu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="945cf-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="945cf-136">`asm` kullanarak klasik dağıtım</span><span class="sxs-lookup"><span data-stu-id="945cf-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="945cf-137">Klasik dağıtım modeli kullanılıyorsa (`asm` CLI moduna), bir SSH-RSA ortak anahtar kullanabilir veya bir RFC4716 biçimlendirilmiş pem kapsayıcısında anahtar.</span><span class="sxs-lookup"><span data-stu-id="945cf-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="945cf-138">SSH-RSA ortak anahtarı, bu makalenin önceki bölümlerinde `ssh-keygen` kullanılarak oluşturulan anahtardır.</span><span class="sxs-lookup"><span data-stu-id="945cf-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="945cf-139">Var olan bir SSH ortak anahtarından RFC4716 biçimli bir anahtar oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="945cf-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="945cf-140">ssh-keygen örneği</span><span class="sxs-lookup"><span data-stu-id="945cf-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="945cf-141">Kaydedilen anahtar dosyaları:</span><span class="sxs-lookup"><span data-stu-id="945cf-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="945cf-142">Bu makale için anahtar çifti adı.</span><span class="sxs-lookup"><span data-stu-id="945cf-142">The key pair name for this article.</span></span>  <span data-ttu-id="945cf-143">Anahtar çiftine **id_rsa** adı verilmesi varsayılandır ve bazı araçlar **id_rsa** özel anahtar adı bekleyebilir, bu nedenle bir tane olması iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="945cf-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="945cf-144">`~/.ssh/` dizini, SSH anahtar çiftleri ve SSH yapılandırma dosyası için varsayılan konumdur.</span><span class="sxs-lookup"><span data-stu-id="945cf-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="945cf-145">Tam yol belirtilmezse `ssh-keygen` tarafından oluşturulan anahtarlar varsayılan `~/.ssh` dizininde değil geçerli çalışma dizininde olur.</span><span class="sxs-lookup"><span data-stu-id="945cf-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="945cf-146">`~/.ssh` dizininin listesi.</span><span class="sxs-lookup"><span data-stu-id="945cf-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="945cf-147">Anahtar Parolası:</span><span class="sxs-lookup"><span data-stu-id="945cf-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="945cf-148">`ssh-keygen`, özel anahtar dosyasının "parolasını" ifade eder.</span><span class="sxs-lookup"><span data-stu-id="945cf-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="945cf-149">Özel anahtarınıza bir parola eklemeniz *önemle* önerilir.</span><span class="sxs-lookup"><span data-stu-id="945cf-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="945cf-150">Anahtar dosyasını koruyan bir parola olmadığında, dosyaya sahip herkes bunu ilgili ortak anahtara sahip herhangi bir sunucuda oturum açmak için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="945cf-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="945cf-151">Bir parola eklemek, birinin özel anahtar dosyanıza erişim sağlama ihtimaline karşı, kimliğinizi doğrulamak için kullanılan anahtarları değiştirmeniz için size zaman tanıyarak daha fazla koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="945cf-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="945cf-152">Özel anahtar parolanızı depolamak için ssh-agent kullanma</span><span class="sxs-lookup"><span data-stu-id="945cf-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="945cf-153">Her SSH oturum açma işleminde özel anahtar dosya parolanızı yazmamak için `ssh-agent` kullanarak özel anahtar dosya parolanızı önbelleğe alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="945cf-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="945cf-154">Mac kullanıyorsanız `ssh-agent` öğesini çağırdığınızda OSX Anahtar Zinciri, özel anahtar parolalarını güvenli bir şekilde depolar.</span><span class="sxs-lookup"><span data-stu-id="945cf-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="945cf-155">SSH sistemini anahtar dosyaları hakkında bilgilendirerek parola kullanma gereksinimini ortadan kaldırmak için ssh-agent ve ssh-add bilgilerini doğrulayıp kullanın.</span><span class="sxs-lookup"><span data-stu-id="945cf-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="945cf-156">Şimdi `ssh-add` komutunu kullanarak özel anahtarı `ssh-agent` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="945cf-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="945cf-157">Özel anahtar parolası artık `ssh-agent` içinde depolanmış olur.</span><span class="sxs-lookup"><span data-stu-id="945cf-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="945cf-158">`ssh-copy-id` kullanarak anahtarı mevcut bir VM’ye kopyalama</span><span class="sxs-lookup"><span data-stu-id="945cf-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="945cf-159">Önceden bir VM oluşturduysanız şu komutu kullanarak Linux VM'nize yeni SSH ortak anahtarını yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="945cf-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="945cf-160">SSH yapılandırma dosyası oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="945cf-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="945cf-161">Oturum açma işlemlerini hızlandırmak ve SSH istemci davranışınızı iyileştirmek için en iyi uygulama olarak bir `~/.ssh/config` dosyası oluşturmanız ve yapılandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="945cf-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="945cf-162">Aşağıdaki örnek, standart bir yapılandırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="945cf-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="945cf-163">Önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="945cf-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="945cf-164">Yeni SSH yapılandırması eklemek için dosyayı düzenleme:</span><span class="sxs-lookup"><span data-stu-id="945cf-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="945cf-165">Örnek `~/.ssh/config` dosyası:</span><span class="sxs-lookup"><span data-stu-id="945cf-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="945cf-166">Bu SSH yapılandırması, size her sunucu için bölümler sunarak her birinin kendi özel anahtar çiftinin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="945cf-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="945cf-167">Varsayılan ayarlar (`Host *`), üst düzey yapılandırma dosyasındaki belirli ana bilgisayarların hiçbiriyle eşleşmeyen tüm ana bilgisayarlar içindir.</span><span class="sxs-lookup"><span data-stu-id="945cf-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="945cf-168">Yapılandırma dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="945cf-168">Config file explained</span></span>

<span data-ttu-id="945cf-169">`Host` = terminal üzerinde çağrılan ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="945cf-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="945cf-170">`ssh fedora22`, `SSH`'ye `Host fedora22` etiketli ayarlar bloğundaki değerlerin kullanılması gerektiğini bildirir. NOT: Konak, kullanımınız için mantıklı olan ve bir sunucunun gerçek konak adını temsil etmeyen herhangi bir etiket olabilir.</span><span class="sxs-lookup"><span data-stu-id="945cf-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="945cf-171">`Hostname 102.160.203.241` = erişim sağlanan sunucuya ilişkin IP adresi veya DNS adı.</span><span class="sxs-lookup"><span data-stu-id="945cf-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="945cf-172">`User ahmet` = sunucuda oturum açarken kullanılacak uzak kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="945cf-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="945cf-173">`PubKeyAuthentication yes`= SSH’ye, oturum açmak için bir SSH anahtarı kullanmak istediğinizi iletir.</span><span class="sxs-lookup"><span data-stu-id="945cf-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="945cf-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`, = kimlik doğrulaması için kullanılacak SSH özel anahtarı ve ilgili ortak anahtar.</span><span class="sxs-lookup"><span data-stu-id="945cf-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="945cf-175">Parolasız Linux içine SSH</span><span class="sxs-lookup"><span data-stu-id="945cf-175">SSH into Linux without a password</span></span>

<span data-ttu-id="945cf-176">Artık bir SSH anahtar çiftiniz ve yapılandırılmış bir SSH yapılandırma dosyasına sahip olduğunuza göre Linux VM'nizde hızlı ve güvenli şekilde oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="945cf-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="945cf-177">SSH anahtarı kullanarak bir sunucuda ilk oturum açışınızda, komut sizden bu anahtar dosyasına ilişkin parolayı ister.</span><span class="sxs-lookup"><span data-stu-id="945cf-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="945cf-178">Komut açıklaması</span><span class="sxs-lookup"><span data-stu-id="945cf-178">Command explained</span></span>

<span data-ttu-id="945cf-179">`ssh fedora22` yürütüldüğünde, SSH önce `Host fedora22` bloğundaki tüm ayarları bulur ve yükler ve sonra son blok olan `Host *` içindeki kalan tüm ayarları yükler.</span><span class="sxs-lookup"><span data-stu-id="945cf-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="945cf-180">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="945cf-180">Next Steps</span></span>

<span data-ttu-id="945cf-181">Sonraki adım, yeni SSH ortak anahtarını kullanarak Azure Linux VM’ler oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="945cf-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="945cf-182">Oturum açma işlemi için SSH ortak anahtarıyla oluşturulan Azure VM'ler, varsayılan oturum açma yöntemiyle (parolalar) oluşturulan VM'lere göre daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="945cf-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="945cf-183">SSH anahtarları kullanılarak oluşturulan Azure VM'ler, varsayılan olarak parola kullanımı devre dışı bırakılmış şekilde yapılandırılır; böylece parola tahminiyle gerçekleştirilen saldırı girişimleri önlenir.</span><span class="sxs-lookup"><span data-stu-id="945cf-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="945cf-184">Azure şablonu kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="945cf-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="945cf-185">Azure portalını kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="945cf-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="945cf-186">Azure CLI kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="945cf-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
