---
title: "Adlandırma yönergeleri - Linux azure altyapı | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde adlandırma anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1b086f0972c02d569a7219820a3d596960b6014b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="58661-103">Azure altyapı Linux VM'ler için adlandırma yönergeleri</span><span class="sxs-lookup"><span data-stu-id="58661-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="58661-104">Bu makalede, ortamınızda çoğaltmanın mantıksal ve kolayca tanımlanabilen bir kaynak kümesi oluşturmak tüm çeşitli Azure kaynaklarınızı için adlandırma kurallarını yaklaşımlardan nasıl anlamaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="58661-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="58661-105">Uygulama yönergeleri için adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="58661-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="58661-106">Kararları:</span><span class="sxs-lookup"><span data-stu-id="58661-106">Decisions:</span></span>

* <span data-ttu-id="58661-107">Azure kaynakları için adlandırma kuralları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="58661-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="58661-108">Görevler:</span><span class="sxs-lookup"><span data-stu-id="58661-108">Tasks:</span></span>

* <span data-ttu-id="58661-109">Kaynaklarınız arasında tutarlılık sağlamak için kullanılacak affixes tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="58661-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="58661-110">Depolama hesabı adları bunları genel olarak benzersiz olması gereksinimini verilen tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="58661-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="58661-111">Kullanılması ve dağıtımlar arasında tutarlılık sağlamak için ilgili tüm taraflara dağıtmak için adlandırma kuralı belge.</span><span class="sxs-lookup"><span data-stu-id="58661-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="58661-112">Adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="58661-112">Naming conventions</span></span>
<span data-ttu-id="58661-113">Herhangi bir şey Azure'da oluşturmadan önce iyi bir adlandırma kuralı yerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58661-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="58661-114">Bir adlandırma kuralı tüm kaynakları yardımcı olan bu kaynakları yönetmeyle ilgili yönetim yükünü azaltmak tahmin edilebilir bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="58661-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="58661-115">Adlandırma kuralları belirli Azure aboneliği veya hesabı veya tüm kuruluşunuz için tanımlanan belirli bir kümesini izlemek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58661-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="58661-116">Azure kaynakları ile çalışırken örtük kuralları oluşturmak kuruluş içinde kişiler için kolay olsa da, birlikte Azure'da çalışan takımlar için ölçeklendirebilirsiniz olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="58661-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span></span>

<span data-ttu-id="58661-117">Adlandırma kuralları Önden kümesinde kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="58661-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="58661-118">Kuralları ayarlar için arasında Kes adlandırma kuralları ile ilgili bazı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="58661-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="58661-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="58661-119">Affixes</span></span>
<span data-ttu-id="58661-120">Bir adlandırma kuralını tanımlamak için konum olarak bir eklemesi adresindeki olup bir karardır:</span><span class="sxs-lookup"><span data-stu-id="58661-120">As you look to define a naming convention, one decision is whether the affix is at:</span></span>

* <span data-ttu-id="58661-121">(Önek) adı başlangıcı</span><span class="sxs-lookup"><span data-stu-id="58661-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="58661-122">Adının sonuna (sonek)</span><span class="sxs-lookup"><span data-stu-id="58661-122">The end of the name (suffix)</span></span>

<span data-ttu-id="58661-123">Örneğin, bir kaynak grubu kullanmak için iki olası adları şunlardır `rg` eklemesi:</span><span class="sxs-lookup"><span data-stu-id="58661-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="58661-124">Rg WebApp (önek)</span><span class="sxs-lookup"><span data-stu-id="58661-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="58661-125">WebApp Rg (sonek)</span><span class="sxs-lookup"><span data-stu-id="58661-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="58661-126">Affixes belirli kaynakları tanımlayan farklı yönleri başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="58661-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="58661-127">Aşağıdaki tabloda, genelde kullanılan bazı örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="58661-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="58661-128">En boy</span><span class="sxs-lookup"><span data-stu-id="58661-128">Aspect</span></span> | <span data-ttu-id="58661-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="58661-129">Examples</span></span> | <span data-ttu-id="58661-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="58661-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="58661-131">Ortam</span><span class="sxs-lookup"><span data-stu-id="58661-131">Environment</span></span> |<span data-ttu-id="58661-132">geliştirme, stg, üretim</span><span class="sxs-lookup"><span data-stu-id="58661-132">dev, stg, prod</span></span> |<span data-ttu-id="58661-133">Amaç ve her ortam adı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="58661-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="58661-134">Konum</span><span class="sxs-lookup"><span data-stu-id="58661-134">Location</span></span> |<span data-ttu-id="58661-135">usw (Batı ABD) kullanın (Doğu ABD 2)</span><span class="sxs-lookup"><span data-stu-id="58661-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="58661-136">Veri merkezi veya kuruluşun bölgesinin bölge bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="58661-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="58661-137">Azure bileşeni, hizmet veya ürünün</span><span class="sxs-lookup"><span data-stu-id="58661-137">Azure component, service, or product</span></span> |<span data-ttu-id="58661-138">Kaynak grubu, sanal ağ için sanal ağ için rg</span><span class="sxs-lookup"><span data-stu-id="58661-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="58661-139">Kaynak sağlayan ürün bağlı olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="58661-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="58661-140">Rol</span><span class="sxs-lookup"><span data-stu-id="58661-140">Role</span></span> |<span data-ttu-id="58661-141">DB, uygulama, web</span><span class="sxs-lookup"><span data-stu-id="58661-141">db, app, web</span></span> |<span data-ttu-id="58661-142">Sanal makine rolüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="58661-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="58661-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="58661-143">Instance</span></span> |<span data-ttu-id="58661-144">01, 02, 03, vs.</span><span class="sxs-lookup"><span data-stu-id="58661-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="58661-145">Birden fazla örneğine sahip kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="58661-145">For resources that have more than one instance.</span></span> <span data-ttu-id="58661-146">Örneğin, web sunucuları bir bulut hizmetinde yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="58661-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="58661-147">Adlandırma kuralları oluşturulurken, bunlar açık bir şekilde her tür kaynağının ve hangi konumda (önek vs sonek) kullanılmak üzere hangi affixes durum emin olun.</span><span class="sxs-lookup"><span data-stu-id="58661-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="58661-148">tarihleri</span><span class="sxs-lookup"><span data-stu-id="58661-148">Dates</span></span>
<span data-ttu-id="58661-149">Genellikle, bir kaynak adı oluşturulma tarihi belirlemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="58661-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="58661-150">YYYYAAGG tarih biçimi öneririz.</span><span class="sxs-lookup"><span data-stu-id="58661-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="58661-151">Bu biçim, yalnızca tam sağlar tarih kaydedilir, ancak ayrıca adları farklı tarih yalnızca bu iki kaynak alfabetik olarak ve tarih sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="58661-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="58661-152">Adlandırma kaynakları</span><span class="sxs-lookup"><span data-stu-id="58661-152">Naming resources</span></span>
<span data-ttu-id="58661-153">Her tür tanımlama adlandırma kuralı kaynak, hangi oluşturulan her bir kaynağın adları atama tanımlayan kurallar olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58661-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="58661-154">Bu kurallar, kaynaklar, tüm türleri için örneğin uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="58661-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="58661-155">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="58661-155">Subscriptions</span></span>
* <span data-ttu-id="58661-156">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="58661-156">Accounts</span></span>
* <span data-ttu-id="58661-157">Depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="58661-157">Storage accounts</span></span>
* <span data-ttu-id="58661-158">Sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="58661-158">Virtual networks</span></span>
* <span data-ttu-id="58661-159">Alt ağlar</span><span class="sxs-lookup"><span data-stu-id="58661-159">Subnets</span></span>
* <span data-ttu-id="58661-160">Kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="58661-160">Availability sets</span></span>
* <span data-ttu-id="58661-161">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="58661-161">Resource groups</span></span>
* <span data-ttu-id="58661-162">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="58661-162">Virtual machines</span></span>
* <span data-ttu-id="58661-163">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="58661-163">Endpoints</span></span>
* <span data-ttu-id="58661-164">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="58661-164">Network security groups</span></span>
* <span data-ttu-id="58661-165">Roller</span><span class="sxs-lookup"><span data-stu-id="58661-165">Roles</span></span>

<span data-ttu-id="58661-166">Adı emin olmak için hangi kaynağa başvuruyor, açıklayıcı adlar kullanmanız gerektiğini belirlemek için yeterli bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="58661-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="58661-167">Bilgisayar adları</span><span class="sxs-lookup"><span data-stu-id="58661-167">Computer names</span></span>
<span data-ttu-id="58661-168">Bir sanal makine (VM) oluşturduğunuzda, Azure kaynak adı için kullanılan bir VM adı en fazla 64 karakter gerektirir.</span><span class="sxs-lookup"><span data-stu-id="58661-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span></span> <span data-ttu-id="58661-169">Azure VM'de yüklü işletim sistemi için aynı adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="58661-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="58661-170">Ancak, bu adlar her zaman aynı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="58661-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="58661-171">Bir VM .vhd görüntü dosyasından bir işletim sistemini zaten içeriyor oluşturduysanız, Azure VM adı VM'ın işletim sistemi bilgisayar adından farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="58661-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="58661-172">Bu durum, bu nedenle değil öneririz VM yönetimi için Zorluk derecesini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58661-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="58661-173">Azure VM kaynak aynı adı taşıyan o VM için işletim sistemini atadığınız bilgisayar atayın.</span><span class="sxs-lookup"><span data-stu-id="58661-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="58661-174">Azure VM adını temel işletim sisteminin bilgisayar adı ile aynı olduğunu öneririz.</span><span class="sxs-lookup"><span data-stu-id="58661-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="58661-175">Depolama hesabı adları</span><span class="sxs-lookup"><span data-stu-id="58661-175">Storage account names</span></span>
<span data-ttu-id="58661-176">Bu bölümde uygulanmaz [Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)ayrı bir depolama hesabı oluşturma gibi.</span><span class="sxs-lookup"><span data-stu-id="58661-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="58661-177">Yönetilmeyen diskler için depolama hesapları adlarını yöneten özel kurallar vardır.</span><span class="sxs-lookup"><span data-stu-id="58661-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="58661-178">Yalnızca küçük harfler ve sayılar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58661-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="58661-179">Daha fazla bilgi için bkz: [depolama hesabı oluşturma](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="58661-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="58661-180">Ayrıca, depolama hesabı adıyla core.windows.net, genel olarak geçerli, benzersiz bir DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="58661-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="58661-181">Örneğin, depolama hesabı mystorageaccount çağrılırsa, aşağıdaki ortaya çıkan DNS adları benzersiz olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="58661-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="58661-182">mystorageaccount.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="58661-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="58661-183">mystorageaccount.Table.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="58661-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="58661-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="58661-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="58661-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58661-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

