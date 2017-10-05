---
title: "Azure Iaas sanal diskler hakkında sık sorulan sorular (SSS) | Microsoft Docs"
description: "Azure Iaas sanal diskler ve (yönetilen ve yönetilmeyen) premium diskler hakkında sık sorulan sorular"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="04032-103">Azure Iaas sanal diskler ve yönetilen ve yönetilmeyen premium diskler hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="04032-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="04032-104">Bu makalede Azure yönetilen diskleri ve Azure Premium Storage hakkında sık sorulan bazı sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="04032-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="04032-105">Yönetilen Diskler</span><span class="sxs-lookup"><span data-stu-id="04032-105">Managed Disks</span></span>

<span data-ttu-id="04032-106">**Azure yönetilen diskleri nedir?**</span><span class="sxs-lookup"><span data-stu-id="04032-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="04032-107">Yönetilen diskleri depolama hesabı yönetimini işleyerek Azure Iaas VM'ler için disk yönetimi basitleştiren bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="04032-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="04032-108">Daha fazla bilgi için bkz: [yönetilen diskleri genel bakış](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04032-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="04032-109">**Standart yönetilen disk 80 GB olan varolan bir VHD'yi oluşturursanız, ne kadar bana maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="04032-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="04032-110">80 GB VHD'den oluşturulan standart yönetilen disk S10 disk olan bir sonraki kullanılabilir standart disk boyutu olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="04032-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="04032-111">S10 disk fiyatlandırma göre ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="04032-112">Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="04032-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="04032-113">**Standart yönetilen disk için herhangi bir işlem maliyetleri vardır?**</span><span class="sxs-lookup"><span data-stu-id="04032-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="04032-114">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-114">Yes.</span></span> <span data-ttu-id="04032-115">Her işlem için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-115">You're charged for each transaction.</span></span> <span data-ttu-id="04032-116">Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="04032-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="04032-117">**Standart yönetilen disk için sağlanan disk kapasitesini veya disk üzerindeki verileri gerçek boyutu için t ücretlendirilir?**</span><span class="sxs-lookup"><span data-stu-id="04032-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="04032-118">Sağlanan disk kapasitesine göre ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="04032-119">Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="04032-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="04032-120">**Nasıl yönetilen premium diskleri yönetilmeyen disklerden farklı fiyatlandırma olduğu?**</span><span class="sxs-lookup"><span data-stu-id="04032-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="04032-121">Yönetilen premium diskleri fiyatlandırma yönetilmeyen premium diskleri aynı değil.</span><span class="sxs-lookup"><span data-stu-id="04032-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="04032-122">**Depolama hesabı türünü (standart veya Premium) yönetilen disklerim değiştirebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="04032-123">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-123">Yes.</span></span> <span data-ttu-id="04032-124">Azure portalı, PowerShell veya Azure CLI kullanarak yönetilen disklerinizi depolama hesabı türünü değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="04032-125">**I kopyalayın veya böylelikle bir özel depolama hesabına yönetilen bir disk verme bir yolu var mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="04032-126">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-126">Yes.</span></span> <span data-ttu-id="04032-127">Azure portalı, PowerShell veya Azure CLI kullanarak yönetilen disklerinizi dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="04032-128">**Farklı bir abonelik ile yönetilen bir disk oluşturmak için Azure storage hesabı VHD dosyasında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="04032-129">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-129">No.</span></span>

<span data-ttu-id="04032-130">**Farklı bir bölgede yönetilen bir disk oluşturmak için Azure storage hesabı VHD dosyasında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="04032-131">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-131">No.</span></span>

<span data-ttu-id="04032-132">**Yönetilen diskler kullanan müşteriler için ölçek sınırlamalar var mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="04032-133">Yönetilen diskleri depolama hesaplarıyla ilişkili sınırları ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="04032-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="04032-134">Ancak, yönetilen disk başına abonelik sayısı 2. 000'varsayılan olarak sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="04032-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="04032-135">Bu sayıyı artırmak için destek çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-135">You can call support to increase this number.</span></span>

<span data-ttu-id="04032-136">**Yönetilen bir diskin artımlı bir anlık görüntüsünü alın?**</span><span class="sxs-lookup"><span data-stu-id="04032-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="04032-137">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-137">No.</span></span> <span data-ttu-id="04032-138">Geçerli anlık görüntü özelliği yönetilen bir disk tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04032-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="04032-139">Ancak, biz artımlı anlık görüntüleri gelecekte destekler planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="04032-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="04032-140">**Sanal makineleri bir kullanılabilirlik kümesinde yönetilen ve yönetilmeyen diskleri birleşiminden oluşabilir?**</span><span class="sxs-lookup"><span data-stu-id="04032-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="04032-141">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-141">No.</span></span> <span data-ttu-id="04032-142">Sanal makineleri bir kullanılabilirlik kümesinde, tüm yönetilen diskleri veya tüm yönetilmeyen diskler kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="04032-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="04032-143">Bir kullanılabilirlik kümesi oluşturduğunuzda, kullanmak istediğiniz disk türünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="04032-144">**Yönetilen diskleri Azure portalında varsayılan seçenektir?**</span><span class="sxs-lookup"><span data-stu-id="04032-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="04032-145">Şu anda değil ancak varsayılan gelecekte olacaktır.</span><span class="sxs-lookup"><span data-stu-id="04032-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="04032-146">**Boş bir yönetilen diski oluşturabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="04032-147">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-147">Yes.</span></span> <span data-ttu-id="04032-148">Boş bir disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-148">You can create an empty disk.</span></span> <span data-ttu-id="04032-149">Yönetilen bir disk için bir VM eklemeden VM bağımsız olarak, örneğin, oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="04032-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="04032-150">**Bir kullanılabilirlik için desteklenen hata etki alanı sayısı yönetilen diskleri kullanan ne ayarlı?**</span><span class="sxs-lookup"><span data-stu-id="04032-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="04032-151">Yönetilen diskleri kullanan kullanılabilirlik kümesi bulunduğu bağlı olarak, desteklenen hata etki alanı sayısı 2 veya 3 bölgedir.</span><span class="sxs-lookup"><span data-stu-id="04032-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="04032-152">**Nasıl Tanılama ayarlamak için standart depolama hesabı mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="04032-153">VM tanılama için özel depolama hesabı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="04032-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="04032-154">Gelecekte, tanılama yönetilen disklere de geçiş planlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="04032-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="04032-155">**Ne tür bir rol tabanlı erişim denetimi desteğini yönetilen disklerde var mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="04032-156">Diskleri desteklediği üç anahtar varsayılan rol yönetilen:</span><span class="sxs-lookup"><span data-stu-id="04032-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="04032-157">Sahibi: erişim dahil her şeyi yönetebilir</span><span class="sxs-lookup"><span data-stu-id="04032-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="04032-158">Katkıda bulunan: erişim dışında her şeyi yönetebilir</span><span class="sxs-lookup"><span data-stu-id="04032-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="04032-159">Okuyucu: her şeyi görüntüleyebilir ancak değişiklik yapamaz</span><span class="sxs-lookup"><span data-stu-id="04032-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="04032-160">**I kopyalayın veya böylelikle bir özel depolama hesabına yönetilen bir disk verme bir yolu var mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="04032-161">Yönetilen disk için bir salt okunur paylaşılan erişim imzası URI alın ve içeriği özel depolama hesabı veya şirket içi depolama birimine kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="04032-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="04032-162">**Yönetilen my disk kopyasını oluşturabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="04032-163">Müşteriler kendi yönetilen diskleri bir anlık görüntüsünü ve sonra yönetilen başka bir disk oluşturmak için anlık görüntüyü kullanın.</span><span class="sxs-lookup"><span data-stu-id="04032-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="04032-164">**Yönetilmeyen diskleri hala desteklenmektedir?**</span><span class="sxs-lookup"><span data-stu-id="04032-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="04032-165">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-165">Yes.</span></span> <span data-ttu-id="04032-166">Yönetilen ve yönetilmeyen diskleri destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="04032-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="04032-167">Yönetilen diskleri yeni iş yükleri için kullanın ve geçerli iş yüklerinizi yönetilen disklere geçirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="04032-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="04032-168">**128 GB disk oluşturun ve ardından 130 GB boyutunu artırın, ı sonraki disk boyutu (512 GB) ücretlendirilir?**</span><span class="sxs-lookup"><span data-stu-id="04032-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="04032-169">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-169">Yes.</span></span>

<span data-ttu-id="04032-170">**Yerel olarak yedekli depolama, coğrafi olarak yedekli depolama, oluşturabiliyorum ve bölge olarak yedekli depolama yönetilen disklerde?**</span><span class="sxs-lookup"><span data-stu-id="04032-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="04032-171">Azure yönetilen diskleri şu anda yönetilen yalnızca yerel olarak yedekli depolama disklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="04032-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="04032-172">**Daraltma veya miyim yönetilen disklerim downsize?**</span><span class="sxs-lookup"><span data-stu-id="04032-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="04032-173">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-173">No.</span></span> <span data-ttu-id="04032-174">Bu özellik şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="04032-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="04032-175">**Bilgisayar adı özelliği değiştirmek bir özel (Sistem Hazırlama aracı kullanılarak oluşturulan veya genelleştirilmiş) işletim sistemi diski VM sağlamak için kullanılır?**</span><span class="sxs-lookup"><span data-stu-id="04032-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="04032-176">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-176">No.</span></span> <span data-ttu-id="04032-177">Bilgisayar adı özelliği güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="04032-177">You can't update the computer name property.</span></span> <span data-ttu-id="04032-178">Yeni VM, işletim sistemi diski oluşturmak için kullanılan VM üstten devralmaz.</span><span class="sxs-lookup"><span data-stu-id="04032-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="04032-179">**Yönetilen disklerle VM'ler oluşturmak için örnek Azure Resource Manager şablonları nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="04032-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="04032-180">Yönetilen diskleri kullanarak şablonları</span><span class="sxs-lookup"><span data-stu-id="04032-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="04032-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="04032-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="04032-182">Diskler ve depolama hizmeti şifrelemesi yönetilen</span><span class="sxs-lookup"><span data-stu-id="04032-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="04032-183">**Azure depolama hizmeti şifrelemesi, yönetilen bir disk oluşturduğunuzda, varsayılan olarak etkindir?**</span><span class="sxs-lookup"><span data-stu-id="04032-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="04032-184">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-184">Yes.</span></span>

<span data-ttu-id="04032-185">**Şifreleme anahtarları yöneten?**</span><span class="sxs-lookup"><span data-stu-id="04032-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="04032-186">Microsoft şifreleme anahtarları yönetir.</span><span class="sxs-lookup"><span data-stu-id="04032-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="04032-187">**I depolama hizmeti şifrelemesi yönetilen disklerim için devre dışı bırakabilirim?**</span><span class="sxs-lookup"><span data-stu-id="04032-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="04032-188">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-188">No.</span></span>

<span data-ttu-id="04032-189">**Depolama hizmeti şifrelemesi, yalnızca belirli bölgelerde kullanılabilir?**</span><span class="sxs-lookup"><span data-stu-id="04032-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="04032-190">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-190">No.</span></span> <span data-ttu-id="04032-191">Tarafından yönetilen diskleri kullanılabilir olduğu tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="04032-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="04032-192">Yönetilen diskleri kullanılabilir tüm genel bölgeler ve Almanya.</span><span class="sxs-lookup"><span data-stu-id="04032-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="04032-193">**Nasıl ı yönetilen my disk şifrelenir öğrenebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="04032-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="04032-194">Yönetilen bir disk Azure portalı, Azure CLI ve PowerShell oluşturulduğu zaman bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="04032-195">Saat 9 Haziran 2017 sonra ise, disk şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="04032-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="04032-196">**10 Haziran 2017 önce oluşturulan mevcut disklerim nasıl şifreleyebilir mi?**</span><span class="sxs-lookup"><span data-stu-id="04032-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="04032-197">10 Haziran 2017 sürümünden itibaren varolan yönetilen diske yazılan yeni veriler otomatik olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="04032-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="04032-198">Biz de var olan verileri şifrelemek planladığınıza ve şifreleme zaman uyumsuz olarak arka planda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="04032-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="04032-199">Var olan verileri artık şifrelemeniz gerekir, diskinizin bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04032-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="04032-200">Yeni disk şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="04032-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="04032-201">Azure CLI kullanarak yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="04032-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="04032-202">PowerShell kullanarak yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="04032-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="04032-203">**Yönetilen anlık görüntüler ve şifrelenmiş görüntüleri misiniz?**</span><span class="sxs-lookup"><span data-stu-id="04032-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="04032-204">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-204">Yes.</span></span> <span data-ttu-id="04032-205">Yönetilen tüm anlık görüntüler ve 9 Haziran 2017 sonra oluşturulan görüntüleri otomatik olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="04032-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="04032-206">**Sanal makineleri veya yönetilen diskleri daha önce şifrelenmiş depolama hesaplarında yer alan yönetilmeyen disklerle dönüştürebilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="04032-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="04032-207">Evet</span><span class="sxs-lookup"><span data-stu-id="04032-207">Yes</span></span>

<span data-ttu-id="04032-208">**Yönetilen bir disk veya bir anlık görüntü dışarı aktarılan bir VHD'den de şifrelenir mi?**</span><span class="sxs-lookup"><span data-stu-id="04032-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="04032-209">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-209">No.</span></span> <span data-ttu-id="04032-210">Ancak, bir VHD şifrelenmiş depolama hesabı için bir şifrelenmiş dışa varsa disk veya anlık görüntü yönetilen sonra şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="04032-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="04032-211">Premium diskler: yönetilen ve yönetilmeyen</span><span class="sxs-lookup"><span data-stu-id="04032-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="04032-212">**VM bir DSv2 gibi Premium Storage destekleyen bir boyutu serisi kullanıyorsa ı premium ve standart veri diskleri ekleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="04032-213">Evet.</span><span class="sxs-lookup"><span data-stu-id="04032-213">Yes.</span></span>

<span data-ttu-id="04032-214">**I premium ve standart veri diskleri Premium depolama D, Dv2, G veya F serisi gibi desteklemiyor boyutu seriye ekleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="04032-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="04032-215">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-215">No.</span></span> <span data-ttu-id="04032-216">Premium Storage destekleyen bir boyutu serisi kullanmayan sanal makineleri yalnızca standart veri diskleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="04032-217">**80 GB varolan bir VHD'den premium veri diski oluşturursanız, ne kadar maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="04032-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="04032-218">80 GB VHD'den oluşturulan bir premium veri diski P10 disk sonraki kullanılabilir premium disk boyutu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="04032-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="04032-219">P10 disk fiyatlandırma göre ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="04032-220">**Premium depolama kullanmak için işlem maliyetleri vardır?**</span><span class="sxs-lookup"><span data-stu-id="04032-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="04032-221">IOPS ve üretilen iş ile belirli sınırları sağlanan gelen her disk boyutu için sabit bir maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="04032-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="04032-222">Diğer maliyetlerin giden bant genişliği ve anlık görüntü kapasite varsa ' dir.</span><span class="sxs-lookup"><span data-stu-id="04032-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="04032-223">Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="04032-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="04032-224">**IOPS ve disk önbellekten elde edebilirsiniz işleme sınırları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="04032-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="04032-225">Önbellek için birleşik sınırları ve DS serisi için yerel SSD çekirdek başına 4.000 IOPS ve çekirdek saniyede 33 MB kümesidir.</span><span class="sxs-lookup"><span data-stu-id="04032-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="04032-226">GS serisi çekirdek başına 5.000 IOPS'yi ve çekirdek saniyede 50 MB sunar.</span><span class="sxs-lookup"><span data-stu-id="04032-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="04032-227">**Yerel SSD yönetilen diskleri VM için destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="04032-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="04032-228">Yerel SSD yönetilen diskleri VM ile birlikte sağlanan geçici depolama ' dir.</span><span class="sxs-lookup"><span data-stu-id="04032-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="04032-229">Var. ek bu geçici depolama için bir maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="04032-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="04032-230">Azure Blob depolama alanına kalıcı değildir çünkü, uygulama verilerini depolamak için bu yerel SSD kullanmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="04032-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="04032-231">**Premium disklerde KIRPMA kullanılmak herhangi varsa var mı?**</span><span class="sxs-lookup"><span data-stu-id="04032-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="04032-232">KIRPMA kullanın ya da premium Azure disklerde veya standart diskler üzerinde hiçbir dezavantajı yoktur.</span><span class="sxs-lookup"><span data-stu-id="04032-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="04032-233">Yeni disk boyutları: yönetilen ve yönetilmeyen</span><span class="sxs-lookup"><span data-stu-id="04032-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="04032-234">**İşletim sistemi ve veri diskleri için desteklenen en büyük disk boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="04032-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="04032-235">Bir işletim sistemi diski için Azure destekleyen bölüm ana önyükleme kaydı (MBR) türüdür.</span><span class="sxs-lookup"><span data-stu-id="04032-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="04032-236">MBR biçimini destekleyen bir diski 2 TB boyut.</span><span class="sxs-lookup"><span data-stu-id="04032-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="04032-237">Bir işletim sistemi diski için Azure desteklediği en büyük boyutu 2 TB'tır.</span><span class="sxs-lookup"><span data-stu-id="04032-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="04032-238">Azure veri diskleri için en fazla 4 TB destekler.</span><span class="sxs-lookup"><span data-stu-id="04032-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="04032-239">**Desteklenen en büyük sayfa blob boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="04032-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="04032-240">Azure desteklediği en büyük sayfa blob boyutu 8 TB (8191 GB) ' dir.</span><span class="sxs-lookup"><span data-stu-id="04032-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="04032-241">Sayfa bloblarını 4 TB veri veya işletim sistemi disklerinde olarak bir VM'ye bağlı (4.095 GB) büyük desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="04032-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="04032-242">**Azure Araçları'nın yeni bir sürüm oluşturma, ekleme, yeniden boyutlandırma ve 1 TB'den büyük olan diskler karşıya yükleme için kullanılacak gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="04032-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="04032-243">Oluşturma, ekleme veya 1 TB'den büyük diskleri yeniden boyutlandırmak için varolan Azure Araçları yükseltmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="04032-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="04032-244">VHD dosyasına şirket içi doğrudan Azure sayfa blobu veya yönetilmeyen disk olarak karşıya yükleme için en son aracı kümeleri kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="04032-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="04032-245">Azure Araçları</span><span class="sxs-lookup"><span data-stu-id="04032-245">Azure tools</span></span>      | <span data-ttu-id="04032-246">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="04032-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="04032-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="04032-247">Azure PowerShell</span></span> | <span data-ttu-id="04032-248">Sürüm numarası 4.1.0'da: Haziran 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="04032-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="04032-249">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="04032-249">Azure CLI v1</span></span>     | <span data-ttu-id="04032-250">Sürüm numarası 0.10.13: May 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="04032-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="04032-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="04032-251">AzCopy</span></span>           | <span data-ttu-id="04032-252">Sürüm numarası 6.1.0: Haziran 2017 sürüm veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="04032-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="04032-253">Azure CLI v2 ve Azure Storage Gezgini desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="04032-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="04032-254">**P4 ve P6 disk boyutları yönetilmeyen diskleri veya sayfa BLOB'ları için destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="04032-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="04032-255">Hayır.</span><span class="sxs-lookup"><span data-stu-id="04032-255">No.</span></span> <span data-ttu-id="04032-256">P4 (32 GB) ve P6 (64 GB) disk boyutları, yalnızca yönetilen diskler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="04032-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="04032-257">Yönetilmeyen diskleri ve sayfa bloblarını desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="04032-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="04032-258">**Nasıl yönetilen my varolan premium (15 Haziran 2017) küçük bir disk etkinleştirilmeden önce 64 GB oluşturulduğu daha az disk varsa, onu faturalandırılır?**</span><span class="sxs-lookup"><span data-stu-id="04032-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="04032-259">Var olan küçük premium göre P10 fiyatlandırma katmanı faturalandırılmaya devam 64 GB daha az diskler.</span><span class="sxs-lookup"><span data-stu-id="04032-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="04032-260">**64 GB P10 ile P4 veya P6 değerinden küçük premium diskler, disk katmanı nasıl geçiş yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="04032-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="04032-261">Küçük disklerinizi bir anlık görüntüsünü ve fiyatlandırma katmanı P4 veya P6 sağlanan boyutuna göre otomatik olarak geçiş yapmak için bir diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04032-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="04032-262">Ne sorumun cevabı burada cevaplanıp değil mi?</span><span class="sxs-lookup"><span data-stu-id="04032-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="04032-263">Sorunuzun yanıtını burada listelenmiyorsa, bize bildirin ve yanıt bulmanıza yardımcı olacağız.</span><span class="sxs-lookup"><span data-stu-id="04032-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="04032-264">Bir soru bu makalenin sonunda yer alan yorumlara nakledebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04032-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="04032-265">Azure depolama ekibi ve diğer topluluk üyeleri bu makale hakkında ile etkileşim için MSDN kullanın [Azure depolama Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="04032-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="04032-266">Özellik isteğinde, istekleri ve için fikirleri göndermek için [Azure Storage geri bildirim Forumunda](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="04032-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
