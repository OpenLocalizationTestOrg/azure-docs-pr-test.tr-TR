---
title: "bir Oracle olağanüstü durum kurtarma senaryosunda Azure ortamınızda aaaOverview | Microsoft Docs"
description: "Bir olağanüstü durum kurtarma senaryosunda bir Oracle veritabanına 12c veritabanı Azure ortamınızda için"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="a81d6-103">Bir Oracle veritabanına 12c veritabanında bir Azure ortamı için olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="a81d6-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="a81d6-104">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="a81d6-104">Assumptions</span></span>

- <span data-ttu-id="a81d6-105">Oracle Data Guard tasarım ve Azure ortamı bir anlama sahip.</span><span class="sxs-lookup"><span data-stu-id="a81d6-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="a81d6-106">Hedefleri</span><span class="sxs-lookup"><span data-stu-id="a81d6-106">Goals</span></span>
- <span data-ttu-id="a81d6-107">Merhaba topoloji ve olağanüstü durum kurtarma (DR) gereksinimlerinizi karşılayacak yapılandırma tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="a81d6-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="a81d6-108">Senaryo 1: Birincil ve kurtarma sitelerinde Azure</span><span class="sxs-lookup"><span data-stu-id="a81d6-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="a81d6-109">Bir müşterinin bir Oracle veritabanı kümesi yukarı hello birincil sitede.</span><span class="sxs-lookup"><span data-stu-id="a81d6-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="a81d6-110">Bir DR, farklı bir bölgede sitedir.</span><span class="sxs-lookup"><span data-stu-id="a81d6-110">A DR site is in a different region.</span></span> <span data-ttu-id="a81d6-111">Merhaba müşteri bu siteler arasında hızlı kurtarma için Oracle Data Guard kullanır.</span><span class="sxs-lookup"><span data-stu-id="a81d6-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="a81d6-112">Merhaba birincil site ayrıca raporlama için ikincil bir veritabanı ve diğer kullanımlar sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a81d6-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="a81d6-113">Topoloji</span><span class="sxs-lookup"><span data-stu-id="a81d6-113">Topology</span></span>

<span data-ttu-id="a81d6-114">Hello Azure kurulumu bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a81d6-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="a81d6-115">İki site (bir birincil site ve bir DR sitesi)</span><span class="sxs-lookup"><span data-stu-id="a81d6-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="a81d6-116">İki sanal ağ</span><span class="sxs-lookup"><span data-stu-id="a81d6-116">Two virtual networks</span></span>
- <span data-ttu-id="a81d6-117">Veri koruma (birincil ve bekleme) ile iki Oracle veritabanları</span><span class="sxs-lookup"><span data-stu-id="a81d6-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="a81d6-118">İki Oracle veritabanları Golden kapısı veya veri koruma (yalnızca birincil site)</span><span class="sxs-lookup"><span data-stu-id="a81d6-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="a81d6-119">İki uygulama hizmetleri, bir birincil ve hello DR sitesi biri</span><span class="sxs-lookup"><span data-stu-id="a81d6-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="a81d6-120">Bir *kullanılabilirlik kümesi* hello birincil site veritabanı ve uygulama hizmeti için kullanılan</span><span class="sxs-lookup"><span data-stu-id="a81d6-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="a81d6-121">Erişim toohello özel ağ kısıtlar ve yalnızca bir yönetici oturum aç sağlayan her sitede bir jumpbox</span><span class="sxs-lookup"><span data-stu-id="a81d6-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="a81d6-122">Jumpbox, uygulama hizmeti, veritabanı ve ayrı alt ağlar üzerinde VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="a81d6-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="a81d6-123">Uygulama ve veritabanı alt ağlar üzerinde zorunlu NSG</span><span class="sxs-lookup"><span data-stu-id="a81d6-123">NSG enforced on application and database subnets</span></span>

![Merhaba DR topoloji sayfasının ekran görüntüsü](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="a81d6-125">Senaryo 2: Birincil site şirket içi ve Azure üzerinde DR sitesi</span><span class="sxs-lookup"><span data-stu-id="a81d6-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="a81d6-126">Bir müşteri, bir şirket içi Oracle Veritabanı Kurulumu (birincil site) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a81d6-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="a81d6-127">Azure üzerinde bir DR sitedir.</span><span class="sxs-lookup"><span data-stu-id="a81d6-127">A DR site is on Azure.</span></span> <span data-ttu-id="a81d6-128">Oracle Data Guard, bu siteler arasında hızlı kurtarma için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a81d6-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="a81d6-129">Merhaba birincil site ayrıca raporlama için ikincil bir veritabanı ve diğer kullanımlar sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a81d6-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="a81d6-130">Bu ayar için iki yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="a81d6-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="a81d6-131">Yaklaşım 1: Şirket içi ve açık TCP bağlantı noktaları hello Güvenlik Duvarı'nda gerektiren Azure arasında doğrudan bağlantıya</span><span class="sxs-lookup"><span data-stu-id="a81d6-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="a81d6-132">Hello world dışında TCP bağlantı noktaları toohello kullanıma biz doğrudan bağlantılar önerilmez.</span><span class="sxs-lookup"><span data-stu-id="a81d6-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="a81d6-133">Topoloji</span><span class="sxs-lookup"><span data-stu-id="a81d6-133">Topology</span></span>

<span data-ttu-id="a81d6-134">Hello Azure kurulumu bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a81d6-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="a81d6-135">Bir DR sitesi</span><span class="sxs-lookup"><span data-stu-id="a81d6-135">One DR site</span></span> 
- <span data-ttu-id="a81d6-136">Bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="a81d6-136">One virtual network</span></span>
- <span data-ttu-id="a81d6-137">Veri koruma (etkin) ile bir Oracle veritabanı</span><span class="sxs-lookup"><span data-stu-id="a81d6-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="a81d6-138">Merhaba DR sitesinde bir uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="a81d6-138">One application service on hello DR site</span></span>
- <span data-ttu-id="a81d6-139">Erişim toohello özel ağ kısıtlar ve yalnızca bir yönetici oturum aç sağlayan bir jumpbox</span><span class="sxs-lookup"><span data-stu-id="a81d6-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="a81d6-140">Jumpbox, uygulama hizmeti, veritabanı ve ayrı alt ağlar üzerinde VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="a81d6-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="a81d6-141">Uygulama ve veritabanı alt ağlar üzerinde zorunlu NSG</span><span class="sxs-lookup"><span data-stu-id="a81d6-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="a81d6-142">Bir NSG ilke/kuralı tooallow gelen TCP bağlantı noktası 1521 (veya kullanıcı tanımlı bir bağlantı noktası)</span><span class="sxs-lookup"><span data-stu-id="a81d6-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="a81d6-143">Bir NSG ilke/kuralı toorestrict yalnızca başlangıç IP adresi/şirket içi (DB ya da uygulama) tooaccess hello sanal ağ adresleri</span><span class="sxs-lookup"><span data-stu-id="a81d6-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Merhaba DR topoloji sayfasının ekran görüntüsü](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="a81d6-145">Yaklaşım 2: Siteden siteye VPN</span><span class="sxs-lookup"><span data-stu-id="a81d6-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="a81d6-146">Siteden siteye VPN daha iyi bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="a81d6-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="a81d6-147">VPN ayarlama hakkında daha fazla bilgi için bkz: [CLI kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="a81d6-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="a81d6-148">Topoloji</span><span class="sxs-lookup"><span data-stu-id="a81d6-148">Topology</span></span>

<span data-ttu-id="a81d6-149">Hello Azure kurulumu bir özeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a81d6-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="a81d6-150">Bir DR sitesi</span><span class="sxs-lookup"><span data-stu-id="a81d6-150">One DR site</span></span> 
- <span data-ttu-id="a81d6-151">Bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="a81d6-151">One virtual network</span></span> 
- <span data-ttu-id="a81d6-152">Veri koruma (etkin) ile bir Oracle veritabanı</span><span class="sxs-lookup"><span data-stu-id="a81d6-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="a81d6-153">Merhaba DR sitesinde bir uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="a81d6-153">One application service on hello DR site</span></span>
- <span data-ttu-id="a81d6-154">Erişim toohello özel ağ kısıtlar ve yalnızca bir yönetici oturum aç sağlayan bir jumpbox</span><span class="sxs-lookup"><span data-stu-id="a81d6-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="a81d6-155">Jumpbox, uygulama hizmeti, veritabanı ve VPN ağ geçidi ayrı alt ağlarda bulunan</span><span class="sxs-lookup"><span data-stu-id="a81d6-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="a81d6-156">Uygulama ve veritabanı alt ağlar üzerinde zorunlu NSG</span><span class="sxs-lookup"><span data-stu-id="a81d6-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="a81d6-157">Şirket içi ve Azure arasında siteden siteye VPN bağlantısı</span><span class="sxs-lookup"><span data-stu-id="a81d6-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Merhaba DR topoloji sayfasının ekran görüntüsü](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="a81d6-159">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a81d6-159">Additional reading</span></span>

- [<span data-ttu-id="a81d6-160">Bir Oracle veritabanına Azure üzerinde tasarlayıp</span><span class="sxs-lookup"><span data-stu-id="a81d6-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="a81d6-161">Oracle Data Guard yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a81d6-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="a81d6-162">Oracle Golden kapısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a81d6-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="a81d6-163">Oracle yedekleme ve kurtarma</span><span class="sxs-lookup"><span data-stu-id="a81d6-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="a81d6-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a81d6-164">Next steps</span></span>

- [<span data-ttu-id="a81d6-165">Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a81d6-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="a81d6-166">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="a81d6-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
