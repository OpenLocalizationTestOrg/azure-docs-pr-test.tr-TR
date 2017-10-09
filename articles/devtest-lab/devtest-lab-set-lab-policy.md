---
title: Azure DevTest Labs aaaManage Laboratuvar ilkeleri | Microsoft Docs
description: "Bilgi toodefine Laboratuvar ilkeleri gibi VM boyutları nasıl kullanıcı başına en fazla VM'ler ve kapatma Otomasyon."
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4d1e2-103">Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="4d1e2-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="4d1e2-104">Azure DevTest Labs maliyet denetlemek ve atık, ortamlarındaki ilkeleri (ayarlar) yöneterek her Laboratuvar için en aza indirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="4d1e2-105">Bu makalede, adım adım ayrıntılı olarak açıklanmaktadır nasıl tooset her ilke.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="4d1e2-106">Sanal makine boyutlarını izin kümesi</span><span class="sxs-lookup"><span data-stu-id="4d1e2-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="4d1e2-107">Hello İlkesi ayarı hello için VM boyutları yardımcı toominimize Laboratuvar hangi VM boyutları hello laboratuvarda izin verilen toospecify etkinleştirerek boşa harcanmasına izin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="4d1e2-108">Bu ilke etkinleştirilirse, yalnızca VM boyutları bu listeden kullanılan toocreate VM'ler olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="4d1e2-109">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **sanal makine boyutları izin**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![İzin verilen sanal makine boyutları](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="4d1e2-111">Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="4d1e2-112">Bu ilkeyi etkinleştirirseniz, laboratuvarınızda oluşturulabilmesi için bir veya daha fazla VM boyutları seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="4d1e2-113">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="4d1e2-114">Kullanıcı başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="4d1e2-114">Set virtual machines per user</span></span>
<span data-ttu-id="4d1e2-115">Hello İlkesi **kullanıcı başına sanal makineler** toospecify hello en fazla ayrı bir kullanıcı tarafından oluşturulan VM'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="4d1e2-116">Merhaba Kullanıcı sınırı sağlandığında bir kullanıcı toocreate veya talep VM çalışırsa, bir hata iletisi VM oluşturulan/talep edilemez edilmesine bu hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="4d1e2-117">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="4d1e2-119">Seçin **Evet** toolimit hello VM'lerin sayısını kullanıcı başına.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="4d1e2-120">Kullanıcı başına VM'ler toolimit hello numarasını istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="4d1e2-121">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="4d1e2-122">Seçin **Evet** toolimit hello SSD (katı hal disk) kullanabilirsiniz VM sayısı.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="4d1e2-123">Toolimit hello SSD kullanabilirsiniz VM'lerin sayısını istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="4d1e2-124">Seçerseniz **Evet**, SSD kullanılarak oluşturulabilir VM'ler hello sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="4d1e2-125">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="4d1e2-126">Laboratuvar başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="4d1e2-126">Set virtual machines per lab</span></span>
<span data-ttu-id="4d1e2-127">Hello İlkesi **Laboratuvar başına sanal makine** hello geçerli Laboratuvar için toospecify hello maksimum oluşturulabilecek VM'lerin sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="4d1e2-128">Bir kullanıcı Hello Laboratuvar sınırı sağlandığında toocreate VM çalışırsa, bir hata iletisi VM oluşturulamıyor, hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="4d1e2-129">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **Laboratuvar başına sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Laboratuvar başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="4d1e2-131">Seçin **Evet** toolimit hello VM'lerin sayısını Laboratuvar başına.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="4d1e2-132">Toolimit hello VM'lerin sayısını Laboratuvar başına istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="4d1e2-133">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="4d1e2-134">Seçin **Evet** toolimit hello SSD (katı hal disk) kullanabilirsiniz VM sayısı.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="4d1e2-135">Toolimit hello SSD kullanabilirsiniz VM'lerin sayısını istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="4d1e2-136">Seçerseniz **Evet**, SSD kullanılarak oluşturulabilir VM'ler hello sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="4d1e2-137">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="4d1e2-138">Set otomatik-kapatma</span><span class="sxs-lookup"><span data-stu-id="4d1e2-138">Set auto-shutdown</span></span>
<span data-ttu-id="4d1e2-139">Merhaba otomatik kapatma ilke bu Laboratuvar ait VM'ler kapatma toospecify hello zaman sağlayarak boşa harcanmasına toominimize Laboratuvar yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="4d1e2-140">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Otomatik kapatma](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="4d1e2-142">Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="4d1e2-143">Bu ilkeyi etkinleştirirseniz, tüm VM'ler aşağı hello saat (ve saat dilimi) tooshut hello geçerli laboratuvarda belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="4d1e2-144">Belirtin **Evet** veya **Hayır** hello seçeneği toosend için otomatik kapatma süresi bir bildirim 15 dakika önceki toohello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="4d1e2-145">Belirtirseniz **Evet**, bir Web kancası URL'si uç nokta tooreceive hello bildirim girin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="4d1e2-146">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası veya API Azure işlevi oluşturma](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="4d1e2-147">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-147">Select **Save**.</span></span>

    <span data-ttu-id="4d1e2-148">Etkinleştirildiğinde, varsayılan olarak, bu ilke tooall VM'ler hello geçerli laboratuarda uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="4d1e2-149">Bu ayar için belirli bir VM'yi tooremove açmak hello VM'in dikey penceresinde ve değişiklik kendi **otomatik kapatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="4d1e2-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="4d1e2-150">Otomatik başlangıcı Ayarla</span><span class="sxs-lookup"><span data-stu-id="4d1e2-150">Set auto-start</span></span>
<span data-ttu-id="4d1e2-151">Merhaba VM'ler hello geçerli laboratuarda yeniden başlatıldığında hello otomatik başlatma ilkesi, toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="4d1e2-152">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik başlatma**.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Otomatik başlatma](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="4d1e2-154">Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="4d1e2-155">Bu ilkeyi etkinleştirirseniz, hello zamanlanmış başlangıç saati, saat dilimi ve hello için hangi hello zaman geçerlidir hello haftanın günleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="4d1e2-156">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-156">Select **Save**.</span></span>

    <span data-ttu-id="4d1e2-157">Etkinleştirildikten sonra bu ilke otomatik olarak uygulanan tooany VM'ler hello geçerli laboratuvarda değil.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="4d1e2-158">tooapply bu ayarı tooa belirli VM, açık hello VM'in dikey ve değişiklik kendi **otomatik başlatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="4d1e2-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="4d1e2-159">Sona erme tarihi ayarlama</span><span class="sxs-lookup"><span data-stu-id="4d1e2-159">Set expiration date</span></span>
<span data-ttu-id="4d1e2-160">Bir süre sonu ayarlayabilirsiniz ne zaman tarih, [hello VM oluşturma](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4d1e2-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="4d1e2-161">İçinde **Gelişmiş ayarları**, üzerinde VM hello tarih otomatik olarak silinmesini hello Takvim simgesi toospecify seçin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="4d1e2-162">Varsayılan olarak, hello VM asla sona erecek.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4d1e2-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d1e2-163">Next steps</span></span>
<span data-ttu-id="4d1e2-164">Uygulanan ve yapılandırdığınız tanımlanan sonra laboratuvarınız için çeşitli VM ilke ayarları Merhaba, İşte bazı şeyleri tootry sonraki:</span><span class="sxs-lookup"><span data-stu-id="4d1e2-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="4d1e2-165">[Paylaşılan IP adreslerini anlamak](devtest-lab-shared-ip.md) -paylaşılan IP açıklar adresleri DevTest Labs toominimize hello sayısında ortak IP adresleri gerekli tooconnect tooyour Laboratuvar VM'ler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="4d1e2-166">[Maliyet yönetimini yapılandırma](devtest-lab-configure-cost-management.md) -gösterilmektedir nasıl toouse hello **aylık tahmini maliyet eğilimi** grafiği</span><span class="sxs-lookup"><span data-stu-id="4d1e2-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="4d1e2-167">tooview, geçerli ayın tahmini maliyet-to-date ve öngörülen hello ayın son maliyet hello.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="4d1e2-168">[Özel görüntü oluşturma](devtest-lab-create-template.md) - bir VM oluşturduğunuzda, özel bir görüntü veya bir Market görüntüsü olabilecek bir taban belirtin.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="4d1e2-169">Bu makalede nasıl toocreate özel bir görüntü bir VHD dosyasından gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="4d1e2-170">[Market görüntülerini yapılandırma](devtest-lab-configure-marketplace-images.md) - VMs Azure Market görüntülerini temel oluşturmayı Azure DevTest Labs destekler.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="4d1e2-171">Bu makalede gösterilmektedir nasıl olabilen, varsa, Azure Market görüntülerini toospecify VM'ler bir laboratuar ortamında oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="4d1e2-172">[Bir laboratuar ortamında bir VM oluşturma](devtest-lab-add-vm-with-artifacts.md) -gösterilmektedir nasıl toocreate temel görüntü bir VM'den (ya da özel veya Market) ve nasıl toowork yapıtlarla birlikte, VM.</span><span class="sxs-lookup"><span data-stu-id="4d1e2-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

