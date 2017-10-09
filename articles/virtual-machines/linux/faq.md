---
title: "Linux VM'ler için Azure'da sorular aaaFrequently | Microsoft Docs"
description: "Merhaba hello Resource Manager modeli ile oluşturulan Linux sanal makineleri hakkında sık sorulan sorular, yanıtlar toosome sağlar."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="96832-103">Linux sanal makineleri hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="96832-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="96832-104">Bu makalede, Azure'da hello Resource Manager dağıtım modeli kullanarak oluşturulan Linux sanal makineleri hakkında bazı sık sorulan soruları giderir.</span><span class="sxs-lookup"><span data-stu-id="96832-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="96832-105">Merhaba Windows sürümü bu konu için bkz: [Windows sanal makineler hakkında sık sorulan bir soru](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="96832-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="96832-106">Azure sanal makinesinde ne çalıştırabilirim?</span><span class="sxs-lookup"><span data-stu-id="96832-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="96832-107">Tüm aboneler bir Azure sanal makinesinde sunucu yazılımı çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="96832-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="96832-108">Daha fazla bilgi için bkz: [Azure-Endorsed dağıtımları Linux'ta](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="96832-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="96832-109">Bir sanal makineyle birlikte ne kadar depolama alanı kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="96832-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="96832-110">Her veri diski too1 TB olabilir.</span><span class="sxs-lookup"><span data-stu-id="96832-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="96832-111">Merhaba kullanabileceğiniz veri diski sayısı hello hello sanal makine boyutuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="96832-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="96832-112">Ayrıntılar için bkz. [Virtual Machines boyutları](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96832-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="96832-113">Bir Azure depolama hesabı hello işletim sistemi diski ve veri diskleri için depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="96832-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="96832-114">Her disk bir sayfa blobu olarak depolanan bir .vhd dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="96832-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="96832-115">Fiyatlandırma ayrıntıları için bkz. [Depolama Fiyatlandırma Ayrıntıları](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="96832-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="96832-116">Sanal Makinem nasıl erişebilir mi?</span><span class="sxs-lookup"><span data-stu-id="96832-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="96832-117">Uzak bağlantı toolog güvenli Kabuk (SSH) kullanarak toohello sanal makinedeki kurun.</span><span class="sxs-lookup"><span data-stu-id="96832-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="96832-118">Merhaba yönergeleri hakkında bkz tooconnect [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [Linux ve Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96832-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="96832-119">Varsayılan olarak, SSH en fazla 10 eş zamanlı bağlantıya izin verir.</span><span class="sxs-lookup"><span data-stu-id="96832-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="96832-120">Merhaba yapılandırma dosyasını düzenleyerek bu sayıyı artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96832-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="96832-121">Sorun yaşıyorsanız, kullanıma [sorun giderme güvenli Kabuk (SSH) bağlantı](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96832-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="96832-122">Merhaba geçici disk (/ dev/sdb1) toostore verileri kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="96832-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="96832-123">Merhaba geçici disk (/ dev/sdb1) toostore veri kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="96832-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="96832-124">Yalnızca geçici depolama için yoktur.</span><span class="sxs-lookup"><span data-stu-id="96832-124">It is only there for temporary storage.</span></span> <span data-ttu-id="96832-125">Kurtarılamaz veri kaybı riski oluşur.</span><span class="sxs-lookup"><span data-stu-id="96832-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="96832-126">I kopyalayabilir veya mevcut bir Azure VM'yi kopyalama?</span><span class="sxs-lookup"><span data-stu-id="96832-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="96832-127">Evet.</span><span class="sxs-lookup"><span data-stu-id="96832-127">Yes.</span></span> <span data-ttu-id="96832-128">Yönergeler için bkz: [nasıl toocreate bir bir Linux sanal makine kopyasını hello Resource Manager dağıtım modeli](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96832-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="96832-129">Neden Kanada merkezi ve Doğu Kanada bölgeler arasında Azure Resource Manager görüyorum değil mi?</span><span class="sxs-lookup"><span data-stu-id="96832-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="96832-130">Merhaba iki yeni bölgeler Kanada merkezi ve Doğu Kanada otomatik olarak mevcut Azure abonelikleri için sanal makine oluşturmak için kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="96832-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="96832-131">Bu kayıt aracılığıyla bir sanal makine dağıtıldığında otomatik olarak yapılır Azure portal tooany Azure Kaynak Yöneticisi'ni kullanarak diğer bölge hello.</span><span class="sxs-lookup"><span data-stu-id="96832-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="96832-132">Bir sanal makine sonra diğer Azure bölgesi dağıtılan tooany olan hello yeni bölgeler sonraki sanal makineler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96832-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="96832-133">NIC toomy VM, oluşturulduktan sonra ekleyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="96832-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="96832-134">Evet, bu artık mümkündür.</span><span class="sxs-lookup"><span data-stu-id="96832-134">Yes, this is now possible.</span></span> <span data-ttu-id="96832-135">Merhaba VM ilk gereksinimlerini toobe deallocated durduruldu.</span><span class="sxs-lookup"><span data-stu-id="96832-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="96832-136">Bir NIC ekleyip sonra (olduğu sürece son NIC hello VM üzerinde hello).</span><span class="sxs-lookup"><span data-stu-id="96832-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="96832-137">Herhangi bir bilgisayar adı gereksinimleri var mı?</span><span class="sxs-lookup"><span data-stu-id="96832-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="96832-138">Evet.</span><span class="sxs-lookup"><span data-stu-id="96832-138">Yes.</span></span> <span data-ttu-id="96832-139">Merhaba bilgisayar adı en fazla 64 karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="96832-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="96832-140">Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kaynaklarınızı adlandırma geçici daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="96832-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="96832-141">Herhangi bir kaynak grubu adı gereksinimleri var mı?</span><span class="sxs-lookup"><span data-stu-id="96832-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="96832-142">Evet.</span><span class="sxs-lookup"><span data-stu-id="96832-142">Yes.</span></span> <span data-ttu-id="96832-143">Merhaba kaynak grubu adı en fazla 90 karakter uzunluğunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="96832-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="96832-144">Bkz: [adlandırma kuralları kuralları ve sınırlamaları](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kaynak grupları hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="96832-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="96832-145">Bir VM oluşturulurken hello kullanıcıadı gereksinimleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="96832-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="96832-146">Kullanıcı adları, 1-64 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96832-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="96832-147">kullanıcı adlarını aşağıdaki hello izin verilmiyor:</span><span class="sxs-lookup"><span data-stu-id="96832-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-148">Yönetici</span><span class="sxs-lookup"><span data-stu-id="96832-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-149">Yönetici</span><span class="sxs-lookup"><span data-stu-id="96832-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-150">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="96832-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-151">Kullanıcı1</span><span class="sxs-lookup"><span data-stu-id="96832-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-152">test etme</span><span class="sxs-lookup"><span data-stu-id="96832-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-153">Kullanıcı2</span><span class="sxs-lookup"><span data-stu-id="96832-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-154">Test1</span><span class="sxs-lookup"><span data-stu-id="96832-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-155">KULLANICI3</span><span class="sxs-lookup"><span data-stu-id="96832-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-156">admin1</span><span class="sxs-lookup"><span data-stu-id="96832-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-157">1</span><span class="sxs-lookup"><span data-stu-id="96832-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-158">123</span><span class="sxs-lookup"><span data-stu-id="96832-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-159">bir</span><span class="sxs-lookup"><span data-stu-id="96832-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-160">actuser</span><span class="sxs-lookup"><span data-stu-id="96832-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="96832-161">adm</span><span class="sxs-lookup"><span data-stu-id="96832-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-162">admin2</span><span class="sxs-lookup"><span data-stu-id="96832-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-163">ASPNET</span><span class="sxs-lookup"><span data-stu-id="96832-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-164">yedekleme</span><span class="sxs-lookup"><span data-stu-id="96832-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-165">Konsol</span><span class="sxs-lookup"><span data-stu-id="96832-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-166">David</span><span class="sxs-lookup"><span data-stu-id="96832-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-167">Konuk</span><span class="sxs-lookup"><span data-stu-id="96832-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-168">John</span><span class="sxs-lookup"><span data-stu-id="96832-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-169">Sahibi</span><span class="sxs-lookup"><span data-stu-id="96832-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-170">kök</span><span class="sxs-lookup"><span data-stu-id="96832-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-171">sunucu</span><span class="sxs-lookup"><span data-stu-id="96832-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-172">SQL</span><span class="sxs-lookup"><span data-stu-id="96832-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-173">Destek</span><span class="sxs-lookup"><span data-stu-id="96832-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="96832-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-175">sys</span><span class="sxs-lookup"><span data-stu-id="96832-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="96832-176">Test2</span><span class="sxs-lookup"><span data-stu-id="96832-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-177">test3</span><span class="sxs-lookup"><span data-stu-id="96832-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-178">Kullanıcı4</span><span class="sxs-lookup"><span data-stu-id="96832-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="96832-179">user5</span><span class="sxs-lookup"><span data-stu-id="96832-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="96832-180">Bir VM oluşturulurken hello parola gereksinimleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="96832-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="96832-181">Parolalar 6 72 karakter uzunluğunda ve 3 4 karmaşıklık gereksinimlerini aşağıdaki hello dışında karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="96832-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="96832-182">Alt karakterler</span><span class="sxs-lookup"><span data-stu-id="96832-182">Have lower characters</span></span>
* <span data-ttu-id="96832-183">Üst karakter</span><span class="sxs-lookup"><span data-stu-id="96832-183">Have upper characters</span></span>
* <span data-ttu-id="96832-184">Bir rakam olması</span><span class="sxs-lookup"><span data-stu-id="96832-184">Have a digit</span></span>
* <span data-ttu-id="96832-185">(Regex eşleşen [\W_]) bir özel karakter sahip</span><span class="sxs-lookup"><span data-stu-id="96832-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="96832-186">parolaları aşağıdaki hello izin verilmiyor:</span><span class="sxs-lookup"><span data-stu-id="96832-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="96832-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="96832-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="96832-188">Pa$ $word</span><span class="sxs-lookup"><span data-stu-id="96832-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="96832-189">Parola!</span><span class="sxs-lookup"><span data-stu-id="96832-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="96832-190">Parola1</span><span class="sxs-lookup"><span data-stu-id="96832-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="96832-191">Password22</span><span class="sxs-lookup"><span data-stu-id="96832-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="96832-192">ILOVEYOU veya!</span><span class="sxs-lookup"><span data-stu-id="96832-192">iloveyou!</span></span></td>
    </tr>
</table>
