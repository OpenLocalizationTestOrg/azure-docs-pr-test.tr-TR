---
title: "bir Azure Linux VM kimliği aaaGet | Microsoft Docs"
description: "Tooget ve kullanım nasıl bir Azure Linux VM benzersiz kimliği açıklar"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="9d399-103">Erişme ve Azure VM benzersiz kimliği kullanma</span><span class="sxs-lookup"><span data-stu-id="9d399-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="9d399-104">Azure VM 128 bit tanımlayıcı kodlanmış ve tüm Azure Iaas sanal makinenin SMBIOS içinde depolanan ve şu anda platform BIOS komutları kullanarak okunabilir kimliktir.</span><span class="sxs-lookup"><span data-stu-id="9d399-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="9d399-105">Azure VM benzersiz kimliği salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="9d399-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="9d399-106">Azure VM kimliği olmaz yeniden başlatma kapatma sonrasında değiştirme (ya da planlanan planlanmamış), Başlat/Durdur ayırmayı, hizmet düzeltme veya geri yerinde.</span><span class="sxs-lookup"><span data-stu-id="9d399-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="9d399-107">Ancak, Hello VM bir anlık görüntü ve kopyalanan toocreate yeni bir örnek ise, yeni bir Azure VM kimliği yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9d399-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9d399-108">Oluşturulan eski VM'ler varsa ve bu yeni özellik (18 Eylül 2014) geri bu yana çalışan Lütfen yeniden başlatın, VM tooautomatically alma Azure benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="9d399-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="9d399-109">Azure benzersiz VM Kimliğinden tooaccess hello VM içinde:</span><span class="sxs-lookup"><span data-stu-id="9d399-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="9d399-110">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d399-110">Create a VM</span></span>
<span data-ttu-id="9d399-111">Daha fazla bilgi için bkz: [bir sanal makine oluşturun](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9d399-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="9d399-112">Toohello VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="9d399-112">Connect toohello VM</span></span>
<span data-ttu-id="9d399-113">Daha fazla bilgi için bkz: [Linux SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9d399-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="9d399-114">Sorgu VM benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="9d399-114">Query VM Unique ID</span></span>
<span data-ttu-id="9d399-115">Komutu (örneğin kullanan **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="9d399-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="9d399-116">Örnek beklenen sonuçları:</span><span class="sxs-lookup"><span data-stu-id="9d399-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="9d399-117">Sıralama tooBig Endian bit hello gerçek benzersiz VM kimliği bu durumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="9d399-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="9d399-118">Merhaba VM Azure üzerinde çalışan veya şirket içi ve Azure Iaas dağıtımlarınızı olabilir, lisans, raporlama veya genel izleme gereksinimlerinizi yardımcı olabilecek olup azure VM benzersiz kimliği farklı senaryolarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d399-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="9d399-119">Azure, şirket içi ya da diğer bulut sağlayıcıları Hello VM çalışıyorsa, uygulamaları geliştirmek ve bunları Azure üzerinde onaylıyor birçok bağımsız yazılım satıcıları tooidentify tootell ve yaşam döngüsü boyunca bir Azure VM gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="9d399-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="9d399-120">Bu platform tanımlayıcı örneğin hello yazılım düzgün şekilde lisanslandığından algılamak ya da herhangi bir VM veri tooits kaynağı hello sağ ölçümleri hello sağ platform ve tootrack ayarlama tooassist gibi toocorrelate Yardım ve Bu ölçümler arasında ilişkilendirmenize yardımcı olabilir diğer kullanır.</span><span class="sxs-lookup"><span data-stu-id="9d399-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

