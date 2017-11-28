---
title: "Azure sanal ağlar etkileyen bir Azure hizmet kesintisi hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure sanal ağlar etkileyen bir Azure hizmet kesintisi hello olayı içinde hangi toodo öğrenin."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a><span data-ttu-id="5b92d-103">Sanal ağ – iş sürekliliği</span><span class="sxs-lookup"><span data-stu-id="5b92d-103">Virtual Network – Business Continuity</span></span>
## <a name="overview"></a><span data-ttu-id="5b92d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5b92d-104">Overview</span></span>
<span data-ttu-id="5b92d-105">Bir sanal ağ (VNet) hello bulut ağınızdaki mantıksal bir gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="5b92d-105">A Virtual Network (VNet) is a logical representation of your network in hello cloud.</span></span> <span data-ttu-id="5b92d-106">Kendi özel IP adres alanı ve segment hello alt ağ toodefine sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b92d-106">It allows you toodefine your own private IP address space and segment hello network into subnets.</span></span> <span data-ttu-id="5b92d-107">Sanal ağlar işlem kaynaklarınızı Azure sanal makineler ve bulut Hizmetleri (web/çalışan rolleri) gibi bir güven sınırı toohost görev yapar.</span><span class="sxs-lookup"><span data-stu-id="5b92d-107">VNets serves as a trust boundary toohost your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span></span> <span data-ttu-id="5b92d-108">VNet içinde barındırılan hello kaynaklar arasında doğrudan özel IP iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b92d-108">A VNet allows direct private IP communication between hello resources hosted in it.</span></span> <span data-ttu-id="5b92d-109">Bir sanal ağ bağlantılı tooan şirket içi ağ üzerinden bir VPN ağ geçidi veya ExpressRoute gibi hello karma seçeneklerden birini de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b92d-109">A Virtual Network can also be linked tooan on-premises network through one of hello hybrid options such as a VPN Gateway or ExpressRoute.</span></span>

<span data-ttu-id="5b92d-110">Bir VNet hello bir bölge kapsamında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5b92d-110">A VNet is created within hello scope of a region.</span></span> <span data-ttu-id="5b92d-111">İki farklı bölgelerdeki aynı adres alanı ile sanal ağlar oluşturabilirsiniz (yani BİZE Doğu ve Batı ABD bunları tooone bağlanamıyor, ancak başka bir doğrudan).</span><span class="sxs-lookup"><span data-stu-id="5b92d-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them tooone another directly).</span></span> 

## <a name="business-continuity"></a><span data-ttu-id="5b92d-112">İş Sürekliliği</span><span class="sxs-lookup"><span data-stu-id="5b92d-112">Business Continuity</span></span>
<span data-ttu-id="5b92d-113">Uygulamanızı kesintiye birkaç farklı yolu olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b92d-113">There could be several different ways that your application could be disrupted.</span></span> <span data-ttu-id="5b92d-114">Belirli bir bölgedeki tooa doğal afet veya birden çok aygıt/hizmetlerini tooa hatası nedeniyle kısmi bir olağanüstü durum nedeniyle tamamen kesilebilir.</span><span class="sxs-lookup"><span data-stu-id="5b92d-114">A given region could be completely cut off due tooa natural disaster or a partial disaster due tooa failure of multiple devices/services.</span></span> <span data-ttu-id="5b92d-115">Merhaba VNet hizmeti Hello etkisini her bu durumlarda farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5b92d-115">hello impact on hello VNet service is different in each of these situations.</span></span>

<span data-ttu-id="5b92d-116">**S: bir kesinti tooan tüm bölgeyi hello olayda ne yapacaksınız? yani bir bölge tooa doğal afet tamamen kesme ise? Sanal ağlar hello bölgede barındırılan toohello ne olur?**</span><span class="sxs-lookup"><span data-stu-id="5b92d-116">**Q: What do you do in hello event of an outage tooan entire region? i.e. if a region is completely cutoff due tooa natural disaster? What happens toohello Virtual Networks hosted in hello region?**</span></span>

<span data-ttu-id="5b92d-117">Y: hello sanal ağ ve hello kaynaklarında hello bölge kalır hello hizmet kesintisi hello süre boyunca erişilemez etkilenen.</span><span class="sxs-lookup"><span data-stu-id="5b92d-117">A: hello Virtual Network and hello resources in hello affected region remains inaccessible during hello time of hello service disruption.</span></span>

![Basit sanal ağ diyagramı](./media/virtual-network-disaster-recovery-guidance/vnet.png)

<span data-ttu-id="5b92d-119">**S: neler yapabilirim toodo yeniden oluşturma, farklı bir bölgede aynı sanal ağ hello?**</span><span class="sxs-lookup"><span data-stu-id="5b92d-119">**Q: What can I toodo re-create hello same Virtual Network in a different region?**</span></span>

<span data-ttu-id="5b92d-120">Y: sanal ağ (VNet) oldukça basit kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="5b92d-120">A: Virtual Network (VNet) is fairly lightweight resource.</span></span> <span data-ttu-id="5b92d-121">Azure API toocreate VNet çağırabileceği hello ile aynı adres alanı farklı bir bölgede.</span><span class="sxs-lookup"><span data-stu-id="5b92d-121">You can invoke Azure APIs toocreate a VNet with hello same address space in a different region.</span></span> <span data-ttu-id="5b92d-122">toore-hello oluşturmak hello yoktu aynı ortamda etkilenen bölge, toomake API çağrıları toore sahip-bulut Hizmetleri (web/çalışan rolleri) ve sahip olduğunuz sanal makineler dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b92d-122">toore-create hello same environment that was present in hello affected region, you have toomake API calls toore-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span></span> <span data-ttu-id="5b92d-123">Ayrıca, bir VPN ağ geçidi ayarlama ve şirket içi bağlantı (bir karma dağıtımı olduğu gibi) olsaydı tooyour şirket içi ağ bağlanmak toospin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="5b92d-123">You will also have toospin up a VPN Gateway and connect tooyour on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span></span>

<span data-ttu-id="5b92d-124">bir VNet oluşturmak için hello yönergeleri bulunduğunda [burada](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="5b92d-124">hello instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span> 

<span data-ttu-id="5b92d-125">**S: sanal ağ içinde belirli bir bölgedeki çoğaltmasını önceden başka bir bölgede yeniden oluşturulabilir?**</span><span class="sxs-lookup"><span data-stu-id="5b92d-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span></span>

<span data-ttu-id="5b92d-126">A: Evet hello kullanarak aynı özel IP adres alanı ve ilerisinde iki farklı bölgelerdeki kaynakları süresi iki sanal ağlar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b92d-126">A: Yes, you can create two VNets using hello same private IP address space and resources in two different regions ahead of time.</span></span> <span data-ttu-id="5b92d-127">Bir müşteri hello VNet Hizmetleri'nde Internet'e barındırma varsa, bunlar etkin olan trafik Yöneticisi toogeo rota trafiği toohello bölgesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5b92d-127">If a customer was hosting internet facing services in hello VNet, they could have set up Traffic Manager toogeo-route traffic toohello region that is active.</span></span> <span data-ttu-id="5b92d-128">Ancak, bir müşteri iki Vnet bağlanamıyor yönlendirme sorununa neden olacağından hello ile aynı alanı tootheir şirket içi ağ adresi.</span><span class="sxs-lookup"><span data-stu-id="5b92d-128">However, a customer cannot connect two VNets with hello same address space tootheir on-premises network as it would cause routing issues.</span></span> <span data-ttu-id="5b92d-129">Bir olağanüstü durum başlangıç saatini ve bir bölgede bulunan bir sanal ağ kaybı, bir müşteri bağlanabilir diğer VNet ile eşleşen bir adres alanı tootheir şirket içi ağ hello kullanılabilir bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="5b92d-129">At hello time of a disaster and loss of a VNet in one region, a customer can connect hello other VNet in hello available region with matching address space tootheir on-premises network.</span></span>

<span data-ttu-id="5b92d-130">bir VNet oluşturmak için hello yönergeleri bulunduğunda [burada](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="5b92d-130">hello instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span>

