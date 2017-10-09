---
title: "S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE ilkesi yapılandırın: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile IPSec/IKE İlkesi S2S veya VNet-VNet bağlantıları için nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="06028-103">S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06028-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="06028-104">Bu makalede, hello adımları tooconfigure hello Resource Manager dağıtım modeli ve PowerShell kullanarak siteden siteye VPN veya VNet-VNet bağlantıları için IPSec/IKE İlkesi adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="06028-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="06028-105"><a name="about"></a>IPSec ve IKE İlkesi parametreleri hakkında Azure VPN ağ geçitleri için</span><span class="sxs-lookup"><span data-stu-id="06028-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="06028-106">IPSec ve IKE protokolü standart çeşitli bileşimlerde çok çeşitli şifreleme algoritmalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="06028-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="06028-107">Çok başvuran[şifreleme gereksinimleri ve Azure VPN ağ geçitleri hakkında](vpn-gateway-about-compliance-crypto.md) toosee nasıl bu yardımcı şirketler arası ve VNet-VNet bağlantısı sağlayarak, uyumluluk ve güvenlik gereksinimleri karşılar.</span><span class="sxs-lookup"><span data-stu-id="06028-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="06028-108">Bu makalede yönergeleri toocreate sağlar ve bir IPSec/IKE ilkesi yapılandırma ve tooa yeni veya var olan bağlantı Uygula:</span><span class="sxs-lookup"><span data-stu-id="06028-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="06028-109">Bölüm 1 - iş akışı toocreate ve IPSec/IKE ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="06028-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="06028-110">Desteklenen bölüm 2 - şifreleme algoritmaları ve anahtar gücü</span><span class="sxs-lookup"><span data-stu-id="06028-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="06028-111">Bölüm 3 - IPSec/IKE İlkesi ile yeni bir S2S VPN bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="06028-112">4 Kısım - yeni bir VNet-VNet bağlantı IPSec/IKE ilkesiyle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06028-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="06028-113">Bölüm 5 - yönetme (oluşturma, ekleme, kaldırma) bir bağlantı için IPSec/IKE İlkesi</span><span class="sxs-lookup"><span data-stu-id="06028-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="06028-114">IPSec/IKE ilkesi yalnızca ağ geçidi SKU'ları aşağıdaki hello üzerinde çalıştığını unutmayın:</span><span class="sxs-lookup"><span data-stu-id="06028-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="06028-115">***VpnGw1, VpnGw2, VpnGw3*** (rota tabanlı)</span><span class="sxs-lookup"><span data-stu-id="06028-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="06028-116">***Standart*** ve ***HighPerformance*** (rota tabanlı)</span><span class="sxs-lookup"><span data-stu-id="06028-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="06028-117">Belirli bir bağlantı için yalnızca ***bir*** ilke birleşimi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06028-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="06028-118">IKE (ana mod) ve IPSec (hızlı mod) için tüm algoritmalar ve parametreleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06028-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="06028-119">Kısmi ilke belirtimine izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="06028-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="06028-120">Şirket içi VPN cihazlarınızı tooensure hello İlkesi desteklenen VPN cihaz Satıcı belirtimleri başvurun.</span><span class="sxs-lookup"><span data-stu-id="06028-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="06028-121">Merhaba ilkeleri uyumlu olup olmadığını S2S veya VNet-VNet bağlantı kurulamıyor.</span><span class="sxs-lookup"><span data-stu-id="06028-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="06028-122"><a name ="workflow"></a>Bölüm 1 - iş akışı toocreate ve IPSec/IKE ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="06028-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="06028-123">Bu bölümde bir S2S VPN veya VNet-VNet bağlantısı hello iş akışı toocreate ve güncelleştirme IPSec/IKE İlkesi özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="06028-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="06028-124">Sanal ağ ve VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="06028-125">Bir şirket içi bağlantı veya başka bir sanal ağ çapraz yerel ağ geçidi için ve VNet-VNet bağlantısı için ağ geçidi oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="06028-126">Seçilen algoritmalar ve parametrelerine sahip bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="06028-127">Merhaba IPSec/IKE ilkesiyle (IPSec veya VNet2VNet) bir bağlantı oluştur</span><span class="sxs-lookup"><span data-stu-id="06028-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="06028-128">Ekleme/güncelleştirme/kaldırma mevcut bir bağlantı için bir IPSec/IKE İlkesi</span><span class="sxs-lookup"><span data-stu-id="06028-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="06028-129">Bu makaledeki yönergeleri Hello ayarlamak ve hello diyagramda gösterildiği gibi IPSec/IKE ilkelerini yapılandırmanıza yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="06028-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![IPSec IKE İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="06028-131"><a name ="params"></a>Desteklenen bölüm 2 - şifreleme algoritmaları ve anahtar gücü</span><span class="sxs-lookup"><span data-stu-id="06028-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="06028-132">Merhaba aşağıdaki tabloda desteklenen hello şifreleme algoritmaları ve anahtar gücü yapılandırılabilir hello müşteriler listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="06028-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="06028-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="06028-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="06028-134">**Seçenekler**</span><span class="sxs-lookup"><span data-stu-id="06028-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="06028-135">IKEv2 Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="06028-135">IKEv2 Encryption</span></span> | <span data-ttu-id="06028-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="06028-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="06028-137">IKEv2 Bütünlüğü</span><span class="sxs-lookup"><span data-stu-id="06028-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="06028-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="06028-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="06028-139">DH Grubu</span><span class="sxs-lookup"><span data-stu-id="06028-139">DH Group</span></span>         | <span data-ttu-id="06028-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, yok</span><span class="sxs-lookup"><span data-stu-id="06028-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="06028-141">IPsec Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="06028-141">IPsec Encryption</span></span> | <span data-ttu-id="06028-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span><span class="sxs-lookup"><span data-stu-id="06028-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="06028-143">IPsec Bütünlüğü</span><span class="sxs-lookup"><span data-stu-id="06028-143">IPsec Integrity</span></span>  | <span data-ttu-id="06028-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="06028-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="06028-145">PFS Grubu</span><span class="sxs-lookup"><span data-stu-id="06028-145">PFS Group</span></span>        | <span data-ttu-id="06028-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="06028-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="06028-147">QM SA Yaşam Süresi</span><span class="sxs-lookup"><span data-stu-id="06028-147">QM SA Lifetime</span></span>   | <span data-ttu-id="06028-148">(**İsteğe bağlı**: varsayılan değerleri kullanılan belirtilmediğinde)</span><span class="sxs-lookup"><span data-stu-id="06028-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="06028-149">Saniye (tamsayı; **en az 300**/varsayılan 27000 saniye)</span><span class="sxs-lookup"><span data-stu-id="06028-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="06028-150">Kilobayt (tamsayı; **en az 1024**/varsayılan 102400000 kilobayt)</span><span class="sxs-lookup"><span data-stu-id="06028-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="06028-151">Trafik Seçicisi</span><span class="sxs-lookup"><span data-stu-id="06028-151">Traffic Selector</span></span> | <span data-ttu-id="06028-152">UsePolicyBasedTrafficSelectors ** ($True/$False; **İsteğe bağlı**, varsayılan $False belirtilmediğinde)</span><span class="sxs-lookup"><span data-stu-id="06028-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="06028-153">**GCMAES IPSec şifreleme algoritması için kullanılırsa, seçmelisiniz hello aynı GCMAES algoritması ve anahtar uzunluğu için IPSec bütünlüğü; Örneğin, GCMAES128 her ikisi için kullanma**</span><span class="sxs-lookup"><span data-stu-id="06028-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="06028-154">Ikev2 ana mod SA ömrü hello Azure VPN ağ geçitlerinde 28.800 saniyedir adresindeki sabit</span><span class="sxs-lookup"><span data-stu-id="06028-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="06028-155">"UsePolicyBasedTrafficSelectors" ayarı $True bir bağlantısı çok yapılandıracak Azure VPN ağ geçidi tooconnect toopolicy tabanlı VPN güvenlik duvarı şirket içi hello.</span><span class="sxs-lookup"><span data-stu-id="06028-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="06028-156">PolicyBasedTrafficSelectors etkinleştirdiğinizde, şirket içi ağ (yerel ağ geçidi) önekleri denetleyicisinden hello Azure sanal ağı önekleri tüm bileşimleri ile tanımlanmış hello eşleşen trafik Seçici VPN Cihazınızı sahip tooensure gerekir, any herhangi yerine.</span><span class="sxs-lookup"><span data-stu-id="06028-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="06028-157">Örneğin, 10.1.0.0/16 ve 10.2.0.0/16, şirket içi ağ ön ekleri ve 192.168.0.0/16 ve 172.16.0.0/16, sanal ağ ön ekleri, trafik Seçici aşağıdaki toospecify hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06028-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="06028-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="06028-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="06028-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="06028-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="06028-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="06028-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="06028-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="06028-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="06028-162">İlke tabanlı trafik Seçici ile ilgili daha fazla bilgi için bkz: [birden çok şirket içi ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="06028-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="06028-163">Aşağıdaki tabloda hello hello özel ilke tarafından desteklenen karşılık gelen Diffie-Hellman grupları hello:</span><span class="sxs-lookup"><span data-stu-id="06028-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="06028-164">**Diffie-Hellman Grubu**</span><span class="sxs-lookup"><span data-stu-id="06028-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="06028-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="06028-165">**DHGroup**</span></span>              | <span data-ttu-id="06028-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="06028-166">**PFSGroup**</span></span> | <span data-ttu-id="06028-167">**Anahtar uzunluğu**</span><span class="sxs-lookup"><span data-stu-id="06028-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06028-168">1</span><span class="sxs-lookup"><span data-stu-id="06028-168">1</span></span>                         | <span data-ttu-id="06028-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="06028-169">DHGroup1</span></span>                 | <span data-ttu-id="06028-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="06028-170">PFS1</span></span>         | <span data-ttu-id="06028-171">768 bit MODP</span><span class="sxs-lookup"><span data-stu-id="06028-171">768-bit MODP</span></span>   |
| <span data-ttu-id="06028-172">2</span><span class="sxs-lookup"><span data-stu-id="06028-172">2</span></span>                         | <span data-ttu-id="06028-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="06028-173">DHGroup2</span></span>                 | <span data-ttu-id="06028-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="06028-174">PFS2</span></span>         | <span data-ttu-id="06028-175">1024 bit MODP</span><span class="sxs-lookup"><span data-stu-id="06028-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="06028-176">14</span><span class="sxs-lookup"><span data-stu-id="06028-176">14</span></span>                        | <span data-ttu-id="06028-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="06028-177">DHGroup14</span></span><br><span data-ttu-id="06028-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="06028-178">DHGroup2048</span></span> | <span data-ttu-id="06028-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="06028-179">PFS2048</span></span>      | <span data-ttu-id="06028-180">2048 bit MODP</span><span class="sxs-lookup"><span data-stu-id="06028-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="06028-181">19</span><span class="sxs-lookup"><span data-stu-id="06028-181">19</span></span>                        | <span data-ttu-id="06028-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="06028-182">ECP256</span></span>                   | <span data-ttu-id="06028-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="06028-183">ECP256</span></span>       | <span data-ttu-id="06028-184">256 bit ECP</span><span class="sxs-lookup"><span data-stu-id="06028-184">256-bit ECP</span></span>    |
| <span data-ttu-id="06028-185">20</span><span class="sxs-lookup"><span data-stu-id="06028-185">20</span></span>                        | <span data-ttu-id="06028-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="06028-186">ECP384</span></span>                   | <span data-ttu-id="06028-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="06028-187">ECP284</span></span>       | <span data-ttu-id="06028-188">384 bit ECP</span><span class="sxs-lookup"><span data-stu-id="06028-188">384-bit ECP</span></span>    |
| <span data-ttu-id="06028-189">24</span><span class="sxs-lookup"><span data-stu-id="06028-189">24</span></span>                        | <span data-ttu-id="06028-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="06028-190">DHGroup24</span></span>                | <span data-ttu-id="06028-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="06028-191">PFS24</span></span>        | <span data-ttu-id="06028-192">2048 bit MODP</span><span class="sxs-lookup"><span data-stu-id="06028-192">2048-bit MODP</span></span>  |

<span data-ttu-id="06028-193">Çok başvuran[RFC3526](https://tools.ietf.org/html/rfc3526) ve [RFC5114](https://tools.ietf.org/html/rfc5114) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="06028-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="06028-194"><a name ="crossprem"></a>Bölüm 3 - IPSec/IKE İlkesi ile yeni bir S2S VPN bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="06028-195">Bu bölümde, bir IPSec/IKE ilkesiyle S2S VPN bağlantısı oluşturma hello adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="06028-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="06028-196">Merhaba aşağıdaki adımları hello bağlantı hello diyagramda gösterildiği gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="06028-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="06028-198">Bkz: [S2S VPN bağlantısı oluşturmak](vpn-gateway-create-site-to-site-rm-powershell.md) daha ayrıntılı bir S2S VPN bağlantısı oluşturmak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="06028-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="06028-199"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="06028-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="06028-200">Azure aboneliğiniz olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="06028-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="06028-201">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06028-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="06028-202">Hello Azure Resource Manager PowerShell cmdlet'lerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="06028-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="06028-203">Bkz: [Azure PowerShell genel bakış](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="06028-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="06028-204"><a name="createvnet1"></a>1. adım - hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="06028-205">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="06028-205">1. Declare your variables</span></span>

<span data-ttu-id="06028-206">Bu alıştırmada, değişkenlerimizi bildirerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="06028-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="06028-207">Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir.</span><span class="sxs-lookup"><span data-stu-id="06028-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="06028-208">2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="06028-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="06028-209">TooPowerShell modu toouse hello Resource Manager cmdlet'lerini geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="06028-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="06028-210">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="06028-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="06028-211">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="06028-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="06028-212">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="06028-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="06028-213">3. Merhaba sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="06028-214">Aşağıdaki örnek hello hello sanal ağ, TestVNet1, üç alt ağ ve hello VPN ağ geçidi ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="06028-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="06028-215">Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır.</span><span class="sxs-lookup"><span data-stu-id="06028-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="06028-216">Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="06028-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="06028-217"><a name="s2sconnection"></a>2. adım - bir IPSec/IKE İlkesi ile bir S2S VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="06028-218">1. Bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="06028-219">Aşağıdaki örnek betik hello oluşturur bir IPSec/IKE İlkesi ile Merhaba algoritmaları ve parametreleri aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="06028-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="06028-220">Ikev2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="06028-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="06028-221">IPSec: AES256, SHA256, PFS24, SA ömrü 7200 saniye & 2048KB</span><span class="sxs-lookup"><span data-stu-id="06028-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="06028-222">IPSec için GCMAES kullanıyorsanız, kullanmalısınız aynı GCMAES algoritması ve anahtar uzunluğu IPSec şifreleme ve bütünlüğünü hello örneğin:</span><span class="sxs-lookup"><span data-stu-id="06028-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="06028-223">Ikev2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="06028-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="06028-224">IPSec: **GCMAES256, GCMAES256**, PFS24, SA ömrü 7200 saniye & 2048 KB</span><span class="sxs-lookup"><span data-stu-id="06028-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="06028-225">2. IPSec/IKE İlkesi hello ile Merhaba S2S VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="06028-226">S2S VPN bağlantısı oluşturun ve daha önce oluşturduğunuz hello IPSec/IKE İlkesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="06028-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="06028-227">İsteğe bağlı olarak ekleyebileceğiniz "-UsePolicyBasedTrafficSelectors $True" toohello oluşturmak bağlantı cmdlet tooenable Azure VPN ağ geçidi tooconnect toopolicy tabanlı VPN aygıtlarını şirket içinde yukarıda açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="06028-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06028-228">Bir IPSec/IKE İlkesi bir bağlantıda belirlendikten sonra hello Azure VPN ağ geçidi yalnızca göndermek veya belirtilen şifreleme algoritmaları ve anahtar gücü belirli bu bağlantıda ile Merhaba IPSec/IKE teklifi kabul edin.</span><span class="sxs-lookup"><span data-stu-id="06028-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="06028-229">Şirket içi VPN aygıtınızın hello bağlantı kullanan veya hello tam İlkesi birleşimi, aksi takdirde hello S2S VPN tüneli değil kuracak kabul emin olun.</span><span class="sxs-lookup"><span data-stu-id="06028-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="06028-230"><a name ="vnet2vnet"></a>4 Kısım - yeni bir VNet-VNet bağlantı IPSec/IKE ilkesiyle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06028-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="06028-231">bir IPSec/IKE İlkesi ile bir VNet-VNet bağlantısı oluşturma hello S2S VPN bağlantısının benzer toothat adımlardır.</span><span class="sxs-lookup"><span data-stu-id="06028-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="06028-232">Merhaba aşağıdaki örnek komutlar hello bağlantı hello diyagramda gösterildiği gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="06028-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="06028-234">Bkz: [bir VNet-VNet bağlantısı oluşturma](vpn-gateway-vnet-vnet-rm-ps.md) daha ayrıntılı bir VNet-VNet bağlantı oluşturma adımları için.</span><span class="sxs-lookup"><span data-stu-id="06028-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="06028-235">Tamamlamanız gereken [bölümü 3](#crossprem) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="06028-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="06028-236"><a name="createvnet2"></a>1. adım - hello ikinci sanal ağ ve VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="06028-237">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="06028-237">1. Declare your variables</span></span>

<span data-ttu-id="06028-238">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="06028-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="06028-239">2. Merhaba yeni kaynak grubunda Hello ikinci sanal ağ ve VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="06028-240">2. adım - bir VNet toVNet bağlantı IPSec/IKE İlkesi hello ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="06028-241">Benzer toohello S2S VPN bağlantısı, bir IPSec/IKE ilkesi oluşturun ardından toopolicy toohello yeni bağlantı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="06028-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="06028-242">1. Bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="06028-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="06028-243">Aşağıdaki örnek betik hello hello ile başka bir IPSec/IKE ilke oluşturur algoritmaları ve parametreleri aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="06028-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="06028-244">Ikev2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="06028-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="06028-245">IPSec: GCMAES128, GCMAES128, PFS14, SA ömrü 7200 saniye ve 4096KB</span><span class="sxs-lookup"><span data-stu-id="06028-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="06028-246">2. VNet-VNet bağlantıları hello ile IPSec/IKE ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06028-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="06028-247">VNet-VNet bağlantı oluşturun ve oluşturduğunuz hello IPSec/IKE İlkesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="06028-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="06028-248">Bu örnekte, her iki ağ geçitleri hello olan aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="06028-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="06028-249">Olası toocreate olduğundan ve her iki bağlantıları ile yapılandırmak için hello aynı IPSec/IKE ilkesinde hello aynı PowerShell oturumunda.</span><span class="sxs-lookup"><span data-stu-id="06028-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="06028-250">Bir IPSec/IKE İlkesi bir bağlantıda belirlendikten sonra hello Azure VPN ağ geçidi yalnızca göndermek veya belirtilen şifreleme algoritmaları ve anahtar gücü belirli bu bağlantıda ile Merhaba IPSec/IKE teklifi kabul edin.</span><span class="sxs-lookup"><span data-stu-id="06028-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="06028-251">Hem bağlantılarını olan hello için aynı, aksi takdirde VNet-VNet bağlantısı olmayan kuracak emin hello IPSec ilkeleri hale getirir.</span><span class="sxs-lookup"><span data-stu-id="06028-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="06028-252">Bu adımları tamamladıktan sonra hello bağlantı birkaç dakika içinde oluşturulur ve ağ topolojisi hello'den itibaren gösterildiği gibi aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="06028-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![IPSec IKE İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="06028-254"><a name ="managepolicy"></a>Bölüm 5 - bir bağlantı için güncelleştirme IPSec/IKE İlkesi</span><span class="sxs-lookup"><span data-stu-id="06028-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="06028-255">Merhaba son Kısım gösterir, nasıl toomanage varolan S2S veya VNet-VNet bağlantı IPSec/IKE ilkesi.</span><span class="sxs-lookup"><span data-stu-id="06028-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="06028-256">Merhaba alıştırma aşağıdaki işlemleri bir bağlantısı aşağıdaki hello size yol göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="06028-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="06028-257">Merhaba IPSec/IKE İlkesi bağlantısının Göster</span><span class="sxs-lookup"><span data-stu-id="06028-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="06028-258">Ekleme veya hello IPSec/IKE İlkesi tooa bağlantısını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="06028-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="06028-259">Merhaba IPSec/IKE İlkesi bir bağlantısından Kaldır</span><span class="sxs-lookup"><span data-stu-id="06028-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="06028-260">Merhaba aynı adımlar tooboth S2S ve VNet-VNet bağlantıları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="06028-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06028-261">IPSec/IKE İlkesi desteklenir *standart* ve *HighPerformance* rota tabanlı VPN ağ geçitleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="06028-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="06028-262">Merhaba temel ağ geçidi SKU veya hello ilke tabanlı VPN ağ geçidi çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="06028-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="06028-263">1. Merhaba IPSec/IKE İlkesi bağlantısının Göster</span><span class="sxs-lookup"><span data-stu-id="06028-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="06028-264">Aşağıdaki örnek hello nasıl tooget hello bağlantı üzerinde yapılandırılmış IPSec/IKE İlkesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="06028-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="06028-265">Merhaba komut dosyaları da alıştırmaları hello yukarıdaki devam edin.</span><span class="sxs-lookup"><span data-stu-id="06028-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="06028-266">varsa hello son komut hello bağlantısında yapılandırılmış hello geçerli IPSec/IKE İlkesi listeler.</span><span class="sxs-lookup"><span data-stu-id="06028-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="06028-267">örnek çıktı aşağıdaki hello hello bağlantı için şöyledir:</span><span class="sxs-lookup"><span data-stu-id="06028-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="06028-268">Yapılandırılmış IPSec/IKE İlkesi yok ise, komut hello (PS > $connection6.policy) boş bir dönüş alır.</span><span class="sxs-lookup"><span data-stu-id="06028-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="06028-269">IPSec/IKE hello bağlantısında yapılandırılmamış, ancak hiçbir özel IPSec/IKE ilke olduğu anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="06028-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="06028-270">Merhaba gerçek bağlantı hello Azure VPN ağ geçidi ve şirket içi VPN aygıtınızın arasında anlaşılan hello varsayılan ilkesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="06028-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="06028-271">2. Eklemek veya bir bağlantı için bir IPSec/IKE ilkesini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="06028-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="06028-272">Merhaba adımları tooadd yeni bir ilke veya var olan bir ilkenin bir bağlantısı olan güncelleştirme aynı hello: yeni bir ilke oluşturun ardından hello yeni ilke toohello bağlantı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="06028-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="06028-273">tooenable "tooan bağlanma ilke tabanlı VPN cihazı şirket içi zaman UsePolicyBasedTrafficSelectors" Merhaba Ekle "-UsePolicyBaseTrafficSelectors" parametresi toohello cmdlet'i ya da çok ayarlayın $False toodisable hello seçeneği:</span><span class="sxs-lookup"><span data-stu-id="06028-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="06028-274">Merhaba bağlantısını Al yeniden hello İlkesi güncelleştirdiyseniz toocheck.</span><span class="sxs-lookup"><span data-stu-id="06028-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="06028-275">Hello aşağıdaki örnekte gösterildiği gibi hello son satırından hello çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="06028-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="06028-276">3. Bir IPSec/IKE İlkesi bir bağlantısından Kaldır</span><span class="sxs-lookup"><span data-stu-id="06028-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="06028-277">Öğesinden bir bağlantı hello özel ilke kaldırdıktan sonra geri toohello hello Azure VPN ağ geçidi döner [IPSec/IKE teklifleri varsayılan listesini](vpn-gateway-about-vpn-devices.md) ve yeniden şirket içi VPN Cihazınızı yeniden anlaşmaya varılır.</span><span class="sxs-lookup"><span data-stu-id="06028-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="06028-278">Kullanabileceğiniz hello İlkesi hello bağlantısından kaldırdıysanız aynı komut dosyasını toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="06028-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06028-279">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06028-279">Next steps</span></span>

<span data-ttu-id="06028-280">Bkz: [birden çok şirket içi ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md) ilke tabanlı trafik Seçici ile ilgili daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="06028-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="06028-281">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06028-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="06028-282">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06028-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
