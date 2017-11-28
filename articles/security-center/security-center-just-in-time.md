---
title: "zaman sanal makinede aaaJust erişim Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge size nasıl yalnızca VM erişim denetimini Azure Güvenlik Merkezi yardımcı olur erişim tooyour Azure zamanında kılavuzluk sanal makineler."
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
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="3ef52-103">Tam zamanında kullanarak sanal makine erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="3ef52-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="3ef52-104">Yalnızca zaman sanal makine (VM) erişim gelen trafiği tooyour Azure VM'ler, gerektiğinde kolay erişim tooconnect tooVMs sağlarken Etkilenme tooattacks azaltma aşağı kullanılan toolock olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="3ef52-105">yalnızca zaman özellik Hello önizlemede hello Güvenlik Merkezi'nin standart katmanı üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="3ef52-106">Bkz: [fiyatlandırma](security-center-pricing.md) toolearn Güvenlik Merkezi hakkında daha fazla fiyatlandırma katmanları.</span><span class="sxs-lookup"><span data-stu-id="3ef52-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="3ef52-107">Saldırı senaryosu</span><span class="sxs-lookup"><span data-stu-id="3ef52-107">Attack scenario</span></span>

<span data-ttu-id="3ef52-108">Deneme yanılma saldırısı, yaygın olarak anlamına gelir toogain erişim tooa VM hedef yönetim noktaları saldırıları.</span><span class="sxs-lookup"><span data-stu-id="3ef52-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="3ef52-109">Başarılı olursa, bir saldırganın hello VM üzerinden denetimini ele geçirmek ve bir açısından ortamınıza oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3ef52-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="3ef52-110">Tek yönlü tooreduce Etkilenme tooa yanılma saldırısı toolimit hello bir bağlantı noktasının açık olduğundan zaman miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="3ef52-111">Yönetim bağlantı noktalarını gerek toobe açık her zaman yapın.</span><span class="sxs-lookup"><span data-stu-id="3ef52-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="3ef52-112">Yalnızca ihtiyaç duydukları toobe çalışırken bağlı toohello VM, örneğin tooperform Yönetimi veya bakım görevlerinin açıktır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="3ef52-113">Tam zamanında etkinleştirilmişse, Güvenlik Merkezi kullanır [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) saldırganlar tarafından hedeflenemez erişim toomanagement bağlantı noktalarını kısıtlamanız (NSG) kuralları.</span><span class="sxs-lookup"><span data-stu-id="3ef52-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Yalnızca zaman senaryoda][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="3ef52-115">Nasıl yalnızca süresi erişimi çalışıyor mu?</span><span class="sxs-lookup"><span data-stu-id="3ef52-115">How does just in time access work?</span></span>

<span data-ttu-id="3ef52-116">Tam zamanında etkinleştirilmişse, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM'ler gelen trafiği tooyour kilitler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="3ef52-117">Merhaba bağlantı noktalarını seçmek aşağı gelen trafiği üzerinde hello VM toowhich kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="3ef52-118">Bu bağlantı noktaları, yalnızca zaman çözümü hello tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="3ef52-119">Kullanıcı erişim tooa VM istediğinde, Güvenlik Merkezi hello kullanıcının sahip denetler [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure kaynak yazma erişimi sağlayan izinler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="3ef52-120">Yazma izinlerine sahip oldukları, hello isteğini onayladı ve Güvenlik Merkezi hello ağ güvenlik grupları (Nsg'ler) otomatik olarak yapılandırır tooallow hello süreyi belirttiğiniz için trafiği toohello yönetim bağlantı noktalarını gelen.</span><span class="sxs-lookup"><span data-stu-id="3ef52-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="3ef52-121">Merhaba süresi dolduktan sonra Güvenlik Merkezi hello Nsg'ler tootheir önceki durumlarına geri yükler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="3ef52-122">Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3ef52-123">Merhaba Klasik ve Resource Manager dağıtım modelleri hakkında daha fazla toolearn [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3ef52-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="3ef52-124">Yalnızca süresi erişimi kullanma</span><span class="sxs-lookup"><span data-stu-id="3ef52-124">Using just in time access</span></span>

<span data-ttu-id="3ef52-125">Merhaba **saat VM erişimi hemen** döşeme hello üzerinde **Güvenlik Merkezi** dikey penceresinde hello yalnızca zaman erişim ve hello sayısında hello geçen hafta yapılan onaylanan erişim istekleri için yapılandırılan VM sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="3ef52-126">Select hello **saat VM erişimi hemen** döşeme ve hello **saat VM erişimi hemen** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Tam zamanında VM erişim döşeme][2]

<span data-ttu-id="3ef52-128">Merhaba **saat VM erişimi hemen** dikey Vm'leriniz hello durumunu bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="3ef52-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="3ef52-129">**Yapılandırılmış** -zaman VM Access'te yalnızca yapılandırılan toosupport silinmiş VM'ler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="3ef52-130">sunulan hello veri Merhaba geçen hafta ve her VM hello sayısı onaylanan istekleri, son erişim tarihi ve saati ve son kullanıcı için içerir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="3ef52-131">**Önerilen** -Vm'lerini yalnızca süresi VM erişimi destekler ancak için yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="3ef52-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="3ef52-132">Yalnızca zaman VM erişim denetimi bu VM'ler için etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="3ef52-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="3ef52-133">Bkz: [yalnızca süresi VM erişimi etkinleştirmek](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="3ef52-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="3ef52-134">**Öneri yok** -VM önerilen toobe neden olabilir nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3ef52-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="3ef52-135">NSG - yalnızca zaman çözümü hello eksik bir NSG toobe yerinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="3ef52-136">Klasik VM - Güvenlik Merkezi'nde yalnızca zaman VM erişim şu anda yalnızca Azure Resource Manager aracılığıyla dağıtılan VM'ler destekler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3ef52-137">Klasik dağıtım hello yalnızca zaman çözümü tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3ef52-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="3ef52-138">Çözüm hello güvenlik ilkesinde hello abonelik veya kaynak grubu hello devre dışı zamanında Hello ya da bu hello VM genel IP eksik ve bir NSG yerinde yoksa diğer - bir VM bu kategorisindedir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="3ef52-139">Yalnızca bir yapılandırma saat erişim ilkesinde</span><span class="sxs-lookup"><span data-stu-id="3ef52-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="3ef52-140">tooselect hello tooenable istediğiniz sanal makineleri:</span><span class="sxs-lookup"><span data-stu-id="3ef52-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="3ef52-141">Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **önerilen** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3ef52-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Yalnızca süresi erişimi etkinleştir][3]

2. <span data-ttu-id="3ef52-143">Altında **VM'ler**, hello VM'ler tooenable istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="3ef52-144">Bir onay işareti sonraki tooa VM koyar.</span><span class="sxs-lookup"><span data-stu-id="3ef52-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="3ef52-145">Seçin **etkinleştirmek JIT vm'lerde**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="3ef52-146">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="3ef52-147">Varsayılan bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="3ef52-147">Default ports</span></span>

<span data-ttu-id="3ef52-148">Güvenlik Merkezi tam zamanında etkinleştirme önerir hello varsayılan bağlantı noktalarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ef52-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="3ef52-149">Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **önerilen** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3ef52-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Varsayılan bağlantı noktalarını görüntüle][6]

2. <span data-ttu-id="3ef52-151">Altında **VM'ler**, bir VM seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="3ef52-152">Bu bir onay işareti sonraki toohello VM ve açılır hello koyar **JIT VM erişim yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="3ef52-153">Bu dikey penceresinde hello varsayılan bağlantı noktalarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="3ef52-154">Bağlantı noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="3ef52-154">Add ports</span></span>

<span data-ttu-id="3ef52-155">Merhaba gelen **JIT VM erişim yapılandırması** dikey penceresinde de ekleyebilir ve tooenable hello yalnızca zaman çözümü istediğiniz yeni bir bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3ef52-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="3ef52-156">Merhaba üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, select **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="3ef52-157">Merhaba açılır **Ekle bağlantı noktası yapılandırmasını** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-157">This opens hello **Add port configuration** blade.</span></span>

  ![Bağlantı noktası yapılandırması][7]

2. <span data-ttu-id="3ef52-159">Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde hello kaynak IP'leri ve en fazla istek süresi izin verilen bağlantı noktası, protokol türü belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="3ef52-160">Kaynak IP izin onaylanmış bir istek üzerine hello IP aralıkları izin verilen tooget erişimi verilir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="3ef52-161">En fazla istek süresi belirli bir bağlantı noktasını açılabilir hello en uzun süre penceredir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="3ef52-162">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="3ef52-163">İstekte bulunan erişim tooa VM</span><span class="sxs-lookup"><span data-stu-id="3ef52-163">Requesting access tooa VM</span></span>

<span data-ttu-id="3ef52-164">toorequest erişim tooa VM:</span><span class="sxs-lookup"><span data-stu-id="3ef52-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="3ef52-165">Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **yapılandırıldı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3ef52-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="3ef52-166">Altında **VM'ler**, hello VM'ler tooenable erişim istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="3ef52-167">Bir onay işareti sonraki tooa VM koyar.</span><span class="sxs-lookup"><span data-stu-id="3ef52-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="3ef52-168">Seçin **erişim isteği**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-168">Select **Request access**.</span></span> <span data-ttu-id="3ef52-169">Merhaba açılır **erişim isteği** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-169">This opens hello **Request access** blade.</span></span>

  ![İstek erişim tooa VM][4]

4. <span data-ttu-id="3ef52-171">Merhaba üzerinde **erişim isteği** dikey penceresinde, yapılandırmanız için her VM hello bağlantı noktaları tooopen hello bağlantı noktası hello kaynak IP yanı sıra hangi hello için bağlantı noktası açıldığında tooand hello zaman penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="3ef52-172">Yalnızca zaman İlkesi'nde hello yapılandırılmış olan erişim yalnızca toohello bağlantı noktaları isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="3ef52-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="3ef52-173">Her bağlantı noktası yalnızca zaman İlkesi'nde hello türetilmiş bir maksimum izin verilen süre içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3ef52-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="3ef52-174">Seçin **bağlantı noktalarını açmak**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="3ef52-175">Yalnızca bir düzenleme zaman erişim ilkesinde</span><span class="sxs-lookup"><span data-stu-id="3ef52-175">Editing a just in time access policy</span></span>

<span data-ttu-id="3ef52-176">VM'in ekleyerek ve o VM için yeni bir bağlantı noktası tooopen yapılandırma yalnızca zaman ilkesinde varolan değiştirebilir veya başka bir parametre değiştirerek ilgili tooan zaten bağlantı noktası korumalı.</span><span class="sxs-lookup"><span data-stu-id="3ef52-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="3ef52-177">İçinde yalnızca bir VM zaman İlkesi'nde hello varolan tooedit sipariş **yapılandırıldı** sekmesi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="3ef52-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="3ef52-178">Altında **VM'ler**, VM tooadd hello üç nokta hello satır içinde o VM için tıklayarak bir bağlantı noktası tooby seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="3ef52-179">Bir menüdeki açılır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-179">This opens a menu.</span></span>
2. <span data-ttu-id="3ef52-180">Seçin **Düzenle** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3ef52-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="3ef52-181">Merhaba açılır **JIT VM erişim yapılandırması** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![İlkeyi Düzenle][8]

3. <span data-ttu-id="3ef52-183">Merhaba üzerinde **JIT VM erişim yapılandırması** dikey penceresinde, bağlantı noktası üzerinde tıklayarak ya da zaten korumalı bir bağlantı noktasının hello mevcut ayarları düzenleyebilirsiniz veya seçebilirsiniz **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="3ef52-184">Merhaba açılır **Ekle bağlantı noktası yapılandırmasını** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-184">This opens hello **Add port configuration** blade.</span></span>

  ![Bir bağlantı noktası ekleme][7]

4. <span data-ttu-id="3ef52-186">Üzerinde **Ekle bağlantı noktası yapılandırmasını** dikey penceresinde hello bağlantı noktası, protokol türü, izin verilen kaynak IP'leri ve en fazla istek süresi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3ef52-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="3ef52-187">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-187">Select **OK**.</span></span>
6. <span data-ttu-id="3ef52-188">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="3ef52-189">Yalnızca zaman erişim etkinliğinde denetleme</span><span class="sxs-lookup"><span data-stu-id="3ef52-189">Auditing just in time access activity</span></span>

<span data-ttu-id="3ef52-190">Günlük arama kullanarak VM etkinlikleri Öngörüler elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ef52-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="3ef52-191">tooview günlükleri:</span><span class="sxs-lookup"><span data-stu-id="3ef52-191">tooview logs:</span></span>

1. <span data-ttu-id="3ef52-192">Merhaba üzerinde **saat VM erişimi hemen** dikey penceresinde, select hello **yapılandırıldı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3ef52-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="3ef52-193">Altında **VM'ler**, o VM için hello üç nokta hello satır içinde tıklayarak hakkında VM tooview bilgileri seçin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="3ef52-194">Bir menüdeki açılır.</span><span class="sxs-lookup"><span data-stu-id="3ef52-194">This opens a menu.</span></span>
3. <span data-ttu-id="3ef52-195">Seçin **etkinlik günlüğü** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="3ef52-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="3ef52-196">Merhaba açılır **etkinlik günlüğü** dikey.</span><span class="sxs-lookup"><span data-stu-id="3ef52-196">This opens hello **Activity log** blade.</span></span>

![Etkinlik günlüğü seçin][9]

<span data-ttu-id="3ef52-198">Merhaba **etkinlik günlüğü** dikey önceki işlem saati, tarih ve abonelik ile birlikte bu VM için filtre uygulanmış bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ef52-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Etkinlik Günlüğü Görüntüle][5]

<span data-ttu-id="3ef52-200">Seçerek hello günlük bilgilerini indirebilirsiniz **toodownload CSV olarak tüm hello öğeleri burayı**.</span><span class="sxs-lookup"><span data-stu-id="3ef52-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="3ef52-201">Merhaba filtreleri değiştirmek ve seçin **Uygula** toocreate arama ve günlük.</span><span class="sxs-lookup"><span data-stu-id="3ef52-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="3ef52-202">Tam zamanında PowerShell aracılığıyla VM erişim kullanma</span><span class="sxs-lookup"><span data-stu-id="3ef52-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="3ef52-203">PowerShell aracılığıyla zaman çözümde hemen sipariş toouse hello içinde hello olduğundan emin olun [son](/powershell/azure/install-azurerm-ps) Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="3ef52-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="3ef52-204">Bunu yaptığınızda tooinstall hello gereksinim [son](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Güvenlik Merkezi'nden hello PowerShell Galerisi.</span><span class="sxs-lookup"><span data-stu-id="3ef52-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="3ef52-205">Yalnızca bir yapılandırma bir VM için zaman İlkesi</span><span class="sxs-lookup"><span data-stu-id="3ef52-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="3ef52-206">tooconfigure bir yalnızca belirli bir VM'de zaman ilkesinde toorun bu komut PowerShell oturumunuzda ihtiyacınız: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="3ef52-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="3ef52-207">Merhaba cmdlet belgeleri toolearn daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="3ef52-208">İstekte bulunan erişim tooa VM</span><span class="sxs-lookup"><span data-stu-id="3ef52-208">Requesting access tooa VM</span></span>

<span data-ttu-id="3ef52-209">tooaccess ile korunan belirli bir VM'yi Merhaba yalnızca zaman çözümde, PowerShell oturumunuzda bu komut toorun gerekir: çağırma ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="3ef52-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="3ef52-210">Merhaba cmdlet belgeleri toolearn daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ef52-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ef52-211">Next steps</span></span>
<span data-ttu-id="3ef52-212">Bu makalede, nasıl tam zamanında VM erişim Güvenlik Merkezi yardımcı olur erişim tooyour Azure denetim öğrenilen sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="3ef52-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="3ef52-213">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="3ef52-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="3ef52-214">[Güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="3ef52-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="3ef52-215">[Güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="3ef52-216">[Güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="3ef52-217">[Yönetme ve toosecurity uyarıları yanıt](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="3ef52-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="3ef52-218">[İş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3ef52-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="3ef52-219">[Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ef52-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="3ef52-220">[Azure Güvenlik blogu](https://blogs.msdn.microsoft.com/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ef52-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
