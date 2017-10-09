---
title: "aaaPrepare Hyper-V çoğaltma tooAzure (System Center VMM) barındıran | Microsoft Docs"
description: "Tooprepare Hyper-V çoğaltma tooAzure için Azure Site RECOVERY'yi kullanarak nasıl barındıran açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="5b6f6-103">6. adım: Hyper-V konakları için çoğaltma tooAzure hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="5b6f6-104">Bu makale tooprepare şirket içi Hyper-V konakları toointeract Azure Site Recovery ile Merhaba yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="5b6f6-105">Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5b6f6-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="5b6f6-106">Ana bilgisayarını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="5b6f6-106">Prepare hosts</span></span>

- <span data-ttu-id="5b6f6-107">Merhaba Hyper-V konakları hello karşıladığından emin olun [Önkoşullar](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="5b6f6-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="5b6f6-108">Merhaba konakları gerekli hello URL'leri erişebildiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="5b6f6-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="5b6f6-109">IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="5b6f6-110">Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="5b6f6-111">IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="5b6f6-112">Site Recovery dağıtımı sırasında tooreplicate tooa Hyper-V sitesinin istediğiniz Vm'leri içeren Hyper-V konakları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="5b6f6-113">Her ana bilgisayarda Hello Site Recovery sağlayıcısı ve kurtarma Hizmetleri Aracısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="5b6f6-114">Merhaba Hyper-V site kurtarma Hizmetleri kasası hello kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5b6f6-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b6f6-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b6f6-115">Next steps</span></span>

<span data-ttu-id="5b6f6-116">Çok Git[adım 7: bir kasa oluşturun](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5b6f6-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

