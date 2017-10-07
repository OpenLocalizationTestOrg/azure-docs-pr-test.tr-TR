---
title: "adlandırma yönergeleri - Windows aaaAzure altyapı | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde adlandırma hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="97448-103">Adlandırma yönergeleri Windows VM'ler için azure altyapı</span><span class="sxs-lookup"><span data-stu-id="97448-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="97448-104">Bu makalede, tüm, çeşitli Azure kaynaklarını toobuild mantıksal ve kolayca tanımlanabilen bir adlandırma kurallarına tooapproach kaynakları ortamınızda çoğaltmanın nasıl ayarlanacağını anlamaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="97448-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="97448-105">Uygulama yönergeleri için adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="97448-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="97448-106">Kararları:</span><span class="sxs-lookup"><span data-stu-id="97448-106">Decisions:</span></span>

* <span data-ttu-id="97448-107">Azure kaynakları için adlandırma kuralları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="97448-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="97448-108">Görevler:</span><span class="sxs-lookup"><span data-stu-id="97448-108">Tasks:</span></span>

* <span data-ttu-id="97448-109">Merhaba affixes toouse, kaynakları toomaintain tutarlılık arasında tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="97448-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="97448-110">Depolama hesabı adları verilen bunları gereksinimini toobe genel benzersiz hello tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="97448-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="97448-111">Belge hello adlandırma kuralı toobe kullanılan ve tooall tarafların dahil edilen tooensure tutarlılık dağıtımlar arasında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97448-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="97448-112">Adlandırma kuralları</span><span class="sxs-lookup"><span data-stu-id="97448-112">Naming conventions</span></span>
<span data-ttu-id="97448-113">Herhangi bir şey Azure'da oluşturmadan önce iyi bir adlandırma kuralı yerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="97448-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="97448-114">Bir adlandırma kuralı tüm hello kaynakları kaynaklarla yönetmeyle ilgili alt hello yönetici yükünü yardımcı olan bir tahmin edilebilir ad sahip olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="97448-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="97448-115">Adlandırma kuralları belirli Azure aboneliği veya hesabı veya tüm kuruluşunuz için tanımlanan belirli bir dizi toofollow seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97448-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="97448-116">Bu bir takım Azure üzerinde bir proje üzerinde toowork gerektiğinde Azure kaynakları ile çalışırken, kuruluşların tooestablish örtük kuralları içinde kişiler için kolay olsa da, bu model iyi ölçeklenmez.</span><span class="sxs-lookup"><span data-stu-id="97448-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="97448-117">Adlandırma kuralları Önden kümesinde kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="97448-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="97448-118">Bu kurallar kümesine arasında Kes adlandırma kuralları ile ilgili bazı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="97448-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="97448-119">Affixes</span><span class="sxs-lookup"><span data-stu-id="97448-119">Affixes</span></span>
<span data-ttu-id="97448-120">Toodefine bir adlandırma kuralı Ara gibi hello eklemesi adresindeki olup bir karar gelir:</span><span class="sxs-lookup"><span data-stu-id="97448-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="97448-121">Merhaba adı (önek) Hello başlangıcı</span><span class="sxs-lookup"><span data-stu-id="97448-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="97448-122">Merhaba adının sonuna kadar hello (sonek)</span><span class="sxs-lookup"><span data-stu-id="97448-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="97448-123">Örneğin, hello kullanarak bir kaynak grubu için iki olası adları şunlardır `rg` eklemesi:</span><span class="sxs-lookup"><span data-stu-id="97448-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="97448-124">Rg WebApp (önek)</span><span class="sxs-lookup"><span data-stu-id="97448-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="97448-125">WebApp Rg (sonek)</span><span class="sxs-lookup"><span data-stu-id="97448-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="97448-126">Affixes hello belirli kaynakları tanımlayan toodifferent yönlerini başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="97448-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="97448-127">Merhaba aşağıdaki tabloda genelde kullanılan bazı örnekler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="97448-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="97448-128">En boy</span><span class="sxs-lookup"><span data-stu-id="97448-128">Aspect</span></span> | <span data-ttu-id="97448-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="97448-129">Examples</span></span> | <span data-ttu-id="97448-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="97448-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="97448-131">Ortam</span><span class="sxs-lookup"><span data-stu-id="97448-131">Environment</span></span> |<span data-ttu-id="97448-132">geliştirme, stg, üretim</span><span class="sxs-lookup"><span data-stu-id="97448-132">dev, stg, prod</span></span> |<span data-ttu-id="97448-133">Merhaba amacı ve her ortam adı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="97448-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="97448-134">Konum</span><span class="sxs-lookup"><span data-stu-id="97448-134">Location</span></span> |<span data-ttu-id="97448-135">usw (Batı ABD) kullanın (Doğu ABD 2)</span><span class="sxs-lookup"><span data-stu-id="97448-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="97448-136">Merhaba hello datacenter veya hello bölge hello kuruluşun bölgesi bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="97448-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="97448-137">Azure bileşeni, hizmet veya ürünün</span><span class="sxs-lookup"><span data-stu-id="97448-137">Azure component, service, or product</span></span> |<span data-ttu-id="97448-138">Kaynak grubu, sanal ağ için sanal ağ için rg</span><span class="sxs-lookup"><span data-stu-id="97448-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="97448-139">Kaynak için hangi hello sağlar hello ürün bağlı olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="97448-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="97448-140">Rol</span><span class="sxs-lookup"><span data-stu-id="97448-140">Role</span></span> |<span data-ttu-id="97448-141">SQL, ya, sp, IIS</span><span class="sxs-lookup"><span data-stu-id="97448-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="97448-142">Merhaba sanal makinenin Hello rolüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="97448-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="97448-143">Örnek</span><span class="sxs-lookup"><span data-stu-id="97448-143">Instance</span></span> |<span data-ttu-id="97448-144">01, 02, 03, vs.</span><span class="sxs-lookup"><span data-stu-id="97448-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="97448-145">Birden fazla örneğine sahip kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="97448-145">For resources that have more than one instance.</span></span> <span data-ttu-id="97448-146">Örneğin, web sunucuları bir bulut hizmetinde yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="97448-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="97448-147">Adlandırma kuralları oluşturulurken, bunlar açıkça hangi durumunda olduğundan emin olun kaynağının ve hangi konumda (önek vs sonek) her tür için toouse affixes.</span><span class="sxs-lookup"><span data-stu-id="97448-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="97448-148">tarihleri</span><span class="sxs-lookup"><span data-stu-id="97448-148">Dates</span></span>
<span data-ttu-id="97448-149">Genellikle, bir kaynağın hello adından oluşturma önemli toodetermine hello tarihi olur.</span><span class="sxs-lookup"><span data-stu-id="97448-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="97448-150">Merhaba YYYYAAGG tarih biçimi öneririz.</span><span class="sxs-lookup"><span data-stu-id="97448-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="97448-151">Bu biçim yalnızca hello tam tarih kaydedilir ancak aynı zamanda adları farklı yalnızca başlangıç tarihi bu iki kaynak hello sıralanmış alfabetik ve kronolojik sağlar aynı anda.</span><span class="sxs-lookup"><span data-stu-id="97448-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="97448-152">Adlandırma kaynakları</span><span class="sxs-lookup"><span data-stu-id="97448-152">Naming resources</span></span>
<span data-ttu-id="97448-153">Merhaba Adlandırma kuralında her kaynak türünü tanımlayın, nasıl tooassign tooeach kaynak, adları tanımlayan kurallar olmalıdır oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="97448-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="97448-154">Bu kurallar tooall türdeki kaynağı örneğin uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="97448-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="97448-155">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="97448-155">Subscriptions</span></span>
* <span data-ttu-id="97448-156">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="97448-156">Accounts</span></span>
* <span data-ttu-id="97448-157">Depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="97448-157">Storage accounts</span></span>
* <span data-ttu-id="97448-158">Sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="97448-158">Virtual networks</span></span>
* <span data-ttu-id="97448-159">Alt ağlar</span><span class="sxs-lookup"><span data-stu-id="97448-159">Subnets</span></span>
* <span data-ttu-id="97448-160">Kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="97448-160">Availability sets</span></span>
* <span data-ttu-id="97448-161">Kaynak grupları</span><span class="sxs-lookup"><span data-stu-id="97448-161">Resource groups</span></span>
* <span data-ttu-id="97448-162">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="97448-162">Virtual machines</span></span>
* <span data-ttu-id="97448-163">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="97448-163">Endpoints</span></span>
* <span data-ttu-id="97448-164">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="97448-164">Network security groups</span></span>
* <span data-ttu-id="97448-165">Roller</span><span class="sxs-lookup"><span data-stu-id="97448-165">Roles</span></span>

<span data-ttu-id="97448-166">başvurduğu yeterli bilgi toodetermine toowhich kaynak adı hello tooensure sağlar, açıklayıcı adlar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="97448-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="97448-167">Bilgisayar adları</span><span class="sxs-lookup"><span data-stu-id="97448-167">Computer names</span></span>
<span data-ttu-id="97448-168">Bir sanal makine (VM) oluşturduğunuzda, Microsoft Azure hello kaynak adı için kullanılan bir VM adı, too15 karakter gerektirir.</span><span class="sxs-lookup"><span data-stu-id="97448-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="97448-169">Azure kullanır hello VM yüklü hello işletim sistemi için aynı adı hello.</span><span class="sxs-lookup"><span data-stu-id="97448-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="97448-170">Ancak, bu adları değil her zaman olması hello aynı.</span><span class="sxs-lookup"><span data-stu-id="97448-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="97448-171">Bir VM zaten bir işletim sistemini içeren bir .vhd görüntü dosyasından oluşturulan durumunda, azure'da hello VM adı VM'nin işletim sisteminin bilgisayar adı hello farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="97448-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="97448-172">Bu durum, bu nedenle değil öneririz zorluk tooVM yönetim derecesini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97448-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="97448-173">Hello Azure VM kaynak hello aynı toohello işletim sistemi, VM atamak hello bilgisayar adı atayın.</span><span class="sxs-lookup"><span data-stu-id="97448-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="97448-174">Bu hello Azure VM adı olduğu hello işletim sisteminin bilgisayar adı altındaki hello aynı öneririz.</span><span class="sxs-lookup"><span data-stu-id="97448-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="97448-175">Depolama hesabı adları</span><span class="sxs-lookup"><span data-stu-id="97448-175">Storage account names</span></span>
<span data-ttu-id="97448-176">Bu bölümde çok uygulanmaz[Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)ayrı bir depolama hesabı oluşturma gibi.</span><span class="sxs-lookup"><span data-stu-id="97448-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="97448-177">Yönetilmeyen diskler için depolama hesapları adlarını yöneten özel kurallar vardır.</span><span class="sxs-lookup"><span data-stu-id="97448-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="97448-178">Yalnızca küçük harfler ve sayılar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97448-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="97448-179">Daha fazla bilgi için bkz: [depolama hesabı oluşturma](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="97448-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="97448-180">Ayrıca, core.windows.net, birlikte hello depolama hesabı adı genel olarak geçerli, benzersiz bir DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="97448-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="97448-181">Merhaba depolama hesabı mystorageaccount çağrılırsa, örneğin, hello aşağıdaki ortaya çıkan DNS adları benzersiz olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="97448-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="97448-182">mystorageaccount.BLOB.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="97448-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="97448-183">mystorageaccount.Table.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="97448-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="97448-184">mystorageaccount.Queue.Core.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="97448-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="97448-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97448-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

