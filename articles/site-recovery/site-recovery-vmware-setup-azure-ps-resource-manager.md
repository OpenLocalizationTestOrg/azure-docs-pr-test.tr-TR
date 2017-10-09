---
title: " Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme | Microsoft Docs"
description: "Bu makalede Azure içinde bir yeniden çalışma yukarı tooset sunucu (Resource Manager) işleminin nasıl açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="c59a0-103">Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="c59a0-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c59a0-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c59a0-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="c59a0-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="c59a0-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="c59a0-106">Yeniden çalışma sırasında hello Azure sanal ağ ve şirket içi ağınız arasında yüksek gecikme ise toodeploy işlem sunucusu azure'da önerilir.</span><span class="sxs-lookup"><span data-stu-id="c59a0-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="c59a0-107">Bu makalede nasıl ayarlamak, yapılandırabilir ve Azure'da çalışan hello işlem sunucuları yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c59a0-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="c59a0-108">Bu makalede kullandıysanız kullanılan toobe olan **Resource Manager** hello sanal makineler yük devretme sırasında hello dağıtım modeli olarak.</span><span class="sxs-lookup"><span data-stu-id="c59a0-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="c59a0-109">Kullandıysanız **Klasik** hello dağıtım modeli hello adımları [nasıl tooset Yukarı & bir yeniden çalışma işlem sunucusu (Klasik) yapılandırma](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="c59a0-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c59a0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c59a0-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="c59a0-111">Azure üzerinde bir işlem sunucusu Dağıt</span><span class="sxs-lookup"><span data-stu-id="c59a0-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="c59a0-112">Merhaba kasa içinde > **Site Recovery altyapısı** (altında hello "Manage" Başlık) > **yapılandırma sunucularına** ("İçin VMware ve fiziksel makineler" başlığı altında), hello yapılandırma sunucusu seçin.</span><span class="sxs-lookup"><span data-stu-id="c59a0-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="c59a0-113">Açılan hello yapılandırma sunucusu Ayrıntıları sayfasında tıklayın "+ sunucu işlemleri"</span><span class="sxs-lookup"><span data-stu-id="c59a0-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![İşlem sunucusu Galeri Ekle](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="c59a0-115">Merhaba üzerinde **işlem Sunucu Ekle** sayfasında, aşağıdaki değerleri seçin hello</span><span class="sxs-lookup"><span data-stu-id="c59a0-115">On hello **Add process server** page, select hello following values</span></span>

  ![İşlem sunucusu galeri öğesi ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="c59a0-117">**Alan adı**</span><span class="sxs-lookup"><span data-stu-id="c59a0-117">**Field Name**</span></span>|<span data-ttu-id="c59a0-118">**Değer**</span><span class="sxs-lookup"><span data-stu-id="c59a0-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="c59a0-119">İşlem sunucunuzu toodeploy istediğiniz yeri seçin</span><span class="sxs-lookup"><span data-stu-id="c59a0-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="c59a0-120">Merhaba değeri seçin **azure'da yeniden çalışma işlem sunucusu Dağıt**</span><span class="sxs-lookup"><span data-stu-id="c59a0-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="c59a0-121">Abonelik</span><span class="sxs-lookup"><span data-stu-id="c59a0-121">Subscription</span></span>|<span data-ttu-id="c59a0-122">Hello Azure hello sanal makineler üzerinde başarısız olduğu abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="c59a0-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="c59a0-123">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="c59a0-123">Resource Group</span></span>|<span data-ttu-id="c59a0-124">Bu işlem sunucusu bir kaynak grubu toodeploy oluşturabilir veya varolan bir kaynak grubunda toodeploy hello işlem sunucusu seçin</span><span class="sxs-lookup"><span data-stu-id="c59a0-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="c59a0-125">Konum</span><span class="sxs-lookup"><span data-stu-id="c59a0-125">Location</span></span>|<span data-ttu-id="c59a0-126">Hangi hello sanal makinelerine Hello Azure veri merkezi seçin içine devredilir burada</span><span class="sxs-lookup"><span data-stu-id="c59a0-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="c59a0-127">Azure Ağı</span><span class="sxs-lookup"><span data-stu-id="c59a0-127">Azure Network</span></span>|<span data-ttu-id="c59a0-128">Select hello sanal makineleri hello Azure sanal Network(VNet) içine yük devredildi durumunda.</span><span class="sxs-lookup"><span data-stu-id="c59a0-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="c59a0-129">Sanal makineler üzerinde birden fazla Azure Vnet başarısız olduysa, sonra VNet dağıtılan bir işlem sunucusu gerekir</span><span class="sxs-lookup"><span data-stu-id="c59a0-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="c59a0-130">Merhaba rest hello işlem sunucusu için hello özelliklerinin doldurun</span><span class="sxs-lookup"><span data-stu-id="c59a0-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![İşlem sunucusu Özet ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="c59a0-132">**Alan adı**</span><span class="sxs-lookup"><span data-stu-id="c59a0-132">**Field Name**</span></span>|<span data-ttu-id="c59a0-133">**Değer**</span><span class="sxs-lookup"><span data-stu-id="c59a0-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="c59a0-134">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="c59a0-134">Server Name</span></span>|<span data-ttu-id="c59a0-135">Görünen ad & işlem sunucusu sanal makinesi için ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="c59a0-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="c59a0-136">User Name</span><span class="sxs-lookup"><span data-stu-id="c59a0-136">User Name</span></span>|<span data-ttu-id="c59a0-137">Bu sanal makinede yönetici hale bir kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="c59a0-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="c59a0-138">Depolama Hesabı</span><span class="sxs-lookup"><span data-stu-id="c59a0-138">Storage Account</span></span>|<span data-ttu-id="c59a0-139">Merhaba hello sanal makinenin sanal diskin yerleştirildiği depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="c59a0-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="c59a0-140">Alt ağ</span><span class="sxs-lookup"><span data-stu-id="c59a0-140">Subnet</span></span>|<span data-ttu-id="c59a0-141">Merhaba alt hello Azure VNet toowhich hello sanal makinenin bağlı</span><span class="sxs-lookup"><span data-stu-id="c59a0-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="c59a0-142">IP Adresi</span><span class="sxs-lookup"><span data-stu-id="c59a0-142">IP Address</span></span>|<span data-ttu-id="c59a0-143">Yukarı önyüklenir hello işlem sunucusu tooassume kez istediğiniz IP adresi</span><span class="sxs-lookup"><span data-stu-id="c59a0-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="c59a0-144">Merhaba işlem sunucusu sanal makine dağıtma hello Tamam düğmesine toostart'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c59a0-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="c59a0-145">toobe mümkün toouse bu işlem sunucunun yeniden çalışma için tooregister gereksinim duyduğunuz hello şirket içi yapılandırma sunucusu ile.</span><span class="sxs-lookup"><span data-stu-id="c59a0-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="c59a0-146">Merhaba işlem (Azure'da çalışan) server tooa yapılandırma (şirket içi çalıştıran) sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="c59a0-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="c59a0-147">Merhaba işlem sunucusu toolatest sürümüne yükseltme.</span><span class="sxs-lookup"><span data-stu-id="c59a0-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="c59a0-148">(Azure'da çalışan) hello işlem sunucusunu yapılandırma (şirket içi çalıştıran) bir sunucudan kaydı siliniyor</span><span class="sxs-lookup"><span data-stu-id="c59a0-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
