---
title: "aaaCreate kullanımı bir SSH anahtar ve çifti Azure Linux VM'ler için | Microsoft Docs"
description: "Nasıl toocreate ve kullanımda bir SSH ortak ve özel anahtar çifti Linux VM'ler için Azure tooimprove hello kimlik doğrulama işlemi güvenliğini hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="49630-103">Azure Linux VM'ler için toocreate ve kullanım bir SSH ortak ve özel anahtarı nasıl eşleştirin</span><span class="sxs-lookup"><span data-stu-id="49630-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="49630-104">Güvenli Kabuk (SSH) anahtar çifti ile azure'da hello parolaları toolog gereksinimini kimlik doğrulaması için SSH anahtarları kullanan sanal makineleri (VM'ler) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49630-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="49630-105">Bu makalede nasıl tooquickly oluşturmak ve bir SSH Protokolü sürüm 2 RSA ortak ve özel anahtar dosyası çifti Linux VM'ler için kullanma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="49630-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="49630-106">Daha ayrıntılı adımları ve ek örnekler için bkz: [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="49630-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="49630-107">SSH anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="49630-107">Create an SSH key pair</span></span>
<span data-ttu-id="49630-108">Kullanım hello `ssh-keygen` komutu hello oluşturulan varsayılan toocreate SSH ortak ve özel anahtar dosyaları `~/.ssh` dizin, ancak farklı bir konum ve ek parolayı (bir parola tooaccess hello özel anahtar dosyası) belirtebilirsiniz olduğunda istenir.</span><span class="sxs-lookup"><span data-stu-id="49630-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="49630-109">Merhaba yanıtlama Bash Kabuk komut aşağıdaki hello çalıştırmak, kendi bilgilerle ister.</span><span class="sxs-lookup"><span data-stu-id="49630-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="49630-110">Merhaba SSH anahtar çiftini kullanın</span><span class="sxs-lookup"><span data-stu-id="49630-110">Use hello SSH key pair</span></span>
<span data-ttu-id="49630-111">azure'da, Linux VM Yerleştir hello ortak anahtarı olan depolanan varsayılan `~/.ssh/id_rsa.pub`, bunları oluşturduğunuzda hello konumu değiştirmediyse.</span><span class="sxs-lookup"><span data-stu-id="49630-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="49630-112">Merhaba kullanırsanız [Azure CLI 2.0](/cli/azure) toocreate, VM hello kullandığınızda bu ortak anahtar hello konumunu belirtin [az vm oluşturma](/cli/azure/vm#create) hello ile `--ssh-key-path` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="49630-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="49630-113">Hello Azure portal veya Resource Manager şablonunda hello ortak anahtar dosyası toouse hello içeriğini kopyalayıp, tüm ek boşluk kopyalama emin olun.</span><span class="sxs-lookup"><span data-stu-id="49630-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="49630-114">Örneğin, OS X kullanıyorsanız hello ortak anahtar dosyası iletebildiğiniz (varsayılan olarak, **~/.ssh/id_rsa.pub**) çok**pbcopy** toocopy hello içeriği (vardır gibiaynışeyihellodiğerLinuxprogramları`xclip`).</span><span class="sxs-lookup"><span data-stu-id="49630-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="49630-115">SSH ortak anahtarları hakkında bilgi sahibi değilseniz, aşağıdaki gibi `~/.ssh/id_rsa.pub` öğesini kendi ortak anahtar dosyası konumunuz ile değiştirip `cat` çalıştırarak ortak anahtarınızı görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49630-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="49630-116">Merhaba ortak anahtarı ile Azure VM'de VM tooyour SSH kullanarak hello IP adresi veya VM DNS adını (tooreplace unutmayın `azureuser` ve `myvm.westus.cloudapp.azure.com` aşağıda hello yönetici kullanıcı adı ve hello tam etki alanı adı--veya IP adresi):</span><span class="sxs-lookup"><span data-stu-id="49630-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="49630-117">Anahtar çifti oluştururken bir parola sağladıysanız hello oturum açma işlemi sırasında istendiğinde hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="49630-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="49630-118">(Merhaba sunucu tooyour eklenen `~/.ssh/known_hosts` klasörü ve olmaz sorulan tooconnect yeniden hello ortak anahtar kadar Azure VM değişikliklerinizi veya hello sunucu adı kaldırılır `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="49630-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="49630-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49630-119">Next steps</span></span>

<span data-ttu-id="49630-120">SSH anahtarları kullanılarak oluşturulan sanal makineleri devre dışı parolaları ile yapılandırılmış varsayılan olarak, böylelikle daha pahalı olması ve bu nedenle zor deneme yanılma yoluyla yapılan zorla toomake tahmin çalışır.</span><span class="sxs-lookup"><span data-stu-id="49630-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="49630-121">Bu konu başlığında, hızlı kullanım için basit bir SSH anahtar çifti oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="49630-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="49630-122">SSH anahtar çifti oluşturma daha fazla yardıma gereksinim veya ek sertifika gerektiren bakın [ayrıntılı adımları toocreate SSH anahtar çiftleriniz ve sertifikaları](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="49630-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="49630-123">Hello Azure portal, CLI ve şablonlar kullanarak, SSH anahtar çifti kullanan sanal makineleri oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49630-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="49630-124">Hello Azure portal kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="49630-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="49630-125">Hello Azure CLI 2.0 kullanarak güvenli bir Linux VM oluşturma)</span><span class="sxs-lookup"><span data-stu-id="49630-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="49630-126">Azure şablonu kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="49630-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
