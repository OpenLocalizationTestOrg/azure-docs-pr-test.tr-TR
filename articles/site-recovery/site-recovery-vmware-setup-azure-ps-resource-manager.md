---
title: " Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme | Microsoft Docs"
description: "Bu makalede bir yeniden çalışma işlem sunucusu (Resource Manager) kurmak Azure'da açıklar."
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
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="af23b-103">Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="af23b-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af23b-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="af23b-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="af23b-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="af23b-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="af23b-106">Yeniden çalışma sırasında Azure sanal ağ ve şirket içi ağınız arasında yüksek gecikme ise işlem sunucusu azure'da dağıtmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="af23b-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="af23b-107">Bu makalede nasıl ayarlamak, yapılandırabilir ve Azure'da çalışan işlem sunucuları yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af23b-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="af23b-108">Bu makalede kullandıysanız kullanılacak olan **Resource Manager** yük devretme sırasında sanal makineler için dağıtım modeli olarak.</span><span class="sxs-lookup"><span data-stu-id="af23b-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="af23b-109">Kullandıysanız **Klasik** dağıtım modeli adımları [nasıl ayarlayın ve yeniden çalışma işlem sunucusu (Klasik) yapılandırma](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="af23b-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af23b-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="af23b-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="af23b-111">Azure üzerinde bir işlem sunucusu Dağıt</span><span class="sxs-lookup"><span data-stu-id="af23b-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="af23b-112">Kasadaki > **Site Recovery altyapısı** (altında "Manage" Başlık) > **yapılandırma sunucularına** ("İçin VMware ve fiziksel makineler" başlığı altında), yapılandırma sunucusu seçin.</span><span class="sxs-lookup"><span data-stu-id="af23b-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="af23b-113">Açılan yapılandırma sunucusu Ayrıntıları sayfasında tıklayın "+ sunucu işlemleri"</span><span class="sxs-lookup"><span data-stu-id="af23b-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![İşlem sunucusu Galeri Ekle](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="af23b-115">Üzerinde **işlem Sunucu Ekle** sayfasında, aşağıdaki değerleri seçin</span><span class="sxs-lookup"><span data-stu-id="af23b-115">On the **Add process server** page, select the following values</span></span>

  ![İşlem sunucusu galeri öğesi ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="af23b-117">**Alan adı**</span><span class="sxs-lookup"><span data-stu-id="af23b-117">**Field Name**</span></span>|<span data-ttu-id="af23b-118">**Değer**</span><span class="sxs-lookup"><span data-stu-id="af23b-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="af23b-119">İşlem sunucunuzu dağıtmak istediğiniz yeri seçin</span><span class="sxs-lookup"><span data-stu-id="af23b-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="af23b-120">Değeri seçin **azure'da yeniden çalışma işlem sunucusu Dağıt**</span><span class="sxs-lookup"><span data-stu-id="af23b-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="af23b-121">Abonelik</span><span class="sxs-lookup"><span data-stu-id="af23b-121">Subscription</span></span>|<span data-ttu-id="af23b-122">Sanal makineler üzerinde başarısız olduğu Azure aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="af23b-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="af23b-123">Kaynak Grubu</span><span class="sxs-lookup"><span data-stu-id="af23b-123">Resource Group</span></span>|<span data-ttu-id="af23b-124">Bu işlem sunucusu dağıtmak veya varolan bir kaynak grubu, işlem sunucusu dağıtmak seçmek için bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="af23b-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="af23b-125">Konum</span><span class="sxs-lookup"><span data-stu-id="af23b-125">Location</span></span>|<span data-ttu-id="af23b-126">Azure veri merkezi içine seçin sanal makineleri içine devredilir burada</span><span class="sxs-lookup"><span data-stu-id="af23b-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="af23b-127">Azure Ağı</span><span class="sxs-lookup"><span data-stu-id="af23b-127">Azure Network</span></span>|<span data-ttu-id="af23b-128">Azure sanal Network(VNet) seçin, sanal makineleri içine yük devredildi durumunda.</span><span class="sxs-lookup"><span data-stu-id="af23b-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="af23b-129">Sanal makineler üzerinde birden fazla Azure Vnet başarısız olduysa, sonra VNet dağıtılan bir işlem sunucusu gerekir</span><span class="sxs-lookup"><span data-stu-id="af23b-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="af23b-130">İşlem sunucusu için özelliklerin doldurun</span><span class="sxs-lookup"><span data-stu-id="af23b-130">Fill in the rest of the properties for the process server</span></span>

  ![İşlem sunucusu Özet ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="af23b-132">**Alan adı**</span><span class="sxs-lookup"><span data-stu-id="af23b-132">**Field Name**</span></span>|<span data-ttu-id="af23b-133">**Değer**</span><span class="sxs-lookup"><span data-stu-id="af23b-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="af23b-134">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="af23b-134">Server Name</span></span>|<span data-ttu-id="af23b-135">Görünen ad & işlem sunucusu sanal makinesi için ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="af23b-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="af23b-136">User Name</span><span class="sxs-lookup"><span data-stu-id="af23b-136">User Name</span></span>|<span data-ttu-id="af23b-137">Bu sanal makinede yönetici hale bir kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="af23b-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="af23b-138">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="af23b-138">Storage Account</span></span>|<span data-ttu-id="af23b-139">Sanal makinenin sanal diskin yerleştirildiği depolama hesabı adı</span><span class="sxs-lookup"><span data-stu-id="af23b-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="af23b-140">Alt ağ</span><span class="sxs-lookup"><span data-stu-id="af23b-140">Subnet</span></span>|<span data-ttu-id="af23b-141">Azure sanal makineye bağlı sanal alt ağ</span><span class="sxs-lookup"><span data-stu-id="af23b-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="af23b-142">IP Adresi</span><span class="sxs-lookup"><span data-stu-id="af23b-142">IP Address</span></span>|<span data-ttu-id="af23b-143">IP adresi kez varsayın için işlem sunucusu istediğiniz önyükleme</span><span class="sxs-lookup"><span data-stu-id="af23b-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="af23b-144">İşlem sunucusu sanal makine dağıtımı başlatmak için Tamam düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="af23b-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="af23b-145">Yeniden çalışma için bu işlem sunucusu kullanabilmek şirket içi yapılandırma sunucusu ile kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="af23b-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="af23b-146">Yapılandırma (şirket içi çalıştıran) bir sunucuya (Azure'da çalışan) işlem sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="af23b-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="af23b-147">İşlem sunucusu son sürümüne yükseltme.</span><span class="sxs-lookup"><span data-stu-id="af23b-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="af23b-148">(Azure'da çalışan) işlem sunucusu yapılandırması (şirket içi çalıştıran) bir sunucudan kaydı siliniyor</span><span class="sxs-lookup"><span data-stu-id="af23b-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
