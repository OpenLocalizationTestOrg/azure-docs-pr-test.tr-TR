---
title: "Azure Site Recovery için çoğaltma ayarlarını aaaSet | Microsoft Docs"
description: "Nasıl toodeploy Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma Hyper-V vm'lerinde VMM Bulutu tooAzure açıklar."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="3da85-103">VMware tooAzure için çoğaltma ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="3da85-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="3da85-104">Çoğaltma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3da85-104">Create a replication policy</span></span>

1. <span data-ttu-id="3da85-105">**Yönet** > **Site Recovery Altyapısı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="3da85-106">**VMware ve Fiziksel makineler için** altındaki **Çoğaltma ilkeleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="3da85-107">**+Çoğaltma ilkesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-107">Select **+Replication policy**.</span></span>

    ![Çoğaltma ilkesi oluşturma](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="3da85-109">Hello ilkesi adı girin.</span><span class="sxs-lookup"><span data-stu-id="3da85-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="3da85-110">İçinde **RPO eşik**, hello RPO sınırını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3da85-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="3da85-111">Sürekli çoğaltma bu limiti aşarsa uyarılar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3da85-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="3da85-112">İçinde **kurtarma noktası bekletme**, (saat olarak) belirtin hello hello bekletme penceresinin süresi her kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="3da85-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="3da85-113">Korumalı makineler olabilir bir bekletme aralığı içinde tooany noktası kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="3da85-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3da85-114">Bekletme too24 saatleri makineler çoğaltılmış toopremium depolama için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3da85-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="3da85-115">Bekletme too72 saatleri makineler çoğaltılmış toostandard depolama için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3da85-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3da85-116">Yeniden çalışmaya yönelik bir çoğaltma ilkesi otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3da85-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="3da85-117">**Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının hangi sıklıkta oluşturulacağını (dakika cinsinden) belirtin.</span><span class="sxs-lookup"><span data-stu-id="3da85-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="3da85-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-118">Click **OK**.</span></span> <span data-ttu-id="3da85-119">Hello İlkesi 30 too60 saniye içinde oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3da85-119">hello policy should be created in 30 too60 seconds.</span></span>

![Çoğaltma ilkesi üretme](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="3da85-121">Yapılandırma sunucusunu çoğaltma ilkesi ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="3da85-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="3da85-122">Merhaba çoğaltma ilkesi toowhich seçin tooassociate hello yapılandırma sunucusu istiyor.</span><span class="sxs-lookup"><span data-stu-id="3da85-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="3da85-123">**İlişkilendir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-123">Click **Associate**.</span></span>
<span data-ttu-id="3da85-124">![Yapılandırma sunucusunu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="3da85-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="3da85-125">Merhaba yapılandırma sunucusu hello sunucuların listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="3da85-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-126">Click **OK**.</span></span> <span data-ttu-id="3da85-127">Merhaba yapılandırma sunucusu bir tootwo dakika cinsinden ilişkilendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="3da85-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Yapılandırma sunucusu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="3da85-129">Çoğaltma ilkesini düzenleme</span><span class="sxs-lookup"><span data-stu-id="3da85-129">Edit a replication policy</span></span>
1. <span data-ttu-id="3da85-130">Tooedit çoğaltma ayarları istediğiniz hello çoğaltma ilkesi seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="3da85-131">![Çoğaltma ilkesini düzenleme](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="3da85-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="3da85-132">**Ayarları Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="3da85-133">![Çoğaltma ilkesi ayarlarını düzenleme](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="3da85-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="3da85-134">Gereksinimleri temelinde hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3da85-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="3da85-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-135">Click **Save**.</span></span> <span data-ttu-id="3da85-136">Hello İlkesi iki toofive dakika içinde kaydedilmelidir, kaç tane sanal makineleri bağlı olarak bu çoğaltma ilkesini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3da85-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Çoğaltma ilkesini kaydetme](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="3da85-138">Yapılandırma sunucusunun çoğaltma ilkesi ile ilişkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="3da85-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="3da85-139">Merhaba çoğaltma ilkesi toowhich seçin tooassociate hello yapılandırma sunucusu istiyor.</span><span class="sxs-lookup"><span data-stu-id="3da85-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="3da85-140">**İlişkilendirmeyi Kaldır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="3da85-141">Merhaba yapılandırma sunucusu hello sunucuların listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="3da85-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="3da85-142">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-142">Click **OK**.</span></span> <span data-ttu-id="3da85-143">Merhaba yapılandırma sunucusu bir tootwo dakika içinde ilkenin ilişkisi.</span><span class="sxs-lookup"><span data-stu-id="3da85-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3da85-144">Hello İlkesi'ni kullanarak en az bir çoğaltılmış öğe ise bir yapılandırma sunucusu ilişkilendirmesini olamaz.</span><span class="sxs-lookup"><span data-stu-id="3da85-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="3da85-145">Merhaba yapılandırma sunucusu ilişkilendirmesini önce hello İlkesi'ni kullanarak çoğaltılan öğe olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3da85-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="3da85-146">Çoğaltma ilkesini silme</span><span class="sxs-lookup"><span data-stu-id="3da85-146">Delete a replication policy</span></span>

1. <span data-ttu-id="3da85-147">Merhaba çoğaltma ilkesi seçin toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="3da85-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="3da85-148">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3da85-148">Click **Delete**.</span></span> <span data-ttu-id="3da85-149">Hello İlkesi 30 too60 saniye içinde silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3da85-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3da85-150">En az bir yapılandırma sunucusu ilişkili tooit varsa, bir çoğaltma ilkesi silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="3da85-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="3da85-151">Hello İlkesi kullanılarak çoğaltılan öğe yok ve hello İlkesi silmeden önce tüm hello delete yapılandırma sunucularına ilişkili emin olun.</span><span class="sxs-lookup"><span data-stu-id="3da85-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
