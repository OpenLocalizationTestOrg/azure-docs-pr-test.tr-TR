---
title: "aaaMove tooand SCP ile Azure Linux Vm'lerden gelen dosyaları | Microsoft Docs"
description: "Güvenli bir şekilde dosyaları tooand SCP ve SSH anahtar çifti kullanarak azure'da bir Linux VM taşıyın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="c1c24-103">SCP'yi kullanarak bir Linux VM dosyaları tooand Taşı</span><span class="sxs-lookup"><span data-stu-id="c1c24-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="c1c24-104">Bu makalede nasıl toomove tooan Azure Linux VM'de istasyonunuzu veya bir Azure güvenli kopyalama (SCP) kullanarak Linux VM tooyour iş istasyonunda, aşağı dosyaları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="c1c24-105">Hızlı ve güvenli bir şekilde, dosyalar, iş istasyonu ve bir Linux VM arasında taşıma Azure altyapınıza yönetmek için kritik öneme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="c1c24-106">Bu makalede, bir Linux VM Azure kullanılarak dağıtılan gereksinim [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1c24-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c1c24-107">Ayrıca, yerel bilgisayarınızda bir SCP istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="c1c24-108">SSH üzerinde oluşturulmuş ve hello varsayılan Bash kabuğunda çoğu Linux ve Mac bilgisayarların ve bazı Windows Kabukları dahil.</span><span class="sxs-lookup"><span data-stu-id="c1c24-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c1c24-109">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="c1c24-109">Quick commands</span></span>

<span data-ttu-id="c1c24-110">Bir Linux VM toohello dosyasını kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c1c24-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="c1c24-111">Linux VM hello aşağı dosya kopyalama</span><span class="sxs-lookup"><span data-stu-id="c1c24-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c1c24-112">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="c1c24-112">Detailed walkthrough</span></span>

<span data-ttu-id="c1c24-113">Örnekler, biz Azure yapılandırma dosyası tooa Linux VM Yukarı Taşı ve bir günlük dosyası dizini, çekme her ikisi de SCP ve SSH anahtarları kullanma.</span><span class="sxs-lookup"><span data-stu-id="c1c24-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="c1c24-114">SSH anahtar çifti kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c1c24-114">SSH key pair authentication</span></span>

<span data-ttu-id="c1c24-115">SCP SSH hello Aktarım katmanı için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1c24-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="c1c24-116">SSH tanıtıcıları hello hello hedef ana bilgisayarda kimlik doğrulaması ve varsayılan olarak SSH ile sağlanan şifrelenmiş tüneli hello dosyasında taşır.</span><span class="sxs-lookup"><span data-stu-id="c1c24-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="c1c24-117">SSH kimlik doğrulaması için kullanıcı adları ve parolalar kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="c1c24-118">Ancak, SSH ortak ve özel anahtar kimlik doğrulaması güvenlik açısından en iyisi önerilir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="c1c24-119">SSH hello bağlantı doğrulaması sonra SCP hello dosya kopyalama sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="c1c24-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="c1c24-120">Düzgün şekilde yapılandırılmış kullanarak `~/.ssh/config` ve yalnızca bir sunucu adı (veya IP adresi) kullanarak SSH ortak ve özel anahtarlar, hello SCP bağlantı kurulabileceği.</span><span class="sxs-lookup"><span data-stu-id="c1c24-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="c1c24-121">Yalnızca bir SSH anahtarı varsa, SCP için hello görünüyor `~/.ssh/` dizini ve varsayılan toolog toohello VM içinde tarafından kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1c24-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="c1c24-122">Yapılandırma hakkında daha fazla bilgi için `~/.ssh/config` ve SSH ortak ve özel anahtarları bkz [oluşturma SSH anahtarları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1c24-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="c1c24-123">SCP dosya tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="c1c24-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="c1c24-124">Merhaba ilk örnek için kullanılan toodeploy Otomasyon olan bir Linux VM tooa bir Azure yapılandırma dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c1c24-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="c1c24-125">Bu dosya gizli kod dizeleri içerir, Azure API kimlik bilgilerini içerdiğinden güvenlik önemlidir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="c1c24-126">SSH tarafından sağlanan hello şifrelenmiş tünel hello hello dosyasının içeriğini korur.</span><span class="sxs-lookup"><span data-stu-id="c1c24-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="c1c24-127">komut kopyaları hello yerel Hello *.azure/config* tooan Azure VM FQDN ile dosya *myserver.eastus.cloudapp.azure.com*. hello yönetici kullanıcı adı'hello Azure VM üzerinde *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="c1c24-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="c1c24-128">Merhaba hedeflenen toohello dosyasıdır */home/azureuser/* dizin.</span><span class="sxs-lookup"><span data-stu-id="c1c24-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="c1c24-129">Bu komutta kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c1c24-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="c1c24-130">SCP bir dizinden bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="c1c24-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="c1c24-131">Bu örnekte, hello Linux VM tooyour iş istasyonu aşağı gelen bir dizin günlük dosyaları kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c1c24-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="c1c24-132">Bir günlük dosyası olabilir veya hassas veya gizli verileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c1c24-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="c1c24-133">Ancak, SCP'yi kullanarak hello günlük dosyalarını Merhaba içeriğine şifrelenmiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="c1c24-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="c1c24-134">SCP tootransfer hello dosyaları kullanmaktır hello en kolay yolu tooget hello günlük dizini ve tooyour iş istasyonu aşağı dosyaları da güvenli devam ederken.</span><span class="sxs-lookup"><span data-stu-id="c1c24-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="c1c24-135">Merhaba aşağıdaki komut dosyaları hello kopyalar */home/azureuser/günlükleri/* hello Azure VM toohello yerel tmp dizininde dizininde:</span><span class="sxs-lookup"><span data-stu-id="c1c24-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="c1c24-136">Merhaba `-r` CLI bayrak SCP toorecursively kopyalama hello dosyaları ve dizinleri hello komutta listelenen hello dizininin hello noktasından söyler.</span><span class="sxs-lookup"><span data-stu-id="c1c24-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="c1c24-137">Ayrıca komut satırı sözdizimi hello bildiriminin benzer tooa geldiği `cp` kopyalama komutu.</span><span class="sxs-lookup"><span data-stu-id="c1c24-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1c24-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1c24-138">Next steps</span></span>

* [<span data-ttu-id="c1c24-139">Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello</span><span class="sxs-lookup"><span data-stu-id="c1c24-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
