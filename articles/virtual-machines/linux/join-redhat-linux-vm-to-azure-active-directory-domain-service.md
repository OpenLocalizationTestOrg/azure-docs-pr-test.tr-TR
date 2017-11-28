---
title: "Bir Azure Active Directory DS RedHat Linux VM katılma | Microsoft Docs"
description: "Bir Azure Active Directory etki alanı hizmeti için mevcut bir RedHat Enterprise Linux 7 VM'yi katılmaya nasıl."
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
ms.openlocfilehash: 2e46a0f3c9bdbe267d121b4bf62e25d5d411fcc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="join-a-redhat-linux-vm-to-an-azure-active-directory-domain-service"></a><span data-ttu-id="590de-103">Bir Azure Active Directory etki alanı hizmeti RedHat Linux VM katılma</span><span class="sxs-lookup"><span data-stu-id="590de-103">Join a RedHat Linux VM to an Azure Active Directory Domain Service</span></span>

<span data-ttu-id="590de-104">Bu makalede bir Red Hat Enterprise Linux (RHEL) 7 sanal makine bir Azure Active Directory etki alanı Hizmetleri (AADDS) yönetilen etki alanına katılma kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="590de-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="590de-105">Gereksinimler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="590de-105">The requirements are:</span></span>

- [<span data-ttu-id="590de-106">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="590de-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="590de-107">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="590de-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="590de-108">DC bir Azure Active Directory etki alanı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="590de-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="590de-109">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="590de-109">Quick Commands</span></span>

<span data-ttu-id="590de-110">_Tüm örnekleri kendi ayarlarınızla değiştirin._</span><span class="sxs-lookup"><span data-stu-id="590de-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-the-azure-cli-to-classic-deployment-mode"></a><span data-ttu-id="590de-111">Azure CLI Klasik dağıtım moduna geç</span><span class="sxs-lookup"><span data-stu-id="590de-111">Switch the azure-cli to classic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="590de-112">RHEL sürüm ve görüntü arayın</span><span class="sxs-lookup"><span data-stu-id="590de-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="590de-113">Redhat Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="590de-113">Create a Redhat Linux VM</span></span>

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

### <a name="ssh-to-the-vm"></a><span data-ttu-id="590de-114">Sanal Makineye SSH uygulama</span><span class="sxs-lookup"><span data-stu-id="590de-114">SSH to the VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="590de-115">Güncelleştirme YUM paketleri</span><span class="sxs-lookup"><span data-stu-id="590de-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="590de-116">Gerekli paketleri yüklemek</span><span class="sxs-lookup"><span data-stu-id="590de-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="590de-117">Gerekli paketleri Linux sanal makinede yüklü olan, sonraki görev sanal makineyi yönetilen etki alanına belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="590de-117">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

### <a name="discover-the-aad-domain-services-managed-domain"></a><span data-ttu-id="590de-118">AAD etki alanı Hizmetleri yönetilen etki Bul</span><span class="sxs-lookup"><span data-stu-id="590de-118">Discover the AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="590de-119">Kerberos başlatma</span><span class="sxs-lookup"><span data-stu-id="590de-119">Initialize kerberos</span></span>

<span data-ttu-id="590de-120">'AAD DC Yöneticiler' grubuna ait bir kullanıcı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="590de-120">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="590de-121">Yalnızca bu kullanıcıların bilgisayarları yönetilen etki alanına katılmasını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="590de-121">Only these users can join computers to the managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-the-machine-to-the-domain"></a><span data-ttu-id="590de-122">Makine etki alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="590de-122">Join the machine to the domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-the-machine-is-joined-to-the-domain"></a><span data-ttu-id="590de-123">Makine etki alanına katılan doğrulayın</span><span class="sxs-lookup"><span data-stu-id="590de-123">Verify the machine is joined to the domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="590de-124">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="590de-124">Next Steps</span></span>

* [<span data-ttu-id="590de-125">Red Hat güncelleştirme altyapısı (RHUI) isteğe bağlı Red Hat Enterprise Linux VM'ler için Azure'da için</span><span class="sxs-lookup"><span data-stu-id="590de-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="590de-126">Sanal makineler Azure Kaynak Yöneticisi'nde için anahtar kasasını oluşturup</span><span class="sxs-lookup"><span data-stu-id="590de-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="590de-127">Dağıtma ve Azure Resource Manager şablonları ve Azure CLI kullanarak sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="590de-127">Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
