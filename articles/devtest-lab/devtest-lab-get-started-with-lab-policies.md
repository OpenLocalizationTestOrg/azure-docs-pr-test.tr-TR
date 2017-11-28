---
title: "Azure DevTest Labs temel Laboratuvar ilkeleri yönetme | Microsoft Docs"
description: "DevTest Labs'de Laboratuvar için temel ilkeleri (ayarlar) bazıları ayarlamak öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="90e56-103">Azure DevTest Labs laboratuvarda için temel ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="90e56-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="90e56-104">Azure DevTest Labs, maliyet denetlemek ve ilkeleri (ayarlar) her Laboratuvar için yöneterek, ortamlarındaki atık en aza indirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="90e56-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="90e56-105">Bu makalede, iki en kritik ilkeleri ayarlamak öğrenme - sanal oluşturduğunuz ya da tek bir kullanıcı tarafından talep makineler (VM) sayısını sınırlama ve Otomatik kapatma yapılandırma ilkeleri ile çalışmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="90e56-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="90e56-106">Her Laboratuvar ilkesini ayarlamak, makale bkz görüntülemek için [Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="90e56-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="90e56-107">Azure DevTest Labs Laboratuvar 's ilkelerinde erişme</span><span class="sxs-lookup"><span data-stu-id="90e56-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="90e56-108">Aşağıdaki adımları ilkeleri için Azure DevTest Labs laboratuvarında kurma yol:</span><span class="sxs-lookup"><span data-stu-id="90e56-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="90e56-109">(Görüntüleyip değiştirmek için) için bir laboratuvar ilkeleri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="90e56-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="90e56-110">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="90e56-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="90e56-111">**More services**’i (Daha fazla hizmet’i) seçip ardından listeden **DevTest Labs**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="90e56-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="90e56-112">İstenen Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="90e56-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="90e56-113">Seçin **yapılandırma ve ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="90e56-113">Select **Configuration and policies**.</span></span>

    ![İlke ayarları dikey penceresini](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="90e56-115">**Yapılandırma ve ilkeleri** dikey belirleyebileceğiniz ayarlar menüsünü içerir.</span><span class="sxs-lookup"><span data-stu-id="90e56-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="90e56-116">Bu makalede yalnızca ayarlarını kapsar **kullanıcı başına sanal makineler** ve **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="90e56-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="90e56-117">Kalan ayarları hakkında bilgi için bkz: [Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetmek](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="90e56-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="90e56-118">Kullanıcı başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="90e56-118">Set virtual machines per user</span></span>
<span data-ttu-id="90e56-119">İlke için **kullanıcı başına sanal makineler** ayrı bir kullanıcı tarafından oluşturulan VM maksimum sayısını belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="90e56-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="90e56-120">Bir kullanıcı veya Kullanıcı sınırı sağlandığında VM talep oluşturmak üzere çalışırsa, oluşturulan ve istenen VM olamaz bir hata iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="90e56-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="90e56-121">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.</span><span class="sxs-lookup"><span data-stu-id="90e56-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="90e56-123">Seçin **Evet** kullanıcı başına VM'ler sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="90e56-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="90e56-124">Kullanıcı başına VM'ler sayısını sınırlamak istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="90e56-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="90e56-125">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler maksimum sayısını gösteren sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="90e56-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="90e56-126">Seçin **Evet** SSD (katı hal disk) kullanabilirsiniz VM'lerin sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="90e56-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="90e56-127">SSD kullanın, seçin VM'lerin sayısını sınırlamak istemiyorsanız **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="90e56-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="90e56-128">Seçerseniz **Evet**, SSD kullanılarak oluşturulan VM maksimum sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="90e56-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="90e56-129">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="90e56-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="90e56-130">Set otomatik-kapatma</span><span class="sxs-lookup"><span data-stu-id="90e56-130">Set auto-shutdown</span></span>
<span data-ttu-id="90e56-131">Bu Laboratuvar ait VM'ler kapatma süresi belirtmenize olanak tanıyarak Laboratuvar atık en aza indirmek için otomatik kapatma ilkesi yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="90e56-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="90e56-132">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="90e56-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Otomatik kapatma](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="90e56-134">Seçin **üzerinde** Bu ilkeyi etkinleştirmek için ve **kapalı** devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="90e56-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="90e56-135">Bu ilkeyi etkinleştirirseniz, geçerli laboratuarda tüm sanal makineleri kapatmaya saat (ve saat dilimi) belirtin.</span><span class="sxs-lookup"><span data-stu-id="90e56-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="90e56-136">Belirtin **Evet** veya **Hayır** belirtilen otomatik kapatma saatten önce 15 dakikada bir bildirim gönderme seçeneği için.</span><span class="sxs-lookup"><span data-stu-id="90e56-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="90e56-137">Belirtirseniz **Evet**, bildirim almak için bir Web kancası URL'si uç noktası girin.</span><span class="sxs-lookup"><span data-stu-id="90e56-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="90e56-138">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası veya API Azure işlevi oluşturma](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="90e56-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="90e56-139">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="90e56-139">Select **Save**.</span></span>

    <span data-ttu-id="90e56-140">Varsayılan olarak, bir kez etkinleştirildikten sonra geçerli laboratuarda tüm VM'ler için bu ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="90e56-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="90e56-141">Bu ayarı belirli bir sanal makineden kaldırmak için VM'ın dikey penceresini açın ve değiştirmek kendi **otomatik kapatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="90e56-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="90e56-142">Otomatik başlangıcı Ayarla</span><span class="sxs-lookup"><span data-stu-id="90e56-142">Set auto-start</span></span>
<span data-ttu-id="90e56-143">Otomatik başlatma ilkesi geçerli laboratuvara sanal makineleri yeniden başlatıldığında belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="90e56-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="90e56-144">Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik başlatma**.</span><span class="sxs-lookup"><span data-stu-id="90e56-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Otomatik başlatma](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="90e56-146">Seçin **üzerinde** Bu ilkeyi etkinleştirmek için ve **kapalı** devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="90e56-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="90e56-147">Bu ilkeyi etkinleştirirseniz, zamanlanmış başlangıç saati, saat dilimi ve saati geçerli olduğu için haftanın günlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="90e56-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="90e56-148">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="90e56-148">Select **Save**.</span></span>

    <span data-ttu-id="90e56-149">Etkinleştirildikten sonra bu ilkenin geçerli laboratuarda herhangi bir VM için otomatik olarak uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="90e56-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="90e56-150">Bu ayar için belirli bir VM'yi uygulamak için VM'ın dikey penceresini açın ve değiştirmek kendi **otomatik başlatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="90e56-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="90e56-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90e56-151">Next steps</span></span>

- <span data-ttu-id="90e56-152">[Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md) -diğer Laboratuvar ilkeleri değiştirmek öğrenin</span><span class="sxs-lookup"><span data-stu-id="90e56-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
