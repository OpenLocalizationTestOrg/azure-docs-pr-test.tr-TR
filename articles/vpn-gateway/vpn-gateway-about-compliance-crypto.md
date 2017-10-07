---
title: "aaaAbout şifreleme gereksinimleri ve Azure VPN ağ geçitleri | Microsoft Docs"
description: "Bu makalede, şifreleme gereksinimleri ve Azure VPN ağ geçitleri açıklanmaktadır"
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
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="0dd25-103">Şifreleme gereksinimleri ve Azure VPN ağ geçitleri hakkında</span><span class="sxs-lookup"><span data-stu-id="0dd25-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="0dd25-104">Bu makalede, Azure VPN ağ geçitleri toosatisfy şifreleme gereksinimlerinizi hem şirket içi S2S VPN tünelleri, hem de VNet-VNet bağlantıları Azure içinde nasıl yapılandırabileceğiniz anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0dd25-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="0dd25-105">IPSec ve IKE İlkesi parametreleri hakkında Azure VPN ağ geçitleri için</span><span class="sxs-lookup"><span data-stu-id="0dd25-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="0dd25-106">IPSec ve IKE protokolü standart çeşitli bileşimlerde çok çeşitli şifreleme algoritmalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="0dd25-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="0dd25-107">Müşteriler, şifreleme algoritmaları ve parametreleri belirli bir bileşimini isteme, Azure VPN ağ geçitleri varsayılan teklifleri kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd25-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="0dd25-108">Merhaba varsayılan ilkeyi ayarlar çeşitli üçüncü taraf VPN aygıtları ile toomaximize birlikte çalışabilirlik varsayılan yapılandırması seçilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0dd25-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="0dd25-109">Sonuç olarak, hello ilkeleri ve tekliflerini hello sayısı kullanılabilir şifreleme algoritmaları ve anahtar gücü tüm olası birleşimlerini ele olamaz.</span><span class="sxs-lookup"><span data-stu-id="0dd25-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="0dd25-110">Varsayılan ilke Azure VPN ağ geçidi hello belgesinde listelenen için kümesi Hello: [VPN cihazları hakkında ve siteden siteye VPN Gateway bağlantıları için IPSec/IKE parametreleri](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="0dd25-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="0dd25-111">Şifreleme gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="0dd25-111">Cryptographic requirements</span></span>
<span data-ttu-id="0dd25-112">Belirli şifreleme algoritmalarının veya parametreler gerektiren iletişimleri için genellikle toocompliance veya güvenlik gereksinimleri, müşteriler artık kendi Azure VPN ağ geçitleri toouse özel bir IPSec/IKE ilke özel şifreleme ile yapılandırabilirsiniz algoritmaları ve anahtar gücü yerine hello Azure varsayılan ilkeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0dd25-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="0dd25-113">Örneğin, müşteriler Grup 14 (2048 bit), Grup 24 (2048 bit MODP grup) ya da ECP (Eliptik gibi IKE kullanılan toospecify daha güçlü grupları toobe gerekebilir ancak hello Ikev2 ana mod ilkelerini Azure VPN ağ geçitleri için Diffie-Hellman grubu 2 (1024 bit), yalnızca kullanma Eğri grupları) 256 veya 384 bit (sırasıyla 19 ve Grup 20, Grup).</span><span class="sxs-lookup"><span data-stu-id="0dd25-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="0dd25-114">Benzer gereksinimleri tooIPsec hızlı mod ilkelerini de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0dd25-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="0dd25-115">Azure VPN ağ geçitleri ile özel IPSec/IKE İlkesi</span><span class="sxs-lookup"><span data-stu-id="0dd25-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="0dd25-116">Azure VPN ağ geçitleri artık bağlantı başına, özel IPSec/IKE ilke destekler.</span><span class="sxs-lookup"><span data-stu-id="0dd25-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="0dd25-117">Siteden siteye veya VNet-VNet bağlantısı için şifreleme algoritmaları belirli bir bileşimini IPSec ve IKE için istenen hello anahtar gücü ile hello aşağıdaki örnekte gösterildiği gibi seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0dd25-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![IPSec IKE İlkesi](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="0dd25-119">Bir IPSec/IKE ilkesi oluşturun ve tooa yeni veya var olan bağlantı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0dd25-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="0dd25-120">İş akışı</span><span class="sxs-lookup"><span data-stu-id="0dd25-120">Workflow</span></span>

1. <span data-ttu-id="0dd25-121">Diğer nasıl toodocuments açıklandığı gibi Hello sanal ağlar, VPN ağ geçitleri veya yerel ağ geçitleri bağlanabilirlik topolojiniz için oluşturun</span><span class="sxs-lookup"><span data-stu-id="0dd25-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="0dd25-122">Bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="0dd25-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="0dd25-123">S2S veya VNet-VNet bağlantısı oluşturduğunuzda hello ilkesi uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="0dd25-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="0dd25-124">Merhaba bağlantıyı zaten oluşturduysanız, uygulama veya hello İlkesi tooan var olan bağlantıyı güncelleştir</span><span class="sxs-lookup"><span data-stu-id="0dd25-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="0dd25-125">IPSec/IKE İlkesi hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="0dd25-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="0dd25-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dd25-126">Next steps</span></span>
<span data-ttu-id="0dd25-127">Bkz: [IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) bir bağlantıda özel IPSec/IKE ilkesini yapılandırma hakkında adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="0dd25-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="0dd25-128">Ayrıca bkz. [birden çok ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn hello UsePolicyBasedTrafficSelectors seçeneği hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="0dd25-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
