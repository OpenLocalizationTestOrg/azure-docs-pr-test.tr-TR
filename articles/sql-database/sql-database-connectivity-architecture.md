---
title: "aaaAzure SQL veritabanı bağlantısı mimarisi | Microsoft Docs"
description: "Bu belge hello Azure SQLDB bağlantı mimarisinden Azure içinde veya gelen açıklar Azure dışında."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="8db3b-103">Azure SQL veritabanı bağlantısı mimarisi</span><span class="sxs-lookup"><span data-stu-id="8db3b-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="8db3b-104">Bu makalede hello Azure SQL veritabanı bağlantısı mimarisini açıklar ve nasıl hello farklı bileşenleri toodirect trafiği tooyour Azure SQL veritabanı örneğini işlev açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8db3b-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="8db3b-105">Bu Azure SQL veritabanı bağlantısı bileşenlerinin toodirect ağ trafiği toohello Azure veritabanı içinden Azure bağlanan istemciler ve Azure dışında bağlantı istemcileri ile işlev.</span><span class="sxs-lookup"><span data-stu-id="8db3b-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="8db3b-106">Bu makalede ayrıca bağlantı nasıl gerçekleştiğini kod örnekleri toochange sağlar ve hello konuları ilgili toochanging hello varsayılan bağlantı ayarları.</span><span class="sxs-lookup"><span data-stu-id="8db3b-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="8db3b-107">Varsa herhangi bir sorunuz bu makaleyi okuduktan sonra Dhruv adresindeki temasa dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8db3b-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="8db3b-108">Bağlantı mimarisi</span><span class="sxs-lookup"><span data-stu-id="8db3b-108">Connectivity architecture</span></span>

<span data-ttu-id="8db3b-109">Aşağıdaki diyagramda hello hello Azure SQL veritabanı bağlantısı mimarisinin üst düzey bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="8db3b-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="8db3b-111">Merhaba aşağıdakileri nasıl bir bağlantı hello Azure SQL veritabanı yazılım yük dengeleyici (SLB) ve hello Azure SQL veritabanı ağ geçidi ile kurulan tooan Azure SQL veritabanı olduğunu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="8db3b-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="8db3b-112">İstemcileri Azure içinde veya Azure dışında toohello bir ortak IP adresi vardır ve 1433 bağlantı noktasını dinler SLB bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8db3b-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="8db3b-113">Merhaba SLB trafiği toohello Azure SQL veritabanı ağ geçidi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="8db3b-114">Merhaba ağ geçidi hello trafiği toohello doğru proxy Ara yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="8db3b-115">Merhaba proxy Ara hello trafiği toohello uygun Azure SQL veritabanı yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8db3b-116">Bu bileşenlerin her birini engelleme (DDoS) hizmeti koruma hello ağ ve hello uygulama katmanı yerleşik dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="8db3b-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="8db3b-117">Azure içinde bağlantısı</span><span class="sxs-lookup"><span data-stu-id="8db3b-117">Connectivity from within Azure</span></span>

<span data-ttu-id="8db3b-118">Azure içinde içinden bağlanan bağlantılarınızı bir bağlantı ilkesi varsa **yeniden yönlendirme** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="8db3b-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="8db3b-119">Bir ilke **yeniden yönlendirme** kurulan toohello Azure SQL veritabanı hello TCP oturumu tamamlandıktan sonra bağlantılar, hello istemci oturumu anlamına gelir sonra toohello proxy Ara yazılımla bir değişiklik toohello hedef sanal IP yeniden yönlendirildi hello Azure SQL veritabanı ağ geçidi toothat hello proxy ara yazılım,.</span><span class="sxs-lookup"><span data-stu-id="8db3b-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="8db3b-120">Bundan sonra tüm sonraki paketlere hello Azure SQL veritabanı ağ geçidi atlayarak doğrudan hello proxy ara yazılımı üzerinden, akış.</span><span class="sxs-lookup"><span data-stu-id="8db3b-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="8db3b-121">Aşağıdaki diyagramda hello Bu trafik akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-121">hello following diagram illustrates this traffic flow.</span></span>

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="8db3b-123">Azure dışında bağlantısı</span><span class="sxs-lookup"><span data-stu-id="8db3b-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="8db3b-124">Dış Azure'dan bağlanıyorsanız, bir bağlantı İlkesi bağlantınız **Proxy** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="8db3b-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="8db3b-125">Bir ilke **Proxy** hello TCP oturumu yoluyla hello Azure SQL veritabanı ağ geçidi kuruldu ve tüm sonraki paketlere aracılığıyla akış anlamına gelir. ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="8db3b-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="8db3b-126">Aşağıdaki diyagramda hello Bu trafik akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-126">hello following diagram illustrates this traffic flow.</span></span>

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="8db3b-128">Azure SQL veritabanı ağ geçidi IP adresi</span><span class="sxs-lookup"><span data-stu-id="8db3b-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="8db3b-129">Şirket içi kaynaklardan tooconnect tooan Azure SQL database, Azure bölgeniz için tooallow giden ağ trafiğini toohello Azure SQL veritabanı ağ geçidi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="8db3b-130">Bağlantılarınızı hello ağ geçidi şirket kaynaklarına bağlanırken hello varsayılandır Proxy modunda bağlanırken yalnızca gidin.</span><span class="sxs-lookup"><span data-stu-id="8db3b-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="8db3b-131">Aşağıdaki tabloda hello hello Azure SQL veritabanı ağ geçidinin tüm veri bölgeleri için birincil ve ikincil IP'leri hello.</span><span class="sxs-lookup"><span data-stu-id="8db3b-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="8db3b-132">Bazı bölgelerde, iki IP adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="8db3b-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="8db3b-133">Bu bölgelerde hello birincil IP adresi hello ağ geçidinin hello geçerli IP adresini ve hello ikinci IP adresi bir yük devretme IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="8db3b-134">Başlangıç adresi toowhich, sunucu tookeep hello hizmet kullanılabilirliği yüksek taşıma Hello yük devretme adresidir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="8db3b-135">Bu bölgeler için giden tooboth hello IP adreslerinin izin öneririz.</span><span class="sxs-lookup"><span data-stu-id="8db3b-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="8db3b-136">Merhaba ikinci IP adresi, Microsoft tarafından sahip olunan ve Azure SQL veritabanı tooaccept bağlantılar tarafından etkinleştirilene kadar hizmetlerin üzerinde dinlemez.</span><span class="sxs-lookup"><span data-stu-id="8db3b-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="8db3b-137">Bölge Adı</span><span class="sxs-lookup"><span data-stu-id="8db3b-137">Region Name</span></span> | <span data-ttu-id="8db3b-138">Birincil IP adresi</span><span class="sxs-lookup"><span data-stu-id="8db3b-138">Primary IP address</span></span> | <span data-ttu-id="8db3b-139">İkincil IP adresi</span><span class="sxs-lookup"><span data-stu-id="8db3b-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="8db3b-140">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="8db3b-140">Australia East</span></span> | <span data-ttu-id="8db3b-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="8db3b-141">191.238.66.109</span></span> | <span data-ttu-id="8db3b-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="8db3b-142">13.75.149.87</span></span> |
| <span data-ttu-id="8db3b-143">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="8db3b-143">Australia South East</span></span> | <span data-ttu-id="8db3b-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="8db3b-144">191.239.192.109</span></span> | <span data-ttu-id="8db3b-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="8db3b-145">13.73.109.251</span></span> |
| <span data-ttu-id="8db3b-146">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="8db3b-146">Brazil South</span></span> | <span data-ttu-id="8db3b-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="8db3b-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="8db3b-148">Orta Kanada</span><span class="sxs-lookup"><span data-stu-id="8db3b-148">Canada Central</span></span> | <span data-ttu-id="8db3b-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="8db3b-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="8db3b-150">Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="8db3b-150">Canada East</span></span> | <span data-ttu-id="8db3b-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="8db3b-151">40.86.226.166</span></span> | |
| <span data-ttu-id="8db3b-152">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="8db3b-152">Central US</span></span> | <span data-ttu-id="8db3b-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="8db3b-153">23.99.160.139</span></span> | <span data-ttu-id="8db3b-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="8db3b-154">13.67.215.62</span></span> |
| <span data-ttu-id="8db3b-155">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="8db3b-155">East Asia</span></span> | <span data-ttu-id="8db3b-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="8db3b-156">191.234.2.139</span></span> | <span data-ttu-id="8db3b-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="8db3b-157">52.175.33.150</span></span> |
| <span data-ttu-id="8db3b-158">Doğu ABD 1</span><span class="sxs-lookup"><span data-stu-id="8db3b-158">East US 1</span></span> | <span data-ttu-id="8db3b-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="8db3b-159">191.238.6.43</span></span> | <span data-ttu-id="8db3b-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="8db3b-160">40.121.158.30</span></span> |
| <span data-ttu-id="8db3b-161">Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="8db3b-161">East US 2</span></span> | <span data-ttu-id="8db3b-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="8db3b-162">191.239.224.107</span></span> | <span data-ttu-id="8db3b-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="8db3b-163">40.79.84.180</span></span> |
| <span data-ttu-id="8db3b-164">Hindistan Orta</span><span class="sxs-lookup"><span data-stu-id="8db3b-164">India Central</span></span> | <span data-ttu-id="8db3b-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="8db3b-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="8db3b-166">Hindistan Güney</span><span class="sxs-lookup"><span data-stu-id="8db3b-166">India South</span></span> | <span data-ttu-id="8db3b-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="8db3b-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="8db3b-168">Hindistan Batı</span><span class="sxs-lookup"><span data-stu-id="8db3b-168">India West</span></span> | <span data-ttu-id="8db3b-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="8db3b-169">104.211.160.80</span></span> | |
| <span data-ttu-id="8db3b-170">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="8db3b-170">Japan East</span></span> | <span data-ttu-id="8db3b-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="8db3b-171">191.237.240.43</span></span> | <span data-ttu-id="8db3b-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="8db3b-172">13.78.61.196</span></span> |
| <span data-ttu-id="8db3b-173">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="8db3b-173">Japan West</span></span> | <span data-ttu-id="8db3b-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="8db3b-174">191.238.68.11</span></span> | <span data-ttu-id="8db3b-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="8db3b-175">104.214.148.156</span></span> |
| <span data-ttu-id="8db3b-176">Kore Orta</span><span class="sxs-lookup"><span data-stu-id="8db3b-176">Korea Central</span></span> | <span data-ttu-id="8db3b-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="8db3b-177">52.231.32.42</span></span> | |
| <span data-ttu-id="8db3b-178">Kore Güney</span><span class="sxs-lookup"><span data-stu-id="8db3b-178">Korea South</span></span> | <span data-ttu-id="8db3b-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="8db3b-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="8db3b-180">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="8db3b-180">North Central US</span></span> | <span data-ttu-id="8db3b-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="8db3b-181">23.98.55.75</span></span> | <span data-ttu-id="8db3b-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="8db3b-182">23.96.178.199</span></span> |
| <span data-ttu-id="8db3b-183">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="8db3b-183">North Europe</span></span> | <span data-ttu-id="8db3b-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="8db3b-184">191.235.193.75</span></span> | <span data-ttu-id="8db3b-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="8db3b-185">40.113.93.91</span></span> |
| <span data-ttu-id="8db3b-186">Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="8db3b-186">South Central US</span></span> | <span data-ttu-id="8db3b-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="8db3b-187">23.98.162.75</span></span> | <span data-ttu-id="8db3b-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="8db3b-188">13.66.62.124</span></span> |
| <span data-ttu-id="8db3b-189">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="8db3b-189">South East Asia</span></span> | <span data-ttu-id="8db3b-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="8db3b-190">23.100.117.95</span></span> | <span data-ttu-id="8db3b-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="8db3b-191">104.43.15.0</span></span> |
| <span data-ttu-id="8db3b-192">UK Kuzey</span><span class="sxs-lookup"><span data-stu-id="8db3b-192">UK North</span></span> | <span data-ttu-id="8db3b-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="8db3b-193">13.87.97.210</span></span> | |
| <span data-ttu-id="8db3b-194">Birleşik Krallık Güney 1</span><span class="sxs-lookup"><span data-stu-id="8db3b-194">UK South 1</span></span> | <span data-ttu-id="8db3b-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="8db3b-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="8db3b-196">UK Güney 2</span><span class="sxs-lookup"><span data-stu-id="8db3b-196">UK South 2</span></span> | <span data-ttu-id="8db3b-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="8db3b-197">13.87.34.7</span></span> | |
| <span data-ttu-id="8db3b-198">Birleşik Krallık Batı</span><span class="sxs-lookup"><span data-stu-id="8db3b-198">UK West</span></span> | <span data-ttu-id="8db3b-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="8db3b-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="8db3b-200">Batı Orta ABD</span><span class="sxs-lookup"><span data-stu-id="8db3b-200">West Central US</span></span> | <span data-ttu-id="8db3b-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="8db3b-201">13.78.145.25</span></span> | |
| <span data-ttu-id="8db3b-202">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="8db3b-202">West Europe</span></span> | <span data-ttu-id="8db3b-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="8db3b-203">191.237.232.75</span></span> | <span data-ttu-id="8db3b-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="8db3b-204">40.68.37.158</span></span> |
| <span data-ttu-id="8db3b-205">Batı ABD 1</span><span class="sxs-lookup"><span data-stu-id="8db3b-205">West US 1</span></span> | <span data-ttu-id="8db3b-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="8db3b-206">23.99.34.75</span></span> | <span data-ttu-id="8db3b-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="8db3b-207">104.42.238.205</span></span> |
| <span data-ttu-id="8db3b-208">Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="8db3b-208">West US 2</span></span> | <span data-ttu-id="8db3b-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="8db3b-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="8db3b-210">Azure SQL veritabanı bağlantı ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="8db3b-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="8db3b-211">toochange hello kullan hello bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı İlkesi [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="8db3b-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="8db3b-212">Bağlantı ilkeniz çok ayarlarsanız**Proxy**, tüm paketlerin akışı hello Azure SQL veritabanı ağ geçidi aracılığıyla ağ.</span><span class="sxs-lookup"><span data-stu-id="8db3b-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="8db3b-213">Bu ayar için tooallow giden tooonly hello Azure SQL veritabanı ağ geçidi IP gerekir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="8db3b-214">Ayarı kullanarak **Proxy** ayarı'den daha fazla gecikme sahip **yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="8db3b-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="8db3b-215">Bağlantı ilkeniz ayarlıyorsanız **yeniden yönlendirme**, tüm ağ paketlerinin doğrudan toohello ara proxy akış.</span><span class="sxs-lookup"><span data-stu-id="8db3b-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="8db3b-216">Bu ayar için tooallow giden toomultiple IP'leri gerekir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="8db3b-217">Komut dosyası toochange bağlantı ayarları</span><span class="sxs-lookup"><span data-stu-id="8db3b-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8db3b-218">Bu komut dosyası hello gerektirir [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8db3b-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="8db3b-219">PowerShell Betiği aşağıdaki hello nasıl toochange hello bağlantı İlkesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="8db3b-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="8db3b-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8db3b-220">Next steps</span></span>

- <span data-ttu-id="8db3b-221">Nasıl toochange hello Azure SQL veritabanı bağlantı ilkesi için bir Azure SQL veritabanı sunucusu hakkında daha fazla bilgi için bkz: [hello REST API'si oluşturma veya güncelleştirme sunucusu bağlantısı İlkesi kullanarak](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="8db3b-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="8db3b-222">ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için Azure SQL veritabanı bağlantı davranışı hakkında bilgi için bkz: [ADO.NET 4.5 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="8db3b-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="8db3b-223">Genel uygulama geliştirme genel bakış bilgileri için bkz: [SQL veritabanı uygulaması geliştirmeye genel bakış](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8db3b-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
