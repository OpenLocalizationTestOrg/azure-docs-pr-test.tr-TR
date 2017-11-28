---
title: "Azure DevTest Labs Laboratuvar ilkeleri yönetme | Microsoft Docs"
description: "Laboratuvar ilkeleri VM boyutları, kullanıcı ve kapatma Otomasyon başına en fazla VMs gibi tanımlar öğrenin."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="78a6b-103">Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="78a6b-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="78a6b-104">Azure DevTest Labs maliyet denetlemek ve atık, ortamlarındaki ilkeleri (ayarlar) yöneterek her Laboratuvar için en aza indirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="78a6b-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="78a6b-105">Bu makalede her ilkesinin nasıl ayarlanacağı hakkında adım adım ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78a6b-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="78a6b-106">Sanal makine boyutlarını izin kümesi</span><span class="sxs-lookup"><span data-stu-id="78a6b-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="78a6b-107">İzin verilen VM boyutları ayarlamak için ilke Laboratuvar atık hangi VM boyutları laboratuar ortamında izin verildiğini belirtmek sağlayarak en aza indirmek için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="78a6b-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="78a6b-108">Bu ilke etkinleştirilirse, yalnızca VM boyutları bu listeden VM'ler oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78a6b-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="78a6b-109">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **sanal makine boyutları izin**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![İzin verilen sanal makine boyutları](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="78a6b-111">Seçin **üzerinde** Bu ilkeyi etkinleştirmek için ve **kapalı** devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="78a6b-112">Bu ilkeyi etkinleştirirseniz, laboratuvarınızda oluşturulabilmesi için bir veya daha fazla VM boyutları seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="78a6b-113">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="78a6b-114">Kullanıcı başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="78a6b-114">Set virtual machines per user</span></span>
<span data-ttu-id="78a6b-115">İlke için **kullanıcı başına sanal makineler** ayrı bir kullanıcı tarafından oluşturulan VM maksimum sayısını belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="78a6b-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="78a6b-116">Bir kullanıcı veya Kullanıcı sınırı sağlandığında VM talep oluşturmak üzere çalışırsa, oluşturulan ve istenen VM olamaz bir hata iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="78a6b-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="78a6b-117">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="78a6b-119">Seçin **Evet** kullanıcı başına VM'ler sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="78a6b-120">Kullanıcı başına VM'ler sayısını sınırlamak istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="78a6b-121">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler maksimum sayısını gösteren sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="78a6b-122">Seçin **Evet** SSD (katı hal disk) kullanabilirsiniz VM'lerin sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="78a6b-123">SSD kullanın, seçin VM'lerin sayısını sınırlamak istemiyorsanız **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="78a6b-124">Seçerseniz **Evet**, SSD kullanılarak oluşturulan VM maksimum sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="78a6b-125">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="78a6b-126">Laboratuvar başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="78a6b-126">Set virtual machines per lab</span></span>
<span data-ttu-id="78a6b-127">İlke için **Laboratuvar başına sanal makine** geçerli Laboratuvar için oluşturulan VM maksimum sayısını belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="78a6b-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="78a6b-128">Laboratuvar sınırı sağlandığında bir VM oluşturmak bir kullanıcı çalışırsa, VM oluşturulamıyor bir hata iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="78a6b-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="78a6b-129">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** menüsünde, select **Laboratuvar başına sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Laboratuvar başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="78a6b-131">Seçin **Evet** Laboratuvar başına VM'ler sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="78a6b-132">Laboratuvar başına VM'ler sayısını sınırlamak istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="78a6b-133">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler maksimum sayısını gösteren sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="78a6b-134">Seçin **Evet** SSD (katı hal disk) kullanabilirsiniz VM'lerin sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="78a6b-135">SSD kullanın, seçin VM'lerin sayısını sınırlamak istemiyorsanız **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="78a6b-136">Seçerseniz **Evet**, SSD kullanılarak oluşturulan VM maksimum sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="78a6b-137">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="78a6b-138">Set otomatik-kapatma</span><span class="sxs-lookup"><span data-stu-id="78a6b-138">Set auto-shutdown</span></span>
<span data-ttu-id="78a6b-139">Bu Laboratuvar ait VM'ler kapatma süresi belirtmenize olanak tanıyarak Laboratuvar atık en aza indirmek için otomatik kapatma ilkesi yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="78a6b-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="78a6b-140">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Otomatik kapatma](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="78a6b-142">Seçin **üzerinde** Bu ilkeyi etkinleştirmek için ve **kapalı** devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="78a6b-143">Bu ilkeyi etkinleştirirseniz, geçerli laboratuarda tüm sanal makineleri kapatmaya saat (ve saat dilimi) belirtin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="78a6b-144">Belirtin **Evet** veya **Hayır** belirtilen otomatik kapatma saatten önce 15 dakikada bir bildirim gönderme seçeneği için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="78a6b-145">Belirtirseniz **Evet**, bildirim almak için bir Web kancası URL'si uç noktası girin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="78a6b-146">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası veya API Azure işlevi oluşturma](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="78a6b-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="78a6b-147">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-147">Select **Save**.</span></span>

    <span data-ttu-id="78a6b-148">Varsayılan olarak, bir kez etkinleştirildikten sonra geçerli laboratuarda tüm VM'ler için bu ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="78a6b-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="78a6b-149">Bu ayarı belirli bir sanal makineden kaldırmak için VM'ın dikey penceresini açın ve değiştirmek kendi **otomatik kapatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="78a6b-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="78a6b-150">Otomatik başlangıcı Ayarla</span><span class="sxs-lookup"><span data-stu-id="78a6b-150">Set auto-start</span></span>
<span data-ttu-id="78a6b-151">Otomatik başlatma ilkesi geçerli laboratuvara sanal makineleri yeniden başlatıldığında belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="78a6b-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="78a6b-152">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik başlatma**.</span><span class="sxs-lookup"><span data-stu-id="78a6b-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Otomatik başlatma](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="78a6b-154">Seçin **üzerinde** Bu ilkeyi etkinleştirmek için ve **kapalı** devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="78a6b-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="78a6b-155">Bu ilkeyi etkinleştirirseniz, zamanlanmış başlangıç saati, saat dilimi ve saati geçerli olduğu için haftanın günlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="78a6b-156">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-156">Select **Save**.</span></span>

    <span data-ttu-id="78a6b-157">Etkinleştirildikten sonra bu ilkenin geçerli laboratuarda herhangi bir VM için otomatik olarak uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="78a6b-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="78a6b-158">Bu ayar için belirli bir VM'yi uygulamak için VM'ın dikey penceresini açın ve değiştirmek kendi **otomatik başlatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="78a6b-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="78a6b-159">Sona erme tarihi ayarlama</span><span class="sxs-lookup"><span data-stu-id="78a6b-159">Set expiration date</span></span>
<span data-ttu-id="78a6b-160">Bir süre sonu ayarlayabilirsiniz ne zaman tarih, [VM oluşturma](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="78a6b-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="78a6b-161">İçinde **Gelişmiş ayarları**, üzerinde VM otomatik olarak silinir bir tarih belirtmek için takvim simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="78a6b-162">Varsayılan olarak, VM asla sona erecek.</span><span class="sxs-lookup"><span data-stu-id="78a6b-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="78a6b-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78a6b-163">Next steps</span></span>
<span data-ttu-id="78a6b-164">Tanımlanan ve çeşitli VM ilke ayarları, laboratuvarınız için uygulanan sonra daha sonra deneyin gereken bazı şeyler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="78a6b-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="78a6b-165">[Paylaşılan IP adreslerini anlamak](devtest-lab-shared-ip.md) -paylaşılan IP açıklar adresleri DevTest Labs'de laboratuvarınız sanal makineleri bağlanmak için gereken genel IP adresleri sayısını en aza indirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="78a6b-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="78a6b-166">[Maliyet yönetimini yapılandırma](devtest-lab-configure-cost-management.md) -nasıl kullanılacağını anlatan **aylık tahmini maliyet eğilimi** grafiği</span><span class="sxs-lookup"><span data-stu-id="78a6b-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="78a6b-167">Geçerli ay görüntülemek için maliyet tarihi tahmini ayın son maliyet tahmini ve.</span><span class="sxs-lookup"><span data-stu-id="78a6b-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="78a6b-168">[Özel görüntü oluşturma](devtest-lab-create-template.md) - bir VM oluşturduğunuzda, özel bir görüntü veya bir Market görüntüsü olabilecek bir taban belirtin.</span><span class="sxs-lookup"><span data-stu-id="78a6b-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="78a6b-169">Bu makalede, bir VHD dosyasından özel bir görüntü oluşturmak nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="78a6b-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="78a6b-170">[Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) - VMs Azure Market görüntülerini temel oluşturmayı Azure DevTest Labs destekler.</span><span class="sxs-lookup"><span data-stu-id="78a6b-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="78a6b-171">Bu makalede, varsa, Azure Market görüntülerini olabilecek belirtmek verilmektedir VM'ler bir laboratuar ortamında oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="78a6b-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="78a6b-172">[Bir laboratuar ortamında bir VM oluşturma](devtest-lab-add-vm-with-artifacts.md) -temel bir görüntüden bir VM oluşturmak nasıl gösterir (ya da özel veya Market) ve VM yapıları çalışmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="78a6b-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

