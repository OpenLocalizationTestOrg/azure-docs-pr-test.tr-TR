---
title: "System Center VMM Hyper-V çoğaltma Azure için hazırlama | Microsoft Docs"
description: "System Center VMM sunucusu Hyper-V çoğaltma Azure Site Kurtarma'yı kullanarak Azure için hazırlamayı açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="2d325-103">6. adım: Hyper-V çoğaltma Azure için VMM sunucuları ve Hyper-V ana bilgisayarları hazırlama</span><span class="sxs-lookup"><span data-stu-id="2d325-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="2d325-104">Ayarladıktan sonra [Azure bileşenleri](vmm-to-azure-walkthrough-prepare-azure.md) şirket içi VMM sunucuları ve Azure Site Recovery ile etkileşim kurmak için Hyper-V konakları hazırlamak için bu makaledeki dağıtımı için yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d325-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="2d325-105">Bu makaleyi okuduktan sonra altındaki bir yorum gönderin ya da teknik sorular [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2d325-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="2d325-106">VMM sunucuları hazırlama</span><span class="sxs-lookup"><span data-stu-id="2d325-106">Prepare VMM servers</span></span>

- <span data-ttu-id="2d325-107">Site Recovery çoğaltma (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) için destek gereksinimlerini karşılayan en az bir VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d325-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="2d325-108">VMM sunucusu için hazır olduğundan emin olun [ağ eşlemesi](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="2d325-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="2d325-109">VMM sunucusunun bu URL'leri erişebildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="2d325-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="2d325-110">IP adresi tabanlı güvenlik duvarı kurallarına sahipseniz bu kuralların Azure ile iletişim kurmaya izin verdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2d325-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="2d325-111">[Azure Veri Merkezi IP Aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)'na ve HTTPS (443) bağlantı noktasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="2d325-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="2d325-112">Aboneliğinizin Azure bölgesi ve Batı ABD (Access Control ve Identity Management için kullanılır) için IP adresi aralıklarına izin verin.</span><span class="sxs-lookup"><span data-stu-id="2d325-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="2d325-113">Site Recovery dağıtımı sırasında Site kurtarma Sağlayıcısı'nı indirin ve her VMM sunucusuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d325-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="2d325-114">VMM sunucusu kurtarma Hizmetleri kasasına kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="2d325-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="2d325-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d325-115">Next steps</span></span>

<span data-ttu-id="2d325-116">Git [adım 7: bir kasa oluşturun](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="2d325-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

