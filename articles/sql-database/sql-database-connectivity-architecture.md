---
title: "Azure SQL veritabanı bağlantısı mimarisi | Microsoft Docs"
description: "Bu belgede Azure SQLDB bağlantı mimarisinden Azure içinde veya gelen açıklanmaktadır Azure dışında."
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
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="679d7-103">Azure SQL veritabanı bağlantısı mimarisi</span><span class="sxs-lookup"><span data-stu-id="679d7-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="679d7-104">Bu makalede, Azure SQL veritabanı bağlantısı mimarisini açıklar ve nasıl doğrudan trafiğe örneğinizi Azure SQL veritabanı için farklı bileşenleri işlev açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="679d7-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="679d7-105">İçinden Azure bağlanan istemciler ve istemcilerin Azure dışında bağlantı ile Azure veritabanı ağ trafiğini yönlendirmek için bu Azure SQL veritabanı bağlantısı bileşenleri işlevi.</span><span class="sxs-lookup"><span data-stu-id="679d7-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="679d7-106">Bu makalede ayrıca bağlantı nasıl gerçekleştiğini değiştirmek için kod örnekleri ve varsayılan bağlantı ayarlarını değiştirmek için ilgili dikkat edilecek noktalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="679d7-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="679d7-107">Varsa herhangi bir sorunuz bu makaleyi okuduktan sonra Dhruv adresindeki temasa dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="679d7-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="679d7-108">Bağlantı mimarisi</span><span class="sxs-lookup"><span data-stu-id="679d7-108">Connectivity architecture</span></span>

<span data-ttu-id="679d7-109">Aşağıdaki diyagramda Azure SQL veritabanı bağlantısı mimarisinin üst düzey bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="679d7-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="679d7-111">Aşağıdaki adımlar, Azure SQL veritabanı yazılım yük dengeleyici (SLB) ve Azure SQL veritabanı ağ geçidi ile bir Azure SQL veritabanı için bir bağlantının nasıl kurulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="679d7-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="679d7-112">İstemcileri Azure içinde veya Azure dışında bir ortak IP adresi vardır ve 1433 bağlantı noktasını dinler SLB bağlayın.</span><span class="sxs-lookup"><span data-stu-id="679d7-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="679d7-113">SLB Azure SQL veritabanı ağ trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="679d7-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="679d7-114">Ağ geçidi doğru proxy Ara trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="679d7-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="679d7-115">Proxy Ara trafiği uygun Azure SQL veritabanına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="679d7-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="679d7-116">Bu bileşenlerin her birini koruma hizmeti (DDoS) ağ ve uygulama katmanı yerleşik reddi dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="679d7-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="679d7-117">Azure içinde bağlantısı</span><span class="sxs-lookup"><span data-stu-id="679d7-117">Connectivity from within Azure</span></span>

<span data-ttu-id="679d7-118">Azure içinde içinden bağlanan bağlantılarınızı bir bağlantı ilkesi varsa **yeniden yönlendirme** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="679d7-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="679d7-119">Bir ilke **yeniden yönlendirme** TCP oturumu Azure SQL veritabanı için istemci oturum kurulduktan sonra bağlantıları sonra yönlendirildiği olduğunu proxy ara yazılımı için bir hedef sanal IP değişiklik olanlardan Azure ile anlamına gelir SQL veritabanı ağ geçidi, proxy ara yazılım.</span><span class="sxs-lookup"><span data-stu-id="679d7-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="679d7-120">Bundan sonra tüm sonraki paketlere Azure SQL veritabanı ağ geçidi atlayarak doğrudan proxy ara yazılımı üzerinden, akış.</span><span class="sxs-lookup"><span data-stu-id="679d7-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="679d7-121">Aşağıdaki diyagramda bu trafik akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="679d7-121">The following diagram illustrates this traffic flow.</span></span>

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="679d7-123">Azure dışında bağlantısı</span><span class="sxs-lookup"><span data-stu-id="679d7-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="679d7-124">Dış Azure'dan bağlanıyorsanız, bir bağlantı İlkesi bağlantınız **Proxy** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="679d7-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="679d7-125">Bir ilke **Proxy** Azure SQL veritabanı ağ geçidi TCP oturumun ve tüm sonraki paketlere akış yoluyla ağ geçidi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="679d7-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="679d7-126">Aşağıdaki diyagramda bu trafik akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="679d7-126">The following diagram illustrates this traffic flow.</span></span>

![mimarisine genel bakış](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="679d7-128">Azure SQL veritabanı ağ geçidi IP adresi</span><span class="sxs-lookup"><span data-stu-id="679d7-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="679d7-129">Şirket içi kaynaklardan bir Azure SQL veritabanına bağlanmak için Azure SQL veritabanı ağ geçidi Azure bölgeniz için giden ağ trafiğine izin vermeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="679d7-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="679d7-130">Bağlantılarınızı yoluyla ağ geçidi şirket içi kaynaklardan bağlanırken varsayılandır Proxy modunda bağlanırken yalnızca gidin.</span><span class="sxs-lookup"><span data-stu-id="679d7-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="679d7-131">Aşağıdaki tabloda Azure SQL veritabanı ağ geçidi tüm veri bölgeleri için birincil ve ikincil IP'leri listeler.</span><span class="sxs-lookup"><span data-stu-id="679d7-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="679d7-132">Bazı bölgelerde, iki IP adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="679d7-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="679d7-133">Bu bölgelerde, birincil IP adresi ağ geçidi geçerli IP adresini ve ikinci IP adresi bir yük devretme IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="679d7-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="679d7-134">Yük devretme adresi için size hizmet kullanılabilirliği yüksek tutmak için sunucu taşıma adresidir.</span><span class="sxs-lookup"><span data-stu-id="679d7-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="679d7-135">Bu bölgeler için her iki IP adreslerine giden izin öneririz.</span><span class="sxs-lookup"><span data-stu-id="679d7-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="679d7-136">İkinci IP adresi, Microsoft tarafından sahip olunan ve bağlantıları kabul etmek üzere Azure SQL veritabanı tarafından etkinleştirilene kadar hizmetlerin üzerinde dinlemez.</span><span class="sxs-lookup"><span data-stu-id="679d7-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="679d7-137">Bölge Adı</span><span class="sxs-lookup"><span data-stu-id="679d7-137">Region Name</span></span> | <span data-ttu-id="679d7-138">Birincil IP adresi</span><span class="sxs-lookup"><span data-stu-id="679d7-138">Primary IP address</span></span> | <span data-ttu-id="679d7-139">İkincil IP adresi</span><span class="sxs-lookup"><span data-stu-id="679d7-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="679d7-140">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="679d7-140">Australia East</span></span> | <span data-ttu-id="679d7-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="679d7-141">191.238.66.109</span></span> | <span data-ttu-id="679d7-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="679d7-142">13.75.149.87</span></span> |
| <span data-ttu-id="679d7-143">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="679d7-143">Australia South East</span></span> | <span data-ttu-id="679d7-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="679d7-144">191.239.192.109</span></span> | <span data-ttu-id="679d7-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="679d7-145">13.73.109.251</span></span> |
| <span data-ttu-id="679d7-146">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="679d7-146">Brazil South</span></span> | <span data-ttu-id="679d7-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="679d7-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="679d7-148">Orta Kanada</span><span class="sxs-lookup"><span data-stu-id="679d7-148">Canada Central</span></span> | <span data-ttu-id="679d7-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="679d7-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="679d7-150">Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="679d7-150">Canada East</span></span> | <span data-ttu-id="679d7-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="679d7-151">40.86.226.166</span></span> | |
| <span data-ttu-id="679d7-152">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="679d7-152">Central US</span></span> | <span data-ttu-id="679d7-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="679d7-153">23.99.160.139</span></span> | <span data-ttu-id="679d7-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="679d7-154">13.67.215.62</span></span> |
| <span data-ttu-id="679d7-155">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="679d7-155">East Asia</span></span> | <span data-ttu-id="679d7-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="679d7-156">191.234.2.139</span></span> | <span data-ttu-id="679d7-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="679d7-157">52.175.33.150</span></span> |
| <span data-ttu-id="679d7-158">Doğu ABD 1</span><span class="sxs-lookup"><span data-stu-id="679d7-158">East US 1</span></span> | <span data-ttu-id="679d7-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="679d7-159">191.238.6.43</span></span> | <span data-ttu-id="679d7-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="679d7-160">40.121.158.30</span></span> |
| <span data-ttu-id="679d7-161">Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="679d7-161">East US 2</span></span> | <span data-ttu-id="679d7-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="679d7-162">191.239.224.107</span></span> | <span data-ttu-id="679d7-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="679d7-163">40.79.84.180</span></span> |
| <span data-ttu-id="679d7-164">Hindistan Orta</span><span class="sxs-lookup"><span data-stu-id="679d7-164">India Central</span></span> | <span data-ttu-id="679d7-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="679d7-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="679d7-166">Hindistan Güney</span><span class="sxs-lookup"><span data-stu-id="679d7-166">India South</span></span> | <span data-ttu-id="679d7-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="679d7-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="679d7-168">Hindistan Batı</span><span class="sxs-lookup"><span data-stu-id="679d7-168">India West</span></span> | <span data-ttu-id="679d7-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="679d7-169">104.211.160.80</span></span> | |
| <span data-ttu-id="679d7-170">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="679d7-170">Japan East</span></span> | <span data-ttu-id="679d7-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="679d7-171">191.237.240.43</span></span> | <span data-ttu-id="679d7-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="679d7-172">13.78.61.196</span></span> |
| <span data-ttu-id="679d7-173">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="679d7-173">Japan West</span></span> | <span data-ttu-id="679d7-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="679d7-174">191.238.68.11</span></span> | <span data-ttu-id="679d7-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="679d7-175">104.214.148.156</span></span> |
| <span data-ttu-id="679d7-176">Kore Orta</span><span class="sxs-lookup"><span data-stu-id="679d7-176">Korea Central</span></span> | <span data-ttu-id="679d7-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="679d7-177">52.231.32.42</span></span> | |
| <span data-ttu-id="679d7-178">Kore Güney</span><span class="sxs-lookup"><span data-stu-id="679d7-178">Korea South</span></span> | <span data-ttu-id="679d7-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="679d7-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="679d7-180">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="679d7-180">North Central US</span></span> | <span data-ttu-id="679d7-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="679d7-181">23.98.55.75</span></span> | <span data-ttu-id="679d7-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="679d7-182">23.96.178.199</span></span> |
| <span data-ttu-id="679d7-183">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="679d7-183">North Europe</span></span> | <span data-ttu-id="679d7-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="679d7-184">191.235.193.75</span></span> | <span data-ttu-id="679d7-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="679d7-185">40.113.93.91</span></span> |
| <span data-ttu-id="679d7-186">Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="679d7-186">South Central US</span></span> | <span data-ttu-id="679d7-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="679d7-187">23.98.162.75</span></span> | <span data-ttu-id="679d7-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="679d7-188">13.66.62.124</span></span> |
| <span data-ttu-id="679d7-189">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="679d7-189">South East Asia</span></span> | <span data-ttu-id="679d7-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="679d7-190">23.100.117.95</span></span> | <span data-ttu-id="679d7-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="679d7-191">104.43.15.0</span></span> |
| <span data-ttu-id="679d7-192">UK Kuzey</span><span class="sxs-lookup"><span data-stu-id="679d7-192">UK North</span></span> | <span data-ttu-id="679d7-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="679d7-193">13.87.97.210</span></span> | |
| <span data-ttu-id="679d7-194">Birleşik Krallık Güney 1</span><span class="sxs-lookup"><span data-stu-id="679d7-194">UK South 1</span></span> | <span data-ttu-id="679d7-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="679d7-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="679d7-196">UK Güney 2</span><span class="sxs-lookup"><span data-stu-id="679d7-196">UK South 2</span></span> | <span data-ttu-id="679d7-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="679d7-197">13.87.34.7</span></span> | |
| <span data-ttu-id="679d7-198">Birleşik Krallık Batı</span><span class="sxs-lookup"><span data-stu-id="679d7-198">UK West</span></span> | <span data-ttu-id="679d7-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="679d7-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="679d7-200">Batı Orta ABD</span><span class="sxs-lookup"><span data-stu-id="679d7-200">West Central US</span></span> | <span data-ttu-id="679d7-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="679d7-201">13.78.145.25</span></span> | |
| <span data-ttu-id="679d7-202">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="679d7-202">West Europe</span></span> | <span data-ttu-id="679d7-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="679d7-203">191.237.232.75</span></span> | <span data-ttu-id="679d7-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="679d7-204">40.68.37.158</span></span> |
| <span data-ttu-id="679d7-205">Batı ABD 1</span><span class="sxs-lookup"><span data-stu-id="679d7-205">West US 1</span></span> | <span data-ttu-id="679d7-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="679d7-206">23.99.34.75</span></span> | <span data-ttu-id="679d7-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="679d7-207">104.42.238.205</span></span> |
| <span data-ttu-id="679d7-208">Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="679d7-208">West US 2</span></span> | <span data-ttu-id="679d7-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="679d7-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="679d7-210">Azure SQL veritabanı bağlantı ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="679d7-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="679d7-211">Bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı ilkesini değiştirmek için kullanın [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="679d7-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="679d7-212">Bağlantı ilkeniz ayarlanmışsa **Proxy**, tüm Azure SQL veritabanı ağ geçidi üzerinden paket akışı ağ.</span><span class="sxs-lookup"><span data-stu-id="679d7-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="679d7-213">Bu ayar, yalnızca Azure SQL veritabanı ağ geçidi IP giden izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="679d7-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="679d7-214">Ayarı kullanarak **Proxy** ayarı'den daha fazla gecikme sahip **yeniden yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="679d7-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="679d7-215">Bağlantı ilkeniz ayarlıyorsanız **yeniden yönlendirme**, tüm paketler akışına doğrudan ara proxy ağ.</span><span class="sxs-lookup"><span data-stu-id="679d7-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="679d7-216">Bu ayar için birden çok IP giden izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="679d7-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="679d7-217">Bağlantı ayarlarını değiştirmek için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="679d7-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="679d7-218">Bu komut dosyası gerektirir [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="679d7-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="679d7-219">Aşağıdaki PowerShell betiğini nasıl bir bağlantı İlkesi değiştirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="679d7-219">The following PowerShell script shows how to change the connection policy.</span></span>

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

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="679d7-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="679d7-220">Next steps</span></span>

- <span data-ttu-id="679d7-221">Bir Azure SQL veritabanı sunucusu için Azure SQL veritabanı bağlantı ilkesini değiştirme hakkında daha fazla bilgi için bkz: [oluşturma veya güncelleştirme sunucusu bağlantısı REST API kullanarak İlkesi](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="679d7-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="679d7-222">ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için Azure SQL veritabanı bağlantı davranışı hakkında bilgi için bkz: [ADO.NET 4.5 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="679d7-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="679d7-223">Genel uygulama geliştirme genel bakış bilgileri için bkz: [SQL veritabanı uygulaması geliştirmeye genel bakış](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="679d7-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
