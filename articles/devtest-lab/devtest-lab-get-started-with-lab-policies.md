---
title: Azure DevTest Labs aaaManage temel Laboratuvar ilkeleri | Microsoft Docs
description: "Bilgi nasıl tooset bazı DevTest Labs laboratuvarda için hello temel ilkeleri (ayarlar)"
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
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="7a768-103">Azure DevTest Labs laboratuvarda için temel ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7a768-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="7a768-104">Azure DevTest Labs, ortamlarındaki atık ilkeleri (ayarlar) yöneterek her Laboratuvar için en aza indirmek ve toocontrol maliyeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a768-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="7a768-105">Bu makalede, nasıl tooset iki hello en kritik ilkeleri - sınırlama sayısı hello öğrenerek ilkelerini kullanmaya başlama sanal oluşturduğunuz ya da bir tek kullanıcı ve yapılandırılırken otomatik kapatma tarafından talep makineler (VM).</span><span class="sxs-lookup"><span data-stu-id="7a768-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="7a768-106">tooview nasıl tooset her Laboratuvar ilke hello makalesine bakın [Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7a768-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="7a768-107">Azure DevTest Labs Laboratuvar 's ilkelerinde erişme</span><span class="sxs-lookup"><span data-stu-id="7a768-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="7a768-108">Merhaba aşağıdaki adımlar, Azure DevTest Labs laboratuvarda ilkelerini kurma yol:</span><span class="sxs-lookup"><span data-stu-id="7a768-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="7a768-109">tooview (ve değişiklik) hello ilkeleri bir laboratuvar için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7a768-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="7a768-110">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7a768-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="7a768-111">Seçin **daha fazla hizmet**ve ardından **DevTest Labs** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="7a768-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="7a768-112">Merhaba istenen Laboratuvar labs Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="7a768-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="7a768-113">Seçin **yapılandırma ve ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="7a768-113">Select **Configuration and policies**.</span></span>

    ![İlke ayarları dikey penceresini](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="7a768-115">Merhaba **yapılandırma ve ilkeleri** dikey belirleyebileceğiniz ayarlar menüsünü içerir.</span><span class="sxs-lookup"><span data-stu-id="7a768-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="7a768-116">Bu makalede yalnızca hello ayarlarını kapsar **kullanıcı başına sanal makineler** ve **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="7a768-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="7a768-117">toolearn ayarları, kalan hello hakkında bkz [Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetmek](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7a768-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="7a768-118">Kullanıcı başına kümesi sanal makineler</span><span class="sxs-lookup"><span data-stu-id="7a768-118">Set virtual machines per user</span></span>
<span data-ttu-id="7a768-119">Hello İlkesi **kullanıcı başına sanal makineler** toospecify hello en fazla ayrı bir kullanıcı tarafından oluşturulan VM'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a768-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="7a768-120">Merhaba Kullanıcı sınırı sağlandığında bir kullanıcı toocreate veya talep VM çalışırsa, bir hata iletisi VM oluşturulan/talep edilemez edilmesine bu hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="7a768-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="7a768-121">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** menüsünde, select **kullanıcı başına sanal makineler**.</span><span class="sxs-lookup"><span data-stu-id="7a768-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Kullanıcı başına sanal makineler](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="7a768-123">Seçin **Evet** toolimit hello VM'lerin sayısını kullanıcı başına.</span><span class="sxs-lookup"><span data-stu-id="7a768-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="7a768-124">Kullanıcı başına VM'ler toolimit hello numarasını istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="7a768-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="7a768-125">Seçerseniz **Evet**, oluşturduğunuz ya da bir kullanıcı tarafından talep VM'ler hello sayısını belirten sayısal bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="7a768-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="7a768-126">Seçin **Evet** toolimit hello SSD (katı hal disk) kullanabilirsiniz VM sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a768-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="7a768-127">Toolimit hello SSD kullanabilirsiniz VM'lerin sayısını istemiyorsanız seçin **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="7a768-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="7a768-128">Seçerseniz **Evet**, SSD kullanılarak oluşturulabilir VM'ler hello sayısını belirten bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="7a768-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="7a768-129">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7a768-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="7a768-130">Set otomatik-kapatma</span><span class="sxs-lookup"><span data-stu-id="7a768-130">Set auto-shutdown</span></span>
<span data-ttu-id="7a768-131">Merhaba otomatik kapatma ilke bu Laboratuvar ait VM'ler kapatma toospecify hello zaman sağlayarak boşa harcanmasına toominimize Laboratuvar yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7a768-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="7a768-132">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik kapatma**.</span><span class="sxs-lookup"><span data-stu-id="7a768-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Otomatik kapatma](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="7a768-134">Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.</span><span class="sxs-lookup"><span data-stu-id="7a768-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="7a768-135">Bu ilkeyi etkinleştirirseniz, tüm VM'ler aşağı hello saat (ve saat dilimi) tooshut hello geçerli laboratuvarda belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a768-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="7a768-136">Belirtin **Evet** veya **Hayır** hello seçeneği toosend için otomatik kapatma süresi bir bildirim 15 dakika önceki toohello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="7a768-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="7a768-137">Belirtirseniz **Evet**, bir Web kancası URL'si uç nokta tooreceive hello bildirim girin.</span><span class="sxs-lookup"><span data-stu-id="7a768-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="7a768-138">Web kancası hakkında daha fazla bilgi için bkz: [bir Web kancası veya API Azure işlevi oluşturma](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="7a768-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="7a768-139">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7a768-139">Select **Save**.</span></span>

    <span data-ttu-id="7a768-140">Etkinleştirildiğinde, varsayılan olarak, bu ilke tooall VM'ler hello geçerli laboratuarda uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7a768-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="7a768-141">Bu ayar için belirli bir VM'yi tooremove açmak hello VM'in dikey penceresinde ve değişiklik kendi **otomatik kapatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="7a768-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="7a768-142">Otomatik başlangıcı Ayarla</span><span class="sxs-lookup"><span data-stu-id="7a768-142">Set auto-start</span></span>
<span data-ttu-id="7a768-143">Merhaba VM'ler hello geçerli laboratuarda yeniden başlatıldığında hello otomatik başlatma ilkesi, toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a768-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="7a768-144">Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** dikey penceresinde, select **otomatik başlatma**.</span><span class="sxs-lookup"><span data-stu-id="7a768-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Otomatik başlatma](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="7a768-146">Seçin **üzerinde** tooenable Bu ilkeyi ve **kapalı** toodisable onu.</span><span class="sxs-lookup"><span data-stu-id="7a768-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="7a768-147">Bu ilkeyi etkinleştirirseniz, hello zamanlanmış başlangıç saati, saat dilimi ve hello için hangi hello zaman geçerlidir hello haftanın günleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a768-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="7a768-148">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="7a768-148">Select **Save**.</span></span>

    <span data-ttu-id="7a768-149">Etkinleştirildikten sonra bu ilke otomatik olarak uygulanan tooany VM'ler hello geçerli laboratuvarda değil.</span><span class="sxs-lookup"><span data-stu-id="7a768-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="7a768-150">tooapply bu ayarı tooa belirli VM, açık hello VM'in dikey ve değişiklik kendi **otomatik başlatma** ayarı</span><span class="sxs-lookup"><span data-stu-id="7a768-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7a768-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a768-151">Next steps</span></span>

- <span data-ttu-id="7a768-152">[Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar](devtest-lab-set-lab-policy.md) -öğrenin nasıl toomodify diğer Laboratuvar ilkeleri</span><span class="sxs-lookup"><span data-stu-id="7a768-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
