---
title: "Azure Site Recovery için çoğaltma ayarları oluşturma | Microsoft Docs"
description: "Site Recovery'nin, VMM bulutlarındaki Hyper-V sanal makinelerinden Azure'a yönelik çoğaltma, yük devretme ve kurtarma işlemlerini gerçekleştirmek üzere nasıl dağıtılacağını açıklar."
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
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="d311f-103">VMware’den Azure’a çoğaltma ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="d311f-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="d311f-104">Çoğaltma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d311f-104">Create a replication policy</span></span>

1. <span data-ttu-id="d311f-105">**Yönet** > **Site Recovery Altyapısı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="d311f-106">**VMware ve Fiziksel makineler için** altındaki **Çoğaltma ilkeleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="d311f-107">**+Çoğaltma ilkesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-107">Select **+Replication policy**.</span></span>

    ![Çoğaltma ilkesi oluşturma](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="d311f-109">İlke adını girin.</span><span class="sxs-lookup"><span data-stu-id="d311f-109">Enter the policy name.</span></span>

5. <span data-ttu-id="d311f-110">**RPO eşiği** bölümünde RPO limitini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d311f-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="d311f-111">Sürekli çoğaltma bu limiti aşarsa uyarılar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d311f-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="d311f-112">**Kurtarma noktası bekletme** kısmında, her kurtarma noktası için bekletme süresini saat cinsinden belirtin.</span><span class="sxs-lookup"><span data-stu-id="d311f-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="d311f-113">Korumalı makineler, bekletme penceresi içindeki herhangi bir noktaya kurtarılabilir.</span><span class="sxs-lookup"><span data-stu-id="d311f-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d311f-114">Premium depolama alanına çoğaltılan makineler için 24 saate kadar bekletme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d311f-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="d311f-115">Standart depolama alanına çoğaltılan makineler için 72 saate kadar bekletme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d311f-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d311f-116">Yeniden çalışmaya yönelik bir çoğaltma ilkesi otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d311f-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="d311f-117">**Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktalarının hangi sıklıkta oluşturulacağını (dakika cinsinden) belirtin.</span><span class="sxs-lookup"><span data-stu-id="d311f-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="d311f-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-118">Click **OK**.</span></span> <span data-ttu-id="d311f-119">İlke, 30 ila 60 saniye içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d311f-119">The policy should be created in 30 to 60 seconds.</span></span>

![Çoğaltma ilkesi üretme](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="d311f-121">Yapılandırma sunucusunu çoğaltma ilkesi ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d311f-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="d311f-122">Yapılandırma sunucusunu ilişkilendirmek istediğiniz çoğaltma ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="d311f-123">**İlişkilendir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-123">Click **Associate**.</span></span>
<span data-ttu-id="d311f-124">![Yapılandırma sunucusunu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="d311f-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="d311f-125">Sunucu listesinden yapılandırma sunucusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="d311f-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-126">Click **OK**.</span></span> <span data-ttu-id="d311f-127">Yapılandırma sunucusu, bir ila iki dakika içinde ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="d311f-127">The configuration server should be associated in one to two minutes.</span></span>

![Yapılandırma sunucusu ilişkilendirme](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="d311f-129">Çoğaltma ilkesini düzenleme</span><span class="sxs-lookup"><span data-stu-id="d311f-129">Edit a replication policy</span></span>
1. <span data-ttu-id="d311f-130">Çoğaltma ayarlarını düzenlemek istediğiniz çoğaltma ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="d311f-131">![Çoğaltma ilkesini düzenleme](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="d311f-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="d311f-132">**Ayarları Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="d311f-133">![Çoğaltma ilkesi ayarlarını düzenleme](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="d311f-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="d311f-134">Gereksinimlerinize göre ayarları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d311f-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="d311f-135">**Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-135">Click **Save**.</span></span> <span data-ttu-id="d311f-136">İlke, bu çoğaltma ilkesini kullanan VM sayısına bağlı olarak iki ila beş dakika içinde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d311f-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Çoğaltma ilkesini kaydetme](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="d311f-138">Yapılandırma sunucusunun çoğaltma ilkesi ile ilişkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="d311f-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="d311f-139">Yapılandırma sunucusunu ilişkilendirmek istediğiniz çoğaltma ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="d311f-140">**İlişkilendirmeyi Kaldır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="d311f-141">Sunucu listesinden yapılandırma sunucusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="d311f-142">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-142">Click **OK**.</span></span> <span data-ttu-id="d311f-143">Yapılandırma sunucusunun ilişkisi, bir ila iki dakika içinde kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d311f-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d311f-144">İlkeyi kullanan en az bir çoğaltılmış öğe varsa yapılandırma sunucusunun ilişkisini kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="d311f-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="d311f-145">Yapılandırma sunucusunun ilişkisini kaldırmadan önce ilkeyi kullanan çoğaltılmış bir öğe bulunmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d311f-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="d311f-146">Çoğaltma ilkesini silme</span><span class="sxs-lookup"><span data-stu-id="d311f-146">Delete a replication policy</span></span>

1. <span data-ttu-id="d311f-147">Silmek istediğiniz çoğaltma ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d311f-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="d311f-148">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d311f-148">Click **Delete**.</span></span> <span data-ttu-id="d311f-149">İlke, 30 ila 60 saniye içinde silinir.</span><span class="sxs-lookup"><span data-stu-id="d311f-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d311f-150">Kendisiyle ilişkili en az bir yapılandırma sunucusu varsa çoğaltma ilkesini silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d311f-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="d311f-151">İlkeyi silmeden önce, ilkeyi kullanan çoğaltılmış öğe bulunmadığından emin olun ve tüm ilişkili yapılandırma sunucularını silin.</span><span class="sxs-lookup"><span data-stu-id="d311f-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>
