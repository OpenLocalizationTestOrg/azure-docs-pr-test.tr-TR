---
title: "Azure portal kullanarak bir sanal makine ölçek kümesi aaaCreate hello | Microsoft Docs"
description: "Azure portalını kullanarak ölçek kümeleri dağıtın."
keywords: "Sanal makine ölçekleme kümeleri"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a><span data-ttu-id="dec3e-104">Nasıl bir sanal makine ölçek kümesi ile toocreate hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="dec3e-104">How toocreate a Virtual Machine Scale Set with hello Azure portal</span></span>
<span data-ttu-id="dec3e-105">Bu öğretici, ne kadar kolay toocreate bir sanal makine ölçek kümesi yalnızca birkaç dakika içinde hello Azure portal kullanarak olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="dec3e-105">This tutorial shows you how easy it is toocreate a Virtual Machine Scale Set in just a few minutes, by using hello Azure portal.</span></span> <span data-ttu-id="dec3e-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dec3e-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-hello-vm-image-from-hello-marketplace"></a><span data-ttu-id="dec3e-107">Merhaba Marketi'nden Hello VM görüntüsü seçin</span><span class="sxs-lookup"><span data-stu-id="dec3e-107">Choose hello VM image from hello marketplace</span></span>
<span data-ttu-id="dec3e-108">Merhaba Portalı'ndan bir ölçeği CentOS, CoreOS, Debian, açık Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server veya Windows Server görüntülerini ile Ayarla kolayca dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dec3e-108">From hello portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="dec3e-109">İlk olarak, toohello gidin [Azure portal](https://portal.azure.com) bir web tarayıcısında.</span><span class="sxs-lookup"><span data-stu-id="dec3e-109">First, navigate toohello [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="dec3e-110">Tıklatın `New`, arama `scale set`seçip hello `Virtual machine scale set` girişi:</span><span class="sxs-lookup"><span data-stu-id="dec3e-110">Click `New`, search for `scale set`, and then select hello `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a><span data-ttu-id="dec3e-112">Merhaba ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dec3e-112">Create hello scale set</span></span>
<span data-ttu-id="dec3e-113">Şimdi hello varsayılan ayarları kullanmak ve hızlı bir şekilde hello ölçek kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dec3e-113">Now you can use hello default settings and quickly create hello scale set.</span></span>

* <span data-ttu-id="dec3e-114">Merhaba üzerinde `Basics` dikey penceresinde hello ölçek kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-114">On hello `Basics` blade, enter a name for hello scale set.</span></span> <span data-ttu-id="dec3e-115">Bu adı hello temel haline hello hello yük dengeleyici hello ölçek kümesini önünde FQDN'sini bu nedenle hello adı benzersiz tüm Azure arasında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="dec3e-115">This name becomes hello base of hello FQDN of hello load balancer in front of hello scale set, so make sure hello name is unique across all Azure.</span></span>
* <span data-ttu-id="dec3e-116">Tercih ettiğiniz seçin, istenen işletim sistemi yazın, istediğiniz kullanıcı adınızı girin ve kimlik doğrulama türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="dec3e-117">Bir parola seçerseniz, en az 12 karakter uzunluğunda ve üç dışında hello dört aşağıdaki karmaşıklık gereksinimlerini karşılayacak olmalıdır: bir küçük harf karakter, bir büyük harf karakter, bir sayı ve bir özel karakter.</span><span class="sxs-lookup"><span data-stu-id="dec3e-117">If you choose a password, it must be at least 12 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="dec3e-118">[Kullanıcı adı ve parola gereksinimleri](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="dec3e-119">Seçerseniz `SSH public key`, emin tooonly Yapıştır ortak anahtarınızı, özel anahtarınızı değil:</span><span class="sxs-lookup"><span data-stu-id="dec3e-119">If you choose `SSH public key`, be sure tooonly paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="dec3e-121">Tooa tek yerleştirme Grup toolimit hello ölçek kümesi gibi veya birden çok yerleştirme grupları yayılacağı olup olmadığını yaptığınız seçin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-121">Choose whether you would like toolimit hello scale set tooa single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="dec3e-122">Ölçek ayarlar belirli kısıtlamalarla 100'den VM'ler Kapasite (yukarı too1, 000) için hello ölçek toospan yerleştirme grupları olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dec3e-122">Allowing hello scale set toospan placement groups allows for scale sets over 100 VMs in capacity (up too1,000) with certain limitations.</span></span> <span data-ttu-id="dec3e-123">Daha fazla bilgi için bkz: [bu belgeleri](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="dec3e-124">İstenen kaynak grubu adı ve konum girin ve ardından `OK`.</span><span class="sxs-lookup"><span data-stu-id="dec3e-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="dec3e-125">Merhaba üzerinde `Virtual machine scale set service settings` dikey: İstenen etki alanı adı etiketi (Merhaba ölçek kümesini önünde hello yük dengeleyici için FQDN hello hello tabanı) girin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-125">On hello `Virtual machine scale set service settings` blade: enter your desired domain name label (hello base of hello FQDN for hello load balancer in front of hello scale set).</span></span> <span data-ttu-id="dec3e-126">Bu etiketi tüm Azure arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dec3e-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="dec3e-127">İstenen işletim sistemi disk görüntüsü, örnek sayısı ve makine boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="dec3e-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="dec3e-128">İstenen disk türünü seçin: yönetilen veya yönetilmeyen.</span><span class="sxs-lookup"><span data-stu-id="dec3e-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="dec3e-129">Daha fazla bilgi için bkz: [bu belgeleri](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="dec3e-130">Toohave hello ölçek kümesini seçerseniz birden çok yerleştirme grupları span, yönetilen disk ölçek kümeleri toospan yerleştirme grupları için gerekli olmadığından bu seçenek kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="dec3e-130">If you chose toohave hello scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets toospan placement groups.</span></span>
* <span data-ttu-id="dec3e-131">Etkinleştirmek veya otomatik ölçeklendirme devre dışı bırakın ve etkinleştirilirse yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="dec3e-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="dec3e-133">Merhaba üzerinde `Summary` doğrulama işiniz bittiğinde, dikey tıklayın `OK` toostart hello ölçek kümesi dağıtım.</span><span class="sxs-lookup"><span data-stu-id="dec3e-133">On hello `Summary` blade, when validation is done, click `OK` toostart hello scale set deployment.</span></span>


## <a name="connect-tooa-vm-in-hello-scale-set"></a><span data-ttu-id="dec3e-134">Merhaba ölçek kümesindeki VM tooa Bağlan</span><span class="sxs-lookup"><span data-stu-id="dec3e-134">Connect tooa VM in hello scale set</span></span>
<span data-ttu-id="dec3e-135">Toolimit seçerseniz, Ölçek tooa tek yerleştirme Grup ayarlayın, ardından hello ölçek kümesini NAT kuralları yapılandırılmış toolet toohello ölçeği kolayca Ayarla bağlandığınız dağıtılan (tooconnect toohello sanal makineleri hello ölçeğinde ayarlı değil, büyük olasılıkla toocreate gerekir bir Merhaba jumpbox hello ölçek kümesi aynı sanal ağ).</span><span class="sxs-lookup"><span data-stu-id="dec3e-135">If you chose toolimit your scale set tooa single placement group, then hello scale set is deployed with NAT rules configured toolet you connect toohello scale set easily (if not, tooconnect toohello virtual machines in hello scale set, you likely need toocreate a jumpbox in hello same virtual network as hello scale set).</span></span> <span data-ttu-id="dec3e-136">toosee bunları gidin toohello `Inbound NAT Rules` hello yük dengeleyici hello ölçek kümesi için sekmesinde:</span><span class="sxs-lookup"><span data-stu-id="dec3e-136">toosee them, navigate toohello `Inbound NAT Rules` tab of hello load balancer for hello scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="dec3e-138">Bu NAT kurallarını kullanarak VM hello ölçek kümesi tooeach bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="dec3e-138">You can connect tooeach VM in hello scale set using these NAT rules.</span></span> <span data-ttu-id="dec3e-139">Gelen bağlantı noktasını 50000, NAT kuralı ise örneği için bir Windows ölçek kümesi için RDP aracılığıyla toothat makine üzerindeki bağlantı kurulamadı `<load-balancer-ip-address>:50000`.</span><span class="sxs-lookup"><span data-stu-id="dec3e-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect toothat machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="dec3e-140">Linux ölçek kümesi için hello komutunu kullanarak bağlandığınız `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span><span class="sxs-lookup"><span data-stu-id="dec3e-140">For a Linux scale set, you would connect using hello command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dec3e-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dec3e-141">Next steps</span></span>
<span data-ttu-id="dec3e-142">Nasıl toodeploy ölçek CLI hello ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-cli-quick-create.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-142">For documentation on how toodeploy scale sets from hello CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="dec3e-143">Toodeploy ölçek Powershell'den nasıl ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-windows-create.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-143">For documentation on how toodeploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="dec3e-144">Nasıl toodeploy ölçek Visual Studio'dan ayarlar ile ilgili belgeler için bkz: [bu belgeleri](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-144">For documentation on how toodeploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="dec3e-145">Merhaba genel belgelerini denetleyin [belgelerine genel bakış sayfasında ölçek kümeleri için](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dec3e-145">For general documentation, check out hello [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="dec3e-146">Genel bilgi için hello denetleyin [ölçek kümeleri için ana giriş sayfasının](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="dec3e-146">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

