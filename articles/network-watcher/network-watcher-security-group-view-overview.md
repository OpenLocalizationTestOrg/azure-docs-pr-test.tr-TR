---
title: "Güvenlik grubu Azure Ağ İzleyicisi görünümünde giriş | Microsoft Docs"
description: "Bu sayfa Ağ İzleyicisi güvenlik görünüm yetenek genel bir bakış sağlar"
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
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="51739-103">Ağ güvenlik grubu Azure Ağ İzleyicisi görünümünde giriş</span><span class="sxs-lookup"><span data-stu-id="51739-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="51739-104">Ağ güvenlik grupları, bir alt ağ düzeyinde veya bir NIC düzeyi ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="51739-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="51739-105">Bir alt düzeyde ilişkili olduğunda, alt ağdaki tüm VM örnekleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="51739-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="51739-106">Ağ güvenlik grubu görünümü yapılandırılan Nsg'ler ve yapılandırma hakkında bilgi sağlayan bir sanal makine için bir NIC ve alt ağ düzeyinde ilişkili kurallarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="51739-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="51739-107">Ayrıca, her bir VM NIC'ler için etkili güvenlik kuralları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="51739-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="51739-108">Ağ güvenlik grubu kullanarak görünüm açık bağlantı noktaları gibi ağ güvenlik açıkları için bir VM değerlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51739-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="51739-109">De doğrulamak, ağ güvenlik grubu temel alarak beklendiği gibi çalışıp çalışmadığını bir [yapılandırılmış ve etkin güvenlik kuralları arasında karşılaştırma](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="51739-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="51739-110">Daha uzun bir kullanım örneği, güvenlik uyumluluğunu ve denetim gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="51739-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="51739-111">Kuruluşunuzdaki güvenlik idare modeli olarak güvenlik kuralları Düzenleyici kümesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51739-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="51739-112">Bir dönemsel uyumluluk denetimi için ağınızda VM'lerin her birinde etkili kurallarla düzenleyici kuralları karşılaştırarak programlı bir şekilde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="51739-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="51739-113">Portalda kuralları etkili, alt ağ, ağ arabirimi ve varsayılan ayrılır.</span><span class="sxs-lookup"><span data-stu-id="51739-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="51739-114">Bu kuralı bir sanal makineye uygulanan basit bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="51739-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="51739-115">Karşıdan Yükle düğmesi kolayca sekmesini olursa olsun tüm güvenlik kuralları bir CSV dosyasına indirmek için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="51739-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![Güvenlik grubu görünümü][1]

<span data-ttu-id="51739-117">Kuralları seçilebilir ve ağ güvenlik grubu ve kaynak ve hedef öneklerinin göstermek için yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="51739-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="51739-118">Bu dikey pencereden doğrudan ağ güvenlik grubu kaynak gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51739-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![ayrıntıya gitme][2]

### <a name="next-steps"></a><span data-ttu-id="51739-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51739-120">Next steps</span></span>

<span data-ttu-id="51739-121">Ağ güvenlik grubu ayarlarınızı ziyaret ederek denetim öğrenin [PowerShell ile ağ güvenlik grubu denetim ayarları](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="51739-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









