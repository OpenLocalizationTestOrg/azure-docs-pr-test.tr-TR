---
title: "Azure Ağ İzleyicisi aaaIntroduction toosecurity Grup görünümünde | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi güvenlik görünüm yetenek genel bir bakış sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="cc317-103">Giriş toonetwork güvenlik grubu Azure Ağ İzleyicisi görünümünde</span><span class="sxs-lookup"><span data-stu-id="cc317-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="cc317-104">Ağ güvenlik grupları, bir alt ağ düzeyinde veya bir NIC düzeyi ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="cc317-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="cc317-105">Bir alt düzeyde ilişkili hello alt ağdaki tooall hello VM örnekleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="cc317-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="cc317-106">Ağ güvenlik grubu görünümü tüm yapılandırılmış hello Nsg'ler ve hello yapılandırma hakkında bilgi sağlayan bir sanal makine için bir NIC ve alt ağ düzeyinde ilişkili kurallar döndürür.</span><span class="sxs-lookup"><span data-stu-id="cc317-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="cc317-107">Ayrıca, her bir VM hello NIC hello etkin güvenlik kuralları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="cc317-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="cc317-108">Ağ güvenlik grubu kullanarak görünüm açık bağlantı noktaları gibi ağ güvenlik açıkları için bir VM değerlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc317-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="cc317-109">De doğrulamak, ağ güvenlik grubu temel alarak beklendiği gibi çalışıp çalışmadığını bir [hello karşılaştırması yapılandırılmış ve etkin güvenlik kuralları hello](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cc317-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="cc317-110">Daha uzun bir kullanım örneği, güvenlik uyumluluğunu ve denetim gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cc317-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="cc317-111">Kuruluşunuzdaki güvenlik idare modeli olarak güvenlik kuralları Düzenleyici kümesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc317-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="cc317-112">Bir dönemsel uyumluluk denetimi hello VM'ler, ağınızdaki her hello düzenleyici kuralları hello etkili kuralları ile karşılaştırarak programlı bir şekilde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="cc317-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="cc317-113">Hello portal kuralları etkili, alt ağ, ağ arabirimi ve varsayılan ayrılır.</span><span class="sxs-lookup"><span data-stu-id="cc317-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="cc317-114">Bu basit bir hello uygulanan kurallar tooa sanal makine görünüme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc317-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="cc317-115">Tooeasily karşıdan hello sekmesini olursa olsun tüm hello güvenlik kuralları bir CSV dosyasına karşıdan yükle düğmesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="cc317-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![Güvenlik grubu görünümü][1]

<span data-ttu-id="cc317-117">Kuralları seçilebilir ve tooshow hello ağ güvenlik grubu ve kaynak ve hedef öneklerinin yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="cc317-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="cc317-118">Bu dikey pencereden toohello ağ güvenlik grubu kaynak doğrudan gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc317-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![ayrıntıya gitme][2]

### <a name="next-steps"></a><span data-ttu-id="cc317-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc317-120">Next steps</span></span>

<span data-ttu-id="cc317-121">Tooaudit ağınızda güvenlik Grup nasıl öğrenin ayarları şu adresi ziyaret ederek [PowerShell ile denetim ağ güvenlik grubu ayarları](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="cc317-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









