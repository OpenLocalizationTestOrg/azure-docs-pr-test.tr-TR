---
title: "Hyper-V çoğaltma tooAzure için System Center VMM aaaPrepare | Microsoft Docs"
description: "Açıklar nasıl tooprepare System Center VMM sunucusuna Azure Site Recovery kullanarak Hyper-V çoğaltma tooAzure için"
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
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="797f7-103">6. adım: VMM sunucuları ve Hyper-V konakları için Hyper-V çoğaltma tooAzure hazırlama</span><span class="sxs-lookup"><span data-stu-id="797f7-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="797f7-104">Ayarladıktan sonra [Azure bileşenleri](vmm-to-azure-walkthrough-prepare-azure.md) hello dağıtımı için Azure Site Recovery ile bu makale tooprepare şirket içi VMM sunucuları ve Hyper-V konakları toointeract hello yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="797f7-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="797f7-105">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="797f7-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="797f7-106">VMM sunucuları hazırlama</span><span class="sxs-lookup"><span data-stu-id="797f7-106">Prepare VMM servers</span></span>

- <span data-ttu-id="797f7-107">Site Recovery çoğaltma (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) hello destek gereksinimlerini karşılayan en az bir VMM sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="797f7-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="797f7-108">Emin olun hello VMM sunucusu için hazır [ağ eşlemesi](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="797f7-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="797f7-109">Merhaba VMM sunucusunun bu URL'leri erişebildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="797f7-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="797f7-110">IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.</span><span class="sxs-lookup"><span data-stu-id="797f7-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="797f7-111">Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="797f7-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="797f7-112">IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.</span><span class="sxs-lookup"><span data-stu-id="797f7-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="797f7-113">Site Recovery dağıtımı sırasında hello Site kurtarma sağlayıcısı indirin ve her VMM sunucusuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="797f7-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="797f7-114">Kurtarma Hizmetleri kasası hello Hello VMM sunucusu kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="797f7-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="797f7-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="797f7-115">Next steps</span></span>

<span data-ttu-id="797f7-116">Çok Git[adım 7: bir kasa oluşturun](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="797f7-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

