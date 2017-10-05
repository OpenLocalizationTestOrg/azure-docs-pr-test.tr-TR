---
title: "Yalnızca zaman sanal makineye erişim Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Size nasıl tam zamanında VM erişim Azure Güvenlik Merkezi yardımcı olur, bu belge yetenekte Azure sanal makinelerinizi erişimi denetler."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="5aa66-103">Tam zamanında kullanarak sanal makine erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="5aa66-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="5aa66-104">Yalnızca zaman sanal makine (VM) erişim gerektiğinde VM'ler bağlamak için kolay erişim sağlarken saldırılara maruz kalma azaltma, Azure vm'lerine gelen trafik kilitlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa66-105">Özellik önizlemededir zaman yalnızca ve Güvenlik Merkezi'nin standart katmanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="5aa66-106">Bkz: [fiyatlandırma](security-center-pricing.md) Güvenlik Merkezi hakkında daha fazla katmanları fiyatlandırma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="5aa66-107">Saldırı senaryosu</span><span class="sxs-lookup"><span data-stu-id="5aa66-107">Attack scenario</span></span>

<span data-ttu-id="5aa66-108">Deneme yanılma saldırısı hedef yönetim noktaları VM erişmek için bir yol olarak sık saldırıları.</span><span class="sxs-lookup"><span data-stu-id="5aa66-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="5aa66-109">Başarılı olursa, bir saldırganın VM üzerinden denetimini ele geçirmek ve bir açısından ortamınıza oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5aa66-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="5aa66-110">Saldırılarına maruz azaltmak için tek bir bağlantı noktasının açık olduğundan süre miktarını sınırlamak için bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="5aa66-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="5aa66-111">Yönetim bağlantı noktalarını her zaman açık olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5aa66-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="5aa66-112">Bunlar yalnızca VM Yönetimi veya bakım görevleri gerçekleştirmek örnek için bağlıyken açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="5aa66-113">Tam zamanında etkinleştirilmişse, Güvenlik Merkezi kullanır [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) saldırganlar tarafından hedeflenemez, yönetim bağlantı noktalarına erişimi sınırlayan (NSG) kuralları.</span><span class="sxs-lookup"><span data-stu-id="5aa66-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Yalnızca zaman senaryoda][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="5aa66-115">Nasıl yalnızca süresi erişimi çalışıyor mu?</span><span class="sxs-lookup"><span data-stu-id="5aa66-115">How does just in time access work?</span></span>

<span data-ttu-id="5aa66-116">Tam zamanında etkinleştirildiğinde, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM’lere gelen trafiği kilitler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="5aa66-117">Aşağı gelen trafik için kilitlenir VM bağlantı noktalarını seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="5aa66-118">Bu bağlantı noktaları yalnızca tarafından denetlenen zaman çözümde.</span><span class="sxs-lookup"><span data-stu-id="5aa66-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="5aa66-119">Bir kullanıcı bir VM erişim istediğinde, Güvenlik Merkezi kullanıcının sahip olduğunu denetler [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) için Azure kaynağını yazma erişimi sağlayan izinler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="5aa66-120">Belirtilen yazma izinlerine sahip oldukları isteğini onayladı ve Güvenlik Merkezi ağ güvenlik zaman miktarı yönetim bağlantı noktalarına gelen trafiğe izin verecek şekilde grupları (Nsg'ler) otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5aa66-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="5aa66-121">Güvenlik Merkezi Nsg'ler süresi dolduktan sonra önceki durumlarına geri yükler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa66-122">Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="5aa66-123">Klasik ve Resource Manager dağıtım modelleri hakkında daha fazla bilgi için [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5aa66-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="5aa66-124">Yalnızca süresi erişimi kullanma</span><span class="sxs-lookup"><span data-stu-id="5aa66-124">Using just in time access</span></span>

<span data-ttu-id="5aa66-125">**Saat VM erişimi hemen** döşemesinin **Güvenlik Merkezi** dikey zamanı erişimi ve onaylanan erişim isteklerinin sayısı yalnızca son bir hafta içinde yapılan için yapılandırılan VM sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="5aa66-126">Seçin **saat VM erişimi hemen** döşeme ve **saat VM erişimi hemen** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5aa66-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Tam zamanında VM erişim döşeme][2]

<span data-ttu-id="5aa66-128">**Saat VM erişimi hemen** dikey Vm'leriniz durumu hakkında bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="5aa66-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="5aa66-129">**Yapılandırılmış** -yalnızca zaman VM erişimini desteklemek üzere yapılandırılmış VM'ler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="5aa66-130">Sunulan veriler son hafta ve her VM için onaylanan istekleri, son erişim tarihi ve saati ve son kullanıcı sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="5aa66-131">**Önerilen** -Vm'lerini yalnızca süresi VM erişimi destekler ancak için yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="5aa66-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="5aa66-132">Yalnızca zaman VM erişim denetimi bu VM'ler için etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="5aa66-133">Bkz: [yalnızca süresi VM erişimi etkinleştirmek](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="5aa66-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="5aa66-134">**Öneri yok** -önerilmez için bir VM neden nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5aa66-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="5aa66-135">NSG - yalnızca eksik zamanında çözüm bir NSG yerinde olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="5aa66-136">Klasik VM - Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="5aa66-137">Klasik dağıtım yalnızca tarafından desteklenmeyen zaman çözümde.</span><span class="sxs-lookup"><span data-stu-id="5aa66-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="5aa66-138">Bu kategorideki diğer - bir VM olan ise yalnızca çözüm kapalı abonelik veya kaynak grubu ya da, güvenlik ilkesi zaman VM, bir ortak IP eksik ve bir NSG yerinde sahip değil.</span><span class="sxs-lookup"><span data-stu-id="5aa66-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="5aa66-139">Yalnızca bir yapılandırma saat erişim ilkesinde</span><span class="sxs-lookup"><span data-stu-id="5aa66-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="5aa66-140">Etkinleştirmek istediğiniz sanal makineleri seçmek için:</span><span class="sxs-lookup"><span data-stu-id="5aa66-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="5aa66-141">Üzerinde **saat VM erişimi hemen** dikey penceresinde, select **önerilen** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Yalnızca süresi erişimi etkinleştir][3]

2. <span data-ttu-id="5aa66-143">Altında **VM'ler**, etkinleştirmek istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="5aa66-144">Bir VM yanında bir onay işareti koyar.</span><span class="sxs-lookup"><span data-stu-id="5aa66-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="5aa66-145">Seçin **etkinleştirmek JIT vm'lerde**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="5aa66-146">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="5aa66-147">Varsayılan bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="5aa66-147">Default ports</span></span>

<span data-ttu-id="5aa66-148">Güvenlik Merkezi tam zamanında etkinleştirme önerir varsayılan bağlantı noktalarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="5aa66-149">Üzerinde **saat VM erişimi hemen** dikey penceresinde, select **önerilen** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Varsayılan bağlantı noktalarını görüntüle][6]

2. <span data-ttu-id="5aa66-151">Altında **VM'ler**, bir VM seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="5aa66-152">Bu VM yanında bir onay işareti koyar ve açılır **JIT VM erişim yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="5aa66-153">Bu dikey varsayılan bağlantı noktalarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5aa66-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="5aa66-154">Bağlantı noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="5aa66-154">Add ports</span></span>

<span data-ttu-id="5aa66-155">Gelen **JIT VM erişim yapılandırması** dikey penceresinde, ayrıca eklemek ve yapılandırmak istediğiniz yalnızca etkinleştirmek yeni bir bağlantı noktası zaman çözümde.</span><span class="sxs-lookup"><span data-stu-id="5aa66-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="5aa66-156">Üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, select **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="5aa66-157">Bu açılır **Ekle bağlantı noktası yapılandırmasını** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-157">This opens the **Add port configuration** blade.</span></span>

  ![Bağlantı noktası yapılandırması][7]

2. <span data-ttu-id="5aa66-159">Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde, sizi tanımlamak bağlantı noktası, izin verilen kaynak IP'leri ve en fazla istek süresi protokol türü.</span><span class="sxs-lookup"><span data-stu-id="5aa66-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="5aa66-160">İzin verilen IP kaynağıdır onaylanmış bir istek üzerine erişmek için izin verilen IP aralıkları.</span><span class="sxs-lookup"><span data-stu-id="5aa66-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="5aa66-161">En fazla istek süresi, belirli bir bağlantı noktasını açılabilir en uzun süre penceredir.</span><span class="sxs-lookup"><span data-stu-id="5aa66-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="5aa66-162">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="5aa66-163">Bir VM erişim isteyen</span><span class="sxs-lookup"><span data-stu-id="5aa66-163">Requesting access to a VM</span></span>

<span data-ttu-id="5aa66-164">Bir VM erişim istemek için:</span><span class="sxs-lookup"><span data-stu-id="5aa66-164">To request access to a VM:</span></span>

1. <span data-ttu-id="5aa66-165">Üzerinde **saat VM erişimi hemen** dikey penceresinde, select **yapılandırıldı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="5aa66-166">Altında **VM'ler**, erişimini etkinleştirmek istediğiniz sanal makineleri seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="5aa66-167">Bir VM yanında bir onay işareti koyar.</span><span class="sxs-lookup"><span data-stu-id="5aa66-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="5aa66-168">Seçin **erişim isteği**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-168">Select **Request access**.</span></span> <span data-ttu-id="5aa66-169">Bu açılır **erişim isteği** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-169">This opens the **Request access** blade.</span></span>

  ![Erişim isteğinde bulunmak için bir VM][4]

4. <span data-ttu-id="5aa66-171">Üzerinde **erişim isteği** dikey penceresinde, yapılandırdığınız her VM için bağlantı noktası için açılmış kaynak IP ve bağlantı noktası açıldığı zaman penceresi birlikte açmak için bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="5aa66-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="5aa66-172">Yalnızca içinde yapılandırılmış olan bağlantı noktalarına erişim isteğinde bulunabileceği zaman ilkesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="5aa66-173">Her bağlantı noktası yalnızca türetilen süresi izin verilen maksimum olan zaman ilkesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="5aa66-174">Seçin **bağlantı noktalarını açmak**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="5aa66-175">Yalnızca bir düzenleme zaman erişim ilkesinde</span><span class="sxs-lookup"><span data-stu-id="5aa66-175">Editing a just in time access policy</span></span>

<span data-ttu-id="5aa66-176">VM'in yalnızca zaman ilkesinde varolan ekleyerek ve o VM için açmak için yeni bir bağlantı noktası yapılandırma ya da zaten korumalı bir bağlantı noktasına ilgili herhangi bir parametre değiştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="5aa66-177">Varolan yalnızca bir VM zaman İlkesi'nde düzenlemek için **yapılandırıldı** sekmesi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="5aa66-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="5aa66-178">Altında **VM'ler**, o VM için üç nokta satırdaki tıklayarak bir bağlantı noktası eklemek için VM seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="5aa66-179">Bir menüdeki açılır.</span><span class="sxs-lookup"><span data-stu-id="5aa66-179">This opens a menu.</span></span>
2. <span data-ttu-id="5aa66-180">Seçin **Düzenle** menüde.</span><span class="sxs-lookup"><span data-stu-id="5aa66-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="5aa66-181">Bu açılır **JIT VM erişim yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![İlkeyi Düzenle][8]

3. <span data-ttu-id="5aa66-183">Üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, bağlantı noktası üzerinde tıklayarak ya da zaten korumalı olan bir bağlantı noktası var olan ayarları düzenleyebilirsiniz veya seçebilirsiniz **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="5aa66-184">Bu açılır **Ekle bağlantı noktası yapılandırmasını** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-184">This opens the **Add port configuration** blade.</span></span>

  ![Bir bağlantı noktası ekleme][7]

4. <span data-ttu-id="5aa66-186">Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde, bağlantı noktası, protokol türü, izin verilen kaynak IP'leri ve en fazla istek süresi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5aa66-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="5aa66-187">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-187">Select **OK**.</span></span>
6. <span data-ttu-id="5aa66-188">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="5aa66-189">Yalnızca zaman erişim etkinliğinde denetleme</span><span class="sxs-lookup"><span data-stu-id="5aa66-189">Auditing just in time access activity</span></span>

<span data-ttu-id="5aa66-190">Günlük arama kullanarak VM etkinlikleri Öngörüler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="5aa66-191">Günlükleri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="5aa66-191">To view logs:</span></span>

1. <span data-ttu-id="5aa66-192">Üzerinde **saat VM erişimi hemen** dikey penceresinde, select **yapılandırıldı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5aa66-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="5aa66-193">Altında **VM'ler**, o VM için üç nokta satırdaki tıklayarak ilgili bilgileri görüntülemek için VM seçin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="5aa66-194">Bir menüdeki açılır.</span><span class="sxs-lookup"><span data-stu-id="5aa66-194">This opens a menu.</span></span>
3. <span data-ttu-id="5aa66-195">Seçin **etkinlik günlüğü** menüde.</span><span class="sxs-lookup"><span data-stu-id="5aa66-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="5aa66-196">Bu açılır **etkinlik günlüğü** dikey.</span><span class="sxs-lookup"><span data-stu-id="5aa66-196">This opens the **Activity log** blade.</span></span>

![Etkinlik günlüğü seçin][9]

<span data-ttu-id="5aa66-198">**Etkinlik günlüğü** dikey önceki işlem saati, tarih ve abonelik ile birlikte bu VM için filtre uygulanmış bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa66-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Etkinlik Günlüğü Görüntüle][5]

<span data-ttu-id="5aa66-200">Günlük bilgilerini seçerek yükleyebilirsiniz **tüm öğeler CSV olarak indirmek için buraya tıklayın**.</span><span class="sxs-lookup"><span data-stu-id="5aa66-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="5aa66-201">Seç ve filtreleri değiştirmek **Uygula** bir arama ve günlük oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5aa66-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="5aa66-202">Tam zamanında PowerShell aracılığıyla VM erişim kullanma</span><span class="sxs-lookup"><span data-stu-id="5aa66-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="5aa66-203">Yalnızca kullanmak için PowerShell aracılığıyla zaman çözümde olduğundan emin olun [son](/powershell/azure/install-azurerm-ps) Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="5aa66-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="5aa66-204">Bunu yaptığınızda, yüklemek gereken [son](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Güvenlik Merkezi PowerShell Galerisi'nden.</span><span class="sxs-lookup"><span data-stu-id="5aa66-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="5aa66-205">Yalnızca bir yapılandırma bir VM için zaman İlkesi</span><span class="sxs-lookup"><span data-stu-id="5aa66-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="5aa66-206">Bir yalnızca yapılandırmak için PowerShell oturumunda bu komutu çalıştırmak gereken belirli bir VM'de zaman ilkesinde: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="5aa66-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="5aa66-207">Daha fazla bilgi için cmdlet belgeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="5aa66-208">Bir VM erişim isteyen</span><span class="sxs-lookup"><span data-stu-id="5aa66-208">Requesting access to a VM</span></span>

<span data-ttu-id="5aa66-209">Yalnızca ile korunan belirli bir VM'yi erişmek için PowerShell oturumunda bu komutu çalıştırmak gereken zaman çözümde: çağırma ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="5aa66-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="5aa66-210">Daha fazla bilgi için cmdlet belgeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5aa66-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5aa66-211">Next steps</span></span>
<span data-ttu-id="5aa66-212">Bu makalede, nasıl tam zamanında VM erişim Güvenlik Merkezi yardımcı olur, Azure sanal makineleriniz için erişim denetim öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="5aa66-213">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="5aa66-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="5aa66-214">[Güvenlik ilkelerini ayarlama](security-center-policies.md) — Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="5aa66-215">[Güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="5aa66-216">[Güvenlik durumunu izleme](security-center-monitoring.md) — Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="5aa66-217">[Yönetme ve güvenlik uyarılarını yanıt](security-center-managing-and-responding-alerts.md) — yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="5aa66-218">[İş ortağı çözümlerini izleme](security-center-partner-solutions.md) — iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5aa66-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="5aa66-219">[Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="5aa66-220">[Azure Güvenlik blogu](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa66-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
