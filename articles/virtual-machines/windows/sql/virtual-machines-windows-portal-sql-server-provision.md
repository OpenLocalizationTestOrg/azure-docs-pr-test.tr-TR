---
title: "Bir SQL Server Sanal Makine Sağlama | Microsoft Belgeleri"
description: "Portal kullanarak Azure’da bir SQL Server sanal makine oluşturun ve bağlanın Bu öğretici, Resource Manager modunu kullanır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: c923f9aae4c7a1b8bd4f5760d0ec4f33923b9321
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="a0080-104">Azure Portal’da bir SQL Server sanal makinesi sağlama</span><span class="sxs-lookup"><span data-stu-id="a0080-104">Provision a SQL Server virtual machine in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0080-105">Portal</span><span class="sxs-lookup"><span data-stu-id="a0080-105">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="a0080-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0080-106">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
> 
> 

<span data-ttu-id="a0080-107">Bu uçtan uca öğretici, SQL Server çalıştıran bir sanal makine sağlamak için Azure Portal’ın nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0080-107">This end-to-end tutorial shows you how to use the Azure portal to provision a virtual machine running SQL Server.</span></span>

<span data-ttu-id="a0080-108">Azure Virtual Machine (VM) galerisi, Microsoft SQL Server içeren birkaç görüntüyü içerir.</span><span class="sxs-lookup"><span data-stu-id="a0080-108">The Azure virtual machine (VM) gallery includes several images that contain Microsoft SQL Server.</span></span> <span data-ttu-id="a0080-109">Birkaç tıklatmayla, galerideki SQL VM görüntülerinden birini seçebilir ve bunu Azure ortamınızda sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-109">With a few clicks, you can select one of the SQL VM images from the gallery and provision it in your Azure environment.</span></span>

<span data-ttu-id="a0080-110">Bu öğreticide şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="a0080-110">In this tutorial, you will:</span></span>

* [<span data-ttu-id="a0080-111">Galeriden bir SQL VM görüntüsü seçme</span><span class="sxs-lookup"><span data-stu-id="a0080-111">Select a SQL VM image from the gallery</span></span>](#select-a-sql-vm-image-from-the-gallery)
* [<span data-ttu-id="a0080-112">VM oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-112">Configure and create the VM</span></span>](#configure-the-vm)
* [<span data-ttu-id="a0080-113">VM'yi Uzak Masaüstü ile açma</span><span class="sxs-lookup"><span data-stu-id="a0080-113">Open the VM with Remote Desktop</span></span>](#open-the-vm-with-remote-desktop)
* [<span data-ttu-id="a0080-114">SQL Server'a uzaktan bağlanma</span><span class="sxs-lookup"><span data-stu-id="a0080-114">Connect to SQL Server remotely</span></span>](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-the-gallery"></a><span data-ttu-id="a0080-115">Galeriden bir SQL VM görüntüsü seçme</span><span class="sxs-lookup"><span data-stu-id="a0080-115">Select a SQL VM image from the gallery</span></span>

1. <span data-ttu-id="a0080-116">Hesabınızı kullanarak [Azure portal](https://portal.azure.com)da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a0080-116">Log in to the [Azure portal](https://portal.azure.com) using your account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0080-117">Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="a0080-117">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

2. <span data-ttu-id="a0080-118">Azure portalda **Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-118">On the Azure portal, click **New**.</span></span> <span data-ttu-id="a0080-119">Portalda **Yeni** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a0080-119">The portal opens the **New** window.</span></span>

3. <span data-ttu-id="a0080-120">**Yeni** penceresinde **İşlem**’e ve ardından **Tümünü gör**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-120">In the **New** window, click **Compute** and then click **See all**.</span></span>

   ![Yeni İşlem penceresi](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. <span data-ttu-id="a0080-122">Arama alanına **SQL Server** yazın ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a0080-122">In the search field, type **SQL Server**, and press ENTER.</span></span>

5. <span data-ttu-id="a0080-123">Ardından **Filtre** simgesine tıklayın ve yayımcı olarak **Microsoft**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-123">Then click the **Filter** icon and select **Microsoft** for the publisher.</span></span> <span data-ttu-id="a0080-124">Sonuçlarda Microsoft tarafından yayımlanan SQL Server görüntülerini filtrelemek için filtre penceresinde **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-124">Click **Done** on the filter window to filter the results to Microsoft published SQL Server images.</span></span>

   ![Azure Sanal Makineleri penceresi](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. <span data-ttu-id="a0080-126">Kullanılabilir SQL Server görüntülerini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a0080-126">Review the available SQL Server images.</span></span> <span data-ttu-id="a0080-127">Her görüntü bir SQL Server sürümü ve işletim sistemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a0080-127">Each image identifies a SQL Server version and an operating system.</span></span>

6. <span data-ttu-id="a0080-128">**Ücretsiz Lisans: Windows Server 2016 üzerinde SQL Server 2016 SP1 Developer** görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-128">Select the image named **Free License: SQL Server 2016 SP1 Developer on Windows Server 2016**.</span></span>

   > [!TIP]
   > <span data-ttu-id="a0080-129">Geliştirme testi amacıyla kullanım için ücretsiz olan tam özellikli SQL Server sürümü olduğundan bu öğreticide Developer sürümü kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a0080-129">The Developer edition is used in this tutorial because it is a full-featured edition of SQL Server that is free for development testing purposes.</span></span> <span data-ttu-id="a0080-130">Yalnızca çalışan VM'ler için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-130">You pay only for the cost of running the VM.</span></span> <span data-ttu-id="a0080-131">Ancak, bu öğreticide kullanmak üzere istediğiniz görüntüyü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-131">However, you are free to choose any of the images to use in this tutorial.</span></span>

   > [!TIP]
   > <span data-ttu-id="a0080-132">SQL VM görüntüleri, oluşturduğunuz VM'nin dakika başına fiyatlandırmasına SQL Server lisans maliyetlerini ekler (Developer ve Express sürümleri hariç).</span><span class="sxs-lookup"><span data-stu-id="a0080-132">SQL VM images include the licensing costs for SQL Server into the per-minute pricing of the VM you create (except for the Developer and Express editions).</span></span> <span data-ttu-id="a0080-133">SQL Server Developer geliştirme/test için (üretim için değil), SQL Express ise hafif iş yükleri (1 GB bellek ve 10 GB depolama alanı sınırının altı) için ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="a0080-133">SQL Server Developer is free for development/testing (not production) and SQL Express is free for lightweight workloads (less than 1GB memory, less than 10 GB storage).</span></span> <span data-ttu-id="a0080-134">Diğer seçenek ise kendi lisansınızı getirmeniz (KLG) ve böylece yalnızca sanal makine için ödeme yapmanızdır.</span><span class="sxs-lookup"><span data-stu-id="a0080-134">There is another option to bring-your-own-license (BYOL) and pay only for the VM.</span></span> <span data-ttu-id="a0080-135">Bu görüntü adlarının başına {BYOL} ön eki getirilir.</span><span class="sxs-lookup"><span data-stu-id="a0080-135">Those image names are prefixed with {BYOL}.</span></span> 
   >
   > <span data-ttu-id="a0080-136">Bu seçeneklerle ilgili daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-136">For more information on these options, see [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

7. <span data-ttu-id="a0080-137">**Dağıtım modeli seçin** altında, **Resource Manager**’ın seçili olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-137">Under **Select a deployment model**, verify that **Resource Manager** is selected.</span></span> <span data-ttu-id="a0080-138">Yeni sanal makineler için önerilen dağıtım modeli Resource Manager’dır.</span><span class="sxs-lookup"><span data-stu-id="a0080-138">Resource Manager is the recommended deployment model for new virtual machines.</span></span> 

8. <span data-ttu-id="a0080-139">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-139">Click **Create**.</span></span>

    ![Resource Manager ile SQL VM oluşturma](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-the-vm"></a><span data-ttu-id="a0080-141">VM yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-141">Configure the VM</span></span>
<span data-ttu-id="a0080-142">Bir SQL Server sanal makinesini yapılandırmak için beş pencere vardır.</span><span class="sxs-lookup"><span data-stu-id="a0080-142">There are five windows for configuring a SQL Server virtual machine.</span></span>

| <span data-ttu-id="a0080-143">Adım</span><span class="sxs-lookup"><span data-stu-id="a0080-143">Step</span></span> | <span data-ttu-id="a0080-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0080-144">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0080-145">**Temel Bilgiler**</span><span class="sxs-lookup"><span data-stu-id="a0080-145">**Basics**</span></span> |[<span data-ttu-id="a0080-146">Temel ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-146">Configure basic settings</span></span>](#1-configure-basic-settings) |
| <span data-ttu-id="a0080-147">**Boyut**</span><span class="sxs-lookup"><span data-stu-id="a0080-147">**Size**</span></span> |[<span data-ttu-id="a0080-148">Sanal makine boyutunu seçme</span><span class="sxs-lookup"><span data-stu-id="a0080-148">Choose virtual machine size</span></span>](#2-choose-virtual-machine-size) |
| <span data-ttu-id="a0080-149">**Ayarlar**</span><span class="sxs-lookup"><span data-stu-id="a0080-149">**Settings**</span></span> |[<span data-ttu-id="a0080-150">İsteğe bağlı özellikleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-150">Configure optional features</span></span>](#3-configure-optional-features) |
| <span data-ttu-id="a0080-151">**SQL Server ayarları**</span><span class="sxs-lookup"><span data-stu-id="a0080-151">**SQL Server settings**</span></span> |[<span data-ttu-id="a0080-152">SQL Server ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-152">Configure SQL server settings</span></span>](#4-configure-sql-server-settings) |
| <span data-ttu-id="a0080-153">**Özet**</span><span class="sxs-lookup"><span data-stu-id="a0080-153">**Summary**</span></span> |[<span data-ttu-id="a0080-154">Özeti gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="a0080-154">Review the summary</span></span>](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a><span data-ttu-id="a0080-155">1. Temel ayarları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-155">1. Configure basic settings</span></span>

<span data-ttu-id="a0080-156">**Temel bilgiler** penceresinde, aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="a0080-156">On the **Basics** window, provide the following information:</span></span>

* <span data-ttu-id="a0080-157">Benzersiz bir sanal makine **adı** girin.</span><span class="sxs-lookup"><span data-stu-id="a0080-157">Enter a unique virtual machine **Name**.</span></span>

* <span data-ttu-id="a0080-158">En iyi performans için VM için disk türü olarak **SSD**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-158">Select **SSD** for VM disk type for optimal performance.</span></span>

* <span data-ttu-id="a0080-159">VM’deki yerel yönetici hesabı için **Kullanıcı adı** belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0080-159">Specify a **User name** for the local administrator account on the VM.</span></span> <span data-ttu-id="a0080-160">Bu hesap aynı zamanda SQL Server **sysadmin** sabit sunucu rolüne de eklenir.</span><span class="sxs-lookup"><span data-stu-id="a0080-160">This account is also added to the SQL Server **sysadmin** fixed server role.</span></span>

* <span data-ttu-id="a0080-161">Güçlü bir **parola** girin.</span><span class="sxs-lookup"><span data-stu-id="a0080-161">Provide a strong **Password**.</span></span>

* <span data-ttu-id="a0080-162">Birden fazla aboneliğiniz varsa, aboneliğin yeni VM için doğru olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a0080-162">If you have multiple subscriptions, verify that the subscription is correct for the new VM.</span></span>

* <span data-ttu-id="a0080-163">**Kaynak grubu** kutusuna, yeni kaynak grubu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="a0080-163">In the **Resource group** box, type a name for a new resource group.</span></span> <span data-ttu-id="a0080-164">Alternatif olarak, varolan bir kaynak grubunu kullanmak için **Varolanı kullan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-164">Alternatively, to use an existing resource group click **Use existing**.</span></span> <span data-ttu-id="a0080-165">Bir kaynak grubu, Azure’daki ilgili kaynakların bir koleksiyonudur (sanal makineler, depolama hesapları, sanal ağlar, vb.).</span><span class="sxs-lookup"><span data-stu-id="a0080-165">A resource group is a collection of related resources in Azure (virtual machines, storage accounts, virtual networks, etc.).</span></span>

  > [!NOTE]
  > <span data-ttu-id="a0080-166">Yalnızca Azure’daki SQL Server dağıtımlarını test ediyor veya öğreniyorsanız, yeni bir kaynak grubu kullanmak faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="a0080-166">Using a new resource group is helpful if you are just testing or learning about SQL Server deployments in Azure.</span></span> <span data-ttu-id="a0080-167">Test işleminizi tamamladıktan sonra, sanal makineyi ve bu kaynak grubu ile ilişkili tüm kaynakları otomatik olarak silmek için kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="a0080-167">After you finish with your test, delete the resource group to automatically delete the VM and all resources associated with that resource group.</span></span> <span data-ttu-id="a0080-168">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a Genel Bakış](../../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-168">For more information about resource groups, see [Azure Resource Manager Overview](../../../azure-resource-manager/resource-group-overview.md).</span></span>

* <span data-ttu-id="a0080-169">Bu dağıtımı barındıracak Azure bölgesi olarak bir **Konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-169">Select a **Location** for the Azure region that will host this deployment.</span></span>

* <span data-ttu-id="a0080-170">Ayarları kaydetmek için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-170">Click **OK** to save the settings.</span></span>

    ![SQL Temel Bilgileri penceresi](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a><span data-ttu-id="a0080-172">2. Sanal makine boyutunu seçme</span><span class="sxs-lookup"><span data-stu-id="a0080-172">2. Choose virtual machine size</span></span>

<span data-ttu-id="a0080-173">**Boyut** adımında, **Boyutu seç** penceresinde bir sanal makine boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-173">On the **Size** step, choose a virtual machine size in the **Choose a size** window.</span></span> <span data-ttu-id="a0080-174">Pencere ilk başta seçtiğiniz görüntüye göre önerilen makine boyutlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a0080-174">The window initially displays recommended machine sizes based on the image you selected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0080-175">**Boyut seçin** penceresinde gösterilen tahmini aylık maliyet, SQL Server lisans maliyetlerini içermez.</span><span class="sxs-lookup"><span data-stu-id="a0080-175">The estimated monthly cost displayed on the **Choose a size** window does not include SQL Server licensing costs.</span></span> <span data-ttu-id="a0080-176">Bu maliyet tek başına VM içindir.</span><span class="sxs-lookup"><span data-stu-id="a0080-176">This is the cost of the VM alone.</span></span> <span data-ttu-id="a0080-177">SQL Server Express ve Developer sürümleri için bu maliyet, tahmin edilen toplam maliyettir.</span><span class="sxs-lookup"><span data-stu-id="a0080-177">For the Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="a0080-178">Diğer sürümler için [Windows Sanal Makineler fiyatlandırma sayfasına](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) bakın ve hedef SQL Server sürümünüzü seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-178">For other editions, see the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) and select your target edition of SQL Server.</span></span> <span data-ttu-id="a0080-179">Ayrıca bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-179">Also see the [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md).</span></span>

![SQL VM Boyut Seçenekleri](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

<span data-ttu-id="a0080-181">Üretim iş yükleri için [Azure Virtual Machines'de SQL Server için en iyi performans uygulamaları](virtual-machines-windows-sql-performance.md)’nda önerilen makine boyutlarına ve yapılandırmalara bakın.</span><span class="sxs-lookup"><span data-stu-id="a0080-181">For production workloads, see the recommended machine sizes and configuration in [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span> <span data-ttu-id="a0080-182">Listede olmayan bir makine boyutu gerekiyorsa **Tümünü görüntüle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-182">If you need a machine size that is not listed, click the **View all** button.</span></span>

> [!NOTE]
> <span data-ttu-id="a0080-183">Sanal makine boyutları hakkında daha fazla bilgi için bkz. [Sanal makineler için boyutlar](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0080-183">For more information about virtual machine sizes see, [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a0080-184">Makine boyutunuzu seçin ve ardından **Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-184">Choose your machine size, and then click **Select**.</span></span>

## <a name="3-configure-optional-features"></a><span data-ttu-id="a0080-185">3. İsteğe bağlı özellikleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-185">3. Configure optional features</span></span>

<span data-ttu-id="a0080-186">**Ayarlar** penceresinde, sanal makine için Azure Storage, ağ ve izlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a0080-186">On the **Settings** window, configure Azure storage, networking, and monitoring for the virtual machine.</span></span>

* <span data-ttu-id="a0080-187">**Depolama** altında, **Yönetilen Diskler** altındaki **Evet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-187">Under **Storage**, select **Yes** under use **Managed Disks**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0080-188">Microsoft, SQL Server için Yönetilen Diskleri önerir.</span><span class="sxs-lookup"><span data-stu-id="a0080-188">Microsoft recommends Managed Disks for SQL Server.</span></span> <span data-ttu-id="a0080-189">Yönetilen Diskler, depolama alanını arka planda yönetir.</span><span class="sxs-lookup"><span data-stu-id="a0080-189">Managed Disks handles storage behind the scenes.</span></span> <span data-ttu-id="a0080-190">Ayrıca, Yönetilen Disklere sahip sanal makineler aynı kullanılabilirlik kümesinde olduğunda Azure uygun artıklık düzeyini sağlamak için depolama kaynaklarını dağıtır.</span><span class="sxs-lookup"><span data-stu-id="a0080-190">In addition, when virtual machines with Managed Disks are in the same availability set, Azure distributes the storage resources to provide appropriate redundancy.</span></span> <span data-ttu-id="a0080-191">Daha fazla bilgi için bkz. [Azure Yönetilen Disklere Genel Bakış](../../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-191">For additional information, see [Azure Managed Disks Overview](../../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="a0080-192">Bir kullanılabilirlik kümesindeki yönetilen diskler hakkında daha fazla ayrıntı için bkz. [Kullanılabilirlik kümesindeki VM’ler için yönetilen diskleri kullanma](../manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-192">For specifics about managed disks in an availability set, see [Use managed disks for VMs in availability set](../manage-availability.md).</span></span>

* <span data-ttu-id="a0080-193">**Ağ** altında, otomatik olarak doldurulan değerleri kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-193">Under **Network**, you can accept the automatically populated values.</span></span> <span data-ttu-id="a0080-194"><seg>
  **Sanal ağ**, **Alt ağ**, **Genel IP adresi** ve **Ağ Güvenlik Grubu**’nu el ile yapılandırmak için her bir özelliğe de tıklayabilirsiniz..</seg></span><span class="sxs-lookup"><span data-stu-id="a0080-194">You can also click on each feature to manually configure the **Virtual network**, **Subnet**, **Public IP address**, and **Network Security Group**.</span></span> <span data-ttu-id="a0080-195">Bu öğreticinin amaçları doğrultusunda, varsayılan değerleri koruyun.</span><span class="sxs-lookup"><span data-stu-id="a0080-195">For the purposes of this tutorial, keep the default values.</span></span>

* <span data-ttu-id="a0080-196">Azure varsayılan olarak, VM için belirlenen aynı depolama hesabıyla **İzleme**’yi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="a0080-196">Azure enables **Monitoring** by default with the same storage account designated for the VM.</span></span> <span data-ttu-id="a0080-197">Burada bu ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-197">You can change these settings here.</span></span>

* <span data-ttu-id="a0080-198">Bu öğreticide, **Kullanılabilirlik kümesi** için varsayılan olarak kullanılan **hiçbiri** değerini değiştirmeden bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-198">Under **Availability set**, you can leave the default of **none** for this tutorial.</span></span> <span data-ttu-id="a0080-199">SQL AlwaysOn Kullanılabilirlik Grupları kurulumunu planlıyorsanız, sanal makinenin yeniden oluşturulmasını önlemek için kullanılabilirliği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a0080-199">If you plan to set up SQL AlwaysOn Availability Groups, configure the availability to avoid recreating the virtual machine.</span></span>  <span data-ttu-id="a0080-200">Daha fazla bilgi için bkz. [Sanal Makinelerin Kullanılabilirliğini Yönetme](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0080-200">For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a0080-201">Yapılandırma ayarlarını tamamladığınızda, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-201">When you are done configuring these settings, click **OK**.</span></span>

## <a name="4-configure-sql-server-settings"></a><span data-ttu-id="a0080-202">4. SQL server ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-202">4. Configure SQL server settings</span></span>
<span data-ttu-id="a0080-203">**SQL Server ayarları** penceresinde, belirli ayarları ve SQL Server iyileştirmelerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a0080-203">On the **SQL Server settings** window, configure specific settings and optimizations for SQL Server.</span></span> <span data-ttu-id="a0080-204">SQL Server için yapılandırabileceğiniz ayarlar aşağıdakileri içerir.</span><span class="sxs-lookup"><span data-stu-id="a0080-204">The settings that you can configure for SQL Server include the following.</span></span>

| <span data-ttu-id="a0080-205">Ayar</span><span class="sxs-lookup"><span data-stu-id="a0080-205">Setting</span></span> |
| --- |
| [<span data-ttu-id="a0080-206">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="a0080-206">Connectivity</span></span>](#connectivity) |
| [<span data-ttu-id="a0080-207">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a0080-207">Authentication</span></span>](#authentication) |
| [<span data-ttu-id="a0080-208">Depolama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a0080-208">Storage configuration</span></span>](#storage-configuration) |
| [<span data-ttu-id="a0080-209">Otomatik Düzeltme Eki Uygulama</span><span class="sxs-lookup"><span data-stu-id="a0080-209">Automated Patching</span></span>](#automated-patching) |
| [<span data-ttu-id="a0080-210">Otomatik Yedekleme</span><span class="sxs-lookup"><span data-stu-id="a0080-210">Automated Backup</span></span>](#automated-backup) |
| [<span data-ttu-id="a0080-211">Azure Anahtar Kasası Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="a0080-211">Azure Key Vault Integration</span></span>](#azure-key-vault-integration) |
| [<span data-ttu-id="a0080-212">R Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a0080-212">R Services</span></span>](#r-services) |

### <a name="connectivity"></a><span data-ttu-id="a0080-213">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="a0080-213">Connectivity</span></span>

<span data-ttu-id="a0080-214">**SQL bağlantısı** altında, bu VM’de SQL Server örneğini istediğiniz erişim türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0080-214">Under **SQL connectivity**, specify the type of access you want to the SQL Server instance on this VM.</span></span> <span data-ttu-id="a0080-215">Bu öğreticinin amacı doğrultusunda, SQL Server’a İnternet’teki makineler ve hizmetlerden bağlantılara izin vermek amacıyla **Genel (internet)**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-215">For the purposes of this tutorial, select **Public (internet)** to allow connections to SQL Server from machines or services on the internet.</span></span> <span data-ttu-id="a0080-216">Bu seçenek seçildiğinde, Azure güvenlik duvarı ve ağ güvenlik grubunu bağlantı noktası 1433'te trafiğe izin verecek şekilde otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a0080-216">With this option selected, Azure automatically configures the firewall and the network security group to allow traffic on port 1433.</span></span>

![SQL Bağlantı Seçenekleri](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> <span data-ttu-id="a0080-218">Varsayılan olarak, SQL Server **1433** gibi iyi bilinen bir bağlantı noktasını dinler.</span><span class="sxs-lookup"><span data-stu-id="a0080-218">By default, SQL Server listens on a well-known port, **1433**.</span></span> <span data-ttu-id="a0080-219">Daha yüksek güvenlik için önceki iletişim kutusunda dinleme bağlantı noktasını 1401 gibi varsayılan olmayan bir bağlantı noktasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a0080-219">For increased security, change the port in the previous dialog to listen on a non-default port, such as 1401.</span></span> <span data-ttu-id="a0080-220">Bunu yaparsanız, bu bağlantı noktasına SSMS gibi bir istemci aracı kullanarak bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0080-220">If you do this, you must connect using that port from any client tools, such as SSMS.</span></span>

<span data-ttu-id="a0080-221">İnternet üzerinden SQL Server'a bağlanmak için, sonraki bölümde açıklanan, SQL Server Kimlik Doğrulamasını etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0080-221">To connect to SQL Server via the internet, you also must enable SQL Server Authentication, which is described in the next section.</span></span>

<span data-ttu-id="a0080-222">İnternet üzerinden Veritabanı Altyapısı’na bağlantıları etkinleştirmek istemiyorsanız, aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="a0080-222">If you would prefer to not enable connections to the Database Engine via the internet, choose one of the following options:</span></span>

* <span data-ttu-id="a0080-223">SQL Server’a Yalnızca VM içinden gelen bağlantılara izin vermek için **Yerel (yalnızca VM dahilinde)** </span><span class="sxs-lookup"><span data-stu-id="a0080-223">**Local (inside VM only)** to allow connections to SQL Server only from within the VM.</span></span>
* <span data-ttu-id="a0080-224">SQL Server’a aynı sanal ağdaki makineler ve hizmetlerden gelen bağlantılara izin vermek için **Özel (Sanal Ağ dahilinde)** </span><span class="sxs-lookup"><span data-stu-id="a0080-224">**Private (within Virtual Network)** to allow connections to SQL Server from machines or services in the same virtual network.</span></span>

<span data-ttu-id="a0080-225">Genel olarak, senaryonuzun izin verdiği en kısıtlayıcı bağlantıyı seçerek güvenliği geliştirin.</span><span class="sxs-lookup"><span data-stu-id="a0080-225">In general, improve security by choosing the most restrictive connectivity that your scenario allows.</span></span> <span data-ttu-id="a0080-226">Ancak tüm seçenekler Ağ Güvenlik Grubu kuralları ve SQL/Windows Kimlik Doğrulaması üzerinden korumaya alınabilir.</span><span class="sxs-lookup"><span data-stu-id="a0080-226">But all the options are securable through Network Security Group rules and SQL/Windows Authentication.</span></span> <span data-ttu-id="a0080-227">VM oluşturulduktan sonra Ağ Güvenlik Grubu’nu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-227">You can edit Network Security Group after the VM is created.</span></span> <span data-ttu-id="a0080-228">Daha fazla bilgi için bkz. [Azure Sanal Makineler'de SQL Server için Güvenlikle İlgili Dikkat Edilmesi Gerekenler](virtual-machines-windows-sql-security.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-228">For more information, see [Security Considerations for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0080-229">SQL Server Express sürümü için sanal makine görüntüsü, TCP/IP protokolünü otomatik olarak etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="a0080-229">The virtual machine image for SQL Server Express edition does not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="a0080-230">Bu durum Genel ve Özel bağlantı seçenekleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a0080-230">This is true even for the Public and  Private connectivity options.</span></span> <span data-ttu-id="a0080-231">Express sürümü için VM'yi oluşturduktan sonra [TCP/IP protokolünü el ile etkinleştirmek](#configure-sql-server-to-listen-on-the-tcp-protocol) üzere SQL Server Yapılandırma Yöneticisi'ni kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0080-231">For Express edition, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#configure-sql-server-to-listen-on-the-tcp-protocol) after creating the VM.</span></span>

### <a name="authentication"></a><span data-ttu-id="a0080-232">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a0080-232">Authentication</span></span>

<span data-ttu-id="a0080-233">SQL Server Kimlik Doğrulaması gerekiyorsa, **SQL kimlik doğrulaması** altında **Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-233">If you require SQL Server Authentication, click **Enable** under **SQL authentication**.</span></span>

![SQL Server Kimlik Doğrulaması](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> <span data-ttu-id="a0080-235">SQL Server’a İnternet üzerinden erişmeyi planlıyorsanız (yani, Genel bağlantı seçeneği), burada SQL kimlik doğrulamasını etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0080-235">If you plan to access SQL Server over the internet (i.e. the Public connectivity option), you must enable SQL authentication here.</span></span> <span data-ttu-id="a0080-236">SQL Server'a genel erişim SQL Kimlik Doğrulaması kullanılması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a0080-236">Public access to the SQL Server requires the use of SQL Authentication.</span></span>
> 
> 

<span data-ttu-id="a0080-237">SQL Server Kimlik Doğrulamasını etkinleştirirseniz, bir **Oturum açma adı** ve **parola** belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0080-237">If you enable SQL Server Authentication, specify a **Login name** and **Password**.</span></span> <span data-ttu-id="a0080-238">Bu kullanıcı adı bir SQL Server Kimlik Doğrulaması oturum açma bilgisi ve **sysadmin** sabit sunucu rolü üyesi olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a0080-238">This user name is configured as a SQL Server Authentication login and member of the **sysadmin** fixed server role.</span></span> <span data-ttu-id="a0080-239">Kimlik Doğrulama Modları hakkında daha fazla bilgi için bkz. [Kimlik Doğrulama Modu Seçme](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)</span><span class="sxs-lookup"><span data-stu-id="a0080-239">See [Choose an Authentication Mode](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) for more information about Authentication Modes.</span></span>

<span data-ttu-id="a0080-240">SQL Server Kimlik Doğrulamasını etkinleştirmezseniz, SQL Server örneğine bağlanmak için VM’deki yerel Yönetici hesabını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-240">If you do not enable SQL Server Authentication, then you can use the local Administrator account on the VM to connect to the SQL Server instance.</span></span>

### <a name="storage-configuration"></a><span data-ttu-id="a0080-241">Depolama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a0080-241">Storage configuration</span></span>

<span data-ttu-id="a0080-242">Depolama gereksinimlerini belirlemek için **Depolama yapılandırması**na tıklayın. </span><span class="sxs-lookup"><span data-stu-id="a0080-242">Click **Storage configuration** to specify the storage requirements.</span></span>

![SQL Storage Yapılandırması](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> <span data-ttu-id="a0080-244">VM’nizi standart depolama kullanmak için el ile yapılandırdıysanız, bu seçenek kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a0080-244">If you manually configured your VM to use standard storage, this option is not available.</span></span> <span data-ttu-id="a0080-245">Otomatik depolama iyileştirmesi yalnızca Premium Storage için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a0080-245">Automatic storage optimization is available only for Premium Storage.</span></span>

> [!TIP]
> <span data-ttu-id="a0080-246">Durak sayısı ve her kaydırıcının üst sınırları seçtiğiniz VM boyutuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a0080-246">The number of stops and the upper limits of each slider is dependent on the size of VM you selected.</span></span> <span data-ttu-id="a0080-247">Daha büyük ve daha güçlü bir VM, daha fazla ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a0080-247">A larger and more powerful VM is able to scale up more.</span></span>

<span data-ttu-id="a0080-248">Gereksinimleri, saniye başına girdi/çıktı işlemleri (IOP), MB/saniyedeki iş ve toplam depolama boyutu olarak belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-248">You can specify requirements as input/output operations per second (IOPs), throughput in MB/s, and total storage size.</span></span> <span data-ttu-id="a0080-249">Hareketli ölçekleri kullanarak bu değerleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a0080-249">Configure these values by using the sliding scales.</span></span> <span data-ttu-id="a0080-250">İş yüküne göre bu depolama ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-250">You can change these storage settings based on workload.</span></span> <span data-ttu-id="a0080-251">Portal, bu gereksinimler temelinde, eklenecek ve yapılandırılacak disk sayısını otomatik olarak hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a0080-251">The portal automatically calculates the number of disks to attach and configure based on these requirements.</span></span>

<span data-ttu-id="a0080-252">**Depolama iyileştirme seçimi** altında aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="a0080-252">Under **Storage optimized for**, select one of the following options:</span></span>

* <span data-ttu-id="a0080-253">**Genel**, varsayılan ayardır ve çoğu iş yükünü destekler.</span><span class="sxs-lookup"><span data-stu-id="a0080-253">**General** is the default setting and supports most workloads.</span></span>
* <span data-ttu-id="a0080-254">**İşlem** işleme depolamayı geleneksel veritabanı OLTP iş yükleri için iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="a0080-254">**Transactional** processing optimizes the storage for traditional database OLTP workloads.</span></span>
* <span data-ttu-id="a0080-255">**Veri depolama**, depolamayı çözümleme ve raporlama iş yükleri için iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="a0080-255">**Data warehousing** optimizes the storage for analytic and reporting workloads.</span></span>

### <a name="automated-patching"></a><span data-ttu-id="a0080-256">Otomatik düzeltme eki uygulama</span><span class="sxs-lookup"><span data-stu-id="a0080-256">Automated patching</span></span>

<span data-ttu-id="a0080-257">**Otomatik düzeltme eki uygulama** varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="a0080-257">**Automated patching** is enabled by default.</span></span> <span data-ttu-id="a0080-258">Otomatik düzeltme eki uygulama Azure’un SQL Server’a ve işletim sistemine otomatik olarak düzeltme eki uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0080-258">Automated patching allows Azure to automatically patch SQL Server and the operating system.</span></span> <span data-ttu-id="a0080-259">Bakım penceresi için haftanın gününü, saati ve süreyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0080-259">Specify a day of the week, time, and duration for a maintenance window.</span></span> <span data-ttu-id="a0080-260">Azure düzeltme eki uygulamayı bu bakım penceresinde gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a0080-260">Azure performs patching in this maintenance window.</span></span> <span data-ttu-id="a0080-261">Bakım penceresi zamanlaması saat için VM yerel saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a0080-261">The maintenance window schedule uses the VM locale for time.</span></span> <span data-ttu-id="a0080-262">Azure’un SQL Server’a ve işletim sistemine otomatik olarak düzeltme eki uygulamasını istemiyorsanız tıklayın **Devre dışı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-262">If you do not want Azure to automatically patch SQL Server and the operating system, click **Disable**.</span></span>  

![SQL Otomatik Düzeltme Eki Uygulama](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

<span data-ttu-id="a0080-264">Daha fazla bilgi için bkz. [Azure Virtual Machines’de SQL Server için Otomatik Düzeltme Eki Uygulama](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-264">For more information, see [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md).</span></span>

### <a name="automated-backup"></a><span data-ttu-id="a0080-265">Otomatik yedekleme</span><span class="sxs-lookup"><span data-stu-id="a0080-265">Automated backup</span></span>

<span data-ttu-id="a0080-266">**Otomatik yedekleme** altında, tüm veritabanları için otomatik veritabanı yedeklemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a0080-266">Enable automatic database backups for all databases under **Automated backup**.</span></span> <span data-ttu-id="a0080-267">Otomatik yedekleme varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="a0080-267">Automated backup is disabled by default.</span></span>

<span data-ttu-id="a0080-268">SQL otomatik yedeklemeyi etkinleştirdiğinizde, aşağıdakileri yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a0080-268">When you enable SQL automated backup, you can configure the following:</span></span>

* <span data-ttu-id="a0080-269">Yedeklemeler için elde tutma süresi (gün)</span><span class="sxs-lookup"><span data-stu-id="a0080-269">Retention period (days) for backups</span></span>
* <span data-ttu-id="a0080-270">Yedeklemeler için kullanılacak depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="a0080-270">Storage account to use for backups</span></span>
* <span data-ttu-id="a0080-271">Yedeklemeler için şifreleme seçeneği ve parola</span><span class="sxs-lookup"><span data-stu-id="a0080-271">Encryption option and password for backups</span></span>
* <span data-ttu-id="a0080-272">Backup sistem veritabanları</span><span class="sxs-lookup"><span data-stu-id="a0080-272">Backup system databases</span></span>
* <span data-ttu-id="a0080-273">Yedekleme zamanlamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a0080-273">Configure backup schedule</span></span>

<span data-ttu-id="a0080-274">Yedeklemeyi şifrelemek için **Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-274">To encrypt the backup, click **Enable**.</span></span> <span data-ttu-id="a0080-275">Ardından **Parola**’yı belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0080-275">Then specify the **Password**.</span></span> <span data-ttu-id="a0080-276">Azure yedeklemeleri şifrelemek için bir sertifika oluşturur ve bu sertifikayı korumak için belirtilen parolayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a0080-276">Azure creates a certificate to encrypt the backups and uses the specified password to protect that certificate.</span></span>

![SQL Otomatik Yedekleme](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 <span data-ttu-id="a0080-278">Daha fazla bilgi için bkz. [Azure Virtual Machines’de SQL Server için Otomatik Yedekleme](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-278">For more information, see [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

### <a name="azure-key-vault-integration"></a><span data-ttu-id="a0080-279">Azure Anahtar Kasası tümleştirme</span><span class="sxs-lookup"><span data-stu-id="a0080-279">Azure Key Vault integration</span></span>

<span data-ttu-id="a0080-280">Şifreleme için güvenlik gizli anahtarlarını depolamak üzere, **Azure anahtar kasası tümleştirme**’ye ve **Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-280">To store security secrets in Azure for encryption, click **Azure key vault integration** and click **Enable**.</span></span>

![SQL Azure Anahtar Kasası Tümleştirme](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

<span data-ttu-id="a0080-282">Aşağıdaki tabloda Azure Anahtar Kasası Tümleştirmeyi yapılandırmak için gereken parametreler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a0080-282">The following table lists the parameters required to configure Azure Key Vault Integration.</span></span>

| <span data-ttu-id="a0080-283">PARAMETRE</span><span class="sxs-lookup"><span data-stu-id="a0080-283">PARAMETER</span></span> | <span data-ttu-id="a0080-284">AÇIKLAMA</span><span class="sxs-lookup"><span data-stu-id="a0080-284">DESCRIPTION</span></span> | <span data-ttu-id="a0080-285">ÖRNEK</span><span class="sxs-lookup"><span data-stu-id="a0080-285">EXAMPLE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0080-286">**Anahtar Kasası URL'si**</span><span class="sxs-lookup"><span data-stu-id="a0080-286">**Key Vault URL**</span></span> |<span data-ttu-id="a0080-287">Anahtar kasası konumu.</span><span class="sxs-lookup"><span data-stu-id="a0080-287">The location of the key vault.</span></span> |<span data-ttu-id="a0080-288">https://contosokeyvault.vault.azure.net/</span><span class="sxs-lookup"><span data-stu-id="a0080-288">https://contosokeyvault.vault.azure.net/</span></span> |
| <span data-ttu-id="a0080-289">**Asıl ad**</span><span class="sxs-lookup"><span data-stu-id="a0080-289">**Principal name**</span></span> |<span data-ttu-id="a0080-290">Azure Active Directory hizmet asıl adı.</span><span class="sxs-lookup"><span data-stu-id="a0080-290">Azure Active Directory service principal name.</span></span> <span data-ttu-id="a0080-291">Bu ad İstemci Kimliği olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="a0080-291">This name is also referred to as the Client ID.</span></span> |<span data-ttu-id="a0080-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span><span class="sxs-lookup"><span data-stu-id="a0080-292">fde2b411-33d5-4e11-af04eb07b669ccf2</span></span> |
| <span data-ttu-id="a0080-293">**Asıl parola**</span><span class="sxs-lookup"><span data-stu-id="a0080-293">**Principal secret**</span></span> |<span data-ttu-id="a0080-294">Azure Active Directory hizmet asıl gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="a0080-294">Azure Active Directory service principal secret.</span></span> <span data-ttu-id="a0080-295">Bu gizli anahtar İstemci Gizli Anahtarı olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="a0080-295">This secret is also referred to as the Client Secret.</span></span> |<span data-ttu-id="a0080-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span><span class="sxs-lookup"><span data-stu-id="a0080-296">9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=</span></span> |
| <span data-ttu-id="a0080-297">**Kimlik bilgisi adı**</span><span class="sxs-lookup"><span data-stu-id="a0080-297">**Credential name**</span></span> |<span data-ttu-id="a0080-298">**Kimlik bilgisi adı**: AKV Tümleştirme, VM’nin anahtar kasasına erişim sağlamasına izin vererek, SQL Server’da bir kimlik bilgisi oluşturur</span><span class="sxs-lookup"><span data-stu-id="a0080-298">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="a0080-299">Bu kimlik bilgisi için bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="a0080-299">Choose a name for this credential.</span></span> |<span data-ttu-id="a0080-300">mycred1</span><span class="sxs-lookup"><span data-stu-id="a0080-300">mycred1</span></span> |

<span data-ttu-id="a0080-301">Daha fazla bilgi için bkz. [Azure VM’lerde SQL Server için Azure Anahtar Kasası Tümleştirmeyi Yapılandırma](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-301">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md).</span></span>

### <a name="r-services"></a><span data-ttu-id="a0080-302">R hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a0080-302">R services</span></span>

<span data-ttu-id="a0080-303">[SQL Server R Hizmetleri](https://msdn.microsoft.com/library/mt604845.aspx) seçeneğini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-303">You have the option to enable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx).</span></span> <span data-ttu-id="a0080-304">Bu özellik, SQL Server 2016 ile gelişmiş analizi kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0080-304">This enables you to use advanced analytics with SQL Server 2016.</span></span> <span data-ttu-id="a0080-305">**SQL Server Ayarları** penceresinde **Etkinleştir** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a0080-305">Click **Enable** on the **SQL Server Settings** window.</span></span>

> [!NOTE]
> <span data-ttu-id="a0080-306">SQL Server 2016 Developer sürümü için bu seçenek portal tarafından yanlış bir şekilde devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a0080-306">For SQL Server 2016 Developer Edition, this option is incorrectly disabled by the portal.</span></span> <span data-ttu-id="a0080-307">Developer sürümü için VM oluşturduktan sonra R Hizmetlerini elle etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-307">For Developer edition, you must enable R Services manually after creating your VM.</span></span>

![SQL Server R Hizmetlerini Etkinleştirme](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

<span data-ttu-id="a0080-309">SQL Server ayarlarını yapılandırmayı bitirdiğinizde, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0080-309">When you are finished configuring SQL Server settings, click **OK**.</span></span>

## <a name="5-review-the-summary"></a><span data-ttu-id="a0080-310">5. Özeti gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="a0080-310">5. Review the summary</span></span>

<span data-ttu-id="a0080-311">**Özet** penceresinde, özeti gözden geçirin ve **Satın al**’a tıklayarak bu VM için belirtilen SQL Server, kaynak grubu ve kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0080-311">On the **Summary** window, review the summary and click **Purchase** to create SQL Server, resource group, and resources specified for this VM.</span></span>

<span data-ttu-id="a0080-312">Azure portalından dağıtımı izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-312">You can monitor the deployment from the Azure portal.</span></span> <span data-ttu-id="a0080-313">Ekranın üst kısmındaki **Bildirimler** düğmesi dağıtımın temel durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0080-313">The **Notifications** button at the top of the screen shows basic status of the deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="a0080-314">Size dağıtım zamanları hakkında bir fikir vermek için,Doğu ABD bölgesinde, varsayılan ayarlarla bir SQL VM dağıttım.</span><span class="sxs-lookup"><span data-stu-id="a0080-314">To provide you with an idea on deployment times, I deployed a SQL VM to the East US region with default settings.</span></span> <span data-ttu-id="a0080-315">Bu test dağıtımının tamamlanması toplam 26 dakika sürdü.</span><span class="sxs-lookup"><span data-stu-id="a0080-315">This test deployment took a total of 26 minutes to complete.</span></span> <span data-ttu-id="a0080-316">Ancak bölgeniz ve seçili ayarlarınıza göre, daha hızlı veya daha yavaş dağıtım süresiyle karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-316">But you might experience a faster or slower deployment time based on your region and selected settings.</span></span>

## <a name="open-the-vm-with-remote-desktop"></a><span data-ttu-id="a0080-317">VM’yi Uzak Masaüstü ile açma</span><span class="sxs-lookup"><span data-stu-id="a0080-317">Open the VM with Remote Desktop</span></span>

<span data-ttu-id="a0080-318">Uzak Masaüstü kullanarak SQL Server sanal makinesine bağlanmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a0080-318">Use the following steps to connect to the SQL Server virtual machine with Remote Desktop:</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="a0080-319">SQL Server sanal makineye bağlandıktan sonra, SQL Server Management Studio'yu başlatabilir ve yerel yönetici kimlik bilgilerinizi kullanarak Windows Kimlik Doğrulamasına bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-319">After you connect to the SQL Server virtual machine, you can launch SQL Server Management Studio and connect with Windows Authentication using your local administrator credentials.</span></span> <span data-ttu-id="a0080-320">SQL Server Kimlik Doğrulamasını etkinleştirdiyseniz, sağlama işlemi sırasında yapılandırdığınız SQL oturum açma adı ve parolasını kullanarak da SQL Kimlik Doğrulamasına bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-320">If you enabled SQL Server Authentication, you can also connect with SQL Authentication using the SQL login and password you configured during provisioning.</span></span>

<span data-ttu-id="a0080-321">Makineye erişim, gereksinimlerinize göre makineyi ve SQL Server ayarlarını doğrudan değiştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a0080-321">Access to the machine enables you to directly change machine and SQL Server settings based on your requirements.</span></span> <span data-ttu-id="a0080-322">Örneğin, güvenlik duvarı ayarlarını yapılandırabilir veya SQL Server yapılandırma ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-322">For example, you could configure the firewall settings or change SQL Server configuration settings.</span></span>

## <a name="enable-tcpip-for-developer-and-express-editions"></a><span data-ttu-id="a0080-323">Developer ve Express sürümleri için TCP/IP’yi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a0080-323">Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="a0080-324">Yeni bir SQL Server VM’si sağlanırken Azure, SQL Server Developer ve Express sürümleri için TCP/IP’yi otomatik olarak etkinleştirmez.</span><span class="sxs-lookup"><span data-stu-id="a0080-324">When provisioning a new SQL Server VM, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="a0080-325">Aşağıdaki adımlarda, uzaktan IP adresiyle bağlanabilmeniz için TCP/IP’yi el ile nasıl etkinleştirebileceğiniz açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a0080-325">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="a0080-326">Aşağıdaki adımlarda, SQL Server Developer ve Express sürümleri için TCP/IP protokolünü etkinleştirme yöntemi olarak **SQL Server Yapılandırma Yöneticisi** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0080-326">The following steps use **SQL Server Configuration Manager** to enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-to-sql-server-remotely"></a><span data-ttu-id="a0080-327">SQL Server'a uzaktan bağlanma</span><span class="sxs-lookup"><span data-stu-id="a0080-327">Connect to SQL Server remotely</span></span>

<span data-ttu-id="a0080-328">Bu öğreticide,sanal makine için **Genel** erişimi ve **SQL Server Kimlik Doğrulaması**’nı seçtik.</span><span class="sxs-lookup"><span data-stu-id="a0080-328">In this tutorial, we selected **Public** access for the virtual machine and **SQL Server Authentication**.</span></span> <span data-ttu-id="a0080-329">Bu ayarlar, İnternet üzerinden tüm istemcilerden gelen (doğru SQL oturum açma bilgilerine sahip oldukları varsayılarak) SQL Server bağlantılarına izin verecek şekilde sanal makineyi yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="a0080-329">These settings automatically configured the virtual machine to allow SQL Server connections from any client over the internet (assuming they have the correct SQL login).</span></span>

> [!NOTE]
> <span data-ttu-id="a0080-330">Sağlama sırasında Genel’i seçmediyseniz, sağlamadan sonra SQL bağlantı ayarlarınızı portal üzerinden değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0080-330">If you did not select Public during provisioning, then you can change your SQL connectivity settings through the portal after provisioning.</span></span> <span data-ttu-id="a0080-331">Daha fazla bilgi edinmek için bkz. [SQL bağlantı ayarlarınızı değiştirme](virtual-machines-windows-sql-connect.md#change).</span><span class="sxs-lookup"><span data-stu-id="a0080-331">For more information, see  [Change your SQL connectivity settings](virtual-machines-windows-sql-connect.md#change).</span></span>

<span data-ttu-id="a0080-332">Aşağıdaki bölümlerde, VM’nizdeki SQL Server örneğinize İnternet üzerinden farklı bir bilgisayarın nasıl bağlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a0080-332">The following sections show how to connect to your SQL Server instance on your VM from a different computer over the internet.</span></span>

> [!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a0080-333">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a0080-333">Next Steps</span></span>

<span data-ttu-id="a0080-334">Azure’da SQL Server'ı kullanma hakkında diğer bilgiler için bkz. [Azure Virtual Machines’de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) ve [Sık Sorulan Sorular](virtual-machines-windows-sql-server-iaas-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a0080-334">For other information about using SQL Server in Azure, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) and the [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).</span></span>