---
title: "aaaInstall Azure Güvenlik Merkezi'nde Endpoint Protection | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** yüklemek Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="82cd9-103">Azure Güvenlik Merkezi'nde Endpoint Protection yükle</span><span class="sxs-lookup"><span data-stu-id="82cd9-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="82cd9-104">Azure Güvenlik Merkezi, uç nokta koruma zaten etkin değilse uç nokta koruma Azure sanal makinelerde (VM'ler) yüklemenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="82cd9-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="82cd9-105">Bu öneri tooWindows VM'ler yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="82cd9-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="82cd9-106">Bu örnek dağıtım Microsoft Antimalware kullanır.</span><span class="sxs-lookup"><span data-stu-id="82cd9-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="82cd9-107">Bkz: [Azure Güvenlik Merkezi'nde iş ortağı tümleştirme](security-center-partner-integration.md#partners-that-integrate-with-security-center) iş ortaklarının listesi için Güvenlik Merkezi ile tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="82cd9-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="82cd9-108">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="82cd9-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="82cd9-109">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="82cd9-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="82cd9-110">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="82cd9-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="82cd9-111">Merhaba, **önerileri** dikey penceresinde, select **Endpoint Protection Yükle**.</span><span class="sxs-lookup"><span data-stu-id="82cd9-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="82cd9-112">![Endpoint Protection yükle seçin][1]</span><span class="sxs-lookup"><span data-stu-id="82cd9-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="82cd9-113">Merhaba **Endpoint Protection Yükle** uç nokta koruması olmadan VM'ler listesini görüntüleyen dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="82cd9-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="82cd9-114">Merhaba listesi hello üzerinde tooinstall endpoint protection istediğiniz VM'ler seçim **Vm'lerinde yükleme**.</span><span class="sxs-lookup"><span data-stu-id="82cd9-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="82cd9-115">![Sanal makineleri tooinstall Endpoint Protection'ı seçin][2]</span><span class="sxs-lookup"><span data-stu-id="82cd9-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="82cd9-116">Merhaba **işaretleyin Endpoint Protection** dikey pencere açılır tooallow toouse istediğiniz, tooselect hello uç nokta koruma çözümü.</span><span class="sxs-lookup"><span data-stu-id="82cd9-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="82cd9-117">Bu örnekte, şimdi seçin **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="82cd9-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="82cd9-118">![Endpoint Protection seçin][3]</span><span class="sxs-lookup"><span data-stu-id="82cd9-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="82cd9-119">Merhaba uç nokta koruma çözümü hakkında ek bilgi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="82cd9-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="82cd9-120">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="82cd9-120">Select **Create**.</span></span>
   <span data-ttu-id="82cd9-121">![Kötü amaçlı yazılımdan koruma çözümü oluşturun][4]</span><span class="sxs-lookup"><span data-stu-id="82cd9-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="82cd9-122">Merhaba üzerinde hello gerekli yapılandırma ayarlarını girin **eklemek uzantısı** dikey ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="82cd9-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="82cd9-123">toolearn hello yapılandırma ayarları hakkında daha fazla bilgi görmek [varsayılan ve özel kötü amaçlı yazılımdan koruma yapılandırma](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="82cd9-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="82cd9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) hello etkin VM'ler seçili artık.</span><span class="sxs-lookup"><span data-stu-id="82cd9-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="82cd9-125">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="82cd9-125">See also</span></span>
<span data-ttu-id="82cd9-126">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Endpoint Protection yükle." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="82cd9-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="82cd9-127">Azure, Microsoft Antimalware etkinleştirme hakkında daha fazla toolearn belge aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="82cd9-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="82cd9-128">[Bulut Hizmetleri ve sanal makineleri için Microsoft Antimalware](../security/azure-security-antimalware.md) --öğrenin nasıl toodeploy Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="82cd9-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="82cd9-129">Güvenlik Merkezi hakkında daha fazla toolearn belgeleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="82cd9-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="82cd9-130">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="82cd9-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="82cd9-131">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="82cd9-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="82cd9-132">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="82cd9-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="82cd9-133">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="82cd9-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="82cd9-134">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="82cd9-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="82cd9-135">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82cd9-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="82cd9-136">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82cd9-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
