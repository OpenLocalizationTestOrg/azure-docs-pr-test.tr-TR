---
title: "Bir Azure Linux VM'de kimliği alma | Microsoft Docs"
description: "Alma ve Azure Linux VM benzersiz bir kimliği nasıl kullanılacağını açıklar"
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="d2a52-103">Erişme ve Azure VM benzersiz kimliği kullanma</span><span class="sxs-lookup"><span data-stu-id="d2a52-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="d2a52-104">Azure VM 128 bit tanımlayıcı kodlanmış ve tüm Azure Iaas sanal makinenin SMBIOS içinde depolanan ve şu anda platform BIOS komutları kullanarak okunabilir kimliktir.</span><span class="sxs-lookup"><span data-stu-id="d2a52-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="d2a52-105">Azure VM benzersiz kimliği salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="d2a52-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="d2a52-106">Azure VM kimliği olmaz yeniden başlatma kapatma sonrasında değiştirme (ya da planlanan planlanmamış), Başlat/Durdur ayırmayı, hizmet düzeltme veya geri yerinde.</span><span class="sxs-lookup"><span data-stu-id="d2a52-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="d2a52-107">VM bir anlık görüntüdür ve yeni bir örneğini oluşturmak için kopyalanır, ancak yeni bir Azure VM kimliği yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d2a52-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="d2a52-108">Eski varsa VM'ler oluşturulur ve bu yeni özellik (Eylül 18 2014), lütfen yeniden başlatma geri bu yana çalışan otomatik olarak Azure benzersiz almak için VM kimliği</span><span class="sxs-lookup"><span data-stu-id="d2a52-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="d2a52-109">Azure benzersiz VM Kimliğinden VM dahilinde erişmek için:</span><span class="sxs-lookup"><span data-stu-id="d2a52-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="d2a52-110">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2a52-110">Create a VM</span></span>
<span data-ttu-id="d2a52-111">Daha fazla bilgi için bkz: [bir sanal makine oluşturun](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d2a52-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="d2a52-112">VM’ye bağlanma</span><span class="sxs-lookup"><span data-stu-id="d2a52-112">Connect to the VM</span></span>
<span data-ttu-id="d2a52-113">Daha fazla bilgi için bkz: [Linux SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d2a52-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="d2a52-114">Sorgu VM benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="d2a52-114">Query VM Unique ID</span></span>
<span data-ttu-id="d2a52-115">Komutu (örneğin kullanan **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="d2a52-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="d2a52-116">Örnek beklenen sonuçları:</span><span class="sxs-lookup"><span data-stu-id="d2a52-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="d2a52-117">Büyük bit sıralama Endian nedeniyle, gerçek benzersiz VM kimliği bu durumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="d2a52-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="d2a52-118">VM Azure üzerinde çalışan veya şirket içi ve Azure Iaas dağıtımlarınızı olabilir, lisans, raporlama veya genel izleme gereksinimlerinizi yardımcı olabilecek olup azure VM benzersiz kimliği farklı senaryolarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d2a52-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="d2a52-119">Bir Azure VM yaşam döngüsü tanımlamak için uygulamalar oluşturmak ve bunları Azure üzerinde onaylıyor birçok bağımsız yazılım satıcıları gerektirebilir ve VM Azure üzerinde çalışan olmadığını bildirmek için şirket içi veya diğer bulut sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="d2a52-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="d2a52-120">Bu bir platform tanımlayıcısı örneğin yazılım düzgün şekilde lisanslandığından algılamak veya sağ platform için doğru ölçümler ayarlama konusunda yardımcı olmak ve izlemek ve bu ölçümleri diğer kullanımlar arasında ilişkilendirmek için onun kaynağına gibi herhangi bir VM veri ilişkilendirmek için Yardım yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2a52-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

