---
title: " İşlem içinde Azure(Classic) çalıştıran bir sunucuyu yönetmek | Microsoft Docs"
description: "Bu makalede nasıl tooset yeniden çalışma işlemi Server(Classic) Azure içinde ayarlama."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="4e409-103">Azure (Klasik) çalışan bir işlem sunucusu yönetme</span><span class="sxs-lookup"><span data-stu-id="4e409-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e409-104">Azure Klasik</span><span class="sxs-lookup"><span data-stu-id="4e409-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="4e409-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e409-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="4e409-106">Yeniden çalışma sırasında hello Azure sanal ağ ve şirket içi ağınız arasında yüksek gecikme ise toodeploy Azure işlem sunucusu önerilir.</span><span class="sxs-lookup"><span data-stu-id="4e409-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="4e409-107">Bu makalede nasıl ayarlamak, yapılandırabilir ve Azure'da çalışan hello işlem sunucuları yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4e409-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="4e409-108">Bu makalede Klasik hello dağıtım modeli olarak hello sanal makineler için yük devretme sırasında kullandıysanız kullanılan toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="4e409-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="4e409-109">Resource Manager dağıtım modeli izleyin hello adımlarda hello olarak kullanılan, [nasıl tooset Yukarı & bir yeniden çalışma işlem sunucusu (Kaynak Yöneticisi) yapılandırın](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="4e409-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e409-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e409-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="4e409-111">Azure üzerinde bir işlem sunucusu Dağıt</span><span class="sxs-lookup"><span data-stu-id="4e409-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="4e409-112">Azure Marketi'nde hello kullanarak bir sanal makine oluşturma **Microsoft Azure Site kurtarma işlemi Server V2**</span><span class="sxs-lookup"><span data-stu-id="4e409-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="4e409-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="4e409-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="4e409-114">Merhaba dağıtım modeli olarak seçtiğinizden emin olun **Klasik**</span><span class="sxs-lookup"><span data-stu-id="4e409-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="4e409-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="4e409-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="4e409-116">Merhaba oluşturma sanal makine Sihirbazı'nda > temel ayarları sağlamak hello sanal makineler üzerinde başarısız hello abonelik ve konumda toowhere seçin.</span><span class="sxs-lookup"><span data-stu-id="4e409-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="4e409-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="4e409-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="4e409-118">Bu hello sanal makineye bağlı olduğundan emin olun devredilen sanal makine üzerinde toohello Azure Virtual Network toowhich hello bağlı.</span><span class="sxs-lookup"><span data-stu-id="4e409-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="4e409-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="4e409-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="4e409-120">Merhaba işlem sunucusu sanal makine sağlandıktan sonra toolog gerekir ve hello yapılandırma sunucusu ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4e409-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="4e409-121">toobe mümkün toouse bu işlem sunucunun yeniden çalışma için tooregister gereksinim duyduğunuz hello şirket içi yapılandırma sunucusu ile.</span><span class="sxs-lookup"><span data-stu-id="4e409-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="4e409-122">Merhaba (Azure'da çalışan) işlem sunucusu tooa yapılandırma (şirket içi çalıştıran) sunucusu kaydetme</span><span class="sxs-lookup"><span data-stu-id="4e409-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="4e409-123">Merhaba işlem sunucusu toolatest sürümüne yükseltme.</span><span class="sxs-lookup"><span data-stu-id="4e409-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="4e409-124">Kaydı siliniyor hello (şirket içi çalıştıran) bir yapılandırma sunucusundan işlem (Azure'da çalışan) sunucusu</span><span class="sxs-lookup"><span data-stu-id="4e409-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
