---
title: "Örnek Yapılandırması - Cisco ASA cihaz için Azure VPN ağ geçitlerini bağlama | Microsoft Docs"
description: "Bu makale Azure VPN ağ geçitleri için bağlanma Cisco ASA cihaz için örnek bir yapılandırma sağlar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="60b21-103">Örnek Yapılandırması: Cisco ASA aygıt (Ikev2/Hayır BGP)</span><span class="sxs-lookup"><span data-stu-id="60b21-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="60b21-104">Bu makale Azure VPN ağ geçitleri için bağlanan Cisco ASA cihazları için örnek yapılandırmalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="60b21-104">This article provides sample configurations for Cisco ASA devices connecting to Azure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="60b21-105">Bir bakışta cihaz</span><span class="sxs-lookup"><span data-stu-id="60b21-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="60b21-106">Cihaz satıcısından</span><span class="sxs-lookup"><span data-stu-id="60b21-106">Device vendor</span></span>          | <span data-ttu-id="60b21-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="60b21-107">Cisco</span></span>                             |
| <span data-ttu-id="60b21-108">Cihaz modeli</span><span class="sxs-lookup"><span data-stu-id="60b21-108">Device model</span></span>           | <span data-ttu-id="60b21-109">ASA (Uyarlamalı güvenlik Gereci)</span><span class="sxs-lookup"><span data-stu-id="60b21-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="60b21-110">Hedef sürümü</span><span class="sxs-lookup"><span data-stu-id="60b21-110">Target version</span></span>         | <span data-ttu-id="60b21-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="60b21-111">8.4+</span></span>                              |
| <span data-ttu-id="60b21-112">Sınanan modeli</span><span class="sxs-lookup"><span data-stu-id="60b21-112">Tested model</span></span>           | <span data-ttu-id="60b21-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="60b21-113">ASA 5505</span></span>                          |
| <span data-ttu-id="60b21-114">Test edilen sürüm</span><span class="sxs-lookup"><span data-stu-id="60b21-114">Tested version</span></span>         | <span data-ttu-id="60b21-115">9.2</span><span class="sxs-lookup"><span data-stu-id="60b21-115">9.2</span></span>                               |
| <span data-ttu-id="60b21-116">IKE sürümü</span><span class="sxs-lookup"><span data-stu-id="60b21-116">IKE version</span></span>            | <span data-ttu-id="60b21-117">**Ikev2**</span><span class="sxs-lookup"><span data-stu-id="60b21-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="60b21-118">BGP</span><span class="sxs-lookup"><span data-stu-id="60b21-118">BGP</span></span>                    | <span data-ttu-id="60b21-119">**Hayır**</span><span class="sxs-lookup"><span data-stu-id="60b21-119">**No**</span></span>                            |
| <span data-ttu-id="60b21-120">Azure VPN ağ geçidi türü</span><span class="sxs-lookup"><span data-stu-id="60b21-120">Azure VPN gateway type</span></span> | <span data-ttu-id="60b21-121">**Rota tabanlı** VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="60b21-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="60b21-122">Yapılandırma bir Azure için Cisco ASA bağlanmasındakiyle **rota tabanlı** açıklandığı gibi özel IPSec/IKE İlkesi "UserPolicyBasedTrafficSelectors" seçeneğiyle kullanarak VPN ağ geçidi [bu makalede](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="60b21-122">The configuration below connects a Cisco ASA device to an Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="60b21-123">ASA cihazlarının kullanmasını gerektirir **Ikev2** erişim listesi temel yapılandırmalarla VTI tabanlı değil.</span><span class="sxs-lookup"><span data-stu-id="60b21-123">It requires ASA devices to use **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="60b21-124">Lütfen ilke şirket içi VPN cihazlarınızı üzerinde desteklenen emin olmak için VPN cihaz Satıcı belirtimleri başvurun.</span><span class="sxs-lookup"><span data-stu-id="60b21-124">Please consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="60b21-125">VPN cihaz gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="60b21-125">VPN device requirements</span></span>
<span data-ttu-id="60b21-126">Azure VPN ağ geçitleri standart IPSec/IKE protokolü paketleri S2S VPN tünelleri oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="60b21-126">Azure VPN gateways use standard IPsec/IKE protocol suites to establish S2S VPN tunnels.</span></span> <span data-ttu-id="60b21-127">Başvurmak [VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Azure VPN ağ geçitleri için varsayılan şifreleme algoritmaları ve ayrıntılı IPSec/IKE protokol parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="60b21-127">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="60b21-128">Bölümünde açıklandığı gibi isteğe bağlı olarak şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için tam birleşimini belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="60b21-128">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="60b21-129">Lütfen şifreleme algoritmaları ve anahtar gücü belirli bir bileşimini seçerseniz, VPN aygıtlarınızda karşılık gelen belirtimleri kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="60b21-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use the corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="60b21-130">Tek VPN tüneli</span><span class="sxs-lookup"><span data-stu-id="60b21-130">Single VPN tunnel</span></span>
<span data-ttu-id="60b21-131">Bu topoloji bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli oluşur.</span><span class="sxs-lookup"><span data-stu-id="60b21-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="60b21-132">İsteğe bağlı olarak VPN tüneli üzerinden BGP yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60b21-132">You can optionally configure BGP across the VPN tunnel.</span></span>

![tek tünel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="60b21-134">Başvurmak [tek tünel Kurulum](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) Azure yapılandırmalarını oluşturmak ayrıntılı, adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="60b21-134">Refer to [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions to build the Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="60b21-135">Ağ ve VPN ağ geçidi bilgileri</span><span class="sxs-lookup"><span data-stu-id="60b21-135">Network and VPN gateway information</span></span>
<span data-ttu-id="60b21-136">Bu bölümde listesinde parametreleri için bu örnek.</span><span class="sxs-lookup"><span data-stu-id="60b21-136">This section list the parameters for the this sample.</span></span>

| <span data-ttu-id="60b21-137">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="60b21-137">**Parameter**</span></span>                | <span data-ttu-id="60b21-138">**Değer**</span><span class="sxs-lookup"><span data-stu-id="60b21-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="60b21-139">VNet adres önekleri</span><span class="sxs-lookup"><span data-stu-id="60b21-139">VNet address prefixes</span></span>        | <span data-ttu-id="60b21-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60b21-140">10.11.0.0/16</span></span><br><span data-ttu-id="60b21-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60b21-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="60b21-142">Azure VPN ağ geçidi IP</span><span class="sxs-lookup"><span data-stu-id="60b21-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="60b21-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="60b21-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="60b21-144">Şirket içi adres önekleri</span><span class="sxs-lookup"><span data-stu-id="60b21-144">On-premises address prefixes</span></span> | <span data-ttu-id="60b21-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60b21-145">10.51.0.0/16</span></span><br><span data-ttu-id="60b21-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="60b21-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="60b21-147">Şirket içi VPN cihazının IP</span><span class="sxs-lookup"><span data-stu-id="60b21-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="60b21-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="60b21-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="60b21-149">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="60b21-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="60b21-150">65010</span><span class="sxs-lookup"><span data-stu-id="60b21-150">65010</span></span>                        |
| <span data-ttu-id="60b21-151">* Azure BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="60b21-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="60b21-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="60b21-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="60b21-153">* Şirket içi BGP ASN</span><span class="sxs-lookup"><span data-stu-id="60b21-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="60b21-154">65050</span><span class="sxs-lookup"><span data-stu-id="60b21-154">65050</span></span>                        |
| <span data-ttu-id="60b21-155">* Şirket içi BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="60b21-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="60b21-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="60b21-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="60b21-157">(*) İsteğe bağlı parametreleri BGP yalnızca.</span><span class="sxs-lookup"><span data-stu-id="60b21-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="60b21-158">IPSec/IKE İlkesi & parametreleri</span><span class="sxs-lookup"><span data-stu-id="60b21-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="60b21-159">Aşağıdaki tabloda IPSec/IKE algoritmaları ve örnekte kullanılan parametreler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="60b21-159">The table below lists the IPsec/IKE algorithms and parameters used in the sample.</span></span> <span data-ttu-id="60b21-160">Lütfen yukarıda listelenen tüm algoritmalar, VPN aygıt modelleri ve bellenim sürümleri tarafından desteklendiğinden emin olmak için VPN aygıt belirtimlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="60b21-160">Please consult your VPN device specifications to make sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="60b21-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="60b21-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="60b21-162">**Değer**</span><span class="sxs-lookup"><span data-stu-id="60b21-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="60b21-163">IKEv2 Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="60b21-163">IKEv2 Encryption</span></span> | <span data-ttu-id="60b21-164">AES256</span><span class="sxs-lookup"><span data-stu-id="60b21-164">AES256</span></span>                               |
| <span data-ttu-id="60b21-165">IKEv2 Bütünlüğü</span><span class="sxs-lookup"><span data-stu-id="60b21-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="60b21-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="60b21-166">SHA384</span></span>                               |
| <span data-ttu-id="60b21-167">DH Grubu</span><span class="sxs-lookup"><span data-stu-id="60b21-167">DH Group</span></span>         | <span data-ttu-id="60b21-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="60b21-168">DHGroup24</span></span>                            |
| <span data-ttu-id="60b21-169">IPsec Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="60b21-169">IPsec Encryption</span></span> | <span data-ttu-id="60b21-170">AES256</span><span class="sxs-lookup"><span data-stu-id="60b21-170">AES256</span></span>                               |
| <span data-ttu-id="60b21-171">IPsec Bütünlüğü</span><span class="sxs-lookup"><span data-stu-id="60b21-171">IPsec Integrity</span></span>  | <span data-ttu-id="60b21-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="60b21-172">SHA1</span></span>                                 |
| <span data-ttu-id="60b21-173">PFS Grubu</span><span class="sxs-lookup"><span data-stu-id="60b21-173">PFS Group</span></span>        | <span data-ttu-id="60b21-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="60b21-174">PFS24</span></span>                                |
| <span data-ttu-id="60b21-175">QM SA Yaşam Süresi</span><span class="sxs-lookup"><span data-stu-id="60b21-175">QM SA Lifetime</span></span>   | <span data-ttu-id="60b21-176">7200 saniye</span><span class="sxs-lookup"><span data-stu-id="60b21-176">7200 seconds</span></span>                         |
| <span data-ttu-id="60b21-177">Trafik Seçicisi</span><span class="sxs-lookup"><span data-stu-id="60b21-177">Traffic Selector</span></span> | <span data-ttu-id="60b21-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="60b21-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="60b21-179">Önceden Paylaşılan Anahtar</span><span class="sxs-lookup"><span data-stu-id="60b21-179">Pre-Shared Key</span></span>   | <span data-ttu-id="60b21-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="60b21-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="60b21-181">(*) Bazı cihazlarda IPSec bütünlüğünü "GCM AES IPSec şifreleme algoritması olarak kullanılıyorsa, null" olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="60b21-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="60b21-182">Cihaz notları</span><span class="sxs-lookup"><span data-stu-id="60b21-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="60b21-183">Ikev2 desteği, ASA sürüm 8.4 gerektirir ve üstü.</span><span class="sxs-lookup"><span data-stu-id="60b21-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="60b21-184">(Ötesinde Grup 5) daha yüksek DH ve PFS grubu desteği ASA sürümünü gerektirir 9.x.</span><span class="sxs-lookup"><span data-stu-id="60b21-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="60b21-185">AES-GCM ve IPSec bütünlüğüyle SHA-256, SHA-384, SHA-512 desteği ile IPSec şifrelemesini gerektiren ASA sürüm 9.x yeni ASA donanımda; ASA 5505, 5510, 5520, 5540, 5550, 5580 olan **değil** desteklenir.</span><span class="sxs-lookup"><span data-stu-id="60b21-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="60b21-186">(Lütfen onaylamak için satıcı belirtimlerine bakın.)</span><span class="sxs-lookup"><span data-stu-id="60b21-186">(Please check the vendor specifications to confirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="60b21-187">Örnek cihaz yapılandırması</span><span class="sxs-lookup"><span data-stu-id="60b21-187">Sample device configurations</span></span>
<span data-ttu-id="60b21-188">Aşağıdaki komut dosyası topoloji ve yukarıda listelenen parametreleri temel alarak örnek bir yapılandırma sağlar.</span><span class="sxs-lookup"><span data-stu-id="60b21-188">The script below provides a sample configuration based on the topology and parameters listed above.</span></span> <span data-ttu-id="60b21-189">S2S VPN tüneli yapılandırma aşağıdaki bölümlerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="60b21-189">The S2S VPN tunnel configuration consists of the following parts:</span></span>

1. <span data-ttu-id="60b21-190">Arabirimleri & yolları</span><span class="sxs-lookup"><span data-stu-id="60b21-190">Interfaces & routes</span></span>
2. <span data-ttu-id="60b21-191">Erişim listeleri</span><span class="sxs-lookup"><span data-stu-id="60b21-191">Access lists</span></span>
3. <span data-ttu-id="60b21-192">IKE İlkesi ve parametreleri (1. aşaması veya ana mod)</span><span class="sxs-lookup"><span data-stu-id="60b21-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="60b21-193">IPSec ilkesi ve parametreleri (Aşama 2 veya hızlı mod)</span><span class="sxs-lookup"><span data-stu-id="60b21-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="60b21-194">Diğer parametreler (TCP MSS clamping, vb.)</span><span class="sxs-lookup"><span data-stu-id="60b21-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="60b21-195">Lütfen aşağıda listelenen ek yapılandırmayı tamamlamak ve yer tutucular yerine gerçek değerler ile emin olun:</span><span class="sxs-lookup"><span data-stu-id="60b21-195">Please make sure you complete the additional configuration listed below and replace the placeholders with the actual values:</span></span>
> 
> - <span data-ttu-id="60b21-196">Arabirim yapılandırması için hem iç ve Dış arabirimler</span><span class="sxs-lookup"><span data-stu-id="60b21-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="60b21-197">İç/özel ve dış/genel ağlar için yollar</span><span class="sxs-lookup"><span data-stu-id="60b21-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="60b21-198">Tüm adlarını ve ilke numaralarını cihazda benzersiz olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="60b21-198">Ensure all names and policy numbers are unique on the device</span></span>
> - <span data-ttu-id="60b21-199">Şifreleme algoritmaları aygıtınızda desteklenen olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="60b21-199">Ensure the cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="60b21-200">Aşağıdaki yer tutucu gerçek değerlerle değiştirin</span><span class="sxs-lookup"><span data-stu-id="60b21-200">Replace the following place holders with the actual values</span></span>
>   - <span data-ttu-id="60b21-201">Arabirim adı dışında: "dış"</span><span class="sxs-lookup"><span data-stu-id="60b21-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="60b21-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="60b21-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="60b21-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="60b21-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="60b21-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="60b21-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="60b21-205">Sanal ağ ve yerel ağ geçidi adları (vnetname adlı, LNGName)</span><span class="sxs-lookup"><span data-stu-id="60b21-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="60b21-206">VNet ve şirket içi adres öneklerini ağ</span><span class="sxs-lookup"><span data-stu-id="60b21-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="60b21-207">Uygun ağ maskeleri</span><span class="sxs-lookup"><span data-stu-id="60b21-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="60b21-208">Örnek Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="60b21-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="60b21-209">Basit hata ayıklama komutları</span><span class="sxs-lookup"><span data-stu-id="60b21-209">Simple debugging commands</span></span>

<span data-ttu-id="60b21-210">Hata ayıklama amacıyla bazı ASA komutlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="60b21-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="60b21-211">IPSec ve IKE SA'ın Göster</span><span class="sxs-lookup"><span data-stu-id="60b21-211">Show the IPsec and IKE SA's</span></span>
    - <span data-ttu-id="60b21-212">"şifre IPSec Göster sa"</span><span class="sxs-lookup"><span data-stu-id="60b21-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="60b21-213">"crypto Göster IKEv2 sa"</span><span class="sxs-lookup"><span data-stu-id="60b21-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="60b21-214">Girme hata ayıklama modu - bu konsolda çok gürültülü alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="60b21-214">Entering debug mode - this can get very noisy on the console</span></span>
    - <span data-ttu-id="60b21-215">"hata ayıklama şifre IKEv2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="60b21-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="60b21-216">"hata ayıklama şifre IKEv2 Protokolü <level>"</span><span class="sxs-lookup"><span data-stu-id="60b21-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="60b21-217">Liste geçerli yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="60b21-217">List current configurations</span></span>
    - <span data-ttu-id="60b21-218">"Göster" Çalıştır - cihazda geçerli yapılandırmaları gösterir; Liste belirli bölümlerine yapılandırmanın çeşitli alt komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60b21-218">"show run" - shows the current configurations on the device; you can use the various sub-commands to list specific parts of the configuration.</span></span> <span data-ttu-id="60b21-219">Örn., "Çalıştır Göster crypto", "Çalıştır Göster erişim listesinde", "Çalıştır Göster tünel grubu", vb.</span><span class="sxs-lookup"><span data-stu-id="60b21-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="60b21-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60b21-220">Next steps</span></span>
<span data-ttu-id="60b21-221">Etkin-etkin şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantıları yapılandırma adımları için bkz. [Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantılar için Etkin-Etkin VPN Gateways Yapılandırma](vpn-gateway-activeactive-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="60b21-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

