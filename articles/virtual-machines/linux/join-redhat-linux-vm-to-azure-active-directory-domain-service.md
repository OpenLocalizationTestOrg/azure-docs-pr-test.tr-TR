---
title: aaaJoin RedHat Linux VM tooan Azure Active Directory DS | Microsoft Docs
description: "Nasıl toojoin var olan bir RedHat Enterprise Linux 7 VM tooan Azure Active Directory etki alanı hizmeti."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="b6109-103">RedHat Linux VM tooan Azure Active Directory etki alanı Hizmeti'ne katılın</span><span class="sxs-lookup"><span data-stu-id="b6109-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="b6109-104">Bu makalede, etki alanı toojoin Red Hat Enterprise Linux (RHEL) 7 sanal makine tooan Azure Active Directory etki alanı Hizmetleri (AADDS) nasıl yönetileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6109-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="b6109-105">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b6109-105">hello requirements are:</span></span>

- [<span data-ttu-id="b6109-106">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="b6109-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="b6109-107">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="b6109-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="b6109-108">DC bir Azure Active Directory etki alanı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="b6109-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="b6109-109">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="b6109-109">Quick Commands</span></span>

<span data-ttu-id="b6109-110">_Tüm örnekleri kendi ayarlarınızla değiştirin._</span><span class="sxs-lookup"><span data-stu-id="b6109-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="b6109-111">Hello azure CLI tooclassic dağıtım moda geç</span><span class="sxs-lookup"><span data-stu-id="b6109-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="b6109-112">RHEL sürüm ve görüntü arayın</span><span class="sxs-lookup"><span data-stu-id="b6109-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="b6109-113">Redhat Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6109-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="b6109-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="b6109-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="b6109-115">Güncelleştirme YUM paketleri</span><span class="sxs-lookup"><span data-stu-id="b6109-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="b6109-116">Gerekli paketleri yüklemek</span><span class="sxs-lookup"><span data-stu-id="b6109-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="b6109-117">Merhaba Linux sanal makinede yüklü gerekli hello paketlerini, hello sonraki görev toojoin hello sanal makine toohello yönetilen etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="b6109-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="b6109-118">Merhaba AAD etki alanı Hizmetleri yönetilen etki Bul</span><span class="sxs-lookup"><span data-stu-id="b6109-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="b6109-119">Kerberos başlatma</span><span class="sxs-lookup"><span data-stu-id="b6109-119">Initialize kerberos</span></span>

<span data-ttu-id="b6109-120">Toohello 'AAD DC Yöneticiler' grubuna üye olduğu bir kullanıcı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b6109-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="b6109-121">Yalnızca bu kullanıcılar, bilgisayarlar toohello yönetilen etki alanına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b6109-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="b6109-122">Merhaba makine toohello etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="b6109-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="b6109-123">Merhaba makine birleştirilmiş toohello etki alanı olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b6109-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="b6109-124">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b6109-124">Next Steps</span></span>

* [<span data-ttu-id="b6109-125">Red Hat güncelleştirme altyapısı (RHUI) isteğe bağlı Red Hat Enterprise Linux VM'ler için Azure'da için</span><span class="sxs-lookup"><span data-stu-id="b6109-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b6109-126">Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="b6109-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b6109-127">Dağıtma ve Azure Resource Manager şablonları ve hello Azure CLI kullanarak sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="b6109-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
