---
title: "aaaService Azure Batch için kotalar ve sınırlar | Microsoft Docs"
description: "Varsayılan Azure Batch kotalar, sınırları ve kısıtlamaları ve nasıl toorequest kota artırır hakkında bilgi edinin"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="5f5ab-103">Batch hizmet kotaları ve limitleri</span><span class="sxs-lookup"><span data-stu-id="5f5ab-103">Batch service quotas and limits</span></span>

<span data-ttu-id="5f5ab-104">Olarak diğer Azure hizmetleriyle sınırlar vardır hello Batch hizmeti ile ilişkilendirilmiş belirli kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="5f5ab-105">Çoğu bu sınırları hello aboneliği veya hesabı düzeyinde Azure tarafından uygulanan varsayılan kotaları bulunur.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="5f5ab-106">Bu makalede bu Varsayılanları ele ve kota nasıl istek artırır.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="5f5ab-107">Batch iş yüklerinizi tasarlayıp ölçeğini artırırken kotaları göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="5f5ab-108">Havuzunuzu hello hedef işlem düğümleri, belirttiğiniz sayısına eriştikten değil, örneğin, hello çekirdek kota Batch hesabınıza veya bölgesel VM çekirdek kota için aboneliğiniz için sınırına ulaştınız.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="5f5ab-109">Tek bir Batch hesabında birden fazla toplu iş yüklerini çalıştırmak veya iş yüklerinizi hello Batch hesapları arasında dağıtabilirsiniz aynı abonelik, ancak farklı Azure bölgelerinde.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="5f5ab-110">Toplu toorun üretim iş yükleri planlıyorsanız, bir veya daha fazla hello kotaları hello varsayılan yukarıda tooincrease gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="5f5ab-111">Tooraise kota istiyorsanız, çevrimiçi açabilirsiniz [müşteri destek isteği](#increase-a-quota) herhangi bir ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="5f5ab-112">Bir kota kapasitesi garantisi bir kredi sınırı ' dir.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="5f5ab-113">Büyük ölçekli kapasite gereksinimlerini varsa, lütfen Azure desteğine başvurun.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="5f5ab-114">Kaynak kotaları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="5f5ab-115">Kullanıcı abonelik modunda kotaları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="5f5ab-116">Toplu işlem hesabı havuzu ayırma moduyla çok ayarlamak için**kullanıcı aboneliği**, Vm'leri ve depolama hesapları gibi başka kaynaklar toplu işlem, bir havuz oluşturduğunuzda, aboneliğinizde doğrudan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="5f5ab-117">Bu modda oluşturulan tooan hesabı Hello Azure Batch çekirdek kota geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="5f5ab-118">Bunun yerine, bölgesel işlem çekirdek ve diğer kaynakları aboneliğinizin hello kotaları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="5f5ab-119">Bu Kotalar hakkında daha fazla bilgi [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ab-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="5f5ab-120">Kaynak kullanımı kullanıcı abonelik modunda oluşturulan bir hesap için planlama yaparken, toplu işlem kaynaklarında (toplama toocompute çekirdekler) aşağıdaki Not hello her 40 Linux VM'ler veya 20 Windows VM'ler için gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="5f5ab-121">Kaynak</span><span class="sxs-lookup"><span data-stu-id="5f5ab-121">Resource</span></span> | <span data-ttu-id="5f5ab-122">Kota</span><span class="sxs-lookup"><span data-stu-id="5f5ab-122">Quota</span></span> | <span data-ttu-id="5f5ab-123">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="5f5ab-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="5f5ab-124">Bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="5f5ab-124">One storage account</span></span> | <span data-ttu-id="5f5ab-125">Depolama Hesapları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-125">Storage Accounts</span></span> | <span data-ttu-id="5f5ab-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="5f5ab-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="5f5ab-127">Bir genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="5f5ab-127">One public IP address</span></span> | <span data-ttu-id="5f5ab-128">Genel IP Adresleri</span><span class="sxs-lookup"><span data-stu-id="5f5ab-128">Public IP Addresses</span></span> | <span data-ttu-id="5f5ab-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="5f5ab-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="5f5ab-130">Bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="5f5ab-130">One virtual network</span></span> | <span data-ttu-id="5f5ab-131">Sanal Ağlar</span><span class="sxs-lookup"><span data-stu-id="5f5ab-131">Virtual Networks</span></span> | <span data-ttu-id="5f5ab-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="5f5ab-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="5f5ab-133">Bir ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="5f5ab-133">One network security group</span></span> | <span data-ttu-id="5f5ab-134">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-134">Network Security Groups</span></span> | <span data-ttu-id="5f5ab-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="5f5ab-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="5f5ab-136">Bir sanal makine ölçek kümesi</span><span class="sxs-lookup"><span data-stu-id="5f5ab-136">One virtual machine scale set</span></span> | <span data-ttu-id="5f5ab-137">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="5f5ab-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="5f5ab-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="5f5ab-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="5f5ab-139">Bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="5f5ab-139">One load balancer</span></span> | <span data-ttu-id="5f5ab-140">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="5f5ab-140">Load Balancers</span></span> | <span data-ttu-id="5f5ab-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="5f5ab-141">Microsoft.Network</span></span> | 

<span data-ttu-id="5f5ab-142">Merhaba çekirdek kota bölgesel düzeyinde ya da VM ailesi başına Batch havuzu veya havuzları için gerekli kümesi according toohello VM boyutu olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="5f5ab-143">Kota</span><span class="sxs-lookup"><span data-stu-id="5f5ab-143">Quota</span></span> | <span data-ttu-id="5f5ab-144">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="5f5ab-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="5f5ab-145">Toplam bölgesel çekirdek</span><span class="sxs-lookup"><span data-stu-id="5f5ab-145">Total Regional Cores</span></span> | <span data-ttu-id="5f5ab-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="5f5ab-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="5f5ab-147">…</span><span class="sxs-lookup"><span data-stu-id="5f5ab-147">…</span></span> <span data-ttu-id="5f5ab-148">Aile çekirdek</span><span class="sxs-lookup"><span data-stu-id="5f5ab-148">Family Cores</span></span> | <span data-ttu-id="5f5ab-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="5f5ab-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="5f5ab-150">Diğer sınırları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-150">Other limits</span></span>
| <span data-ttu-id="5f5ab-151">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="5f5ab-151">**Resource**</span></span> | <span data-ttu-id="5f5ab-152">**Üst Sınır**</span><span class="sxs-lookup"><span data-stu-id="5f5ab-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="5f5ab-153">[Eş zamanlı görevleri](batch-parallel-node-tasks.md) işlem düğümü başına</span><span class="sxs-lookup"><span data-stu-id="5f5ab-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="5f5ab-154">düğüm çekirdeği 4 x sayısı</span><span class="sxs-lookup"><span data-stu-id="5f5ab-154">4 x number of node cores</span></span> |
| <span data-ttu-id="5f5ab-155">[Uygulamaları](batch-application-packages.md) toplu işlem hesabı başına</span><span class="sxs-lookup"><span data-stu-id="5f5ab-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="5f5ab-156">20</span><span class="sxs-lookup"><span data-stu-id="5f5ab-156">20</span></span> |
| <span data-ttu-id="5f5ab-157">Uygulama başına uygulama paketleri</span><span class="sxs-lookup"><span data-stu-id="5f5ab-157">Application packages per application</span></span> |<span data-ttu-id="5f5ab-158">40</span><span class="sxs-lookup"><span data-stu-id="5f5ab-158">40</span></span> |
| <span data-ttu-id="5f5ab-159">Uygulama paketi boyutu (her)</span><span class="sxs-lookup"><span data-stu-id="5f5ab-159">Application package size (each)</span></span> |<span data-ttu-id="5f5ab-160">Yaklaşık 195 GB'den<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="5f5ab-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="5f5ab-161">En fazla başlangıç görevi boyutu</span><span class="sxs-lookup"><span data-stu-id="5f5ab-161">Maximum start task size</span></span> | <span data-ttu-id="5f5ab-162">32768 karakter<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="5f5ab-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="5f5ab-163"><sup>1</sup> en büyük blok blob boyutu için azure depolama sınırı</span><span class="sxs-lookup"><span data-stu-id="5f5ab-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="5f5ab-164">
<sup>2</sup> kaynak dosyaları ve ortam değişkenleri içerir</span><span class="sxs-lookup"><span data-stu-id="5f5ab-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="5f5ab-165">Toplu kotaları görüntüle</span><span class="sxs-lookup"><span data-stu-id="5f5ab-165">View Batch quotas</span></span>
<span data-ttu-id="5f5ab-166">Toplu işlem hesabı kotası hello görüntülemek [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="5f5ab-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="5f5ab-167">Seçin **Batch hesapları** hello Portalı'nda, ardından, ilgilendiğiniz hello toplu işlem hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="5f5ab-168">Seçin **özellikleri** hello Batch hesabının menü dikey.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="5f5ab-169">Merhaba özellikleri dikey penceresinde hello görüntüler **kotaları** toohello toplu işlem hesabı uygulanmakta</span><span class="sxs-lookup"><span data-stu-id="5f5ab-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Toplu işlem hesabı kotası][account_quotas]

<span data-ttu-id="5f5ab-171">Kullanıcı abonelik modunda oluşturulan bir toplu işlem hesabı için abonelik kotaları hello Azure Portal görünümü hello ilgili.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="5f5ab-172">Seçin **abonelikleri**ve hello toplu işlem hesabı için kullandığınız hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="5f5ab-173">Merhaba üzerinde **abonelik** dikey penceresinde, select **kullanım + kotaları**.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="5f5ab-174">Kota artırma</span><span class="sxs-lookup"><span data-stu-id="5f5ab-174">Increase a quota</span></span>
<span data-ttu-id="5f5ab-175">Kota artırma hello kullanarak aboneliğinizi veya toplu iş hesabınız için bu adımları toorequest izleyin [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="5f5ab-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="5f5ab-176">Kota artışı Hello türü hello havuzu ayırma moduna Batch hesabınızın bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="5f5ab-177">Toplu işlem çekirdek kota artırma</span><span class="sxs-lookup"><span data-stu-id="5f5ab-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="5f5ab-178">Batch hesabınıza oluşturulursa **Batch hizmeti** modu, bu adımları toorequest toplu çekirdek kota artışı izleyin:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="5f5ab-179">Select hello **Yardım + Destek** döşeme portal Panonuzda veya hello soru işareti (**?**) hello sağ üst köşesindeki hello portal.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="5f5ab-180">Seçin **yeni destek isteği** > **Temelleri**.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="5f5ab-181">Merhaba üzerinde **Temelleri** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="5f5ab-182">a.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-182">a.</span></span> <span data-ttu-id="5f5ab-183">**Sorun türü** > **kota**</span><span class="sxs-lookup"><span data-stu-id="5f5ab-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="5f5ab-184">b.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-184">b.</span></span> <span data-ttu-id="5f5ab-185">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-185">Select your subscription.</span></span>
   
    <span data-ttu-id="5f5ab-186">c.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-186">c.</span></span> <span data-ttu-id="5f5ab-187">**Kota türü** > **toplu işlem**</span><span class="sxs-lookup"><span data-stu-id="5f5ab-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="5f5ab-188">d.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-188">d.</span></span> <span data-ttu-id="5f5ab-189">**Destek planınız** > **kota desteği - dahil**</span><span class="sxs-lookup"><span data-stu-id="5f5ab-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="5f5ab-190">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-190">Click **Next**.</span></span>
4. <span data-ttu-id="5f5ab-191">Merhaba üzerinde **sorun** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="5f5ab-192">a.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-192">a.</span></span> <span data-ttu-id="5f5ab-193">Seçin bir **önem** tooyour göre [iş etkisi][support_sev].</span><span class="sxs-lookup"><span data-stu-id="5f5ab-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="5f5ab-194">b.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-194">b.</span></span> <span data-ttu-id="5f5ab-195">İçinde **ayrıntıları**, toochange, hello toplu işlem hesabı adı ve hello yeni sınır istediğiniz her kotasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="5f5ab-196">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-196">Click **Next**.</span></span>
5. <span data-ttu-id="5f5ab-197">Merhaba üzerinde **kişi bilgileri** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="5f5ab-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="5f5ab-198">a.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-198">a.</span></span> <span data-ttu-id="5f5ab-199">Seçin bir **tercih edilen iletişim yöntemi**.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="5f5ab-200">b.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-200">b.</span></span> <span data-ttu-id="5f5ab-201">Doğrulayın ve gerekli hello kişi ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="5f5ab-202">Tıklatın **oluşturma** toosubmit hello destek isteği.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="5f5ab-203">Destek İsteği gönderdikten sonra Azure destek, sizinle iletişim kuracaktır.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="5f5ab-204">Merhaba isteği Tamamlanıyor too2 iş günleri alabileceğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="5f5ab-205">Abonelik çekirdek kota artırma</span><span class="sxs-lookup"><span data-stu-id="5f5ab-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="5f5ab-206">Batch hesabınıza oluşturulursa **kullanıcı aboneliği** modu ve gerektiğinde ek bölge veya VM ailesi çekirdek, kota bir istek aboneliğinizde artırın.</span><span class="sxs-lookup"><span data-stu-id="5f5ab-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="5f5ab-207">Adımlar için bkz: [Resource Manager çekirdek Kotayı artırmak istekleri](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ab-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="5f5ab-208">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="5f5ab-208">Related topics</span></span>
* [<span data-ttu-id="5f5ab-209">Hello Azure portal kullanarak bir Azure Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f5ab-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="5f5ab-210">Azure Batch özelliklerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="5f5ab-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="5f5ab-211">Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="5f5ab-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
